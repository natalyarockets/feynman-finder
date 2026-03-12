# Frontier Map: Ion Evaporation in Ionic Liquid Ion Sources

## The Landscape

Ionic liquid ion sources (ILIS) exploit the remarkable property that room-temperature molten salts---ionic liquids (ILs)---can be made to emit pure ion beams under sufficiently strong electric fields, without the formation of droplets characteristic of conventional electrospray [1][2]. This "pure ionic regime" (PIR) is prized for spacecraft micro-propulsion (high specific impulse, precise thrust) [3][4], focused ion beam nanofabrication [5], and reactive ion etching [6]. The central physical process enabling all of these applications is **field-assisted ion evaporation from a curved liquid-vacuum interface**.

Despite three decades of work since Romero-Sanz, Fernandez de la Mora, and collaborators first demonstrated pure ion emission from IL Taylor cones [7], and despite increasingly sophisticated computational models [8][9][10], the fundamental theory of ion evaporation from ionic liquids remains incomplete. The field operates with a patchwork of semi-empirical rate equations, continuum approximations applied at the nanoscale, and molecular dynamics simulations whose connection to macroscopic observables is mediated by poorly constrained bridging assumptions.

This report maps the governing equations, traces their assumptions to root causes, identifies the highest-leverage theoretical branch points, and proposes research directions where genuine first-principles progress is possible.

---

## Key Governing Equations

### 1. The Ion Evaporation Rate (Iribarne-Thomson / Field-Enhanced Thermionic Emission)

The central equation governing ion emission from a liquid surface under electric field is [11][12][13]:

$$\Gamma = \frac{k_B T}{h} \exp\left(-\frac{\Delta G^*}{k_B T}\right)$$

where the activation free energy barrier is:

$$\Delta G^* = \Delta G_{\text{solv}} - \Delta G_{\text{Schottky}}(E) \approx \Delta G_{\text{solv}} - \sqrt{\frac{e^3 E_n}{4\pi\varepsilon_0}}$$

The Schottky barrier-lowering term reduces the activation energy approximately as $\sqrt{E_n}$, where $E_n$ is the electric field normal to the surface.

### 2. Taylor Cone Equilibrium

The static balance between electric stress and surface tension yields Taylor's cone with half-angle 49.3 degrees [14]:

$$\frac{1}{2}\varepsilon_0 E_n^2 = \gamma \kappa$$

where $\gamma$ is surface tension and $\kappa$ is surface curvature. The 49.3-degree angle emerges from solving $P_{1/2}(\cos\theta_0) = 0$ under the assumptions of (i) equipotential conical surface, (ii) perfect static equilibrium, (iii) no space charge, and (iv) no ion emission [14].

### 3. Fernandez de la Mora Scaling Law

For the current emitted from a Taylor cone-jet [15][16]:

$$I \propto (\gamma K Q)^{1/2}$$

where $K$ is electrical conductivity and $Q$ is volumetric flow rate. This scaling breaks down at conductivities above ~1 S/m precisely because ion evaporation from the meniscus (rather than the jet) becomes the dominant emission mechanism [16].

### 4. Electrohydrodynamic (EHD) Model Equations

The Coffman-Lozano-Gallud model solves coupled equations [8][9][10]:

- **Stokes flow** in the liquid (low Reynolds number): $\nabla p = \mu \nabla^2 \mathbf{u} + \rho_e \mathbf{E}$
- **Laplace equation** in vacuum: $\nabla^2 \phi = 0$
- **Poisson equation** in liquid: $\nabla \cdot (\varepsilon \nabla \phi) = -\rho_e$
- **Charge conservation**: $\frac{\partial \rho_e}{\partial t} + \nabla \cdot (K \mathbf{E} + \rho_e \mathbf{u}) = 0$
- **Stress balance at interface**: $[[\mathbf{T}_E + \mathbf{T}_H]] \cdot \hat{n} = \gamma \kappa \hat{n}$

The ion evaporation rate enters as a **boundary condition** on the surface charge equation [9][10].

### 5. Born Solvation Energy

$$\Delta G_{\text{solv}}^{\text{Born}} = -\frac{e^2}{8\pi\varepsilon_0 a}\left(1 - \frac{1}{\varepsilon_r}\right)$$

