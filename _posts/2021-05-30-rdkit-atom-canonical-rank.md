---
published: true
title: RDKit Canonical Rank of Atoms in a Molecule
---
## Atom Ordering

Atoms in a molecule are uniquely aligned in an arbitrary way. Each cheminformatics software has such a standardization process, called canonicalization, in it. RDKit, a most popular Python chemoinformatics open source library has the canonicalization mechanism. According to a [RDKit discussion](https://github.com/rdkit/rdkit/issues/2637#issuecomment-527582728), RDKit aligns atoms in a molecule during graph traversal. The atom order is not the same one in the canonical SMILES's atom order. We must pay attention to this, if the atom order impacts the calculation results.
