# Working Notes: Ion Evaporation in ILIS

## Status: Report complete, follow-up in progress
Report written to: reports/ion-evaporation-ilis.md

## Key findings summary

### 5 Root-cause clusters identified:
1. Continuum electrostatics at molecular scales (image charge, Schottky barrier)
2. Born solvation model in neat ionic liquid (highest leverage)
3. TST pre-exponential factor at extreme fields (never validated)
4. Decoupling of evaporation from meniscus dynamics
5. Conflation of evaporation and fragmentation processes

### Ranked PhD directions:
1. Ab initio ion extraction energy from IL surfaces (bypassing Born)
2. Interface structure-emission connection (layered vs sharp boundary)
3. Direct measurement from flat IL/vacuum interface (the missing experiment)
4. Unified evaporation-fragmentation kinetic model
5. First-principles electrochemical degradation model

## Open questions / follow-up threads

### MLFF viability (raised by user 2026-03-12)
- User confirmed AIMD has historically been too expensive for this problem
- New development: MACE/DPMD MLFFs now achieve near-DFT accuracy for ILs
- Gap: nobody has applied MLFF to IL/vacuum interface under field
- Gap: enhanced sampling + MLFF for ion extraction free energy is untested
- This could be the "new tool" that makes PhD direction #1 viable NOW
- Should update report with this analysis

### Sources not yet fetched (interrupted):
- MIT OCW 16.522 Lectures 20, 22-23, 24 (PDFs available, fetches were interrupted)
- Gallud & Lozano 2023 J. Fluid Mech. (Cambridge Core PDF available)
- Coffman 2016 PhD thesis (MIT DSpace)
- Miller 2019 SM thesis (MIT DSpace)
- Coles et al. 2024 Physics of Fluids
