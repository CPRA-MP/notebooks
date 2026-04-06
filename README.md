<a id="readme-top"></a>

<h3 align="center"> Analysis Notebook User Guide</h3>

  <p align="left">
    This repository contains standardized Python Jupyter notebook templates with example best-practices for pulling data generated for the 2029 Louisiana Coastal Master Plan using <a href="https://github.com/pscedu/cpra.mp.data?tab=readme-ov-file"><strong>the Master Plan Data Package</strong></a> to analyze the outputs of the ICM, CLARA, and PT models that are not currently visualized in the QAQC Portal. These templates aim to streamline the process of data extraction, transformation, visualization, and analysis, and serve as a staging ground for future QAQC Portal development. 
    <br />
    <br />
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#getting-started">Getting Started with Analysis Notebooks and IDE</a>
      <ul>
        <li><a href="#jupyter-lab-set-up">Jupyter Lab Set Up</a></li>
      </ul>
    </li>
    <li><a href="#naming-conventions">Naming Conventions</a></li>
    <li>
      <a href="#explore-template-notebooks">Explore Template Notebooks</a>
      <ul>
        <li><a href="#master-plan-data-package">Master Plan Data Package</a></li>
        <li><a href="#crosswalk-grids">Crosswalk Grids</a></li>
      </ul>
    </li>
    <li><a href="#github-management">GitHub Management</a>
        <ul>
        <li><a href="#strip-notebook-outputs">Strip Notebook Ouputs</a></li>
        <li><a href="#additional-package-requirements">Additional Package Requirements</a></li>
      </ul>
    </li>
    <li><a href="#project-structure">Project Structure</a></li>
  </ol>
</details>

<!-- GETTING STARTED -->
### Getting Started with Analysis Notebooks and IDE

There are two options for accessing Anlaysis Notebooks:
- **OnDemand Jupyter Lab**
  - Connect to CPRA Master Plan kernel
- **OnDemand VSCode Server**
  - Connect to CPRA Master Plan kernel

#### Jupyter Lab Set Up

1) Log in to [Bridges-2 Open OnDemand](https://ondemand.bridges2.psc.edu/) with your PSC credentials.
2) Choose Jupyter Lab: Bridges-2.

    <img src="images/on_demand_options.png" alt="Screenshot of OnDemand Menu Page with Jupyter Lab option surrounded by red rectangle." width="500" height="300">

3) Enter the settings shown below. Be sure to use the RM-shared partition unless you want a whole node (128 cores). You can also adjust the `--ntasks-per-node=1` parameter to specify the number of cores you want. 1 or 2 cores is probably enough to get started.
4) This step only needs to be done the first time you log into OnDemand: From the File menu, choose New -> Terminal. In the terminal run this script: `/ocean/projects/bcs200002p/shared/jupyter/setup.sh`. This will install the custom Python kernel Matt Yoder created and make a link to the shared jupyter directory in your home directory on Bridges-2. After running the script, refresh your browser as instructed in the script output.
5) In the Jupyter file browser, browse to the jupyter link created in the previous step and open the `read_data_example.ipynb` notebook (or create a new notebook). Be sure to run the notebook using the CPRA Master Plan (Python) kernel, which includes the `cpra.mp.data` library and its dependencies. 

### Naming Conventions

When creating new notebooks for your analyses, please follow these conventions to keep things organized and easily searchable. The naming structure should indicate model/domain, the general purpose, and a brief detail describing the notebook's content (e.g., `prefix_generalpurpose_detail.ipynb`). The general purpose can be qaqc, analysis etc., and the detail should provide a brief description of what the code does. Examples include: qaqc_salinity_veg_investigation.ipynb, analysis_project_benefits.ipynb with the prefix 'template_' added for these demonstration notebooks.

#### Prefix Definitions

- icm_ : ICM notebooks  
- clara_ : CLARA notebooks  
- pct_ : PCT notebooks  
- cma_ : CMA notebooks  
- template_ : shared example and demonstration notebooks

#### Naming Guidance

- Use lowercase letters.
- Separate words with underscores.
- Keep names concise but descriptive.
- Start with the correct prefix, then include the topic and purpose.

#### Examples

- icm_qaqc_salinity_veg_investigation.ipynb
- icm_qaqc_habitat_change_summary.ipynb
- clara_analysis_project_benefits.ipynb
- icm_analysis_land_area_timeseries.ipynb
- template_analysis_project_benefits.ipynb

### Explore Template Notebooks

Review example notebooks to learn best practices on accessing/manipulating data

#### Template Notebook One `template_qaqc_salinity_veg_investigation.ipynb` Description:

