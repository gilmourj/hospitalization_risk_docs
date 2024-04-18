# Hospitalization Risk

[DE-SynPUF Hospitalization Risk](https://github.com/gilmourj/NSAPH-Homework-Gilmour) is a project by [Jonathan Gilmour](https://gilmourj.github.io/)

## What is this Project?
This is a python project for accessing US CMS DE-SynPUF data and calculating all-cause inpatient hospitalization risk from the data, using prespecified groups.

## Getting Started


## Usage
All the methods to download CMS DE-SynPUF data and to calculate all-cause inpatient hospitalization risk can be run on the command line or imported as a package and used in other projects.

### To import the package
It is recommended to create a virtual environment to run the code. This can be done with the following
```
python3 -m venv myenv
source myenv/bin/activate
```

Install the package
`pip install git+https://github.com/gilmourj/NSAPH-Homework-Gilmour.git`


Download and install dependencies
`pip download -d https://github.com/gilmourj/NSAPH-Homework-Gilmour -r requirements.txt`

### Functions
* download_files('path/to/output/directory')
* hospitalization_risk(stratifications, 'path/to/data/directory', 'path/to/output/directory')
    * stratifications should be in a list format and the options are ['sex', 'race', 'age', 'all']

Example usage:
```
import synpuf_hospitalization_risk as hr

# download DE-SynPUF files
hr.download_files('data/')

# calculate all-cause hospitalization risk with Sex and Race prespecified stratification. 
# We will read from the data/ directory and write to output/
hr.hospitalization_risk(['sex', 'race'], 'data/', 'output/')

# calculate all-cause hospitalization risk with Sex, Race, and Age stratifications. 
# We will read from the data/ directory and write to output/
hr.hospitalization_risk(['all'], 'data/', 'output/')
```

## Project layout

    src/
        synpuf_hospitalization_risk/
            __init__.py
            get_hospitalization_risk.py
            get_synpuf_files.py

## Decisions and Considerations
The way that I calculate age is a shorthand. I'm calculating age using the year of the beneficiary file and the beneficiary birth date. For those beneficiaries with hospitalization claims, the more correct age calculation would take the date of the inpatient admission and calculate age (though this works _only_ for those beneficiaries that can be matched to an inpatient claim). If I had more time, I would implement this logic.

I spent a lot of time working to make sure that the functions in this project were accessible both on the command line and as a python package. I probably should have just focused on the aim of the assignment and saved myself some time! It's very satisfying that they all run, though.

This was the first time I worked with dask, and it took some getting used to (and the process of trying to group by stratifications and count unique DESYNPUF_IDs and CLM_ADMSN_DTs was painful). That said, it's immensely powerful for manipulating large datasets.

## Acknowledgments: 
* the vast majority of the code to download DE-SynPUF data in the get_synupf_files.py file comes from OHDSI https://github.com/OHDSI/ETL-CMS/blob/master/scripts/get_synpuf_files.py.
* Starter code and assignment direction by Michelle Audirac