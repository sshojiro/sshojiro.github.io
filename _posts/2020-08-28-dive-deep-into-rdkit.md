---
published: true
title: Investigation of Conformer Generation via RDKit
---

A famous cheminformatics library in Python, RDKit, has functions to generate conformers for molecules, such as ETKDGv2. Where on earth does the source file exist?

I found the file:
[Parameter definition: Embedder.cpp](https://github.com/rdkit/rdkit/blob/master/Code/GraphMol/DistGeomHelpers/Embedder.cpp)
Based on the source, as I cannot read C++, it is inferred that ETKDGv2 or other functions are defined as a function and parameters. Therefore, ETKDGv2 and other methods are found in separate functions. I have found another clue:
[Interface for Python](https://github.com/rdkit/rdkit/blob/master/Code/GraphMol/DistGeomHelpers/Wrap/rdDistGeom.cpp)

In short note, ETKDGv2 and other functions are compiled by Cython from the C++ source code.