The Salinity Analysis notebook aims to demonstrate a few different functionalities provided by the cpra.mp.data package and raster data. The main goal of this notebook is to identify areas where salinity levels have exceeded a certain threshold and have caused the die-off of freshwater marsh vegetation. This notebook demonstrates a block-wise raster workflow to identify the first year freshwater marsh pixels meet a salinity threshold condition for a selected scenario and model group. It loads salinity and vegetation data from CPRA sources, maps hydrocompartment salinity values to vegetation grid cells with a crosswalk raster, and processes windows to handle large coastal datasets efficiently. It then writes the threshold-year output raster, converts results to polygons, and builds an interactive map for QA/QC and interpretation.

#### Template Notebook Two Description `template_analysis_project_benefits.ipynb` Description:

Template Notebook Two demonstrates how to do efficient, large-raster coastal analysis end to end: define project/scenario scope, process rasters in windows (instead of loading full grids), and aggregate pixel counts to meaningful project metrics. This notebook computes project land area and project benefits over time by comparing Future With Action (FWA) model groups to a Future Without Action (FWOA) baseline across selected scenarios. It uses windowed raster processing with an ecoregion crosswalk to efficiently count land pixels by year and ecoregion, then converts those counts into area metrics (acres or square meters) and project-level benefit values. Finally, it produces faceted interactive time-series charts that let users switch between benefit and land-area views for each project and model group.

### Master Plan Data Package

The [cpra.mp.data](https://github.com/pscedu/cpra.mp.data) package reads and writes data pertaining to the CPRA Master Plan.

### Crosswalk Grids

For ease of use, several single band crosswalk rasters were developed.

>[!IMPORTANT]
>The naming convention for CPRA crosswalks is: GridCellSize__IdCastOn.tif. For example, `veg_grid_cell_v001__hydro_compartment_v001.tif` contains the v001 hydrocompartment id values cast on to the veg grid cells. All rasters and csvs can be found in shared/grid folder

| Name | File Name | Grid Cell | Id Cast On |
| ---- | --------- | --------- | ---------- |
| Morph-Hydro Raster | morph_pixel_v001__hydro_compartment_v001.tif | Morph Pixel | Hydrocompartment Id |
| Morph-Veg Raster | morph_pixel_v001__veg_grid_cell_v001.tif | Morph Pixel | Veg Grid Cell Id |
| Morph-Ecoregion Raster | morph_pixel_v001__ecoregion_v001.tif | Morph Pixel | EcoRegion Id |
| Veg-Hydro Raster | veg_grid_cell_v001__hydro_compartment_v001.tif | Veg Grid Cell | Hydrocompartment Id |
| Veg-EcoRegion Raster | veg_grid_cell_v001__ecoregion_v001.tif | Veg Grid Cell | EcoRegion Id |


## GitHub Management

This repository is managed on GitHub, changes and additions to the notebooks are automatically pushed daily from Bridges-2. Additionally, the repository utilizes [`nbstripout`](https://pypi.org/project/nbstripout/) to remove output cells for cleaner version control.

### Strip Notebook Outputs

This repository uses `nbstripout` to remove output cells from Jupyter Notebooks before committing them to the repository. This helps keep the repository clean and reduces file size. To set up `nbstripout` in your local environment, follow these steps:

1. Install `nbstripout` using conda: `conda install -c conda-forge nbstripout`
2. Navigate to the repository directory in your terminal.
3. Run the command: `nbstripout --install`

### Daily Push from Bridges-2

This `notebooks` folder is configured to sync from Bridges-2 to this GitHub repository on a daily schedule, so updates generated on Bridges-2 are automatically pushed each day.

### Additional Package Requirements

- IF YOU NEED TO explore new libraries for manipulating data:
  - Create a conda environment in your personal folder on bridges using standard python version 
  - Test/figure out workflow
  - Confer with Matt on adding to the Kernal if needed
- If this is something that ultimately will go into QAQC portal workflow
  - Confer with Matt on development plan

_For more documentation, please refer to the [PSC Bridges-2 User Guide](https://www.psc.edu/resources/bridges-2/user-guide/)_

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- Project Structure  -->
## Project Structure

```
notebooks/
├── images/                                          # Screenshot/documentation images
├── production/
│   ├── template_analysis_project_benefits.ipynb
│   ├── template_qaqc_salinity_veg_investigation.ipynb
│   ├── template_read_data_example.ipynb
│   ├── template_visualization_examples.ipynb
├── README.md                                        # This file
└── LICENSE                                          # Project license
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[product-screenshot]: images/screenshot.png
[Python.js]: https://www.python.org/static/community_logos/python-powered-w-140x56.png
[Python-url]: https://www.python.org/
