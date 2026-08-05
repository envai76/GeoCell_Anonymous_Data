# GeoCell Anonymous Data

This directory contains anonymized retinal ganglion cell (RGC) image data. The data are organized into a structured dataset and a location reserved for an approximate dataset representation.

## Directory hierarchy

```text
GeoCell_Anonymous_Data/
|-- GeoCell_Anonymous_Data_Struct/
|   |-- Dataset_rgc_cell_counts.csv
|   |-- readme.md
|   |-- dots/
|   |   `-- 791 *_centroids.png files
|   `-- images/
|       `-- 791 *.tif files
|-- GeoCell_Anonymous_Data_Approx/
|   `-- (currently empty)
|-- folder-hierarchy.txt
`-- README.md
```

The hierarchy above summarizes repeated files instead of listing every image individually. The complete generated file listing is available in `folder-hierarchy.txt`.

## Folder and file contents

### `GeoCell_Anonymous_Data_Struct/`

Contains the structured RGC dataset. The TIFF images, centroid visualizations, and cell-count table use related file identifiers so records can be matched across the dataset.

#### `images/`

Contains **791 TIFF (`.tif`) image files**. Example file identifiers include:

```text
01-L-C-01.tif
01-L-M-01.tif
01-R-P-04.tif
```

#### `dots/`

Contains **791 PNG centroid images**. Their names correspond to the TIFF images in `images/`, with `_centroids` appended to the identifier. For example:

```text
images/01-L-C-01.tif
dots/01-L-C-01_centroids.png
```

These PNG files appear to provide centroid/dot annotations or visualizations for the corresponding RGC images.

#### `Dataset_rgc_cell_counts.csv`

Contains image-level cell-count information. Its columns are:

| Column | Description |
|---|---|
| `file name` | Image identifier used to match the CSV record to files in `images/` and `dots/`. |
| `manual count` | Manually recorded cell count. |
| `auto count` | Automatically generated cell count; some entries may be empty. |

#### `readme.md`

The original README inside the structured dataset. This root README provides the expanded dataset documentation.

### `GeoCell_Anonymous_Data_Approx/`

This folder is intended for the approximate form of the dataset. It was empty when the hierarchy was generated, so its eventual file format and internal organization could not be verified.


## File naming

Most image identifiers follow a pattern similar to:

```text
<subject-or-sample>-<L-or-R>-<retinal-region>-<index>
```

For example, `01-L-C-01` is the identifier shared by the TIFF image, centroid PNG, and corresponding CSV record. Its components indicate:

- `L` and `R`: left and right eyes, respectively.
- `C`: central region of the retina.
- `M`: middle region of the retina.
- `P`: peripheral region of the retina.

The precise meanings of the leading numeric identifier and final index should be documented separately.

Some filenames vary from the dominant hyphenated convention (for example, identifiers beginning with `06L` or `51L`), and a few contain additional punctuation or numbering. Consumers should use the stored identifier exactly rather than reconstructing filenames from an assumed pattern.

## Usage notes

- Preserve folder names and relative paths when downloading or extracting the data.
- Match images, centroid files, and count records using the complete file identifier.
- Do not rename files solely to normalize their format, because existing tables or processing code may depend on the current names.
- Treat blank `auto count` values as missing unless the associated analysis documentation specifies another meaning.
- Follow all applicable privacy, data-use, and redistribution requirements for the anonymized dataset.

