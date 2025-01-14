---
layout: archive
title: "Graduate Research"
permalink: /grad_research/
author_profile: false
sidebar:
  title: "Graduate Research"
  nav: current_res_sidebar
---
{% include base_path %}
_(This page might take a few seconds to load. Thank you for your patience!)_

# _Introduction_
<hr style="border:2px solid grey">

My master's research focused on formulating frameworks to design transfer trajectories between periodic orbits by leveraging quasi-periodic orbits (QPOs) and their associated manifolds. 

The trajectory and orbit design in a multi-body gravitational system is a challenging task due to chaotic dynamics and numerical complexities. However, certain assumptions can be made to aid in the description and analysis of the dynamics of a spacecraft for preliminary design, which enables the realization of dynamical structures that can then be utilized to systematically design desired trajectories and orbits. I employed the Circular Restricted Three Body Problem (CR3BP) to model the dynamics of a spacecraft under the influence of two primaries.

The CR3BP is a hamiltonian system, hence, the dynamical systems theory is leveraged to obtain fundamental solutions and their manifolds to characterize the global dynamics. The three types of fundamental solutions are the equilibrium, periodic and quasi-periodic solutions. The construction of QPOs to realize the said applicaitons begins by identifying the Lagrange points, which are the equilibrium solutions, and periodic orbit families.
<br>
<br>

# _Lagrange Points and Periodic Orbits_
<hr style="border:2px solid grey">

