<a id="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://www.github.com/CPRA-MP/notebooks">
    <img src="images/Primary Logo 1 Full Color RGB HighRes.png" alt="Logo" width="400" height="80">
  </a>

<h3 align="center">CPRA - Jupyter Notebook User Guide</h3>

  <p align="center">
    Lorem ipsum dolor sit amet consectetur adipiscing elit. Quisque faucibus ex sapien vitae pellentesque sem placerat. In id cursus mi pretium tellus duis convallis. Tempus leo eu aenean sed diam urna tempor. Pulvinar vivamus fringilla lacus nec metus bibendum egestas. Iaculis massa nisl malesuada lacinia integer nunc posuere. Ut hendrerit semper vel class aptent taciti sociosqu. Ad litora torquent per conubia nostra inceptos himenaeos.
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
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#clone-repo">Clone</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

<img src="images/website_ad_screenshot.png" alt="Public Website" width="400" height="200">

  
<p align="right">(<a href="#readme-top">back to top</a>)</p>


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


### Explore Sample Jupyter Notebooks

Review example notebooks to learn best practices on accessing/manipulating data

#### Sample Notebook One Salinity Analysis: 

The Salinity Analysis notebook aims to demonstrate a few different functionalities provided by the cpra.mp.data package and raster data. 
  - Two week salinity with freshwater vegetation (to show where this change would have caused a change in vegetation / vegetation die-off)
    - Two conditions (A True and B True) and export map or IDs 
    - Finding where salinity wiped out vegetation, salty areas surpassed two-week salinity find where salinity crossed a threshold and WHERE THERE was freshwater species - spit out IDs (VEG GRID CELL IDS)
  - Functionality Demonstrated:
    - Maps of input data directly pulled from api/bridges for this analysis
      - Raster (Veg cell) map of vegetation
      - Vector (hydro comp) map of salinity
    - OUTPUT: Raster (Veg cell) map of outputs
      - Ability to zoom in/out of maps
      - Filtering data 


#### Sample Notebook 2 Description:

This notebook demonstrates a project-level cost-benefit analysis through map display functionalities and timeseries plots are demonstrated. 

        - OVERALL PROCESS:
          - Loop through land rasters at veg cell resolution and aggregate at project level based on veg->hydro->eco-region->project/model group crosswalks and plot timeseries of total land over year for a single project.
        - come back for February - spatial aggregation of matt's 3-digit concatenation on land type (to add maintained land as benefit)
    - Example of how to change font sizes/types/colors
    - Generally connect to MPD PostgreSQL db (New Name Alert: Model Attribute Database?)
      - Should this connection function be stored in PSC library?

## Usage 

### Set Up Your Own Jupyter Notebook

#### Using On Demand 

Navigate to your personal folder on On Demand

#### Git Management

#### Additional Package Requirements

- IF YOU NEED TO play around with new libraries for manipulating data:
  - Create a conda environment in your personal folder on bridges using standard python version 
  - Test/figure out workflow
  - Confer with matt on adding to the Kernal if needed
- If this is something that ultimately will go into QAQC portal workflow
  - Confer with Matt on development plan

_For more documentation, please refer to the [PSC Bridges-2 User Guide](https://www.psc.edu/resources/bridges-2/user-guide/)_

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- ROADMAP -->
## Roadmap

### Milestones

- [Track our progress here](https://www.google.com)


See the [open issues](https://www.google.com) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- Folder Structure  -->
## Project Structure

```
project_folder/
├── project_subfolder/                             # NOTE: Description
│   ├── script_01.py                               # NOTE: Description
│   └── script_02.py                               # NOTE: Description
├── project_subfolder/                             # NOTE: Description
│   ├── script_03.py                               # NOTE: Description
│
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

First Name Last Name - Organization Name - Email Address

Project Link: [https://github.com/CPRA-MP/notebooks](https://github.com/CPRA-MP/notebooks)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments


<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[product-screenshot]: images/screenshot.png
[Python.js]: https://www.python.org/static/community_logos/python-powered-w-140x56.png
[Python-url]: https://www.python.org/