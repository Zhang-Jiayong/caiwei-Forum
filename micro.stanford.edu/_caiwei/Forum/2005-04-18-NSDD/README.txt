**************************************************************
Wei Cai, caiwei@stanford.edu

This directory provides matlab codes that implement the 
non-singular expressions for stress field, self and interaction
energies of straight dislocation segments in an isotropic
elastic medium.

Singularity is removed by allowing the dislocation core to 
spread isotropically in space (specified by width a).

Ref: Wei Cai, Athanasios Arsenlis, Christopher R. Weinberger and Vasily V. Bulatov
     A non-singular continuum theory of dislocations
     J. Mech. Phys. Solids (2005)

The codes here can be used in Dislocation Dynamics (DD) simulations.
However, they do not consistute a complete DD simulation.  The 
purpose of this package is to provide the stress, energy, force 
calculation tools for education and exploratory research purposes, 
e.g. on the nature of dislocation interactions.

A stand-alone matlab package for DD simulations is provided 
elsewhere.  While it uses the tools provided here, further
optimizations are required that make the codes more difficult
to understand than the ones provided here.

**************************************************************
Test utilities

testloop.m
 self-consistency check for a circular dislocation loop
 compute energy, and nodal driving force
 force are computed in three ways (they should all agree):
  by numerically integrating stress field
  by analytic formula (of the above integration)
  by numerically differentiating energy

testtetra.m
 self-consistency check for a random dislocation tetrahedra
 compute energy, and nodal driving force
 force are computed in three ways as above (they should all agree)
 For data structure of dislocation network, see elasticenergy.m

**************************************************************
Stress calculation tools

calsegstr3da.m

 Provides: function s=calsegstr3da(MU, NU, b, r1, r2, r, a)
           % s(3,3)=calsegstr3d2a(MU, NU, b(3), r1(3), r2(3), r(3), a)

 Computes the stress field of a straight dislocation segment going
 from r1 to r2 with Burgers vector b. 
 MU is shear modulus, NU is Poisson ratio, a is core spread radius
 r1, r2, r, b are all vectors of length 3.  MU, NU, a are scalars.
 The return value s is a 3x3 array for the stress tensor.

 This function calls function calsegstrhor3da.m, which calculates
 the stress field of a dislocation segment lying on z-axis.

 When a=0, the function reduces to the original singular expression
 given in Hirth-Lothe (Theory of Dislocations, 1982, p.133), which 
 is implemented in calsegstr3d2.m for comparison.

**************************************************************
Energy calculation tools

loopenergy.m
 Provides: function E=loopenergy(MU,NU,b,rn,a)
           Easier to use but only apply to loops

 Computes total elastic energy (E) of a dislocation loop.
 The loop is specified by an array of node positions: rn.
 The segment from each node to the next one has Burgers vector b.
 MU is shear modulus, NU is Poisson ratio, a is core spread radius.

elasticenergy.m

 Provides: function E = elasticenergy(MU,NU,a,rn,links)
           Applies to general dislocation network

 Computes total elastic energy (E) of an arbitrary dislocation network
 The dislocations are specified by rn (nodal positions)
    and links (connectivity and Burgers vector)
 MU is shear modulus, NU is Poisson ratio, a is core spread radius
 The data structures of rn and links array are described
 in detail in the comment section of this function

[Supporing functions]

engself.m
 Provides: function [fs0,fs1]=selfforce(MU,NU,b,r0,r1,a)

 Computes self energy of a dislocation segment r0-r1 with Burgers vector b
 MU is shear modulus, NU is Poisson ratio, a is core spread radius

enginteract.m
 Provides: function W=enginteract(MU,NU,b1,b2,r1,r2,r3,r4,a)

 Computes interaction energy between two straight dislocation segments
 r1-r2 (Burgers vector b1) and r3-r4 (Burgers vector b2)
 MU is shear modulus, NU is Poisson ratio, a is core spread radius

**************************************************************
Node force calculation (by numerical integration of stress field)

