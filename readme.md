# This is a sample

The file in this repo is a deidentified and simplified version of a sql ETL and analysis workflow for medical data. I've created many similar scripts in work settings, but can't share those files for obvious reasons:

1. They contain private medical information
2. They are proprietary property and contained proprietary data from the company where I worked
3. The sql scripts are typically part of a larger workflow that incorporates multiple systems, for example;
    Multiple data sources from disparate databases or other data storage solutions -> python transformation -> load into sql database -> sql ETL -> load into Tableau or other analytics platform

Given that I couldn't share copies of my work, I decided to independently create an ETL script using public data. Specifically, I pulled a synthetic data set created by CMS for public use. [This is a link to that data](https://www.cms.gov/data-research/statistics-trends-and-reports/medicare-claims-synthetic-public-use-files/cms-2008-2010-data-entrepreneurs-synthetic-public-use-file-de-synpuf/de10-sample-1).

This script illustrates my understanding of common sql functions and past experience transforming complex medical data within a database environment. 