where $a$ is the effective ionic radius and $\varepsilon_r$ is the dielectric constant [17][18].

---

## Key Empirical Breakdowns

| Parameter / Model Element | Classification | Status | Root Issue |
|---|---|---|---|
| Pre-exponential factor $k_BT/h$ in evaporation rate | Semi-empirical (TST assumption) | Assumed, not validated for IL surfaces | TST assumes equilibrium at transition state; questionable at ~1 V/nm fields |
| Solvation free energy $\Delta G_{\text{solv}}$ in ILs | Empirical / poorly constrained | Born model fails qualitatively for ILs [18] | ILs are not dielectric continua; ionic strength breaks Born assumptions |
| Schottky barrier lowering $\propto \sqrt{E}$ | Semi-empirical (image charge model) | Classical; validity at nm-scale unproven | Uses macroscopic image charge in a medium that has molecular structure |
| Effective ionic radius $a$ | Empirical | Not well-defined for polyatomic IL ions | Shape and charge distribution of EMI+, BF4- are far from spherical |
| Electric field at emission site $E_n$ | Derived (from EHD model) | Model-dependent | Depends on continuum assumptions at sub-nm tip radii |
| Conductivity $K$ | Measured macroscopic property | Applied locally at nm-scale | Bulk conductivity assumed constant; breaks down in structured interfacial layers [19] |
| Taylor cone angle (49.3 deg) | First principles (within assumptions) | Systematically violated by real emitting menisci [9][10] | Derivation assumes no emission, no space charge, static equilibrium |
| Cluster fragmentation rates | Empirical | Measured via RPA/TOF but mechanism unclear [20][21] | Binding energies ~1 eV; fragmentation competes with evaporation |
| Electrochemical window / degradation rate | Empirical | Critical for lifetime; poorly predicted [22][23] | Couples ion evaporation to electrochemistry at emitter substrate |
| Liquid permittivity $\varepsilon_r$ in ILs | Measured, but context-dependent | Static $\varepsilon_r \sim 10$-15, but frequency/field-dependent [18] | IL permittivity concept itself is problematic at molecular scales |

---

## The Assumption Tree

### Branch 1: Continuum Electrostatics at the Emission Site

**Assumption chain:**
1. The liquid-vacuum interface is a sharp, smooth boundary (continuum)
2. The electric field at the surface can be computed from solving Laplace/Poisson equations with bulk material properties
3. The departing ion interacts with the surface via a classical image charge
4. This image charge produces a Schottky barrier that lowers the activation energy as $\sqrt{E}$

**Where it breaks:** MD simulations show the IL/vacuum interface has layered structure extending ~2-3 nm into the liquid [19][24]. The "surface" is not a sharp boundary but a transition zone of alternating cation-anion layers. The concept of an image charge in a molecularly structured medium is questionable. At the emission site (tip radius ~1 nm), the continuum description of the liquid itself may fail.

**Evidence of breakdown:** MD simulations find that the emitting ion must cross **two distinct energy barriers** before emission [25], not the single Schottky hump predicted by the continuum model. The critical field for emission (~1 V/nm) agrees with experiment, but this may be coincidental---the activation energy and pre-exponential factor could be individually wrong while their combination accidentally matches.

### Branch 2: The Born Model for Solvation Energy in Ionic Liquids

**Assumption chain:**
1. The ion is a charged sphere of radius $a$
2. The surrounding medium is a uniform dielectric continuum with permittivity $\varepsilon_r$
3. The solvation energy is purely electrostatic (Born model)
4. This energy must be overcome for ion extraction

**Where it breaks:** Ionic liquids are **themselves composed entirely of ions** [18]. The concept of a "dielectric constant" for a neat ionic liquid is fundamentally problematic---there is no neutral solvent providing the dielectric response. Experiments show ILs deviate strongly from Born model predictions, yielding solvation energies much larger than expected from their bulk $\varepsilon_r$ [18][26]. The high intrinsic ionic strength of ILs enhances electrostatic screening in ways the Born model cannot capture.

