---
hide:
  - navigation
---

HabitusGUI simplifies movement behaviour data analysis by combining GGIR, hbGPS, and hbGIS in a user-friendly interface with several analysis options that perform the following:

1. Processing multi-day RAW accelerometer data for physical activity and sleep research (via [GGIR](https://cran.r-project.org/web/packages/GGIR/) package).
2. Analyzing spatiotemporal behaviour patterns using geospatial data (via [hbGPS](/gps), [hbGIS](/gis)).


## Installation

The [R language](https://cran.r-project.org/) must be installed as a prerequisite. We highly recommend using [RStudio](https://posit.co/downloads/), an IDE that simplifies working with R. The next step is to install the required R packages.

``` r
install.packages("remotes") # (1)!
remotes::install_github("habitus-eu/HabitusGUI", dependencies=TRUE) # (2)!
```

1. R package for installation from remote repositories (Github).
2. Installing the Habitus GUI package with all dependencies from the GitHub repository.

## Usage

In order to launch the HabitusGUI application, the user needs to execute the following lines of code:

``` r
library(HabitusGUI)

options("sp_evolution_status" = 2) # (1)!
HabitusGUI::myApp(homedir="C:/path_to_project/folder") # (2)!
```

1. Ignore evolution warnings.
2. A directory that contains all necessary data in its root or subdirectories.

Upon launching the HabitusGUI application, the user will be prompted to select the data sets they want to analyze. The user has the option to choose one or multiple input data sets.

Once the user selects the desired analyses, a help menu appears on the screen. Depending on the selected analysis, the menu recommends suitable packages that are required for the analysis. The user can then modify the packages per the recommendations before proceeding with the analysis.

In the following steps, the user must upload the required files, which may include datasets and [configuration files]() depending on the chosen analysis. Additionally, the user may be required to name the dataset.

## Configuration files
Examples of configuration files to download include:

1. GGIR (data in [RAW format](#) or in [counts](#))
2. [hbGPS](#)
3. [hbGIS](#)
