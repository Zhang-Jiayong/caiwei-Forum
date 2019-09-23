Description :

 This is a set of codes to compute the entanglement of formation between
 two qudits that are specified by a density matrix (rho).

 For more details, see  Ryu, Cai and Caro, "Quantum Entanglement of
  Formation between Qudits", Phys. Rev. A, 77, 052312 (2008). 

=================================================
This package include following source files

cgr7.c
util.h
util.c
optdecomp.c
testlapack.c
makefile

- - - - - -

cgr7.c optimizes decomposition by minimizing entanglement using the
       hybrid steepest descent - conjugate gradient algorithm
       (most efficient)

optdecomp.c optimizes decomposition by minimizing entanglement using the
            steepest descent algorithm (not very efficient)

util.h & util.c includes supporting functions for matrix operations.

testlapack.c some test program, please ignore

- - - - - -

1. How to Compile

  make all

  This will create executable files "cgr7" and "optdecomp".

2. How to Run 

  the command line format for running cgr7 is the following

  ./cgr7 [seed=0] [tol=1e-15] [tol1=1e-15] [N0=5] [N=8] [na=2] [Ndm=128]

  all command line values are optional and have default values
  (for an explanation of the meaning of the input parameters, see cgr7.c
   function: main())

  for example, you can run a test case as

  ./cgr7 0 1e-10 1e-10 4 8 2 3 


  (This takes about 90 seconds to finish on a Linux machine.)
  In this case, seed=0, meaning that random number generator will be
  randomized by time.  tol=1e-10 and tol1=1e-10.  

  This run will generate Ndm=3 random density matrices each with dimension
  NxN, with N=8 (default).  (N = na*nb)

  For each density matrix, the code will find N0=4 local minima.  The lowest
  minimum among these local minima will be saved in file "E_R_t_stat.dat", in
  the format of 

    E   R   t

  where E is entanglement, R is participation ratio, and t is negativity.
  In this test case, you should see 3 (new) lines in your dat file.

