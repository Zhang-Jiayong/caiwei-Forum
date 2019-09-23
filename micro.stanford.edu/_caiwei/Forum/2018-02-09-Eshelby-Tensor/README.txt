***************************************************************************************

Wei Cai, caiwei@stanford.edu

This directory provides matlab codes that calculates the Eshelby tensor for arbitrary ellipsoidal inclusion in isotropic and anisotropic media and its eigenvalues.  The codes verify that all eigenvalues are real and between 0 and 1, and the sum of the 6 eigenvalues always equal 3.

Reference: 
Barnett, D.M., Cai, W., Properties of the Eshelby Tensor and Existence of the Equivalent Ellipsoidal Inclusion Solution, J. Mech. Phys. Solids, resubmitted (2018).

****************************************************************************************
Test cases:

test_eshelby_tensor_eig_iso.m
    Compute eigenvalues for Eshelby tensor in isotropic medium, based on analytic expressions implemented in eshelby_tensor_iso.m.
    By default, it only plots the previously computed data saved in 'eig_SE_iso_data.mat'.
    To re-run calculations, change 
       if (1)
    to
       if (0)
    The number of cases is specified in variable N_test (default = 100).
    The tolerance of numerical integration is specified by tol (default = 1e-5).

test_eshelby_tensor_eig_cubic.m
    Compute eigenvalues for Eshelby tensor in anisotropic medium with cubic symmetry, based on numerical quadrature implemented in eshelby_tensor_aniso.m.
    By default, it only plots the previously computed data saved in 'eig_SE_cubic_data_2.mat'.
    To re-run calculations, change 
       if (1)
    to
       if (0)
    The number of cases is specified in variable N_test (default = 500).
    The tolerance of numerical integration is specified by tol (default = 1e-5).

test_eshelby_tensor_eig_aniso.m
    Compute eigenvalues for Eshelby tensor in anisotropic medium with randomly chosen (positive definite) elastic stiffness tensor, based on numerical quadrature implemented in eshelby_tensor_aniso.m.
    By default, it only plots the previously computed data saved in 'eig_SE_aniso_data.mat'.
    To re-run calculations, change 
       if (1)
    to
       if (0)
    The number of cases is specified in variable N_test (default = 1).
    The tolerance of numerical integration is specified by tol (default = 1e-5).

test_eshelby_tensor_eig_triclinic.m
    Compute eigenvalues for Eshelby tensor in anisotropic medium with a class of triclinic symmetry, based on numerical quadrature implemented in eshelby_tensor_aniso.m.
    By default, it only plots the previously computed data saved in 'eig_SE_triclinic_data.mat'.
    To re-run calculations, change 
       if (1)
    to
       if (0)
    The number of cases is specified in variable N_test (default = 5).
    The tolerance of numerical integration is specified by tol (default = 1e-5).

