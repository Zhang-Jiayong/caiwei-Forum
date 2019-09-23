The matlab scripts:

madsum_iso.m    (isotropic elasticity)
madsum_aniso.m  (general anisotropic elasticity)
madsum_cubic.m  (anisotropic medium with cubic symmetry)

calculates the elastic energy of a dislocation
dipole in a supercell under periodic boundary conditions
   
  Geometry:

    (x1,y1)   A-------------------------------------
               \                                    \
                \      P                             \
                 \    (-) (x2r,y2r)                   \
                  \   /                                \
                   \ /                                  \
                   (+)-----------------------------------B (x0,0)

  Input:
     C0:    C0(i,j,k,l) general elastic constant tensor (in eV/A^3,  1eV/A^3 = 160.22GPa )
     b0 = [ bx, by, bz ] Burgers vector in unit cell frame (in Angstrom)
                        e.g. b0 = [ 1 1 1 ]/2 * 3.1472 (for Molybdenum)
     M = [ e1, e2, e3 ] coordinate transformation matrix, 
                        e3 is parallel to dislocation line
     rc:   cut-off radius
     coords = [ x0, x1, y1, x2r, y2r ]
           x0            x coord of B     (0, infty)     (in A)
           x1            x coord of A     (-infty,infty) (in A)
           y1            y coord of A     (0,  infty)
           x2r   reduced x coord of P     (-0.5, 0.5]
           y2r   reduced y coord of P     (-0.5, 0.5]
    trunc = [ xcut, ycut ] truncation paramters
           -xcut:xcut times -ycut:ycut number of images will be added
     
  Output:
     Eel:  total elastic energy, Eel = Eprm + Eimg
     Eprm: primary dipole energy
     Eimg: image energy

----------------------------------------------------------------------
Binary executables (compiled for Linux i386)

 maddiso   (isotropic elasticity)
 maddaniso (anisotropic elasticity)

are earlier versions with the same function (written in C, faster but less readable)
             
For comparison, run

  matlab> testmadsumcubic
  ./maddaniso -cx=10 -cy=10 1 0.2 2 0 0.5 < phRI.dat

  matlab> testmadsumiso
  ./maddiso -cx=10 -cy=10 1 0.2 2 0 0.5

----------------------------------------------------------------------

References:

  1. Wei Cai, Atomistic and Mesoscale Modeling of Dislocation Mobility, 
     Ph. D. Thesis, Massachusetts Institute of Technology, 2001. 
     ( http://micro.stanford.edu/~caiwei/papers/CaiWeiThesis.pdf 
       p. 296, for dislocation interaction energy in anisotropic medium. )

  2. Wei Cai, Vasily V. Bulatov, Jinpeng Chang, Ju Li and Sidney Yip,
     Periodic image effects in dislocation modelling,
     Philosophical Magazine A, 83, 539 (2003).
     ( for regularization of conditional convergence )

