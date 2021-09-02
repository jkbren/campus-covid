# Campus COVID Data
Institutes of higher education (IHEs) can play a large role in mitigating the spread of COVD-19. There is not a national repository for recording the amount of testing and case counts for individuals affiliated with universities, and as such, many administrators and local policymakers are not equipped with the most up-to-date data to inform their decision-making. This dataset is designed to be a stopgap to this problem.

In creating this dataset, we primarily relied on IHEs' "COVID Dashboards", which vary in their sophistication and informativeness. More often than not, they report the number of student/faculty/staff cases affiliated with the IHE. If a college or university has put in place a regular testing protocol, they often report the daily or weekly number of tests that have been conducted as well. These data help us piece together an ever-incomplete picture of the impact / role that IHEs have on the broader community and taken together should inform decision-making at the local and institutional levels (i.e. whether to allow students back for in-person classes, hybrid classes, online only, etc.).

In order to collect this data, we first collected the urls of thousands of IHEs' COVID Dashboards. we did this with a Python package that uses the [Google Search API](https://pypi.org/project/gsearch/). Using data from IPEDS (i.e. institution name, state, etc.), we automated several Google searches for each IHE that included the IHE's name along with keywords like "covid cases" and "covid dashboard" and "covid testing" etc. we aggregated these urls into a single dataframe, which we then used to pre-populate thousands of individual Google Sheets, one per IHE. This streamlined the data collection process, since all you need to do to collect data is click on the url for the Google Sheet of the IHE, click on the its dashboard url, and start copying the data into the sheet.

To my knowledge, this has turned into the largest dataset with time series of campus COVID cases and testing in the United States. That said, **this is not meant to replace or stand-in for expert knowledge about how to enact policy.** we hope it inspires policymakers to assemble a national database for this information, one that institutions of higher education are required to report to. This is already done in several states. In the meantime, we encourage folks to check this one out, contribute to it, and share it widely.


## Limitations
Because this dataset was formed to address the lack of nationwide (or in most cases, statewide) standards that compel institutes of higher education to report their testing and case count data---much of these data were gathered through a huge crowdsourcing effort. As such, there is possibly human error in the collection or reporting of data. Second, many schools rely on self-reported data, which can also present an opportunity for human error. Third, as time goes on, IHEs may update their own counts of testing and cases, which might produce inconsistencies with the data used here.


