# Raw X-ray diffraction data for suboptimal apo Mac1 datasets (`mac1-suboptimal`)

This repository contains raw diffraction images from apo Mac1 (SARS-CoV-2 nsp3 macrodomain) crystals that gave lower-quality data, owing to humidity control, radiation dose, or crystal size. They are analyzed in the article below to identify the experimental factors that matter for high-quality diffuse scattering data:

Zielinski K, Meisburger S, Lu K, Bassim V, Holton J, Fraser JS, Ando N. (2026). Iterating diffuse scattering protocols in parallel leads to reproducible, high-quality data from Mac1. The Stacks. [DOI: 10.82153/hrpy-t681](https://doi.org/10.82153/hrpy-t681)

It is a [DataLad](https://www.datalad.org) dataset. The images are tracked with git-annex and hosted on public object storage, so they can be downloaded anonymously and verified by checksum. Code that processes these data with DIALS and mdx2 is provided in [diffuse-processing-mac1-east-west](https://github.com/prism-science/diffuse-processing-mac1-east-west), which includes this repository as the subdataset `inputs/raw/mac1-suboptimal`. The high-quality datasets are in the sibling repository [diffuse-data-pub-mac1-east-west](https://github.com/prism-science/diffuse-data-pub-mac1-east-west).

## Contents

Data are organized by beamtime and crystal. Crystal names are unique only within a beamtime (for example, `mac1_7` appears in two beamtimes).

```
<beamtime>/
    README.md           description of the beamtime and its crystals
    <crystal>/
        crystal/        diffraction images of the crystal
        background/     background images (no crystal)
metadata.csv            one row per crystal
```

The `als_20250701` crystals (`xtal3`, `xtal7`, `xtal9`, `xtal10`) contain Bragg images only, placed directly in the crystal folder, with no `crystal/` or `background/` subfolders.

| Beamtime | Date | Series | Crystals | Images per crystal (data / background) | Size |
|---|---|---|---|---|---|
| `als_20250701` | 2025-07-01 | Humidity control | `xtal3`, `xtal7`, `xtal9`, `xtal10` | 7200 / none | 179 GB |
| `als_20251015` | 2025-10-15 | Radiation damage (high dose) | `mac1_7` | 3600 / 360 | 25 GB |
| `als_20260423` | 2026-04-23 | Crystal size (small crystals) | `mac1_4`, `mac1_6`, `mac1_7` | 3600 / 360 | 74 GB |

All data were collected at beamline 8.3.1 of the Advanced Light Source (ALS), Berkeley, CA, and are stored as CBF files. The total size is approximately 278 GB.

## Metadata

- [`metadata.csv`](metadata.csv) has one row per crystal with the columns `beamtime`, `crystal`, `logbook_entry` (link to the electronic logbook), `sample`, `data_type`, `date_collected`, `subject_composition`, `beamline`, `beamline_ror` ([ROR](https://ror.org) identifier of the facility), `has_background_images`, `has_braggs`, and `has_diffuse`.
- Each beamtime directory has a `README.md` describing the experiment and linking to the logbook, which gives details on sample preparation and the beamtime: [`als_20250701`](als_20250701/README.md) (includes the humidity conditions and DIALS statistics for each crystal), [`als_20251015`](als_20251015/README.md) (includes DIALS statistics), and [`als_20260423`](als_20260423/README.md) (includes the logbook entry for each crystal).

## Usage

Install [DataLad](https://handbook.datalad.org/en/latest/intro/installation.html), which requires git-annex (for example, `mamba install -c conda-forge datalad`). Cloning downloads only file names and metadata; the images are fetched on request.

```bash
datalad clone https://github.com/prism-science/diffuse-data-pub-mac1-suboptimal.git
cd diffuse-data-pub-mac1-suboptimal

# fetch one crystal
datalad get als_20260423/mac1_4

# fetch a whole beamtime using four parallel jobs
datalad get -J4 als_20251015

# free up disk space when finished
datalad drop als_20251015
```

Downloads are checked against the recorded checksums. Plain git-annex works as well (`git annex get <path>`). To use these data with the processing scripts, clone [diffuse-processing-mac1-east-west](https://github.com/prism-science/diffuse-processing-mac1-east-west) instead; each script fetches the data it needs.
