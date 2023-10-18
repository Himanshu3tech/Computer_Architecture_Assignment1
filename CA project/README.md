# Evaluating performance of different Branch Predictors on SPEC Benchmarks

## Introduction
We will Champsim simulator to evaluate performance of our branch predictors.Champsim is a trace driven simulator which have several parameters like branch_predictor,no of cores,replacement policy,branch table e.t.c.


We Used Following SPEC Benchmarks.

|605.mcf_s-1152B.champsimtrace.xz|
|619.lbm_s-2676B.champsimtrace.xz|
|623.xalancbmk_s-592B.champsimtrace.xz|

## Below is the program files description:

### Program files for Question 1:- ###
We have three predictors to test for question 1. All the steps to get program files for question 1 is below:
1. Go to the folder named Solution_1.
2. G-share folder have implementation for G-share predictor, 
3. Perceptron folder have implementation for Perceptron predictor and
4. Tage folder have implementation for Tage predictor.

### Program files for Question 2 ###
In question 2 we are trying three variations in tage predictor:
1. Variation in number of entries in Tage table.
2. Variation in tag bit size.
3. Variation in min History and max history.
#### Program files for Variation 1 are inside folder Variation_1: ####
1. Tage_size_512 have implementation for Tage predictor variant with 512 
entries in each tage component i.e no of entries in Tage table.
2. Tage_size_2048 have implementation for Tage 2048 predictor variant 
with 2048 entries in each tage component.
3. Tage_size_8192 have implementation for Tage predictor variant with 
8192 entries in each tage component i.e no of entries in Tage table.
#### Program files for Variation 2 are inside folder Variation_2: ####
1. Tage_bitsize_7 have implementation for Tage predictor variant with tag 
bit size of 7 bits.
2. Tage_bitsize_11 have implementation for Tage predictor variant with tag 
bit size of 11 bits.
3. Tage_bitsize_15 have implementation for Tage predictor variant with tag 
bit size of 15 bits.
#### Program files for Variation 3 are inside folder Variation_3 ####
We have two sub variation for part 3 

**a) Variation in maximum history length**
Program files for max history variation available at folder 
Variation_3/max-history, inside max-history folder: 
1. Tage_max_history_64 have implementation for Tage predictor variant 
with max-history length 65.
2. Tage_max_history_131 have implementation for Tage predictor 
variant with max-history length 131.
3. Tage_max_history_255 have implementation for Tage predictor 
variant with max-history length 255.
**b) Variation in minimum history length**
Program files for max history variation available at folder 
Variation_3/max-history, inside max-history folder: 
1. Tage_min_history_5 have implementation for Tage predictor variant 
with minimum history length 5.
2. Tage_min_history_10 have implementation for Tage predictor variant 
with minimum history length 10.
3. Tage_min-history_40 have implementation for Tage predictor variant 
with minimum history length 40.
### Program files for Question 3 ###
Program files for hybrid predictors are in folder Solution_3
1. Hybrid_30 contains implementation for hybrid predictor with 30 percent 
budget allocation for Perceptron predictor and 70 percent budget 
allocation for Tage predictor.
2. Hybrid_50 contains implementation for hybrid predictor with 50 percent 
budget allocation for Perceptron predictor and 50 percent budget 
allocation for Tage predictor.
3. Hybrid_70 contains implementation for hybrid predictor with 70 percent 
budget allocation for Perceptron predictor and 30 percent budget 
allocation for Tage predictor.



Now we will look at how to test predictors against given traces

Step 1. Get open source code for Champsim simulator 
```
    $ git clone https://github.com/ChampSim/ChampSim.git

```
Step 2. Download dependencies for Champsim
```
    $ git submodule update --init
    $ vcpkg/bootstrap-vcpkg.sh
    $ vcpkg/vcpkg install

```
Step 3 . Go to Champsim/btb folder. Open basic_btb.cc file.

Step 4 . As we have budget constraint of having 2048 entries in btb. Update entry 
BTB_SET to 512 and BTB_WAY =4.

Step 5. Take the program file of needed predictor that you want to test from 
appropriate folders mentioned above and paste it inside Champsim/branch folder.

Step 6:- Open champsim_config.json file present inside Champsim folder.

Step 7:- Set branch_predictor to the name of folder which contains implementation 
for predictor that need to be tested and save the file.

Step 8. Run below command to make binary executable file for champsim.
$ ./config.sh champsim.config.json
$ make 
Above command will create a binary executable file inside Champsim/bin folder.

Step 9 :- Run below command 
``` 
    $ bin/champsim –warmup-instructions 200000000 –simulation-instructions 
    500000000 ~/path/to/traces/trace_name

```
where “champsim” is the binary executable we got from previous step.
“~/path/to/traces” is the path to the folder which contain traces.
“trace_name” is name of the trace on which predictor will be tested.

Step 10:- Note the MPKI,IPC and Accuracy reported by predictor


