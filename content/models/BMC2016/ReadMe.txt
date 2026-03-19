The .cys files are the Cytoscape session files with the models from the paper. You can open it in Cytoscape with File --> Open. In particular:
 - Model_Drosophila_Circadian_Clock_initial.cys contains the model of the Drosophila Melanogaster circadian clock with the parameter settings copied from the original ODE model (Fig. 3A in the main text for model topology)
 - Model_Drosophila_Circadian_Clock_final.cys contains the model of the Drosophila Melanogaster circadian clock with the final parameters (Fig. 3 in the main text and Fig. S5 in the Additional Materials)
 - Model_TNF_EGF_first_version.cys contains the first version of the TNF-alpha and EGF pathways, which were initially modelled separately (Figs. S6 and S7 in the Additional Materials)
 - Model_TNF_EGF_no_hypotheses.cys contains the merged model of the TNF-alpha and EGF pathways, without the hypotheses (Fig. 5A in the main text)
 - Model_TNF_EGF_final.cys contains the improved model of the TNF-alpha and EGF pathways (Fig. 6A in the main text)
 - Small_TNF_model.cys contains the small model used as example in the Methods section (Fig. 8C in the main text)
 
The .csv files contain the normalized series for some of the model results and experimental data, respectively taken from [1] and [2]. You can add them to a simulation graph with the graph right-click menu "Add data from CSV" (see ANIMO's User Manual available at http://fmt.cs.utwente.nl/tools/animo/content/Manual.pdf).
Initial activity levels and interaction parameters can be changed by the double-clicking the corresponding nodes.
Pressing the "Analyze network" button makes ANIMO automatically perform the analysis and show the results in graphical form.
Right-clicking on a graph gives access to additional options. For example, to change between line and heat-map graphs, see the "Graph type" submenu. A slider under the graph allows to see the activiy levels of  the nodes at each point in time reflected in the Network panel.
For more details about these and other features of ANIMO, please consult ANIMO's User Manual.

[1] Fathallah-Shaykh, H.M., Bona, J.L., Kadener, S.: Mathematical model of the drosophila circadian clock: Loop
regulation and transcriptional integration. Biophysical Journal 97(9), 2399–2408 (2009)
[2] S. Gaudet, K. A. Janes, J. G. Albeck, E. A. Pace, D. A. Lauffenburger, P. K. Sorger, A compendium of signals and responses triggered by prodeath and prosurvival cytokines.  Mol. Cell Proteomics 4, 1569-1590 (2005)
