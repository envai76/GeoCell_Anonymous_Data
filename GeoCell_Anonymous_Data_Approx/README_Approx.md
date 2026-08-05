# GeoCell Anonymous Approximate RGC Dataset

## Overview

`GeoCell_Anonymous_Data_Approx` contains the approximate RGC dataset associated with the GeoCell study. It includes retinal images, corresponding ground-truth annotations, a set of test images for which ground truth is not released, and a table relating manual and automated cell counts.

The dataset is intended for RGC counting and localization work using the supplied image-level counts and point-based annotations. Files should be associated through their stored identifiers rather than their directory order.

## Dataset summary

| Item | Count |
|---|---:|
| RGC microscopy images with released ground truth | 893 |
| Ground-truth annotation images | 893 |
| Image annotation pairs | 893 |
| Test images without released ground truth | 30 |
| Total microscopy images | 923 |
| Cell-count CSV files | 1 |

The released annotated portion contains **893 paired samples**. An additional **30 unannotated test images** bring the dataset total to **923 microscopy images**.
## Tissue staining and image acquisition

As described in the GeoCell paper, the RGC images were obtained from **whole-mounted mouse retinas immunolabeled for RNA-binding protein with multiple splicing (RBPMS)**. RBPMS is used as a selective retinal ganglion cell marker; accordingly, the fluorescently labeled RBPMS-positive cell bodies are the structures counted and annotated in these images.

The stained retinal whole mounts were imaged using a **Zeiss Axio Imager M2** microscope. The paper reports images of 1400 × 1400 pixels covering approximately 318 × 318 µm.

Additional laboratory parameters—such as antibody supplier and dilution, fluorophore, fixation conditions, incubation times, and exposure settings—are not stated here because they are not confirmed by the available dataset documentation. Consult the associated paper's complete experimental methods and cited protocols when reproducing the staining procedure.
## Folder and file contents

```text
GeoCell_Anonymous_Data_Approx/
├── RGC_images/
├── Ground_truth_annotations/
├── test_RGC_Samples_no_Ground_Truth/
└── match_auto_and_manaull_counts_corrected_high_discrepancy.csv
```

### `RGC_images/`

Contains the RGC microscopy images used with the released ground-truth annotations. Preserve the complete stored filename when processing the data, because filename components beyond the region code have not all been confirmed.

### `Ground_truth_annotations/`

Contains point-based ground-truth annotations corresponding to images in `RGC_images/`. Pair an annotation with an image using their shared stored identifier and any annotation-specific suffix present in the files.

The annotations should be interpreted as annotated RGC locations. They are not full cell outlines or pixel-level instance-segmentation masks unless a particular file explicitly provides such information.

### `test_RGC_Samples_no_Ground_Truth/`

Contains held-out RGC test images for which ground-truth annotations are not included. These files may be used for inference or qualitative assessment, but annotation-based accuracy cannot be calculated from this release alone.

### `match_auto_and_manaull_counts.csv`

Contains records used to associate dataset files with manual and automated RGC counts. The exact header names should be read directly from the CSV rather than assumed from the filename. In interpretation:

- a manual count is the human-recorded image-level reference count;
- an automated count is calculated from the corresponding ground-truth annotation image as a quality-control check; and
- blank count cells, if present, should be treated as missing values rather than zeros.

The filename contains the spelling `manaull`; consumers should use the filename exactly as distributed.

## Filename encoding

The confirmed region encoding is the **terminal digit** of the relevant Approx identifier:

| Terminal digit | Retinal region |
|---|---|
| `1` | Central |
| `2` | Middle |
| `3` | Peripheral |

For example, an identifier ending in `1` denotes a central-region sample, while identifiers ending in `2` and `3` denote middle- and peripheral-region samples, respectively.


## Image and annotation pairing

For each released annotated sample:

1. Start with the complete image identifier in `RGC_images/`.
2. Locate the annotation in `Ground_truth_annotations/` that carries the same identifier, accounting only for its file extension and any explicit ground-truth suffix.
3. Locate the associated CSV record using the identifier field stored in the table.


## Ground-truth interpretation

- Ground-truth annotations represent RGC locations using points/centroids.
- Point annotations support counting and localization evaluation.
- They do not specify exact cell boundaries, morphology, or cell area.
- Manual image-level counts are the reference counts for count-based evaluation.
- Automated counts were computed directly from the ground-truth annotation images using computer-vision techniques. These counts serve as a quality-control measure to verify that the number of annotated cells agrees with the manually reported cell count for each image. This validation is important because the annotation images are used as the reference ground truth in our procedure.
- Test images in `test_RGC_Samples_no_Ground_Truth/` have no released annotations in this dataset.



## Appropriate uses

This dataset is suitable for:

- RGC counting;
- RGC centroid or point localization;
- comparing automated counts with manual image-level counts;
- studying performance across central, middle, and peripheral retinal regions; and
- running inference on the held-out images without released ground truth.

