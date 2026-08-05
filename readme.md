# GeoCell Anonymous RGC Datasets

This repository contains two anonymized retinal ganglion cell (RGC) microscopy datasets associated with the paper:

**GeoCell: A Unified Geometric Field for Cell Counting, Localization, and Coarse Delineation**

Both datasets provide RGC microscopy images, point-based ground-truth annotations, and CSV files containing image-level manual counts and annotation-derived automated counts. The automated counts are calculated from the ground-truth annotation images using computer-vision techniques as a quality-control check against the manually reported counts; they are not predictions made directly from the microscopy images.

## Dataset summary

| Dataset | Annotated images | Ground-truth images | Test images without ground truth | Total microscopy images |
|---|---:|---:|---:|---:|
| `GeoCell_Anonymous_Data_Approx` | 893 PNG | 893 PNG | 30 PNG | 923 |
| `GeoCell_Anonymous_Data_Struct` | 791 TIFF | 791 PNG | 0 | 791 |
| **Repository total** | **1,684** | **1,684** | **30** | **1,714** |

## Repository structure

```text
GeoCell_Anonymous_Data/
|-- README.md
|-- folder-hierarchy.txt
|-- .gitattributes
|-- GeoCell_Anonymous_Data_Approx/
|   |-- README_Approx.md
|   |-- RGC_images/                         # 893 PNG images
|   |-- Ground_truth_annotations/           # 893 PNG annotations
|   |-- test_RGC_Samples_no_Ground_Truth/   # 30 PNG test images
|   `-- match_auto_and_manaull_counts.csv
`-- GeoCell_Anonymous_Data_Struct/
    |-- readme.md
    |-- RGC_images/                         # 791 TIFF images
    |-- Ground_truth_annotations/           # 791 PNG centroid annotations
    `-- Dataset_rgc_cell_counts.csv
```

## Included datasets

### `GeoCell_Anonymous_Data_Approx`

The Approx dataset contains **893 annotated RGC image samples** and **30 additional test images without released ground-truth annotations**, for a total of **923 microscopy images**.

- `RGC_images/` contains 893 PNG microscopy images.
- `Ground_truth_annotations/` contains 893 corresponding PNG point-annotation images.
- `test_RGC_Samples_no_Ground_Truth/` contains 30 PNG test images without released annotation images.
- `match_auto_and_manaull_counts.csv` contains image-level manual counts and annotation-derived automated counts.
- `README_Approx.md` documents the folder contents, filename encoding, pairing rules, ground-truth interpretation, appropriate uses, and caveats.

For annotated samples, microscopy images and ground-truth annotations share the same filename. Approx filenames use a terminal digit to encode retinal region: `1` denotes central, `2` middle, and `3` peripheral. Meanings of other filename components should not be assumed without an authoritative mapping.

### `GeoCell_Anonymous_Data_Struct`

The Structured dataset contains **791 RGC microscopy images** and **791 corresponding centroid annotation images**, forming **791 paired samples**.

- `RGC_images/` contains 791 TIFF (`.tif`) microscopy images.
- `Ground_truth_annotations/` contains 791 PNG centroid annotation images.
- `Dataset_rgc_cell_counts.csv` contains the image identifier, manual count, and annotation-derived automated count.
- `readme.md` documents the folder contents, filename encoding, pairing rules, ground-truth interpretation, appropriate uses, and caveats.

Structured identifiers generally follow:

```text
<animal_id>-<eye_side>-<retinal_region>-<field_number>
```

Here, `L` and `R` denote left and right eyes; `C`, `M`, and `P` denote central, middle, and peripheral retinal regions; and the final field number distinguishes sampled imaging fields within a region. Annotation filenames append `_centroids` to the corresponding image identifier.

## Tissue staining and image acquisition

As described in the GeoCell paper, the images were obtained from whole-mounted mouse retinas immunolabeled for RNA-binding protein with multiple splicing (RBPMS), a selective RGC marker. The stained retinal whole mounts were imaged using a Zeiss Axio Imager M2 microscope. The paper reports images of 1400 x 1400 pixels covering approximately 318 x 318 micrometers.

## Ground-truth interpretation

- Ground-truth images provide point or centroid annotations of RGC locations.
- These annotations are suitable for cell counting and point-localization tasks.
- They should not be interpreted as pixel-accurate cell boundaries or instance-segmentation masks.
- Manual counts are the image-level reference counts reported by a domain expert.
- Automated counts are computed from the annotation images to verify that the number of annotation marks agrees with the reported manual count.
- Images, annotations, and CSV records should be matched by their stored identifiers, not by directory order.


## Dataset-specific documentation

Consult the README inside each dataset folder before using the data:

- [`GeoCell_Anonymous_Data_Approx/README_Approx.md`](GeoCell_Anonymous_Data_Approx/README_Approx.md)
- [`GeoCell_Anonymous_Data_Struct/readme.md`](GeoCell_Anonymous_Data_Struct/README_Struct.md)

Those files contain the authoritative dataset-specific descriptions of filename encoding, image-annotation pairing, CSV contents, intended uses, and important caveats.
