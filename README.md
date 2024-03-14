## Step 1: Tile Extraction

**Dependencies:**

* [HistoLab](https://github.com/histolab/histolab) for cellularity estimation.

**1. Create a list of the whole slide images (WSIs) you would like to tile**

* (see `generate_tiling_csv.ipynb` for example)

**2. Perform tiling using the WSI list**

* (see tiling_scripts/tiling_script_CPTAC_LUAD.sh for example)
* Be sure to modify/doublecheck the following arguments:

  * `FILE_LIST:` The WSI list mentioned above
  * `SBATCH --array`: Number of slides in that WSI list
  * `OUTPATH`: Output directory
  * `PROJ`: dataset name (also will be the subfolder name)
* Submit the slurm script to O2 job scheduler. For example:

  ```
  sbatch step1_tile_extraction/tiling_scripts/tiling_script_CPTAC_LUAD.sh
  ```

The output will be stored in `[OUTPATH]/[PROJ]`, which will contain 3 subfolders :

* `thumbnail`: thumbnails for WSIs
* `overlay_vis`: thumbnails with tiled areas highlighted. Can be used for troubleshooting.
* `tileStats`: Spreadsheets storing the coordinates of the extracted tiles (which will be used in the next steps). Each WSI will have its own .csv file.
* *Note: Currently to save storage space I chose not to save tiles as images. Instead the tiles are extracted from WSI during inference*