**Implications:** Since $\Delta G_{\text{solv}}$ appears in the exponential of the rate equation, even modest errors (~0.3 eV, which is the known Born model error for simple ions in water [17]) lead to order-of-magnitude errors in predicted evaporation rates. For ILs, the error may be much larger.

### Branch 3: Transition State Theory at Extreme Fields

**Assumption chain:**
1. Ion evaporation is a thermally activated process
2. The system is in quasi-equilibrium (TST applies)
3. The pre-exponential factor is $k_BT/h$ (~$6 \times 10^{12}$ s$^{-1}$ at 300K)
4. The activation barrier is field-dependent but temperature-independent in shape

**Where it breaks:** At fields of ~1-2 V/nm, the barrier is ~0.5-1 eV [25][27]. The barrier width is ~1 nm. These are conditions where:
- Quantum tunneling may contribute (barrier width comparable to de Broglie wavelength of ~0.1 nm for ions, so this is marginal)
- The "attempt frequency" $k_BT/h$ from TST is not validated for surface evaporation from a structured liquid
- The assumption of equilibrium at the barrier top is questionable when the field is driving the system far from equilibrium
- Coffman found "anomalously low activation energies" in certain configurations [8], suggesting the TST framework may be incomplete

### Branch 4: Decoupling of Evaporation from Meniscus Dynamics

**Assumption chain:**
1. The EHD meniscus problem and the ion evaporation problem can be solved sequentially
2. The evaporation rate is a local function of the local field
3. Back-reaction of emission on meniscus shape is captured through charge/mass conservation
4. Steady-state solutions exist and are stable

**Where it breaks:** Gallud and Lozano [10] found that stable emitting menisci exist only in a **narrow parameter window**: meniscus radii of 0.5-3 micrometers, a minimum hydraulic impedance, and a maximum current. Static stability is lost when the electric pressure exceeds twice the surface tension stress [10]. This suggests the system operates near a critical point where the decoupling assumption is most strained. Ohmic heating near the emission region further couples the problems [10].

### Branch 5: Species-Agnostic Emission Model

**Assumption chain:**
1. The evaporation rate depends on a single activation energy
2. Monomers, dimers, and trimers can be treated with the same rate equation (different $\Delta G$)
3. Cluster formation/fragmentation occurs independently of the evaporation process

**Where it breaks:** Beam composition measurements show ~45% monomers, 30-43% dimers, 13-25% trimers [20][21]. Dimer binding energies are ~1 eV [21], comparable to the activation barrier for monomer emission. This means cluster formation/fragmentation is energetically competitive with the evaporation process itself. The distinction between "evaporating a dimer" and "evaporating a monomer that immediately captures a neutral pair" is unclear. Hydrogen bonding is identified as the main cause for the much slower fragmentation rate of [EMIM-BF4] dimers compared to other ILs [21], a chemistry-specific effect invisible to the generic rate equation.

---

## Promising Branch Points (Ranked)

### 1. The Solvation Energy Problem in Neat Ionic Liquids (Highest Leverage)

**Why it matters:** $\Delta G_{\text{solv}}$ sits inside the exponential of the rate equation. It is the single most important parameter, yet the Born model used to estimate it is fundamentally inappropriate for a medium composed entirely of ions. This is not a correction-factor problem---it is a conceptual mismatch.

**Adjacent fields:** The failure of Born/continuum solvation models for ILs is well-documented in electrochemistry [18][26] but has not been systematically incorporated into ILIS theory. The electrochemistry community has developed Debye-Huckel corrections, cluster-continuum models, and explicit-solvent DFT approaches that could be adapted.

**Status:** Known problem in principle, but the ILIS community continues to use Born-derived or empirically fitted $\Delta G_{\text{solv}}$ values. No first-principles theory of ion extraction energy from a neat IL surface under field exists.

### 2. The Interface Structure Problem (High Leverage)

**Why it matters:** MD simulations reveal that IL/vacuum interfaces are layered, not sharp [19][24]. This layering extends 2-3 nm into the bulk and includes alternating cation-rich and anion-rich layers. The entire continuum EHD model---Schottky barrier, image charge, surface charge density---assumes a sharp boundary. The evaporation process happens precisely in this structured region.

