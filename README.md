# SemProject_MLEngine — Deliverable 1: Dataset Exploration

This repository contains a Google Colab notebook prepared for ICS 3202 Deliverable 1. The notebook examines the `stop_times.txt` table from the Digital Matatus Nairobi transport dataset; this deliverable does not build a model or application.

## Team

| Name | Registration number |
|---|---|
| Dwalo Aaron Lawanda | 190519 |
| Asiaba Bradley | 168970 |
| Wanjiru C Catherine Njoki | 189125 |

## The notebook

File: `DigitalMatatusNairobi_Exploration.ipynb`

The notebook downloads the dataset when it is run, loads the `stop_times.txt` table, and answers four exploration questions in separate cells.

It shows:

- the number of rows and columns;
- the datatype of each column;
- the number of missing values in each column of `stop_times.txt`; and
- a dataframe named `df_sample`, made by combining the first 15 rows with the last 20 rows.


## Dataset

**Name:** Digital Matatus Nairobi GTFS, a public transport dataset containing matatu routes, stops, and scheduled times.

Original source: [Digital Matatus](https://www.digitalmatatus.com/)

Retrieved from: Mobility Database feed `mdb-1815`, dated snapshot:  
<https://files.mobilitydatabase.org/mdb-1815/mdb-1815-202406071505/mdb-1815-202406071505.zip>

Retrieved on: 10 September 2026

SHA-256 of the downloaded zip:`d18b4890281efeb54b1bb02e45db8adc26b54c6f39c991124ef5a896aa0c68c4`

This feed is a Digital Transport for Africa training distribution of the Digital Matatus survey conducted in 2019. The `feed_info.txt` file identifies the publisher as “TRAINING”, but the underlying data comes from the genuine 2019 survey.

Table explored: `stop_times.txt`, containing the columns `trip_id`, `arrival_time`, `departure_time`, `stop_id`, and `stop_sequence`.

This is historical data. It was surveyed in 2019, and its service calendar ends on 31 December 2020. Routes, stops, fares, and operating times may have changed since then, so the feed should be treated as a historical baseline rather than a current timetable.

### Licence and provenance

The publisher does not state an explicit data licence for this download. An older openAFRICA record for the Digital Matatus GTFS, last updated in March 2016, links to CC0 but labels the licence as “other-license-specified”; it also predates the 2019 survey used here. The CC BY-NC-ND licence attached to the 2015 Digital Matatus paper applies to the article and does not establish a licence for this dataset. For that reason, we identify the dataset by its source URL, retrieval date, and SHA-256 checksum instead of assigning it a licence tag. Until the publisher confirms the reuse terms, the data files are not re-hosted in this repository; the notebook downloads the source archive when it runs.



