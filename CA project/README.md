# Evaluating performance of different Branch Predictors on SPEC Benchmarks

## Introduction
We will Champsim simulator to evaluate performance of our branch predictors.Champsim is a trace driven simulator which have several parameters like branch_predictor,no of cores,replacement policy,branch table e.t.c.


We Used Following SPEC Benchmarks.

| 605.mcf_s-1152B.champsimtrace.xz|
|--|
| 619.lbm_s-2676B.champsimtrace.xz|
|--|
| 623.xalancbmk_s-592B.champsimtrace.xz|

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
** a) Variation in maximum history length **
Program files for max history variation available at folder 
Variation_3/max-history, inside max-history folder: 
1. Tage_max_history_64 have implementation for Tage predictor variant 
with max-history length 65.
2. Tage_max_history_131 have implementation for Tage predictor 
variant with max-history length 131.
3. Tage_max_history_255 have implementation for Tage predictor 
variant with max-history length 255.
** b) Variation in minimum history length **
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


###  502.gcc_r

    perf stat -I 15 -o per_out_502.txt -e cpu-cycles,instructions,l1d.replacement,dTLB-load-misses,dTLB-store-misses,iTLB-load-misses,l2_rqsts.all_demand_miss,longest_lat_cache.miss,br_inst_retired.all_branches,frontend_retired.itlb_miss,itlb_misses.walk_completed,dtlb_load_misses.walk_completed,dtlb_store_misses.walk_completed,branch-misses exe/cpugcc_r_base.mytest-m64 data/refrate/input/gcc-pp.c -O3 -finline-limit=0 -fif-conversion -fif-conversion2 -o gcc-pp.opts-O3_-finline-limit_0_-fif-conversion_-fif-conversion2.s

We truncated All ' , ' From the Number so that we can easily convert it into python float data type

    tr -d ',' < per_out_502.txt > perout1_502.txt

###  523.xalancbmk_r

    perf stat -I 15 -o per_out.txt -e cpu-cycles,instructions,branch-misses,cache-misses,L1-dcache-loads,L1-dcache-load-misses,L1-dcache-stores,L1-dcache-store-misses,L1-dcache-prefetches,L1-dcache-prefetch-misses,L1-icache-loads,L1-icache-load-misses,L1-icache-prefetches,L1-icache-prefetch-misses,LLC-loads,LLC-load-misses,mem-loads,mem-stores,l2_rqsts.code_rd_miss,l2_rqsts.demand_data_rd_miss,l2_rqsts.rfo_miss,l1d_pend_miss.pending,frontend_retired.l1i_miss,frontend_retired.itlb_miss,frontend_retired.stlb_miss exe/cpuxalan_r_base.mytest-m64 -v data/refrate/input/t5.xml data/refrate/input/xalanc.xsl

    tr -d ',' < per_out.txt > perout1_523.txt

###  526.blender_r

    perf stat -I 15 -o per_out_526.txt -e cpu-cycles,instructions,branch-misses,cache-misses,L1-dcache-loads,L1-dcache-load-misses,L1-dcache-stores,L1-dcache-store-misses,L1-dcache-prefetches,L1-dcache-prefetch-misses,L1-icache-loads,L1-icache-load-misses,L1-icache-prefetches,L1-icache-prefetch-misses,LLC-loads,LLC-load-misses,mem-loads,mem-stores,l2_rqsts.code_rd_miss,l2_rqsts.demand_data_rd_miss,l2_rqsts.rfo_miss,l1d_pend_miss.pending,frontend_retired.l1i_miss,frontend_retired.itlb_miss,frontend_retired.stlb_miss exe/blender_r_base.mytest-m64 data/refrate/input/sh3_no_char.blend --render-output sh3_no_char_--threads1 -b -F RAWTGA -s 849 -e 849 -a


     tr -d ',' < per_out_526.txt > perout1_526.txt

### 544.nab_r

    perf stat -I 15 -o per_out_526.txt -e cpu-cycles,instructions,branch-misses,cache-misses,L1-dcache-loads,L1-dcache-load-misses,L1-dcache-stores,L1-dcache-store-misses,L1-dcache-prefetches,L1-dcache-prefetch-misses,L1-icache-loads,L1-icache-load-misses,L1-icache-prefetches,L1-icache-prefetch-misses,LLC-loads,LLC-load-misses,mem-loads,mem-stores,l2_rqsts.code_rd_miss,l2_rqsts.demand_data_rd_miss,l2_rqsts.rfo_miss,l1d_pend_miss.pending,frontend_retired.l1i_miss,frontend_retired.itlb_miss,frontend_retired.stlb_miss exe/nab_r_base.mytest-m64 1am0 1122214447 122

    tr -d ',' < per_out_544.txt > perout1_544.txt




## How To Use Data to plot Linear Regression
Unzip the Problem_2 Folder.

    cd Problem_2

Now We have .txt File of the benchmark output.
We Have to give path of that txt file as input to the Main.py.
All the Text files are in Test folder.We can use Any one of those text file.
It will take text file and then internally it will create csv file from that text file.
And Do Linier Regression using csv and give various parameters as output.
And also plot CPI Stack and Residual Plot.

    python3 Main.py path/to/text/file

## Output

We Have All Parameters like RMSE , F State , P-value , R Square etc.
And We have Stack Graph of Cpi and get Residuals Plot.

    Base :  0.15327224279399115
    Mean Square Error: 0.03509010472581555
    R_Square :  0.9351548068220135
    Adj :  0.9345556212587671
    fstat : 660.1770591848838
    Predicted :  0.4184557996221837
    True : 0.5512553770464241
    P value : 1.1102230246251565e-16



