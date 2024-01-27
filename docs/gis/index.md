---
hide:
  - navigation
---

R package for analyzing spatiotemporal behaviour patterns using geospatial data and output from hbGPS or PALMS. Inspired by [palmsplusr](https://thets.github.io/palmsplusr), hbGIS offers features to answer questions about when, where, and what:

- How much time participants spend in parks?
- How much moderate to vigorous physical activity (MVPA) is accumulated in parks?
- What proportion of sedentary time is accumulated during vehicular travel?
- What is the average distance of home-to-school trips?
- How much MVPA is accumulated inside the schoolyard during school time?
- What proportion of commuters use different travel modes in their trip chain (e.g., walk-bus-walk)?
- What is the average speed of bicycle trips during peak travel times?

## Installation

``` r
install.packages("remotes") # (1)!
remotes::install_github("wadpac/GGIR") # (2)!
remotes::install_github("habitus-eu/hbGIS") # (3)!
```

1. R package for installation from remote repositories (Github).
2. Installing GGIR package from GitHub repository.
3. Installing hbGIS package from GitHub repository.

## Usage

``` r
library(hbGIS)

hbGIS(gisdir = "C:/path_to_your_input_gis_file/or/folder_with_gis_files",
      palmsdir = "C:/path_to_your_hbgps_or_palms_output_folder",
      gislinkfile = "C:/path_to_your_linkage_file/participant_basis.csv", # (1)! 
      outputdir = "C:/path_to_your_output_folder",
      dataset_name = "project_name",
      configfile = "C:/path_to_your_config_file/participant_basis.csv", # (2)! 
      baselocation = "home", # (3)! 
      groupinglocation = "school", # (4)! 
      write_shp = FALSE, # (5)! 
      split_GIS = TRUE, # (6)! 
      sublocationID = "ID_NR") # (7)!
```

1. See more below (Linkage file).
2. See more below (Config file).
3. Base for individuals (leave empty if not available).
4. Grouping for individuals (leave empty if not available).
5. Option to store shape files as output.
6. Option to split GIS files in sublocations (only for public places).
7. Column name in GIS file to identify sublocation.

!!! note

    GIS filenames are used as location names and at the moment the code can only handle names that are shorter than 6 characters.

### Linkage file

TO-DO...

### Config file

TO-DO...

## Output files

hbGIS will generate four output files.

| Filename                    | Description                                                        |
| --------------------------- | ------------------------------------------------------------------ |
| `datasetname_whenwhatwhere` | Time series with information about when and where things happened. |
| `datasetname_days.csv`      | Day-level summaries.                                               |
| `datasetname_trajectories`  | Trajectory-based summaries.                                        |
| `datasetname_multimodal`    | Breakdown of trajectories by mode of transport.                    |

### Used abbrevations

| Abbrevation | Description      |
| ------------- | -------------- |
| `mot` | mode of transport      |
| `iov` | indoor-outdoor-vehicle |
| `nbh` | neighbourhood          |
| `dow` | day of week            |

## License

This project is licensed under the terms of the Apache License 2.0.