**Adjacent fields:** Surface science (LEED, XPS on IL surfaces), neutron reflectometry of IL films, and the broader field of interfacial ionic liquid science have characterized this layering extensively [19][24]. Connection to ILIS theory is minimal.

**Status:** The existence of layering is well-known. Its quantitative effect on ion evaporation rates is essentially unexplored.

### 3. The Pre-Exponential Factor / Attempt Frequency Problem

**Why it matters:** The $k_BT/h$ pre-exponential from TST is ~$6 \times 10^{12}$ s$^{-1}$. This is assumed, never validated for ion evaporation from an IL surface. The analogous problem in atom probe tomography (field evaporation from metals) has seen extensive work challenging this assumption [28], with measured pre-exponential factors varying by orders of magnitude from the TST prediction.

**Feynman simplicity test:** What is the simplest system where you could directly measure the attempt frequency? A single well-characterized flat IL/vacuum interface under a uniform field, monitored by single-ion-sensitive detection. This experiment has essentially been done in MD [25][27] but not experimentally.

### 4. The Coupled Evaporation-Fragmentation Problem

**Why it matters:** If a significant fraction of the beam is dimers and trimers that subsequently fragment, then the "ion evaporation rate" measured in experiments is not the monomer evaporation rate---it is a convolution of evaporation and fragmentation. Fitting the Iribarne-Thomson rate equation to total beam current conflates two distinct processes with different physics.

**Einstein parsimony check:** The current model has separate fitted $\Delta G$ values for each species, separate fragmentation rates, and composition fractions---a large number of free parameters relative to independent predictions.

### 5. The Electrochemical Coupling Problem

**Why it matters:** Every ion that leaves must have a counterion left behind. This couples ion evaporation to electrochemistry at the emitter substrate [22][23]. The degradation rate determines practical device lifetime. Current mitigation (polarity alternation at ~1 Hz [22]) is empirical. The coupling between emission current, counterion accumulation, and electrochemical reaction kinetics is not modeled from first principles.

**Hamming's question:** This is arguably the most important *practical* problem for ILIS applications. A first-principles model would enable rational design of electrode materials, operating protocols, and IL selection for lifetime.

---

## Proposed Research Directions (Ranked)

### 1. First-Principles Ion Extraction Energy from Ionic Liquid Surfaces

**Title:** Ab initio computation of field-dependent ion extraction energies from ionic liquid surfaces

**Question:** What is the actual free energy cost to remove a specific ion (monomer, dimer) from a specific ionic liquid surface under a specific applied field, computed without the Born model or image-charge approximations?

**Why it matters:** This is the single parameter ($\Delta G^*$) that determines the evaporation rate. Every model in the field uses it; none computes it from first principles for the actual system. Getting this right would either validate the existing semi-empirical framework or reveal that the field has been fitting the wrong functional form for decades.

**Approach:** (a) Constrained ab initio MD (AIMD) of an IL slab in vacuum under external field, computing the potential of mean force for ion extraction via umbrella sampling or metadynamics. Start with EMI-BF4, the most-studied IL in ILIS. (b) Compare with classical MD using polarizable force fields. (c) Decompose the extraction energy into electrostatic, van der Waals, and reorganization contributions. (d) Map the field dependence and compare with the $\sqrt{E}$ Schottky prediction.

**Success criteria:** (i) Computed $\Delta G^*(E)$ that can be compared quantitatively with experimental evaporation rates. (ii) Identification of whether the $\sqrt{E}$ scaling holds or a different functional form emerges. (iii) Explanation of why different ILs with similar bulk properties can have very different emission characteristics.

**Risk assessment:** AIMD of IL interfaces is computationally expensive. Slab models may not capture the curvature effects present at real emitter tips. Force field accuracy for ILs under extreme fields is uncertain. **Medium risk, high reward.**

**Critical tool update (March 2025):** Machine learning force fields have recently become viable for ionic liquids, fundamentally changing the feasibility of this direction:

