# GeoCell Anonymous Structured RGC Dataset

## Overview

`GeoCell_Anonymous_Data_Struct` contains the structured retinal ganglion cell (RGC) dataset associated with the GeoCell study. It provides retinal microscopy images, corresponding centroid/dot annotation images, and image-level manual and automated cell counts.

The shared file identifier allows an image, its centroid annotation, and its CSV record to be matched without relying on file order.

## Dataset summary

| Item | Count |
|---|---:|
| RGC microscopy images | 791 |
| Ground-truth centroid images | 791 |
| Image annotation pairs | 791 |
| Cell-count CSV files | 1 |

Each microscopy image has one corresponding centroid annotation image. The dataset therefore contains **791 paired samples**.
## Tissue staining and image acquisition

As described in the GeoCell paper, the RGC images were obtained from **whole-mounted mouse retinas immunolabeled for RNA-binding protein with multiple splicing (RBPMS)**. RBPMS is used as a selective retinal ganglion cell marker; accordingly, the fluorescently labeled RBPMS-positive cell bodies are the structures counted and annotated in these images.

The stained retinal whole mounts were imaged using a **Zeiss Axio Imager M2** microscope. The paper reports images of 1400 × 1400 pixels covering approximately 318 × 318 µm.

Additional laboratory parameters—such as antibody supplier and dilution, fluorophore, fixation conditions, incubation times, and exposure settings—are not stated here because they are not confirmed by the available dataset documentation. Consult the associated paper's complete experimental methods and cited protocols when reproducing the staining procedure.
## Folder and file contents

```text
GeoCell_Anonymous_Data_Struct/
├── RGC_images/
│   └── 791 TIFF images
├── Ground_truth_annotations/
│   └── 791 PNG centroid images
├── Dataset_rgc_cell_counts.csv
└── readme.md
```

### `images/`

Contains **791 TIFF (`.tif`) retinal images**. Example filenames include:

```text
01-L-C-01.tif
01-L-M-01.tif
01-R-P-04.tif
```

### `dots/`

Contains **791 PNG centroid annotation images**. Each annotation normally uses the same identifier as its source TIFF image, followed by `_centroids`:

```text
RGC_images/01-L-C-01.tif
Ground_truth_annotations/01-L-C-01_centroids.png
```

Thus, remove the image extension and the annotation suffix when matching records:

```text
01-L-C-01.tif  <->  01-L-C-01_centroids.png  <->  CSV identifier 01-L-C-01
```

The PNG files encode centroid/dot ground truth for RGC locations. A marked centroid represents an annotated cell location; it should not be interpreted as a full cell boundary or pixel-level segmentation mask.

### `Dataset_rgc_cell_counts.csv`

Contains image-level cell counts with these columns:

| Column | Description |
|---|---|
| `file name` | Identifier used to associate the row with files in `RGC_images/` and `Ground_truth_annotations/`. |
| `manual count` | Manually recorded RGC count for the image. |
| `auto count` | Count calculated from the corresponding ground-truth annotation image using computer-vision techniques. It is provided as a quality-control check against the manually reported count; some entries may be empty. |

Missing automated counts should be treated as missing data, not as zero.

## Filename encoding

The dominant naming format is:

```text
<animal_id>-<eye_side>-<retinal_region>-<field_number>
```

For example:

```text
01-L-C-01
```

means animal `01`, left eye (`L`), central retinal region (`C`), field `01`.

| Component | Meaning |
|---|---|
| `<animal_id>` | An anonymized animal identifier. |
| `<eye_side>` | `L` = left eye; `R` = right eye. |
| `<retinal_region>` | `C` = central, `M` = middle, `P` = peripheral. |
| `<field_number>` | One of the sampled imaging fields within that retinal region, generally numbered `01` through `04`. |

The retina is represented by central, middle, and peripheral radial regions, with four image fields sampled from each region. The field number distinguishes those four samples. It must **not** be assumed to encode a particular direction (such as up, down, left, or right) unless a separate authoritative mapping is supplied.

Some stored identifiers differ from the dominant hyphenated form—for example, some begin with `06L` or `51L`, and a small number contain additional punctuation or numbering. Software should use the identifier exactly as stored and match files by normalized suffix/extension removal rather than rebuilding names from the nominal pattern.

## Image and annotation pairing

Each TIFF image in `RGC_images/` is paired with the PNG centroid annotation in `Ground_truth_annotations` that has the same identifier plus the `_centroids` suffix.

```text
RGC_images/01-L-C-01.tif
Ground_truth_annotations/01-L-C-01_centroids.png
```

Pair files by their complete identifier rather than by directory order. Remove only the known file extension and `_centroids` suffix when comparing identifiers.
## Ground-truth interpretation

- The files in `Ground_truth_annotations/` are point-based centroid annotations or visualizations corresponding to the TIFF images.
- A centroid indicates the annotated location of an RGC.
- The annotations do not, by themselves, define precise cell contours, areas, or instance masks.
- The CSV `manual count` is the image-level manual reference count.
- The CSV `auto count` is calculated from the ground-truth annotation image using computer-vision techniques. It is a quality-control measurement used to confirm that the number of annotation marks agrees with the manually reported cell count; it is not a prediction made from the original microscopy image.
- Image, annotation, and count-table matching should be performed by identifier, never by row position or directory listing order.

## Appropriate uses

This dataset is suitable for:

- RGC counting;
- RGC centroid or point localization;
- comparing annotation-derived quality-control counts with manually reported image-level counts;
- evaluating performance across left and right eyes and central, middle, and peripheral retinal regions; and
- animal-disjoint training and evaluation when splits are constructed by anonymized animal identifier.