The Lagrange points are trivial to compute and there exist five of them in any system in the CR3BP model, namely L1, L2, L3, L4, and L5. Periodic and quasi-periodic orbits can be computed around the points to enable space exploration, economy, and surveillance. Periodic Orbits have a key characteristic, as their name suggests, that a spacecraft in orbit returns to its initial state after a finite period. The computation of periodic orbits is challenging due to the chaotic dynamics and lack of a useful analytical solution. Thus, [numerical methods](https://github.com/DhruvJ22/Numerical-Methods) are used to obtain families of orbits and orbits with desired characteristics. A part of my research code can be found [here](https://github.com/DhruvJ22/Astrodynamics_Research), which can be used to compute the Lagrange points and the periodic orbit families. 

NASA [CAPSTONE](https://www.nasa.gov/directorates/spacetech/small_spacecraft/capstone/) and [ARTEMIS 1](https://www.nasa.gov/image-feature/artemis-i-map) mission leveraged a L2 Halo and a DRO orbit in the Earth-Moon system respectively. The _L2 Halo orbit family_(left) and _DRO family_(right), whose members were utilized for the two missions, are plotted below using my publicly available [code](https://github.com/DhruvJ22/Astrodynamics_Research) and the family members are colored by Jacobi Constant. 

<figure class="half">
    <figcaption>These are interactive plots. Hold and drag the cursor to change the view and zoom</figcaption>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://dhruvj22.github.io/Astrodynamics_Research/example_plots/EM_L2_HaloS_family.html" height="450" width="50%"></iframe>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://dhruvj22.github.io/Astrodynamics_Research//misc/EM_DRO_family.html" height="450" width="50%"></iframe>
</figure>
The periodic orbits have various applications, as exemplified by the above two NASA missions, and are essential in identifying quasi-periodic orbits. 
<br>
<br>

# _QPOs and their Applications_
<hr style="border:2px solid grey">

Quasi-periodic orbits are a higher dimensional solutions than periodic orbits of the CR3BP. A spacecraft in the orbit is bounded to a surface of quasi-periodic solutions but it does not return to a previously traversed state. The orbits are non-trivial to compute because of the dynamical and numerical complexities. Nonetheless, with the recent improvements in our understanding of the dynamics and computational power, it is feasible to compute the orbit families and leverage them in mission design. The below animation depicts how a spacecraft(red) traverses a QPO (blue surface) and its 2D projections: 

![DJ Animation]({{ site.baseurl }}/files/em_l1_quasilyap_JC_3_01_projections.gif){: .align-center}

The computation of QPO involves using multiple shooting with multiple nodes to target the quasi-periodic behavior and then utilizing a numerical continuation scheme to compute three different families of QPOs. Despite their complexities, they fundamentally expand the solution space, which makes them an attractive choice to host spacecrafts, formation flying, and transfer design. I have worked on recreating some of the applications and I have been able to come up with two novel frameworks that leverage their assocuated manifolds, as detailed in my [thesis](https://hammer.purdue.edu/articles/thesis/Transfer_Trajectory_Design_Strategies_Informed_by_Quasi-Periodic_Orbits/24718713/1) and a [conference paper](https://engineering.purdue.edu/people/kathleen.howell.1/Publications/Conferences/2024_AIAA_JaiHow.pdf). 
<br>

## 1. Host Orbit

[James Webb Space Telescope (JWST)](https://webb.nasa.gov/) is the most recent example of a mission that uses a QPO as a host orbit. The telescope is hosted in a [Sun-Earth L2 Quasi-Halo orbit](https://jwst-docs.stsci.edu/jwst-observatory-characteristics/jwst-orbit). I was able to recreate the orbit(green) and how the trajectory(grey) of the telescope(red point on orbit) evolves using the CR3BP model as shown below

![image-center]({{ site.baseurl }}/files/jwst_10revs.gif){: .align-center}
<br>

## 2. Maneuver Free Transfers

Maneuver free transfers, also known as heteroclinic transfers, between QPOs can be computed by leveraging their manifolds. The same is not guaranteed for periodic orbits because of their lower dimensionality than QPOs. The construction of these types of transfers relies on identifying a good initial guess, which was done by using a Poincare map and k-d tree, and differential correction. The following interactive plot shows 2 maneuver-free trajectories(yellow and green) that can be used to travel from a L2-Quasi Halo orbit(red) to get to a L1 Quasi-Halo Orbit(blue), JC = 3.13.

<figure>
    <figcaption>This is an interactive plot. Hold and drag the cursor to change the view and zoom</figcaption>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://dhruvj22.github.io/Astrodynamics_Research//misc/EM_L2qHalo_L1qHalo_JC_3_13_heteroclinc2tramsfers.html" height="550" width="100%"></iframe>
</figure>

## 3. Transfers between Periodic Orbits, informed by QPOs

The existence and method to compute QPOs have been known since the 1980's and they have been leveraged in a previous [NASA mission](https://solarsystem.nasa.gov/missions/artemis/in-depth/). However, it is only recently that engineers have developed algorithms to compute QPOs and their manfiolds of desired characteristics to enable the use of QPOs directly for mission design. My work builds on these developments and purposes a few improvements to the cutting-edge algorithms to more efficiently compute transfer trajectories between periodic orbits with different stability characterisitcs. 

### A. Transfers between nearly/maringally stable periodic orbits

Stable periodic orbits lack useful transfer manifolds, hence, motivates the use of an alternate dynamical structure to inform the transfer design process. I propose a framework that leverages the stable and unstable manifolds of QPOs and decomposes the design into multiple segments to increase the number of transfer options. One such example is showcased for transfers between L2 9:2 NRHO to DRO in the Earth-Moon system and two types of transfers (interior- and exterior-type) are uncovered as plotted below, informed by a QPO:
<figure class="half">
    <figcaption>The different colored portions of the transfer trajectory are the post corrections remnanats of the segments.</figcaption>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="{{ site.baseurl }}/files/int_qvert_opt_sol_config.png" height="300" width="40%"></iframe>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="{{ site.baseurl }}/files/ext_qp2ho2_dpo_opt_sol_config.png" height="300" width="50%"></iframe>
</figure>
It is notable through this work ([1](https://hammer.purdue.edu/articles/thesis/Transfer_Trajectory_Design_Strategies_Informed_by_Quasi-Periodic_Orbits/24718713/1), [2](https://engineering.purdue.edu/people/kathleen.howell.1/Publications/Conferences/2024_AIAA_JaiHow.pdf)) that QPOs extend the number of solutions with lower maneuver costs than obtained from their underlying periodic orbits. This framework can be expanded to other types of departure and arrival orbits, and allow for intuitive addition of QPOs to inform the design of transfer trajectories. 

### B. Transfers between unstable periodic orbits in the same family

The construction of direct transfers between unstable periodic orbits in the same family is challenging as their corresponding manifolds might not offer solutions with desired geometries. Hence, two methodologies are leveraged to uncover families of two maneuver direct pathways that link different members of the same family. The first method expands on the work of Gomez et al. [1] to realize locally fuel-optimal transfers and the procedure is illustrated for a departure orbit with Az = 10,000 km and the transfers link the departure orbit with the halo orbits with higher Az values as shown below: 
<figure class="half">
    <figcaption>The departure halo orbit appears in grey in the left plot.</figcaption>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="{{ site.baseurl }}/files/halo_locally_opt_transfers.png" height="400" width="50%"></iframe>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="{{ site.baseurl }}/files/tmdv_ig_opt_Az_vs_tot_dv.png" height="450" width="50%"></iframe>
</figure>
It is notable that this method reveals a linear relationship between the maneuver cost and the parameteric diffeence between the departure and arrival orbits, and the cost of the optimal transfer is well approximated by the initial guesses. The second method utilizes the unstable manifold trajectories corresponding to constant energy families of QPOs to uncover local 1 parameter families of solutions as depicted below: 
<figure class="half">
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="{{ site.baseurl }}/files/compare_halo_unstable_transfer.png" height="380" width="50%"></iframe>
    <iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="{{ site.baseurl }}/files/compare_opt_with_qpo_cost.png" height="450" width="50%"></iframe>
</figure>

This work is detailed in my [conference paper](https://engineering.purdue.edu/people/kathleen.howell.1/Publications/Conferences/2024_AIAA_JaiHow.pdf) and can be extended to other periodic orbit families in the Earth-Moon system, as well as other systems. 

[1] Gomez, G., Jorba, A., Masdemont, A., and Simo, C., “Study of the transfer between halo orbits,” Acta Astronautica, Vol. 43,
No. 9-10, 1998, pp. 493–52.

**Technologies used**: Python(numpy, scipy, pandas, scikit-learn, plotly, matplotlib), MATLAB, C++, Git, Command Line Interface, Latex

**Concepts learned**: Dynamics Modelling, Numerical Methods, Optimization, Data Analysis, Data Visualization, Technical Communication, Automation, Software Development, Independent and Creative Work