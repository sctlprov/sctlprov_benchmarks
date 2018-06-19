# 1 Introduction

The repository contains CTL benchmark files for model checker [Verds](http://lcs.ios.ac.cn/~zwh/verds/index.html), [NuSMV](http://nusmv.fbk.eu/), [NuXMV](https://nuxmv.fbk.eu/), theorem prover [iProver Modulo](http://www.ensiie.fr/~guillaume.burel/blackandwhite_iProverModulo.html.en), and our tool [SCTLProV](https://github.com/terminatorlxj/SCTLProV). The benchmarks consists of two set of programs: randomly generated boolean program, and fairness programs.

## 1.1 Randomly generated programs
Benchmark #1, #2, and #3 are all randomly generated programs. 

- The original description of benchmark #1 is in the website of model checker [Verds](http://lcs.ios.ac.cn/~zwh/verds/verds_pdf/verds1.30eeq.pdf) and also restated in the file `description.md` of the folder `random_programs`.
- Based on benchmark #1, we extend the number of variables to tens, hundreds, and even thousands in benchmark #2 and #3.
- For benchmark #3, the input files for iProver Modulo is not presented here. It is due to the fact that these input files are too large to upload (more than 26GB in total). However, thanks to Kailiang Ji (the author of the paper "CTL Model Checking in Deduction Modulo" that describe the use of iProver Modulo in CTL model checking), interested readers may refer to this little [converting tool](https://github.com/kailiangji/SMV2TPTP) that can convert `.smv` files into `.p` files for iProver Modulo.


The randomness of the test cases in three benchmarks makes it rather fair for different CTL model checking approaches, and helps us recognize the strengths and weaknesses of each tool. 

## 1.2 Fairness programs

Benchmark #4 is also based on a [benchmark](http://lcs.ios.ac.cn/~zwh/verds/verds_code/bp12.rar) on the Verds website. We added input files for SCTLProV in benchmark #4.
Benchmark #4 consists of two sets of concurrent programs: the mutual exclusion algorithms and the ring algorithms. The description of the fairness programs are in the file `description.md` of the folder `fairness_programs`.

Both kinds of algorithms consist of a set of concurrent processes running in parallel, and some formulae to be verified. Each formula in the algorithms needs to be verified under the fairness constraint that each process does not starve, i.e., no process waits infinitely often.

# 2 Program generators

### 2.1 Randomly generated progrems

The OCaml programs to generate the randomly programs are in the folder `random_programs_generator`:

1. `generator_p1.ml`: for concurrent processes;
2. `generator_p2.ml`: for concurrent sequential processes.

### 2.2 Fairness programs

The OCaml programs to generate the fairness programs are in folder `fairness_programs_generator`:

1. `generate_mutual.ml`: for mutual exclusion algorithms;
2. `generate_ring.ml`: for ring algorithms.

# 3 Test these examples

## 3.1 Run test cases one-by-one

- Files with `.vvm` in the extension is in the input format 
  of the model verifier verds. Run these examples using command

  	verds -QBF \<filename\> 

- Files with `.smv` in the extension is in the input format of the model verifier NuSMV and NuXMV. Run these examples using command

   NuSMV -dcx \<filename\>
   or

   	NuXMV -dcx \<filename\>

- Files with `.model` in the extension is in the input format of the model verifier SCTLProV. Run these examples using command

   sctl \<filename\>
   or

   	sctl -bdd \<filename\>

- Files with `.p` in the extension is in the input format of the theorem prover iProver Modulo. Run these examples using command

   iproveropt  \`cat basic_resolution_options\`  --modulo true --res_passive_queue_flag false --res_lit_sel ctl_sel  \<filename\>


## 3.2 Testing script 
See the [this repository](https://github.com/sctlprov/sctlprov_testing).