- **MACE** achieves near-DFT force accuracy (RMSE 0.011 eV/A) for ILs, trained on ~30k DFT structures [35]. This is 3-4 orders of magnitude cheaper than AIMD per MD step while retaining quantum accuracy.
- **DPMD** (DeePMD-kit) also works but has accuracy issues for IL density (~20% error) [35].
- A MLFF trained on ~200 DFT frames can reasonably reproduce bulk IL properties [36].
- GPU-accelerated MLFF MD can now reach microsecond timescales and million-atom systems.

**The gap:** Nobody has yet trained a MLFF for an IL/vacuum interface under external electric field. The existing MACE/DPMD work covers only bulk properties (density, diffusion, RDFs). The specific application to field evaporation is untouched.

**Revised approach:** (a) Generate DFT training data for EMI-BF4 slab in vacuum, including configurations under applied fields of 0-2 V/nm. Include both equilibrated and non-equilibrated structures (shown to be critical [35]). (b) Train a MACE potential on this dataset. (c) Run ns-scale umbrella sampling or metadynamics with the MLFF to compute the potential of mean force for ion extraction — something previously impossible with AIMD (~ps timescale) or unreliable with classical force fields. (d) Compare the resulting $\Delta G^*(E)$ with both the Born/$\sqrt{E}$ prediction and experimental rates.

This MLFF + enhanced sampling combination is the attack vector that makes this PhD viable *now* rather than in 5 years. The timing is ideal: the tools exist but the application is unexplored.

### 2. Resolving the Interface Structure-Emission Connection

**Title:** Quantitative effect of ionic liquid interfacial layering on field-evaporation dynamics

**Question:** How does the known layered structure of the IL/vacuum interface modify the energy landscape for ion extraction, and can incorporating this structure into EHD models resolve the discrepancy between predicted and measured activation energies?

**Why it matters:** The entire macroscopic modeling framework assumes a sharp interface. The actual interface has molecular-scale structure that fundamentally changes the local electric field, charge distribution, and energy barriers. This is the single largest unexamined assumption in ILIS theory.

**Approach:** (a) Use MD simulations of IL/vacuum interfaces under field to extract density-functional profiles of the interfacial region. (b) Develop a "structured interface" boundary condition for the EHD model that replaces the sharp-interface assumption. (c) Compute effective evaporation rates from the structured model and compare with the sharp-interface prediction. (d) Validate against experimental I-V curves and beam composition data.

**Success criteria:** (i) Demonstration that interfacial layering quantitatively changes predicted emission rates. (ii) A corrected boundary condition that can be incorporated into existing EHD codes. (iii) Prediction of IL-specific differences traceable to interfacial structure.

**Risk assessment:** The structured-to-continuum bridging is conceptually challenging. Experimental validation requires comparing model predictions against multiple ILs. **Medium risk, medium-high reward.**

### 3. Direct Measurement of Ion Evaporation Dynamics at Flat IL/Vacuum Interfaces

**Title:** Single-ion-resolved measurement of field evaporation rates from planar ionic liquid films

**Question:** What is the actual temperature dependence, field dependence, and species selectivity of ion evaporation from a well-characterized flat IL surface, decoupled from meniscus geometry and flow effects?

**Why it matters:** All existing ILIS experiments conflate the evaporation process with meniscus dynamics, flow, and space-charge effects. Isolating the evaporation step would provide the first clean test of the rate equation and its parameters.

**Approach:** (a) Prepare thin IL films (~10-100 nm) on conductive substrates in UHV. (b) Apply uniform fields using a parallel-plate geometry or STM-like probe. (c) Detect emitted ions with single-ion sensitivity (channel electron multiplier or MCP) and mass-resolve using TOF. (d) Measure rate vs. field, temperature, film thickness, and IL chemistry. (e) Compare with MD predictions and continuum theory.

**Success criteria:** (i) Measurement of the activation energy and pre-exponential factor independently. (ii) Direct determination of whether the $\sqrt{E}$ Schottky scaling holds. (iii) Species-resolved rates (monomer vs. dimer).

**Risk assessment:** Achieving uniform, stable fields of ~1 V/nm over macroscopic areas is technically challenging. Film stability under field may be limited (tip streaming instability [29]). Single-ion detection at rates compatible with the measurement timescale is feasible with existing detectors. **Medium-high risk, high reward.** This is the experiment the field needs but has not done.