## Notebooks
1. [Automate the creation of individual Google Sheets](https://github.com/jkbren/campus-covid/blob/main/code/create_google_sheets.ipynb)
2. [Pull data from Google Sheets](https://github.com/jkbren/campus-covid/blob/main/code/retrieve_data_from_google_sheets.ipynb)
3. [Campus COVID dataset map](https://github.com/jkbren/campus-covid/blob/main/code/campus-covid_map.ipynb)
4. [Explore data from different colleges in the dataset](https://github.com/jkbren/campus-covid/blob/main/code/campus-covid-data_exploration.ipynb)
5. [Set up matching procedure](https://github.com/jkbren/campus-covid/blob/main/code/matching-jsd_minimization.ipynb)
6. [Main figures](https://github.com/jkbren/campus-covid/blob/main/code/main-figures.ipynb)
7. [Massachusetts analysis](https://github.com/jkbren/campus-covid/blob/main/code/analysis-massachusetts.ipynb)
8. [Case study: UMass Amherst](https://github.com/jkbren/campus-covid/blob/main/code/case-study-umass.ipynb)
9. [Statistical controls - negative binomial regression](https://github.com/jkbren/campus-covid/blob/main/code/regression-negativebinomial.ipynb)
10. [Misc: Pull county tesing data from CDC](https://github.com/jkbren/campus-covid/blob/main/code/county-level-diagnostic-testing-volume-cdc.ipynb)
11. [Misc: NYT case count data](https://github.com/jkbren/campus-covid/blob/main/code/nyt-college-data.ipynb)

## Other datasets
1. data/nyt_data_asof_2021-05-26.csv - [New York Times case counts](https://www.nytimes.com/interactive/2021/us/college-covid-tracker.html)
2. data/campus_covid_ipeds.csv - [IPEDS school data](https://nces.ed.gov/ipeds/use-the-data)
3. data/countypres_2000-2020.csv - [MIT Election data](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/VOQCHQ)
4. data/campus_covid_census.csv - subset of variables from [2018 ACS data](https://www.census.gov/programs-surveys/acs)
5. data/campus_covid_jhu_county.csv.gz - [Johns Hopkins University county-level COVID-19 data](https://linkinghub.elsevier.com/retrieve/pii/S1473309920301201)

### College Crisis Initiative (C2i) data
To access the data/campus_covid_status.csv file used in some of this work, permission is required from the College Crisis Initiative. From the [C2i website](https://collegecrisis.shinyapps.io/dashboard/): "Use of the C2i Dataset is restricted to College Crisis Intiative research affiliates and Davidson College students, faculty, and staff. Use of the data without permission is prohibited. For permission, please contact C2i@davidson.edu.".


### Main packages used  <a name="requirements"/>

This code is written in [Python 3.x](https://www.python.org) and uses the following packages:

* [Pandas](https://pandas.pydata.org/)
* [Numpy](http://numpy.scipy.org/)
* [geopandas](https://geopandas.org/) (for replicating the map figures)
* [gspread](https://gspread.readthedocs.io/en/latest/) 


## Data and findings
To download the csv of the full dataset, see data folder. This dataset was built by heavily relying on a Python to Google sheets interface. I learned about this tool [here](https://www.twilio.com/blog/2017/02/an-easy-way-to-read-and-write-to-a-google-spreadsheet-in-python.html). To recreate the dataset entirely, you will need to go through the steps to enable API acccess [here](https://gspread.readthedocs.io/en/latest/oauth2.html#enable-api-access).

State-by-state Google sheets (with separate tabs for each school) and a [Reference](https://docs.google.com/spreadsheets/d/1GMu4fful47nUIFlwl293cPqPGG0XX3uIl0zno-bTJbY/edit?usp=sharing) Google sheet can be found in this drive [here](https://drive.google.com/drive/folders/19MLhkjQl3qhlGSmwD2MVbqOE_7ZaID0j?usp=sharing).

The main finding of this work so far concerns campus testing from IHEs. 

- - - -

<p align="center">
<img src="figs/pngs/campus_covid_map.png" alt="county_level" width="95%"/>
</p>

**<p align="center">Current status of the Campus Covid dataset.**

- - - -

<p align="center">
<img src="figs/pngs/matching_casedeaths_x1.png" alt="county_level" width="95%"/>
</p>

**<p align="center">Counties with IHEs with primarily in-person vs. primarily online Fall 2020.**

- - - -

## Citation
If you use this data or would like to cite this work:

Bibtex: 
```text
@article{Klein2021campus,
    title = {{Higher education responses to COVID-19 in the United States: Evidence for the impacts of university policy}},
    author = {Klein, Brennan and Generous, Nicholas and McCabe, Stefan and Bhadricha, Zarana and Gunashekar, Rishab and Kori, Preeti and Li, Bodian and Green, Jon and Chinazzi, Matteo and Lazer, David and Marsicano, Christopher R. and Scarpino, Samuel V. and Vespignani, Alessandro}
    journal = {medRxiv},
    year = {2021},
    pages = {1--30},
    volume = {2021},
}
```

## See also:

* [New York Times data](https://www.nytimes.com/interactive/2020/us/covid-college-cases-tracker.html)
* [NPR article about testing](https://www.npr.org/2020/10/06/919159473/even-in-covid-hot-spots-many-colleges-arent-aggressively-testing-students)
* [College Crisis Initiative](https://collegecrisis.shinyapps.io/dashboard/)


# Example time series of testing and case counts:

<p align="center">
<img src="figs/pngs/example_Northeastern.png" alt="county_level" width="75%"/>
</p>

<p align="center">
<img src="figs/pngs/example_UofA.png" alt="county_level" width="75%"/>
</p>

<p align="center">
<img src="figs/pngs/example_NCState.png" alt="county_level" width="75%"/>
</p>

<p align="center">
<img src="figs/pngs/example_UCLA.png" alt="county_level" width="75%"/>
</p>

<p align="center">
<img src="figs/pngs/example_UIUC.png" alt="county_level" width="75%"/>
</p>

Find these and many more in the code/campus-covid-data_exploration.ipynb file, or in the figs/pngs/ file.
