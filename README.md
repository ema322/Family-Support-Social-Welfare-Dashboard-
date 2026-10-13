# Family Needs & Food/Housing Analytics \| Power BI

An interactive Power BI project using two Excel datasets ---
`Needs.xlsx` and `Food.xlsx` --- to explore family needs, household
composition, breadwinner status, work status, income, accommodation
types, and population summaries across **Syria, Yemen, Iraq, and
Libya**.
--------------------------------------------------------------------

####
<img width="602" height="340" alt="Screenshot 2026-10-13 041206" src="https://github.com/user-attachments/assets/7b36af36-58e4-4463-8a05-c0d4140614d0" />



---------------------------------------------------------------------

> **Important:** This README documents the two uploaded workbooks and a
> suggested Power BI setup. Update the repository URL, screenshots, and
> any measure names to match your final `.pbix` report. The data files
> contain personal names and location information; check permissions and
> remove or anonymize sensitive data before publishing them publicly.

## Table of Contents

-   [Project Overview](#project-overview)
-   [Business Questions](#business-questions)
-   [Datasets](#datasets)
-   [Data Dictionary](#data-dictionary)
-   [Data Quality Notes](#data-quality-notes)
-   [Tools and Technologies](#tools-and-technologies)
-   [Recommended Repository
    Structure](#recommended-repository-structure)
-   [Getting Started](#getting-started)
-   [Power BI Setup](#power-bi-setup)
-   [Data Model and Relationships](#data-model-and-relationships)
-   [Suggested Measures](#suggested-measures)
-   [Suggested Dashboard Pages](#suggested-dashboard-pages)
-   [How to Use the Report](#how-to-use-the-report)
-   [Validation Checklist](#validation-checklist)
-   [Privacy and Responsible Use](#privacy-and-responsible-use)
-   [Limitations](#limitations)
-   [Future Improvements](#future-improvements)
-   [License](#license)
-   [Author](#author)

## Project Overview

This project brings together two workbooks that describe related family
and household information:

-   **Needs.xlsx** --- record-level family information, household
    demographics, breadwinner, work status, income, and indicated needs.
-   **Food.xlsx** --- dated country/city/place summaries with houses,
    members, male/female counts, and accommodation-type counts.

The files have different row structures and levels of detail. They
should be explored separately first and only related in Power BI after
checking whether a reliable shared key exists. Do not append them
directly: their columns and grain are different.

## Business Questions

The analysis can help investigate questions such as:

1.  How many family records and members are represented in the Needs
    dataset?
2.  How are records distributed across countries, cities, and places?
3.  How many records identify the mother or father as breadwinner?
4.  What work-status and income information is recorded?
5.  Which needs --- food, clothes, education, or money --- are most
    frequently indicated?
6.  How do members and male/female counts vary in the Food dataset over
    time and by location?
7.  How are recorded housing types distributed across places?
8.  How do results change when filtering by country, date, city, place,
    or household type?

These are analysis questions, not conclusions about the wider
populations represented by the data.

## Datasets

### 1. `Needs.xlsx`

-   **Worksheet:** `Sheet1`
-   **Rows:** 1,701
-   **Columns:** 21
-   **Countries present:** Syria, Yemen, Iraq, and `Lybia` (spelled this
    way in the source)
-   **Breadwinner categories observed:** `Father`, `Mother`
-   **House categories observed:** `Flat`, `Room`, `Tent`, `House`

This workbook appears to contain one row per family/household record,
but confirm the intended record grain with the data provider before
describing it as a unique family. It includes a `Name` column and
detailed place information, so it may contain personal or sensitive
data.

#### Columns in `Needs.xlsx`

  -----------------------------------------------------------------------
  Column                  Description based on    Notes
                          the field name          
  ----------------------- ----------------------- -----------------------
  `Index`                 Source record/index     Check uniqueness and
                          identifier              meaning before using as
                                                  a key.

  `Country`               Country label           Source uses `Lybia`;
                                                  consider standardizing
                                                  to `Libya` after
                                                  documenting the change.

  `City`                  City or area            Text field.

  `PlaceName`             Place, camp, or         Contains Arabic and
                          settlement name         other text values.

  `Name`                  Person/family name      Potentially
                                                  identifying; remove or
                                                  anonymize for public
                                                  sharing.

  `Breadwinner`           Recorded breadwinner    Values observed:
                          category                `Father`, `Mother`.

  `Male`                  Male count              Confirm whether this
                                                  includes all ages.

  `Female`                Female count            Confirm whether this
                                                  includes all ages.

  `Under 5 Male`          Male children under age Numeric count.
                          5                       

  `Under 5 Female`        Female children under   Numeric count.
                          age 5                   

  `6-18 Male`             Males aged 6--18        Numeric count.

  `6-18 Female`           Females aged 6--18      Numeric count.

  `Over 18`               Count over age 18       The field does not
                                                  distinguish gender;
                                                  confirm definition.

  `House`                 Household accommodation Values observed:
                          type                    `Flat`, `Room`, `Tent`,
                                                  `House`.

  `Work/Yes`              Indicator associated    Nonblank values
                          with work status "Yes"  observed are `1`; blank
                                                  values are common.

  `Work/No`               Indicator associated    Nonblank values
                          with work status "No"   observed are `1`; blank
                                                  values are common.

  `Income`                Income value or         Units, period, and
                          indicator               meaning must be
                                                  confirmed.

  `Need/food`             Food need indicator     Nonblank values
                                                  observed are `1`;
                                                  confirm coding.

  `Need/Clothes`          Clothing need indicator Nonblank values
                                                  observed are `1`;
                                                  confirm coding.

  `Need/Education`        Education need          Nonblank values
                          indicator               observed are `1`;
                                                  confirm coding.

  `Need/Money`            Money/financial need    Nonblank values
                          indicator               observed are `1`;
                                                  confirm coding.
  -----------------------------------------------------------------------

### 2. `Food.xlsx`

-   **Worksheet:** `Sheet1`
-   **Rows:** 12,654
-   **Columns:** 12
-   **Date range:** 1 January 2016 -- 20 November 2018
-   **Countries present:** Syria, Yemen, Iraq, and `Lybia` (source
    spelling)
-   **Distinct dates in the file:** 1,055

This workbook contains dated summaries by country, city, and place. It
includes house totals, member totals, male/female counts, and separate
accommodation-type fields.

#### Columns in `Food.xlsx`

  -----------------------------------------------------------------------
  Column                  Description based on    Notes
                          the field name          
  ----------------------- ----------------------- -----------------------
  `Date`                  Date associated with    Use a Date data type in
                          the record              Power BI.

  `Country`               Country label           Source uses `Lybia`;
                                                  standardize
                                                  consistently if
                                                  appropriate.

  `City`                  City or area            Text field.

  `PlaceName`             Place, camp, or         May contain Arabic
                          settlement name         text.

  `Houses`                Number of               Confirm whether this
                          houses/households       means housing units,
                          reported                households, or another
                                                  measure.

  `Members`               Total members reported  Confirm the source
                                                  definition and whether
                                                  rows are additive over
                                                  time.

  `Male`                  Male count              Confirm whether it
                                                  reconciles with
                                                  `Members`.

  `Female`                Female count            Confirm whether it
                                                  reconciles with
                                                  `Members`.

  `Room`                  Count associated with   Blank for many records;
                          room accommodation      blank does not
                                                  automatically mean
                                                  zero.

  `Flat`                  Count associated with   Blank for many records;
                          flat accommodation      blank does not
                                                  automatically mean
                                                  zero.

  `House`                 Count associated with   Blank for many records;
                          house accommodation     blank does not
                                                  automatically mean
                                                  zero.

  `Tent`                  Count associated with   Blank for many records;
                          tent accommodation      blank does not
                                                  automatically mean
                                                  zero.
  -----------------------------------------------------------------------

## Data Quality Notes

The following checks were observed in the uploaded workbooks:

-   `Needs.xlsx` contains 1,701 rows and 21 columns. Several fields have
    missing values, especially `Work/Yes`, `Work/No`, `Income`, and the
    `Need/...` fields.
-   `Food.xlsx` contains 12,654 rows and 12 columns, with dates from
    2016-01-01 to 2018-11-20.
-   The country label `Lybia` appears in both files. If the report
    displays `Libya`, apply the same documented standardization to both
    datasets.
-   In `Food.xlsx`, `Room`, `Flat`, and `House` are blank in about 22.6%
    of rows; `Tent` is blank in about 77.4% of rows.
-   In `Needs.xlsx`, `Work/Yes` is blank in about 62.1% of rows and
    `Work/No` is blank in about 37.9% of rows. The need indicators also
    contain many blanks.
-   The initial inspection found no fully duplicated rows in either
    workbook. This does **not** prove there are no duplicate families or
    repeated place/date summaries.
-   The files have no obvious single shared unique key. Matching only on
    country, city, or place name could create many-to-many relationships
    or incorrect totals.

### How to handle blanks

Do not automatically replace every blank with zero. First determine what
blanks mean in the source: - **No / not applicable:** may be converted
according to the data definition. - **Unknown / not recorded:** should
usually remain blank or be categorized as unknown. - **Zero:** should be
used only when the source confirms the count is zero.

Document any replacements or category standardization performed in Power
Query.

## Tools and Technologies

-   **Microsoft Power BI Desktop** --- report design, data model, and
    visuals.
-   **Power Query** --- import, cleaning, and transformation of the
    Excel workbooks.
-   **DAX** --- measures and calculations, if used in the report.
-   **Microsoft Excel** --- source datasets.
-   **Git and GitHub** --- version control and project documentation.

## Recommended Repository Structure

``` text
family-needs-food-housing-analytics/
├── README.md
├── Family-Needs-Food-Housing-Analytics.pbix
├── data/
│   ├── README.md
│   ├── Needs.xlsx
│   └── Food.xlsx
├── images/
│   └── dashboard-preview.png
└── LICENSE
```

This is a recommended structure. Rename the `.pbix` file to match your
actual report. Only commit the original Excel files if you have
permission to share them and have checked them for personal,
confidential, or licensed data. Otherwise, keep them private and provide
a sanitized sample or data dictionary.

## Getting Started

### Prerequisites

1.  Windows computer.
2.  **Power BI Desktop** installed. Official download:
    https://powerbi.microsoft.com/desktop/
3.  The two Excel workbooks, if they are not already included in the
    repository.
4.  Permission to access and use the source data.

### Download or clone the repository

``` bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

Replace `YOUR-USERNAME` and `YOUR-REPOSITORY` with the actual GitHub
account and repository names.

### Open the report

1.  Open the `.pbix` file in Power BI Desktop.
2.  If Power BI asks for the data source, point it to `Needs.xlsx` and
    `Food.xlsx` in your local `data/` folder.
3.  Select **Home → Transform data** to inspect the Power Query steps.
4.  Check that column names and data types match the workbooks.
5.  Select **Close & Apply**.
6.  Select **Home → Refresh** and resolve any source-path or
    transformation errors.
7.  Save a local copy after confirming that the report refreshes.

Menu labels may vary slightly by Power BI Desktop version.

## Power BI Setup

### Import the workbooks

For each workbook:

1.  Select **Home → Get data → Excel workbook**.
2.  Select `Needs.xlsx`.
3.  Choose `Sheet1` and select **Transform Data** to inspect the data
    before loading.
4.  Repeat for `Food.xlsx`.
5.  Rename the queries clearly, for example `Needs` and `Food`.
6.  Set numeric count fields to Whole Number, `Date` to Date, and
    descriptive fields to Text.
7.  Review missing values, country spellings, and category labels before
    applying changes.

### Suggested Power Query preparation

-   Rename `Sheet1` queries to `Needs` and `Food`.
-   Standardize country labels consistently, if approved by the data
    definition.
-   Trim extra spaces in text fields where appropriate.
-   Check that `Date` is stored as a date, not text.
-   Confirm numeric fields are numeric and not accidentally imported as
    text.
-   Do not remove repeated date/place records unless the source confirms
    they are duplicates.
-   Keep an audit note of any replacements, filters, or removed rows.
-   Remove or anonymize `Name` before sharing data publicly.

## Data Model and Relationships

**Start with two separate fact tables unless you can identify a reliable
relationship.** The datasets differ in granularity: `Needs` contains
detailed family/household records, while `Food` contains dated location
summaries. Joining them on `Country`, `City`, or `PlaceName` alone may
duplicate values.

A robust model may use shared dimension tables if appropriate:

-   `DimCountry` --- standardized country key and label.
-   `DimLocation` --- city/place identifiers, if reliable identifiers
    exist.
-   `DimDate` --- calendar table for the `Food[Date]` field.
-   `Needs` --- detailed needs records.
-   `Food` --- dated summary records.

Create one-to-many relationships from dimensions to fact tables where
keys are unique and the relationship is valid. Avoid connecting the two
fact tables directly without a validated key and a clear reason. If no
reliable location/date key exists, keep their visuals separate and use
slicers independently.

## Suggested Measures

The examples below are starting points only. Verify the meaning of each
field and match table names to your Power BI model before using them.

### Needs table

``` dax
Needs Records =
COUNTROWS(Needs)
```

``` dax
Mother Breadwinner Records =
CALCULATE(
    COUNTROWS(Needs),
    Needs[Breadwinner] = "Mother"
)
```

``` dax
Father Breadwinner Records =
CALCULATE(
    COUNTROWS(Needs),
    Needs[Breadwinner] = "Father"
)
```

``` dax
Records with Food Need =
CALCULATE(
    COUNTROWS(Needs),
    Needs[Need/food] = 1
)
```

``` dax
Records with Clothing Need =
CALCULATE(
    COUNTROWS(Needs),
    Needs[Need/Clothes] = 1
)
```

``` dax
Records with Education Need =
CALCULATE(
    COUNTROWS(Needs),
    Needs[Need/Education] = 1
)
```

``` dax
Records with Money Need =
CALCULATE(
    COUNTROWS(Needs),
    Needs[Need/Money] = 1
)
```

These measures count rows where the indicator equals `1`; they do not
prove that each row represents a unique family. Use `DISTINCTCOUNT` only
if a valid unique family identifier is available.

### Food table

``` dax
Food Summary Rows =
COUNTROWS(Food)
```

``` dax
Total Members =
SUM(Food[Members])
```

``` dax
Total Houses =
SUM(Food[Houses])
```

``` dax
Total Male =
SUM(Food[Male])
```

``` dax
Total Female =
SUM(Food[Female])
```

**Important:** the sums above add all rows currently in filter context.
If each row is a repeated daily snapshot, summing across multiple dates
may overcount the same population or housing stock. Consider using a
single selected date, latest available date, or a validated
period-specific calculation instead.

### Percentage measures

Only calculate gender percentages after confirming the source
definitions and that male/female values are comparable and complete.

``` dax
Male Percentage =
DIVIDE(
    [Total Male],
    [Total Male] + [Total Female]
)
```

``` dax
Female Percentage =
DIVIDE(
    [Total Female],
    [Total Male] + [Total Female]
)
```

Format the measures as percentages in Power BI. If the dataset includes
missing or overlapping categories, document how they affect the
denominator.

## Suggested Dashboard Pages

Possible report layout:

### 1. Overview

-   KPI cards for the selected reporting scope.
-   Country slicer.
-   Date slicer for `Food`.
-   Clear labels and a visible data-period note.

### 2. Family Needs

-   Breadwinner distribution.
-   Food, clothing, education, and money need indicators.
-   Work-status breakdown, after validating how blanks are coded.
-   Filters for country, city, place, and accommodation type.

### 3. Population and Housing

-   Members, male, and female measures.
-   Housing type distribution (`Room`, `Flat`, `House`, `Tent`).
-   Country/place comparisons using a consistent date selection.

### 4. Data Quality

-   Missing-value counts.
-   Country and category spelling checks.
-   Validation of male/female totals and housing totals.
-   Reporting-period and source notes.

## How to Use the Report

1.  Open the report in Power BI Desktop.
2.  Select a country or location using the available slicers.
3.  For `Food` visuals, select a date or a clearly defined reporting
    period.
4.  Review KPI cards and charts under the selected filters.
5.  Check the measure definitions if comparing totals across dates.
6.  Clear slicers to return to the full available view.

The exact interactions depend on the slicers, relationships, and visual
interactions configured in the `.pbix` file.

## Validation Checklist

Before publishing or presenting the report:

-   [ ] Confirm the source and meaning of every column and measure.
-   [ ] Confirm whether each `Needs` row represents one unique
    family/household.
-   [ ] Confirm whether `Food` records are daily snapshots, updates, or
    independent observations.
-   [ ] Check whether `Male + Female` reconciles with `Members`.
-   [ ] Check whether housing-type fields are mutually exclusive and
    complete.
-   [ ] Check how blanks in work, income, needs, and housing columns
    should be interpreted.
-   [ ] Standardize `Lybia`/`Libya` consistently if appropriate.
-   [ ] Check that country totals and KPIs update correctly under
    filters.
-   [ ] Avoid adding repeated daily snapshot values across time unless
    that is the intended metric.
-   [ ] Refresh the report from the documented data-source paths.
-   [ ] Remove personal or confidential information before making the
    repository public.

## Privacy and Responsible Use

`Needs.xlsx` contains a `Name` field alongside location and family
details. Before uploading data to a public repository:

-   Confirm you have explicit permission to share the data.
-   Remove direct identifiers and review whether combinations of
    location and household attributes could identify people.
-   Do not upload confidential records, access credentials, or
    restricted data.
-   Prefer a sanitized sample dataset, aggregated extracts, or
    screenshots that do not expose private information.
-   Clearly identify the source, reporting period, and any known
    limitations when permitted.

## Limitations

-   The source provider, collection methodology, and official
    definitions were not included with the two workbooks.
-   Column names alone do not establish whether a blank means zero, no,
    unknown, or not applicable.
-   `Food.xlsx` includes many dates and may contain repeated snapshots;
    totals across dates can be misleading without a clear time rule.
-   The two workbooks have different structures and should not be merged
    without a validated key.
-   The analysis describes only the records supplied and should not be
    treated as a representative estimate of a whole country or
    population without evidence.


## Author

**\[Emma S]**
***EMAN SALEH ***


