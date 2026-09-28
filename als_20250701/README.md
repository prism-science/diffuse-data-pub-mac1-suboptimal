# als_20250701 — humidity series (4 datasets)

This directory contains X-ray Bragg datasets from four Mac1 crystals generated as part of Prism, Astera Institute's effort to develop reproducible methods for generating high quality, diffuse scattering data. These datasets resulted from experimenting with humidity conditions and are considered poor quality.

Beamline: 8.3.1, ALS (Advanced Light Source), Berkeley, CA — July 1st, 2025

[Logbook entry](https://diffuse.science/logbook/beamtime/20250701-als/)

| dataset | condition | Wilson B (Å²) | Mosaicity (deg) | cell a=b (Å) | cell c (Å) |
| --- | --- | --- | --- | --- | --- |
| xtal3 | no sleeve + paratone | 20.525 | 0.120 | 89.048 | 39.482 |
| xtal7 | sleeve + paratone | 12.316 | 0.022 | 89.002 | 39.699 |
| xtal10 | sleeve + santovac | 11.714 | 0.186 | 89.171 | 39.648 |
| xtal9 | sleeve + no oil | 12.642 | 0.009 | 89.235 | 40.132 |

Each `xtalN/` folder contains the raw Bragg frames (`.cbf`) for that crystal.