### 4. Unified Evaporation-Fragmentation Kinetic Model

**Title:** Coupled evaporation-fragmentation theory for ionic liquid ion source beam composition

**Question:** Can a single kinetic framework predict both the emitted species distribution and the downstream fragmentation, using a self-consistent set of energy parameters?

**Why it matters:** Current practice fits evaporation and fragmentation independently with separate empirical parameters [20][21]. If the same intermolecular interactions govern both processes (they must), then the parameters should be related. A unified model would dramatically reduce the number of free parameters and enable prediction rather than fitting.

**Approach:** (a) Compute cluster binding energies (monomer-neutral pair, dimer-neutral pair) using DFT and compare with experimental fragmentation data. (b) Develop a kinetic model that includes evaporation of all species (monomer, dimer, trimer) and fragmentation of all species, with rate constants derived from a consistent energy surface. (c) Predict beam composition as a function of field, temperature, and IL chemistry. (d) Compare with TOF and RPA measurements.

**Success criteria:** (i) Prediction of beam composition without fitting to composition data. (ii) Explanation of why different ILs produce different monomer/dimer/trimer ratios. (iii) Prediction of fragmentation timescales consistent with RPA step structure.

**Risk assessment:** DFT calculations of cluster energies are feasible. The kinetic model coupling is straightforward. The main risk is that additional processes (e.g., collisional activation in the plume) may be important. **Low-medium risk, medium-high reward.** Good first PhD project.

### 5. First-Principles Electrochemical Degradation Model

**Title:** Coupled ion-emission / electrochemical-degradation model for ILIS lifetime prediction

**Question:** Can the electrochemical degradation rate be predicted from the emission conditions (current, polarity, frequency) and the IL/electrode system properties, enabling rational design for lifetime?

**Why it matters:** Lifetime is the primary barrier to ILIS deployment in spacecraft propulsion [3][22][23]. Current understanding is empirical: polarity alternation at ~1 Hz helps [22], distal electrodes help [23], but the quantitative relationship between operating parameters and degradation rate is unknown.

**Approach:** (a) Model the counterion accumulation at the emitter-IL interface during emission half-cycles. (b) Compute electrochemical reaction rates using Marcus theory / Butler-Volmer kinetics with IL-specific parameters. (c) Couple to the emission model to get self-consistent current-degradation dynamics. (d) Predict optimal alternation frequency and validate against lifetime data.

**Success criteria:** (i) Prediction of degradation rate vs. operating conditions. (ii) Identification of IL/electrode combinations that maximize lifetime. (iii) Design rules for alternation protocol.

**Risk assessment:** Requires electrochemical data (ESW, exchange current densities) for specific IL/electrode combinations, some of which may not be available. The coupling between emission dynamics and electrochemistry adds complexity. **Medium risk, high practical reward.**

---

## Cross-Cutting Observations

### Feynman's 12 Problems Test
The solvation energy problem (Direction 1) connects to: the statistical mechanics of strongly correlated Coulomb systems, the dielectric response of ionic media, and the theory of activated processes far from equilibrium. These are independently important open problems in condensed matter physics.

### Polya's Reformulation
The ILIS community has largely framed the problem as "improve the EHD model" (better numerics, finer grids, more physics). But the governing equation most in need of improvement is the **rate equation itself**, which enters as a boundary condition. The community may be optimizing the wrong part of the model.

### Kuhn's Anomaly Accumulation
The Iribarne-Thomson model has accumulated significant patches: ions with very different solvation energies show similar evaporation rates; ions with similar solvation energies show very different rates [13]; "anomalously low activation energies" appear [8]; the pre-exponential factor is never validated; the Born model is used in a medium where it is known to fail. Each anomaly has been addressed with an ad hoc correction rather than a fundamental revision.

### Einstein's Parsimony
A typical ILIS model has: fitted $\Delta G$ for each ion species, empirical cluster fragmentation rates for each species, a conductivity treated as a free parameter (despite being measurable), a contact angle or hydraulic impedance as a fitting parameter, and empirically adjusted emitter geometry. The ratio of free parameters to independent predictions is unfavorable.

---

## References

### Review Papers and Textbooks

