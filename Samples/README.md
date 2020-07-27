## Samples

This section contains a few sample models and translations to demonstrate pram2mesa in action and to show the differences between PRAMs and ABMs. The PRAMs are originally from the PyPRAM [simulation examples](https://github.com/momacs/pram/tree/master/src/sim), although they may be slightly modified. The ABMs are translated using pram2mesa.

### How to Navigate the Samples
Each sample folder will always contain a few things:
* `run_pram.py`: This simply runs and plots the original PRAM. Slight modifications may have been made.
* `translate.py`: This instantiates the PRAM and translates it using pram2mesa.
* `run_abm.py`: This runs and plots the new ABM.
* `run_abm_batch.py`: This runs and plots the new ABM across several trials (default: 10).  
* A folder containing all the files for the ABM, generated by pram2mesa in `translate.py`.
* `output`: A folder containing generated graphs for the PRAM, ABM, and ABM batch run.

### The Models

The models on display are:
* A basic SIRS model
    * Agents flow between Susceptible, Infected, Recovered, and return to Susceptible
* A simple model of segregation between two sites
    * Agents are either red or blue
    * If an agent is in the minority color at their site, they may migrate to the other site
* A model of migration from a devastating conflict
    * Agents start at the conflict site
    * Agents may die from the conflict, or migrate to a neighboring country
    * Each country takes a different amount of time to migrate to
    * Agents may die on the journey, or they will settle when they reach their destination
    * After 3 years (4 years are simulated), the conflict ends and no new migration starts
* Another SIRS model, this one generated from a synthetic population of students in Allegheny County, PA
    * Infection probability is proportional to the number of infected students at a school
    * Students may stay home if infected, but low-income students are far less likely to do so
    
#### Model-Specific Details
The basic SIRS and Segregation models are fairly straightforward. The others have a few quirks:

##### Migration Model
* The original PRAM models 1,000,000 agents. This could take weeks for the ABM to model, so it has been reduced to 1000 for the ABM. To change it back, simply edit the `m` field in `MigrationGroups.json`.
* A minor change has been manually applied to the Agent class; see line 254 of `MigrationAgent.py` in the `ConflictRule`.

##### Allegheny Flu Model
* This model's population is synthetic. It is based off of the US population dataset located [here](https://gitlab.com/momacs/dataset-pop-us-2010-midas). The actual data used here is in the `Data` directory.
* This PRAM stores results in an SQLite3 database, located in `output`. This is not used by the ABM. 
* Plotting the PRAM is done in a separate file named `plot_pram.py`.
* Two specific schools are plotted: one with mostly low-income students, and one with mostly medium-income students. They are plotted on separate graphs.
* As with the Migration model, for time's sake, the ABM only runs the simulation with students from these schools (this shouldn't change the outcome much since schools do not interact at all).