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

Before using the hbGIS package to process spatiotemporal behaviour patterns, two additional files must be prepared: a linkage and configuration files.

### 1. Required files for hbGIS analysis
#### Linkage file

The linkage file is a CSV file that contains three specific columns:

| Column               | Description                                                                                                                                       |
| ---------------------| ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `identifier`         | Used to identify a participant. This is necessary to link shape files with processed hbGPS output.                                                |
| `school_id`          | For grouping spatiotemporal information. This means that the school shape (polygon) can be mapped to a group of participants.                     |
| `class_id`           | For sub-grouping. Participants from the same school have separate results (class-based).                                                          |

An example of a linkage file can be downloaded [here](#).

#### Configuration file

| Column             | Description                                                                                                                                       |
| -------------------| ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `context`          | palmplusr fields tables (TO-DO: List of contexts...)                                                                                              |
| `name`             | User specified name of formula                                                                                                                    |
| `formula`          | Formula (see more at [palmsplur](https://thets.github.io/palmsplusr/articles/article-3-building-formulas.html))                                   |
| `is_where_field`   | TO-DO..                                                                                                                                           |
| `after_conversion` | TO-DO..                                                                                                                                           |

An example of a configuration file can be downloaded [here](#).

### 2. Analysis
#### Configuration

| Parameter               | Description                                                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `gisdir`                | Path to input shape file or folder with shapes.                                                                                                   |
| `palmsdir`              | Path to input file or folder (hbGPS/PALMS).                                                                                                       |
| `gislinkfile`           | Path to linkage file.                                                                                                                             |
| `outputdir`             | Path to output folder.                                                                                                                            |
| `dataset_name`          | User specified project name.                                                                                                                      |
| `configfile`            | Path to configuration file.                                                                                                                       |
| `baselocation`          | Base for individuals (leave empty if not available).                                                                                              |
| `groupinglocation`      | Grouping for individuals (leave empty if not available).                                                                                          |
| `write_shp`             | Store shape files as output.                                                                                                                      |
| `split_GIS`             | Split GIS files in sublocations (only for public places).                                                                                         |
| `sublocationID`         | Column name in GIS file to identify sublocation.                                                                                                  |


!!! note

    GIS filenames are used as location names and at the moment the code can only handle names that are shorter than 6 characters.

#### Example

``` r
library(hbGIS)

hbGIS(gisdir = "C:/path_to_input_gis_file/or/folder",
      palmsdir = "C:/path_to_hbgps_or_palms_output_folder",
      gislinkfile = "C:/path_to_linkage_file/participant_basis.csv",
      outputdir = "C:/path_to_output_folder",
      dataset_name = "project_name",
      configfile = "C:/path_to_config_file/palmsplus.csv",
      baselocation = "home",
      groupinglocation = "school",
      write_shp = FALSE, 
      split_GIS = TRUE, 
      sublocationID = "ID_NR")
```

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