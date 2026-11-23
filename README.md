# SiC_AO_MD_simulation

Molecular dynamics simulation data for the interaction of hyperthermal atomic
oxygen (AO) with amorphous SiC using the ReaxFF reactive force field.

## Overview

This directory contains seven independent LAMMPS case directories. Each case
contains the LAMMPS input script, the initial equilibrated structure, a
minimised structure, and the final structure written at the end of the
simulation. The ReaxFF parameter file must be obtained separately.

The simulations use:

- LAMMPS with ReaxFF and charge equilibration (QEq) support;
- `real` units and a 0.25 fs time step;
- 400,000 production steps (100 ps);
- a 300 K Langevin thermostat applied to the lower substrate region;
- a fixed bottom layer and reflecting walls in the surface-normal direction.

## Directory contents

```text
SiCCombin5eV5AOps/
SiCCombin10eV/
SiCCombin20eV/
SiCCombin30eV/
SiCCombin10AOps/
SiCCombin20AOps/
SiCCombin40AOps/
```

Each case directory contains:

- `combin.lmp` - LAMMPS input script;
- `anne.data` - initial equilibrated amorphous SiC structure;
- `Mini.data` - structure written after energy minimisation;
- `deposit.data` - final structure written after the production run.

The ReaxFF parameter file `ffield.reax.choSiC.txt` must be obtained separately
and placed in each case directory before running a simulation. See
`THIRD_PARTY_NOTICES.md` for the relevant reference and redistribution status.

## Case conditions

The confirmed nominal conditions are:

| Case | Incident energy (eV) | Nominal AO flux (AOs/ps) | Deposit insertions | Final atoms |
|---|---:|---:|---:|---:|
| `SiCCombin5eV5AOps` | 5 | 5 | 500 | 6288 |
| `SiCCombin10eV` | 10 | 5 | 500 | 6297 |
| `SiCCombin20eV` | 20 | 5 | 500 | 2765 |
| `SiCCombin30eV` | 30 | 5 | 500 | 2797 |
| `SiCCombin10AOps` | 5 | 10 | 1000 | 2791 |
| `SiCCombin20AOps` | 5 | 20 | 2000 | 3185 |
| `SiCCombin40AOps` | 5 | 40 | 4000 | 3212 |

A machine-readable version, including the initial atom count, timestep, run
length, and trajectory availability, is provided in
`docs/simulation_conditions.csv`.

## Requirements

A LAMMPS executable is required. The data files were written by a LAMMPS build
identified in their headers as version **29 Aug 2024**. The executable used for
the original runs must support the commands present in `combin.lmp`, including
`pair_style reaxff`, `fix qeq/reaxff`, `fix deposit`, and `fix evaporate`.

The exact compiler, MPI implementation, and LAMMPS build settings used for the
original production runs still need to be added to
`docs/software_environment.md`.

Before running any case, obtain `ffield.reax.choSiC.txt` from a lawful source
and place it in the case directory. The parameter file is not redistributed in
the public package; see `THIRD_PARTY_NOTICES.md`.

## Running a case

Run each case from inside its own directory so that the relative file names in
`combin.lmp` are preserved:

```bash
cd SiCCombin10eV
<LAMMPS executable> -in combin.lmp -log log.lammps
```

Replace `<LAMMPS executable>` with the local executable name, for example
`lmp` or `lmp_mpi`.

## Expected outputs

The input script produces or attempts to produce:

- `Mini.data` - minimised structure;
- `deposit.data` - final structure;
- `norm_mass.txt` - time series printed every 100 steps;
- `bomb.lammpstrj` - production trajectory;
- `log.lammps` - LAMMPS screen and thermodynamic output, when `-log` is used.

`norm_mass.txt`, `Mini.lammpstrj`, and LAMMPS log files are not present in all
case directories of the current source archive. Users should not assume that
these intermediate files are included.

## Large trajectory

The original source archive contains one large trajectory:

```text
SiCCombin40AOps/bomb.lammpstrj
```

It is approximately 1.22 GB and contains 4001 frames. It is not included in
this GitHub repository because it exceeds the normal single-file limit. The
full trajectory will be distributed through the Mendeley Data record; the
final DOI is to be confirmed before submission.

## Code availability

- Code and input scripts:
  https://github.com/LG199705/SiC_AO_MD_simulation

## Licenses and attribution

- Code and input scripts: MIT License, Copyright (c) 2026 Gang Luo.
  See `LICENSE-CODE`.
- Data: Creative Commons Attribution 4.0 International (CC BY 4.0),
  attribution to Gang Luo. See `LICENSE-DATA`.
- ReaxFF parameter file: not redistributed with the public package.
  See `THIRD_PARTY_NOTICES.md`.

## Documentation

Additional documentation is provided in:

- `docs/file_dictionary.md`
- `docs/software_environment.md`
- `docs/simulation_conditions.csv`
- `THIRD_PARTY_NOTICES.md`

## Verification status

This repository preserves the original directory layout and file names.
Checksums are provided in `checksums.sha256`. The scripts have not been re-run
as part of preparing this repository.
