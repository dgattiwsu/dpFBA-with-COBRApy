# dpFBA-with-COBRApy

The key idea of *dynamic parallel FBA* (**dpFBA**) is to perform dFBA on individual models while keeping track of the shared pool of external metabolites from which all models can take up nutrients. The concentrations of each biomass and of the external metabolites is updated at each time interval. 

COBRApy currently offers only a static optimization approach (SOA) implementation of dFBA for the simulation of the batch growth of a single species over an integration interval from $t_0$ to $t_f$,  divided in $n$ time steps. Here we describe a simple method to extend COBRApy dFBA to dpFBA for the simulation of a community of species without the need for any modification of the current package.

Our method involves 6 steps:

    1. k species in the community are represented as separate compartments with the same identical initial extracellular concentrations of metabolites at time t_0.

    2. Given a time interval from t_0 to t_f,  divided in n time steps, dFBA is carried out separately for each of the k compartments for 1 time step. 

    3. At the end of each time step biomass and external metabolites are first updated separately in each of the k compartments.  

    4. Then, the concentration of external metabolites that are shared by different species are updated in each of the k compartment by adding to their values at the beginning of the iteration the changes produced in all the k compartments at the end of the iteration. 

    5. The next iteration of 1 time step is carried out with updated biomasses and external metabolites. 

    6. Iterations continue until t_f is reached or the FBA solution for all the k species becomes infeasible.

In pseudocode:

```
INPUT:
    k = number of species/compartments
    n = number of time steps
    t0 = initial time
    tf = final time
    Δt = (tf - t0) / n   # time step size
    Biomass[i] = initial biomass of species i for i = 1..k
    Exchange_rates[i] = initial exchange rates for compartment i for i = 1..k
    Metabolites = initial extracellular metabolite concentrations (shared)

PROCEDURE:
    Set time = t0

    WHILE time < tf:

        FOR i = 1 to k:
            Solve FBA for compartment i 
            Compute biomass growth and metabolites changes in compartment i over Δt
            Store results:
                ΔBiomass[i], ΔMetabolites[i]

        FOR i = 1 to k:
            Biomass[i] = Biomass[i] + ΔBiomass[i]
            Update Exchange_rates[i] based on updated Biomass[i]

        FOR each metabolite m:
            Metabolites[m] = Metabolites[m] + Σ(ΔMetabolites[i][m]) over all i

        time = time + Δt

        IF FBA solution infeasible for ALL species:
            EXIT loop

    END WHILE

OUTPUT:
    Time-course trajectories of Biomass[i] and Metabolites
```


Since at each iteration the concentration of external metabolites in the shared pool is updated independently for each one of the k species, the consumption/production of shared metabolites due to all the other species during the $\Delta t$ covered by the iteration is ignored. Although, before the next iteration the concentration of shared metabolites is updated taking into consideration the contribution of all the species, the initial individual updates introduce an integration error that make the procedure again akin to a Forward Euler method with 1st order accuracy $\mathcal{O}\left(\Delta T\right)$. Therefore, a very small $\Delta T$ must be taken to ensure the dpFBA solution is as correct as possible.

Applications of the method to a few test cases are presented in our ArXiv paper: ***"A simple method to extend COBRApy dynamic FBA protocol to the metabolic simulation of communities"***. All the test cases, and the corresponding figures of the manuscript can be reproduced running the jupyter notebooks in the `tests` folder of this repository. 