loopnodeforce_strint.m
 Provides: function fn=loopnodeforce_strint(MU,NU,b,rn,a,nsub,nsubn)

 Computes driving force on all nodes in a dislocation loop,
 by numerically integrating stress on dislocation segments.
 The loop is specified by an array of node positions: rn.
 The segment from each node to the next one has Burgers vector b.
 MU is shear modulus, NU is Poisson ratio, a is core spread radius.
 nsub is the subdivision points on a segment when integrating 
    the stress field from remote segments.
 nsubn is the subdivision points on a segment when integrating
    the stress field from its two neighboring segments.
 The contribution from self stress field is computed from analytic
    expressions.


nodeforce_strint.m
 Provides: function fn=nodeforce_strint(MU,NU,a,rn,links,nsub,nsubn,sigext)

 Computes driving force on all nodes in an arbitrary dislocation loop.
 Similar to loopnodeforce_strint, except that dislocation now specified
    by two arrays: rn and links.  
 External stress (sigext) can also be applied.
 Uses function: selfforce, hingeforce_strint, remoteforce_strint


[Supporing functions]

selfforce.m
 Provides: function [fs0,fs1]=selfforce(MU,NU,b,r0,r1,a)

 Computes driving force on two end nodes of a segment due to self stress
 MU is shear modulus, NU is Poisson ratio, b(3) is Burgers vector
 r0(3) is position of one node, r1(3) is position of the other node
 a is core spread radius

pkforce.m
 Provides: function f=pkforce(sigext,b01,r0,r1)

 Computes nodal force on dislocation segment r0-r1 due to applied stress sigext
 Burgers vector of this segment is b01.
 Both nodes will experience the same force f/2. 


remoteforce_strint.m
 Provides: function [f0,f1]=remoteforce_strint(MU,NU,b01,r0,r1,b23,r2,r3,a,nsub)

 Computes force on two nodes of segment r0-r1 (Burgers vector b01)
 due to segment r2-r3 (Burgers vector b23) by numerically integrating the 
 stress field of segment r2-r3 on segment r0-r1.
 MU is shear modulus, NU is Poisson ratio, a is core spread radius
 nsub is the subdivision points for numerical integration
 
hingeforce_strint.m
 Provides: function [f0,f1,f2]=hingeforce_strint(MU,NU,b1,b2,r0,r1,r2,a,nsub)

 Computes force on three nodes r0-r1-r2 forming a hinge 
 Burgers vector of segment r0-r1 is b1, Burgers vector of segment r1-r2 is b2
 MU is shear modulus, NU is Poisson ratio, a is core spread radius
 nsub is the subdivision points for numerical integration

**************************************************************
Node force calculation (using analytic expressions)

[Stress field integration above is obtained analytically]

loopnodeforce_analyt.m
 Provides: function fn=loopnodeforce_analyt(MU,NU,b,rn,a)

 Computes driving force on all nodes in a dislocation loop.
    by analytic expressions of stress integral.
 Uses function: ..., ..., ...

**************************************************************
Node force calculation (by numerically differentiating energy)

[To demonstrate self-consistency. Not recommended in real calculation]

loopnnodeforce_engdif
 Provides: function fn=loopnodeforce_engdif(MU,NU,b,rn,a,i,Delta)

 Computes driving force on all nodes (for i==0) in a dislocation loop,
 by finite difference of elastic energy.
 The loop is specified by an array of node positions: rn.
 The segment from each node to the next one has Burgers vector b.
 MU is shear modulus, NU is Poisson ratio, a is core spread radius.
 Delta is the step size of finite difference.
 For i>0, only the force for node i is computed

nodeforce_engdif.m
 Provides: function fn=nodeforce_engdif(MU,NU,a,rn,links,i,Delta)

 Computes driving force on all nodes (for i==0) in an arbitrary
 dislocation network by finite difference of elastic energy.
 The dislocation is specified by two arrays: rn and links
 See elasticenergy for explanation of rn and links.
 MU is shear modulus, NU is Poisson ratio, a is core spread radius.
 Delta is the step size of finite difference.
 For i>0, only the force for node i is computed
