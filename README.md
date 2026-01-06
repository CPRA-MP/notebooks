<a id="readme-top"></a>

<h3 align="center">CPRA - Jupyter Notebook User Guide</h3>

  <p align="center">
    This repository contains standardized Python Jupyter notebook templates that can be utilized to pull data from the Master Plan API to visualize and analyze the outputs of the ICM, CLARA, and PT models that are not currently visualized in the QAQC Portal. These templates aim to streamline the process of data extraction, transformation, visualization, and analysis, enabling users to perform these tasks efficiently and consistently. The templates serve as a staging ground for future QAQC Portal development.  
    <br />
    <a href="https://coastal.la.gov/our-plan/"><strong>Louisiana’s Coastal Master Plan »</strong></a>
    <br />
    <br />
    <a href="https://www.google.com"> View Sub Sample Link</a>
    ·
    <a href="https://www.google.com">View Public Site</a>
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#jupyter-notebook-set-up">Jupyter Notebook Set Up</a></li>
        <li><a href="#explore-sample-notebooks">Explore Sample Notebooks</a></li>
      </ul>
    </li>
    <li><a href="#github-management">GitHub Management</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

<!-- GETTING STARTED -->
## Getting Started

There are three options for accessing Jupyter Notebooks:

	1. Step 1: Set up your IDE:
		a. OnDemand Jupyter Lab
			i. Connect to CPRA Master Plan kernel
		b. OnDemand VSCode Server
			i. Connect to CPRA Master Plan kernel
		c. Local IDE SSH-ed into Bridges
			i. Connect to CPRA Master Plan kernel - still troubleshooting

### Jupyter Notebook Set Up

1) Log in to [Bridges-2 Open OnDemand](https://ondemand.bridges2.psc.edu/) with your PSC credentials.
2) Choose Jupyter Notebook: Bridges-2.

    <img src="images/on_demand_options.png" alt="Screenshot of OnDemand Menu Page with Jupyter Lab option surrounded by red rectangle." width="500" height="300">

3) Enter the settings shown below. Be sure to use the RM-shared partition unless you want a whole node (128 cores). You can also adjust the `--ntasks-per-node=1` parameter to specify the number of cores you want. 1 or 2 cores is probably enough to get started.
4) This step only needs to be done the first time you log into OnDemand: From the File menu, choose New -> Terminal. In the terminal run this script: `/ocean/projects/bcs200002p/shared/jupyter/setup.sh`. This will install the custom Python kernel Matt Yoder created and make a link to the shared jupyter directory in your home directory on Bridges-2. After running the script, refresh your browser as instructed in the script output.
5) In the Jupyter file browser, browse to the jupyter link created in the previous step and open the `read_data_example.ipynb` notebook (or create a new notebook). Be sure to run the notebook using the CPRA Master Plan (Python) kernel, which includes the `cpra.mp.data` library and its dependencies. 

### Explore Sample Notebooks

Review example notebooks to learn best practices on accessing/manipulating data

#### Template Notebook One `templates/scenario_one_v4.ipynb` Description:

The Salinity Analysis notebook aims to demonstrate a few different functionalities provided by the cpra.mp.data package and raster data. The main goal of this notebook is to identify areas where salinity levels have exceeded a certain threshold and have caused the die-off of freshwater marsh vegetation.
    - OVERALL PROCESS:
        - Pull two week salinity data from Master Plan API for selected scenario and time period
        - Pull freshwater marsh vegetation raster data from Master Plan API for selected scenario, model, and time period
        - Join salinity and vegetation data using rasterio and numpy to create windowed lookup arrays
        - Analyze the joined data to identify areas where salinity levels exceed the threshold and have caused die-off of freshwater marsh vegetation
        - Visualize results using matplotlib and altair

#### Template Notebook Two Description:

This notebook demonstrates a project-level cost-benefit analysis through map display functionalities and timeseries plots are demonstrated. 

    - OVERALL PROCESS:
          - Loop through land rasters at veg cell resolution and aggregate at project level based on veg->hydro->eco-region->project/model group crosswalks and plot timeseries of total land over year for a single project.
        - come back for February - spatial aggregation of matt's 3-digit concatenation on land type (to add maintained land as benefit)
    - Example of how to change font sizes/types/colors
    - Generally connect to MPD PostgreSQL db (New Name Alert: Model Attribute Database?)
      - Should this connection function be stored in PSC library?

