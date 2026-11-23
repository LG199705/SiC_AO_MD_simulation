# Software environment

## LAMMPS

The structure files contain the header:

```text
LAMMPS data file via write_data, version 29 Aug 2024, units = real
```

This identifies the LAMMPS version that wrote the data files. The exact
executable, compiler, MPI library, and build flags used for the production runs
must be added by the data authors before public release.

The executable must support the commands used in `combin.lmp`, including:

- `pair_style reaxff`
- `fix qeq/reaxff`
- `fix deposit`
- `fix evaporate`
- `fix wall/reflect`
- `compute ave/sphere/atom`
- `compute property/atom`

## Running a case

```bash
cd SiCCombin10eV
<LAMMPS executable> -in combin.lmp -log log.lammps
```

Use the same procedure for the other six case directories. Run from inside the
case directory so that `anne.data` resolves correctly. Obtain the third-party
`ffield.reax.choSiC.txt` separately and place it in that directory before
running; see `THIRD_PARTY_NOTICES.md`.

## Simulation settings recorded in the input scripts

| Setting | Value |
|---|---|
| Units | `real` |
| Atom style | `full` |
| Boundary | `p p f` |
| Time step | 0.25 fs |
| Production steps | 400,000 |
| Nominal production time | 100 ps |
| Thermostat | Langevin, 300 K |
| Temperature-coupling region | lower substrate region |
| Fixed region | bottom layer |
| Surface-normal wall | reflecting wall at the upper boundary |

## Validation status

The files were inventoried and checksummed while preparing this repository,
but the simulations were not re-run. A clean-room test with the documented
LAMMPS build remains to be performed before public release.