[1] Lozano, P.C. "Electrospray Propulsion." *Encyclopedia of Aerospace Engineering*, Wiley, 2010.

[2] Borrajo-Pelaez, R. and Gamero-Castano, M. "Ionic liquid ion sources for focused ion beam applications: A review." *Vacuum*, 2025.

[3] Courtney, D.G. et al. "Ionic liquid ion source emitter arrays fabricated on bulk porous substrates for spacecraft propulsion." MIT, 2011.

[4] Martinez-Sanchez, M. and Lozano, P.C. MIT OCW 16.522 Space Propulsion, Lectures 20 and 24, Spring 2015. Available: https://ocw.mit.edu/courses/16-522-space-propulsion-spring-2015/

### Key Original Papers

[5] Perez Martinez, C.S. "Engineering ionic liquid ion sources for ion beam applications." PhD thesis, MIT, 2016. https://dspace.mit.edu/handle/1721.1/105605

[6] Perez Martinez, C.S. and Lozano, P.C. "Ionic liquid ion sources for silicon reactive machining." *Microelectronic Engineering*, 2010.

[7] Romero-Sanz, I., Bocanegra, R., Fernandez de la Mora, J., and Gamero-Castano, M. "Source of heavy molecular ions based on Taylor cones of ionic liquids operating in the pure ion evaporation regime." *J. Appl. Phys.*, 2003.

[8] Coffman, C.S. "Electrically-assisted evaporation of charged fluids: fundamental modeling and studies on ionic liquids." PhD thesis, MIT, 2016. https://dspace.mit.edu/handle/1721.1/103421

[9] Coffman, C.S., Martinez-Sanchez, M., and Lozano, P.C. "Electrohydrodynamics of an ionic liquid meniscus during evaporation of ions in a regime of high electric field." *Phys. Rev. E*, 99:063108, 2019.

[10] Gallud, X. and Lozano, P.C. "The emission properties, structure and stability of ionic liquid menisci undergoing electrically assisted ion evaporation." *J. Fluid Mech.*, 933, 2022. arXiv:2109.12274.

[11] Iribarne, J.V. and Thomson, B.A. "On the evaporation of small ions from charged droplets." *J. Chem. Phys.*, 64:2287, 1976.

[12] Thomson, B.A. and Iribarne, J.V. "Field induced ion evaporation from liquid surfaces at atmospheric pressure." *J. Chem. Phys.*, 71:4451, 1979.

[13] Wilm, M. "Principles of Electrospray Ionization." *Mol. Cell. Proteomics*, 10(7), 2011. PMC3134074.

[14] Taylor, G.I. "Disintegration of water drops in an electric field." *Proc. R. Soc. Lond. A*, 280:383, 1964.

[15] Fernandez de la Mora, J. and Loscertales, I.G. "The current emitted by highly conducting Taylor cones." *J. Fluid Mech.*, 260:155, 1994.

[16] Gallud, X. and Fernandez de la Mora, J. "Modelling and scaling laws of the ion emission regime in Taylor cones." *J. Fluid Mech.*, 2023.

[17] Labowsky, M.J., Fenn, J.B., and Fernandez de la Mora, J. "A continuum model for ion evaporation from a drop: effect of curvature and charge on ion solvation energy." *Anal. Chim. Acta*, 406:105, 2000.

[18] Lau, G.P.S. et al. "When Dielectric Constants Deceive: Interrogating Solvation in Ionic Liquids with Cyclic Voltammetry." *J. Phys. Chem. B*, 2016.

[19] Lynden-Bell, R.M. et al. "Layering at an Ionic Liquid-Vapor Interface: A Molecular Dynamics Simulation Study of [bmim][PF6]." *J. Am. Chem. Soc.*, 128:12462, 2006.

[20] Miller, C.E. and Lozano, P.C. "Characterization of Ion Cluster Fragmentation in Ionic Liquid Ion Sources." SM thesis, MIT, 2019. https://dspace.mit.edu/bitstream/handle/1721.1/122372/1119667865-MIT.pdf

[21] Li, J. et al. "Fragmentation modeling of gas-phase ionic liquid clusters in high-voltage electric field." *Fuel*, 2023.

