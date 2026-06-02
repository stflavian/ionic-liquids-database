# Ionic Liquids Geometry Database

A public, open repository of geometry files for ionic liquid (IL) ions and ion pairs, suitable for training or fine-tuning machine learning interatomic potentials (MLIPs), force fields, and semi-empirical models. All geometries are provided in the extended XYZ format for immediate interoperability with common computational chemistry and materials tools.

> [!CAUTION]
> The structure of the repositoty is still subject to change.

## Contents

- **Single ions**: Equilibrium geometries for common IL anions and cations (DFT optimized).
- **Ion pairs (neutral combinations)**: Multiple conformations per pair, computed at three levels:
  - DFT (PBE+D3(BJ))
  - DFTB (GFN1-xTB)
  - UFF

All entries include atom types, coordinates, forces, charges, dipole moment, HOMO-LUMO gap, and total energy.

## Format and Structure

### File Format
- **Extension**: `.xyz` (extended XYZ format)
- **Comment**: energy (also free_energy), dipole, homo_lumo
- **Fields**: atom_name, x, y, z (Å), fx, fy, fz (eV/Å), charge

## Units

- Coordinates are in Ångströms.
- Forces are in eV per Ångströms.
- Energies and HOMO-LUMO gaps are in eV.
- Atom names correspond to standard element symbols and force-field types used in the calculations.

### Directory Layout
```
Anions/<AnionName>/<AnionName>.xyz       # Single optimized anion geometry
Cations/<CationName>/<CationName>.xyz    # Single optimized cation geometry
Pairs/<CationName>/<AnionName>/*.xyz     # Ion pair conformations (e.g., <Cation>_<Anion>_<method>_[1-10].xyz)
```
Examples:
- `Anions/BF4/BF4.xyz`
- `Cations/BuMeIM/BuMeIM.xyz`
- `Pairs/BuMeIM/BF4/BuMeIM_BF4_dft_1.xyz`

### Naming Convention (Pairs)
- `<Cation>_<Anion>_<method>_<conformation>.xyz`
  - method: `dft`, `dftb`, `uff`
  - conformation: 1–10 (for multiple relaxed geometries per method)

## Methodology

- **DFT**: PBE functional with D3 dispersion corrections and Becke-Johnson damping (PBE+D3(BJ)).
- **DFTB**: Semi-empirical tight-binding (GFN1-xTB)
- **UFF**: Universal Force Field (UFF) molecular mechanics relaxations

Geometry files are provided "as-is" from geometry optimizations. Some entries may have duplicate low-energy conformers.

## Usage Examples

### Read with ASE
```python
from ase.io import read
geom = read("Pairs/BuMeIM/BF4/BuMeIM_BF4_dft_1.xyz")
```

---

**License**: CC0 1.0 Universal (see [LICENSE](LICENSE))