## Data:

### Master Plan Data Package

Created by Matt Yoder the [cpra.mp.data](https://github.com/pscedu/cpra.mp.data) package reads and writes data pertaining to the CPRA Master Plan. 

### Crosswalk Grids

For ease of use, several single band crosswalks were developed.

>[!IMPORTANT]
>The naming convention for CPRA crosswalks is: GridCellSize__IdCastOn.tif. For example, `veg_grid_cell_v001__hydro_compartment_v001.tif` contains the v001 hydrocompartment id values cast on to the veg grid cells. All rasters and csvs can be found in shared/grid folder

| Name | File Name | Grid Cell | Id Cast On |
| ---- | --------- | --------- | ---------- |
| Morph-Hydro Raster | morph_pixel_v001__hydro_compartment_v001.tif | Morph Pixel | Hydrocompartment Id |
| Morph-Veg Raster | morph_pixel_v001__veg_grid_cell_v001.tif | Morph Pixel | Veg Grid Cell Id |
| Veg-Hydro Raster | veg_grid_cell_v001__hydro_compartment_v001.tif | Veg Grid Cell | Hydrocompartment Id |
| Veg-EcoRegion Raster | veg_grid_cell_v001__ecoregion_v001.tif | Veg Grid Cell | EcoRegion Id |

*In Development:* 
- [ ] Morph -> region
- [ ] Morph -> ecoregion
- [ ] Morph -> hydro compartment
- [ ] Veg -> region
- [ ] Veg-> ecoregion
- [ ] Veg -> hydro compartment

## GitHub Management

**COPY NEEDED**

#### Additional Package Requirements

- IF YOU NEED TO play around with new libraries for manipulating data:
  - Create a conda environment in your personal folder on bridges using standard python version 
  - Test/figure out workflow
  - Confer with matt on adding to the Kernal if needed
- If this is something that ultimately will go into QAQC portal workflow
  - Confer with Matt on development plan


#### File Saving Conventions 

If you need to save outputs from your analysis to raster files, please use the following profile settings for consistency with other CPRA Master Plan raster data.
```
veg_profile = {
        "compress": "zstd".upper(),
        "compression_level": 6,
        "count": 1,
        "crs": "epsg:26915",
        "driver": "COG",
        "dtype": np.int32,
        "nodata": -9999,
        "resampling": "NEAREST",
        "width": 1052,
        "height": 365,
        "transform": rio.transform.from_bounds(404710, 3199480, 909670, 3374680, width=1052, height=365)
    }
```
*From Matt:*

Settings for the cogs are:
Compression algorithm: zstd
 
Compression level: 6
Nodata value: -9999
Resampling algorithm: nearest neighbor
 
_For more documentation, please refer to the [PSC Bridges-2 User Guide](https://www.psc.edu/resources/bridges-2/user-guide/)_

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- Project Structure  -->
## Project Structure

```
notebooks/
├── templates/                                     # Sample/template notebooks for common workflows
│   └── scenario_one_v4.ipynb                      # Salinity & vegetation die-off analysis example
├── images/                                        # Screenshot/documentation images
├── README.md                                      # This file
└── LICENSE                                        # Project license
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTRIBUTING -->
## Contributing

If you have a suggestion that would make this better, please *COPY NEEDED*

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- LICENSE -->
## License

Distributed under the project_license. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- CONTACT -->
## Contact

Matt Yoder - CPRA/PSC - myoder@psc.edu (or relevant point of contact)

Project Link: [https://github.com/CPRA-MP/notebooks](https://github.com/CPRA-MP/notebooks)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

- Matt Yoder for the `cpra.mp.data` package and kernel setup
- PSC Bridges-2 support team
- CPRA Master Plan modeling team



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[product-screenshot]: images/screenshot.png
[Python.js]: https://www.python.org/static/community_logos/python-powered-w-140x56.png
[Python-url]: https://www.python.org/