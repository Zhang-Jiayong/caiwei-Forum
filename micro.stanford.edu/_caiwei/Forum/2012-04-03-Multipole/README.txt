***************************************************************************************

Jie Yin, jieyin@stanford.edu

Wei Cai, caiwei@stanford.edu


This directory provides matlab codes that implement the expressions for calculating the 
stress fields of dislocation segments in an anisotropic elastic medium using multipole
expansion. 

To calculate the segment stress field using the multipole expansion method, the derivatives
of the Green's functions need to be evaluated first.

Results are compared against exact solutions evaluated using the Willis-Steeds-Lothe(WSL)
formula.

Reference: 
Yin J., Barnett, D.M., Fitzgerald S.P., Cai, W., Computing Dislocation Stress Field
using Multipole Expansions, Model. Sim. Mater. Sci. Eng. in press (2012).

****************************************************************************************
Test cases:

compute_dnGr_sparse.m
    Compute derivatives of Green's function to arbitrary order (up to 12).
    This program implements the fastest algorithm in this folder.

    To run it, type, e.g.
     clear all
     mat = 'Mo'; dG_order = 8; Nint = 21; compute_dnGr_sparse;
     Gr_np = dnGr_full; 
     save dG8_Mo_100_21 Gr_np

    This computes the derivatives up to 12-th order for Mo using 21 integration points.
    The results is then saved in a file that can be used in future stress evaluations, e.g.
    in plot_disl_loop_stress.m.

compare_dnGr_sparse_vs_fast.m
    Compare two algorithms to compute the derivatives of the Green's function.
    - dnGreen_sparse.m (the preferred method)
    - dnGreen_fast.m   (not so fast actually...)

    To run it, type, e.g.
      clear all
      mat = 'Na'; dG_order = 3; Nint = 41; compare_dnGr_sparse_vs_fast

    This computes the derivatives up to 3rd order for Na using 41 integration points.
    The default values are specified at the beginning of compare_dnGr_sparse_vs_fast.m

    Note that using dnGreen_sparse.m we can compute the derivatives up to 12-th order
    within 2 minutes.  But dnGreen_fast.m would be very slow above 6-th order.
    So don't run compare_dnGr_sparse_vs_fast.m above 6-th order.

plot_disl_loop_stress.m
    compute the stress field of a dislocation loop using multipole expansion
    and compare results with exact solutions from the WSL formulat

    To run it, type
      clear all
      plot_disl_loop_stress

    You can choose mat, dG_order, Nint, MT_ORDER in the first line by
    commenting/uncommenting various lines.
    
    If the necessary file containing the derivatives of Green's function
    does not exist, the code will automatically compute them and create the file.
    
plot_stress_discont.m
    compute the stress field of a dislocation loop using multipole expansion
    and evaluate the discontinuity at cell boundary
    
    To run it, type
      clear all
      plot_stress_discont

    You can choose mat, dG_order, Nint, MT_ORDER in the first line by
    commenting/uncommenting various lines.
    
    If the necessary file containing the derivatives of Green's function
    does not exist, the code will automatically compute them and create the file.


