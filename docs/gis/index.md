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

TO-DO...Something like: Before you start you need to have linkage and configuration file with shape files...

### Linkage file

TO-DO...

### Configuration file

TO-DO...

### Configuration

| Parameter               | Description                                                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `gisdir`                 | Option to find participant ID. More on methods of finding ID can be found in [GGIR documentation](https://cran.r-project.org/web/packages/GGIR/). |
| `gislinkfile`              | Path to input file or folder.                                                                                                                     |
| `outputdir`             | Path to output folder.                                                                                                                            |
| `dataset_name`              | Path to GGIR output folder (ms5).                                                                                                                 |
| `configfile`          | indoor-outdoor-vehicle.                                                                                                                           |
| `baselocation`           | Correct [date and time format](https://sparkbyexamples.com/r-programming/dates-and-times-in-r/).                                                  |
| `groupinglocation`                    | Timezone in which experiments took place [TZ identifier list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).                      |
| `write_shp`         | Acceleration thresholds corresponding to the intensity levels.                                                                                    |
| `split_GIS` | Maximum trip break duration in seconds.                                                                                                           |
| `sublocationID`         | Minimum trip distance in meters.                                                                                                                  |

### Example

``` r
library(hbGIS)

hbGIS(gisdir = "C:/path_to_input_gis_file/or/folder",
      palmsdir = "C:/path_to_hbgps_or_palms_output_folder",
      gislinkfile = "C:/path_to_linkage_file/participant_basis.csv", # (1)! 
      outputdir = "C:/path_to_output_folder",
      dataset_name = "project_name",
      configfile = "C:/path_to_config_file/palmsplus.csv", # (2)! 
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