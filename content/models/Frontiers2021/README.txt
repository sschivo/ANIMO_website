"An ECHO of cartilage: in silico prediction of combinatorial treatments to switch between transient and permanent cartilage phenotypes with ex vivo validation"
Sakshi Khurana, Stefano Schivo, Jacqueline R.M. Plass, Nikolas Mersinis,  Jetse Scholma, Johan Kerkhofs, Leilei Zhong, Jaco van de Pol, Rom Langerak, Liesbet Geris, Marcel Karperien, Janine N. Post

This file contains the description of the models and scripts used to obtain the figures shown in the paper.

Individual README.txt files are available inside each experiment directory, together with input files. Scripts to run the experiments and to analyze the results are also included.
The two different versions of the ECHO model are called "GP" for "Growth plate" and "AC" for "Articular cartilage". Figure 2A displays the differences among the different versions of ECHO: Model 1 is the "GP" model, and Model 4 is the "AC" model.

1)
Figure 3 - Effects of node perturbations on cell fate.
* K.O. *
knock-out for one node (each node in turn is set to 0% activity and kept fixed there), then compute 10 thousand simulations setting random activity for all other nodes. Compute the % of final states that are Sox9-positive, Runx2-positive or Null (the only possible final states).
* Overactivation *
overactivation for one node (each node in turn is set to 100% activity and kept fixed there), then compute 10 thousand simulations setting random activity for all other nodes. Compute the % of final states that are Sox9-positive, Runx2-positive or Null (the only possible final states).


2)
Figure 4 / Supplemental Figure S6 - Combinations of two-node perturbations.
The "AC Model" and "GP Model" folders contain the experiments made starting from the AC and GP model respectively.
Each folder contains in turn a "Runx2" and a "Sox9" folder: those represent the initial state used in the simulations "Runx2" stands for "Runx2-positive state" and "Sox9" stands for "Sox9-positive state".
Interesting results are selected according to the following selection algorithm, and are shown in Figure 4:
   - keep only node perturbations that cause a switch. In particular, the final state must not be Null, nor the initial state, nor the state "0" (which we use to describe where both selected reactants are actually the same, such as BMP=0 together with BMP=100).
   - remove those node perturbations that only work in combination with sigle-node perturbations that are known to cause the switch by themselves.
   - in the case of SOX9+ initial state: keep those node perturbations that, in combination with a single-node perturbation that would generate a switch, KEEP the SOX9+ state instead. These node perturbations are interesting because they successfully help prevent the switch to RUNX2+.
The full results are shown in Supplemental Figure S6.


3)
Figure 5 / Model checking
The model checking experiments were all performed on the Articular Chondrocyte (AC) model. The Cytoscape model in its SOX9+ and RUNX2+ activity states is provided in the folder of this experiment. Basic model checking queries can be performed directly via the ANIMO user interface by pressing the "Model checking..." button and selecting the proper parameters for the query, then pressing "Start model checking". N.B.: model checking is a computationally intensive process that can take several minutes even on powerful machines, and requires several gigabytes of available RAM memory. It is strongly advised to couple ANIMO to the latest available 64bit version of UPPAAL.
In order to perform the additional model checking experiments that are presented in the paper when discussing the delayed addition of IGF1 to the model (see treatment 2 in Table 3), we slightly modified the Timed Automata model in order to allow for some variability w.r.t. the moment in which IGF1 is introduced in the network. The modified model is also made available in the folder of the experiment, and is named "AC_Model_Runx2_IGF_addition.xml". Open this model in UPPAAL, and choose Options --> Diagnostic Trace --> Fastest in order to determine the first possible moment in which IGF1 is added to the model. The addition of IGF1 is represented in ECHO by a secondary node called "IGF1 src", which activates IGF1 very strongly (k=1). Here are a few notes and remarks that will help to understand how the model works:
- The reactant "Erk 1/2" is not present in this UPPAAL model, as it was already knocked-out in the Cytoscape interface before the base version of the model was generated with ANIMO. - In this UPPAAL model, the template that describes the choice of the time when IGF1 is added to the model (i.e., when "IGF1 src" gets activated) is called "InsertIGF1" and can be found in the list of automata templates.
- UPPAAL queries use reactant IDs instead of names: the queries in the Verifier tab show "R78" for "Runx2" and "R85" for "Sox9".
- As the model is a discrete representation of reality, and it can only run up to a finite amount of time, the constant "MAX_TIME" has been defined (see "Declarations" section in the UPPAAL model) to explicitly freeze the model when such time has been reached during its evolution. The default value of MAX_TIME is the maximum integer value that can be handled by UPPAAL, which is 1073741822. In addition, in order to limit the model checking times, the constant "STOP_TIME" has been defined: this allows us to freeze the model before the computational limits are reached, and look for an answer only in the "earlier" behavior of the model. Lowering the value of STOP_TIME is a good idea to considerably speed up model checking. However, if STOP_TIME is too low interesting processes may be missed entirely. In the provided model, we lowered STOP_TIME to 10700000, and this allows us to catch the switch from RUNX2+ to SOX9+ in its early stages before the model freezes. This allows us to find an answer to the query "E<> R85 >= 20 && R78 < 10" (which asks whether it is possible to reach a state where Sox9 activity is rising while Runx2 activity is low) whithin one minute and using about 2 gigabyte of memory. Increasing the value of STOP_TIME would allow us to find reliable answers also to queries where we look for higher values of Sox9 activity.
- In order to check that IGF1 needs to be added "not too early, yet not too late", choose Options --> Diagnostic Trace --> Fastest from the UPPAAL menu and verify the query "E<> R85 >= 20 && R78 < 10" by pressing "Get Trace" in the UPPAAL interface. A trace will be computed and will be available in the Simulator tab. An inspection of the value of variable "currentTime" under "<Global variables>" allows us to see what the earliest possible moment is in which the switch RUNX2+ --> SOX9+ starts occurring. Scrolling backwards in the trace allows us to find the point in which the choice to add IGF1 was made (i.e. when the InsertIGF1 automaton left its initial location). Applying a binary search strategy allows to rapidly trace the point in which the choice has been made. Manually selecting an earlier time for the addition of IGF1 results in the E<>.. query to evaluate to false.



N.B.: More recent versions of UPPAAL accept a different syntax for "simulate" queries.
The queries are in the .q files, and need to be changed according to the version of UPPAAL that is used:
 - for versions 4.1.20 and below: leave the file as it is
 - for versions 4.1.21 and above: open the file and change "simulate 1" to "simulate" (remove the " 1").