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
<animal_or_sample>-<L-or-R>-<retinal-region>-<index>
```

For example, `01-L-C-01` is the identifier shared by the TIFF image, centroid PNG, and corresponding CSV record. Its components indicate:

- `L` and `R`: left and right eyes, respectively.
- `C`: central region of the retina.
- `M`: middle region of the retina.
- `P`: peripheral region of the retina.

Final index shows that .

Some filenames vary from the dominant hyphenated convention (for example, identifiers beginning with `06L` or `51L`), and a few contain additional punctuation or numbering. Consumers should use the stored identifier exactly rather than reconstructing filenames from an assumed pattern.