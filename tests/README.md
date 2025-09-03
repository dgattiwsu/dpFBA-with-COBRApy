This folder contains the jupyter notebooks with the examples of COBRApy code implementing dynamic parallel dFBA for the tests cases and corresponding figures presented in the ArXiv manuscript.

##### pdFBA_test1.ipynb. 

**Figure 1**. Panels show superimposed the changes in glucose and biomass concentrations calculated using the original COBRApy dFBA protocol with BDF solver (shaded circles), and those calculated using the discretized dFBA method (continuous lines) with RK45 solver and different integration stepsize, $\Delta t\ =\ 1.00,\ 0.20,\ 0.05,\ 0.01\ hrs$. A shaded green area displays the part of the time span in which the solution provided by the discretized method becomes infeasible.


##### pdFBA_tests_2_to_4.ipynb.

**Figure 2**. Metabolites and biomass concentrations changes for the collaborative growth of a respiration deficient strain and a fermentation deficient strain of E. coli in an open system in rapid equilibrium with air at 1 atm. A shaded green/purple area displays the part of the interval in which the FBA solution becomes infeasible.

**Figure 3**. Metabolites and biomass concentrations changes for the collaborative growth of a respiration deficient strain and a fermentation deficient strain of E. coli in a bioreactor with periodic (3 min) feeding of oxygen to maintain an approximate concentration of 1.0 mM. A shaded green/purple area displays the part of the time span in which the FBA solution becomes infeasible.

**Figure 4**. Metabolites and biomass concentrations changes for the collaborative growth of a respiration deficient strain and a fermentation deficient strain of E. coli in an closed system with periodic (3 min) feeding of glucose at ~20.0 mM and oxygen at ~1.0 mM. A shaded green/purple area displays the part of the time span in which the FBA solution becomes infeasible.


##### pdFBA_test_5.ipynb. 

**Figure 5**. Metabolites and biomass concentrations changes for the growth of E. coli (using glucose) and Strep. thermophilus (using both glucose and lactose) in a shared environment. A shaded green/purple area displays the part of the time span in which the solutions provided by the discretized method for each model become infeasible.