[22] Lozano, P.C. and Martinez-Sanchez, M. "Ionic liquid ion sources: suppression of electrochemical reactions using voltage alternation." *J. Colloid Interface Sci.*, 280:149, 2004.

[23] Lozano, P.C. "The role of upstream distal electrodes in mitigating electrochemical degradation of ionic liquid ion sources." *Appl. Phys. Lett.*, 101:193504, 2012.

[24] Hantal, G. et al. "Probing the ionic liquid/vacuum interface." *Phys. Chem. Chem. Phys.*, 2018.

[25] Coles, T.E. et al. "Electric-field-driven ion emission from the free surface of room temperature ionic liquids." *J. Phys. Chem. Lett.*, 12:1990, 2021.

[26] Endres, F. et al. "Ionic liquids: solvation properties and physicochemical characterization." Various publications, 2006-2020.

[27] Coles, T.E. "Electric-field-induced ion evaporation from the ionic liquid-vacuum interface." *Physics of Fluids*, 2024.

[28] Tsong, T.T. "Field evaporation rates of tungsten." *Phys. Status Solidi (a)*, 1:451, 1970.

[29] Lozano, P.C. et al. "Ion evaporation-induced tip streaming from liquid drops of ionic liquids." *Physics of Fluids*, 36:032013, 2024.

### PhD Theses

[5] Perez Martinez, C.S. MIT, 2016. (cited above)

[8] Coffman, C.S. MIT, 2016. (cited above)

[20] Miller, C.E. MIT, 2019. (cited above)

[30] Coles, T.E. "On the fundamentals of pure ionic emission in [ILIS]." PhD thesis, Queen Mary University of London, 2025. https://qmro.qmul.ac.uk/xmlui/handle/123456789/99380

### Course Materials

[4] MIT OCW 16.522 Lectures 20, 24. (cited above)

### Adjacent Field Sources

[13] Wilm, M. "Principles of ESI." (electrospray mass spectrometry community)

[17] Labowsky et al. (electrospray mass spectrometry community)

[28] Tsong, T.T. (atom probe tomography / field evaporation from metals)

### Multiscale Modeling

[31] Petro, E. et al. "Multiscale modeling of electrospray ion emission." *J. Appl. Phys.*, 131:193301, 2022.

[32] Asher, S. et al. "Multi-scale modeling of ionic electrospray emission." *J. Appl. Phys.*, 131:014902, 2022.

### Recent Reviews and Perspectives

[33] Pedrini, D. et al. "Design and microstructuring of materials to boost spacecraft ion propulsion." *Nature Reviews Materials*, 2024.

[34] Chen, S. et al. "Effect of ion solvation energy on electrohydrodynamic behavior of ionic liquid droplets in electrospray thrusters." *Chinese J. Aeronautics*, 2024.

### Machine Learning Force Fields (added 2026-03-12)

[35] "Ionic Liquid Molecular Dynamics Simulation with Machine Learning Force Fields: DPMD and MACE." arXiv:2503.18249, March 2025. https://arxiv.org/html/2503.18249

[36] "Transferability and Accuracy of Ionic Liquid Simulations with Equivariant Machine Learning Interatomic Potentials." *J. Phys. Chem. Lett.*, 2024. https://pubs.acs.org/doi/10.1021/acs.jpclett.4c01942 (paywalled — accessed via abstract only)

---

## Source Limitations Caveat

This report is biased toward open-access sources: MIT theses (DSpace), arXiv preprints, PMC articles, and MIT OCW materials. Several important papers behind paywalls (particularly in *Journal of Fluid Mechanics*, *Physical Review E*, and *Journal of Applied Physics*) could only be assessed through their abstracts and metadata. The QMUL thesis [30] could not be fetched due to access restrictions. Key experimental papers by Fernandez de la Mora and colleagues in *J. Fluid Mech.* and by Gamero-Castano in *J. Appl. Phys.* are underrepresented relative to their importance. The MIT/Lozano group is overrepresented because their theses and preprints are openly available. Commercial ILIS work (Accion Systems, now acquired) is not covered. The molecular dynamics literature from the QMUL group (Coles et al.) is rapidly evolving and some 2024-2025 results may not be captured here.
