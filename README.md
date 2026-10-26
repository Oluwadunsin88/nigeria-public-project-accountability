 Nigeria Public Project Accountability Intelligence System

A data analytics project exploring public project delivery, reporting
completeness, and accountability in Anambra State, Nigeria.

Project status: Initial data audit and exploratory analysis\
Dataset: 201 public project records retrieved from the Anambra
State Government Solution Lens portal\
Tools: Python, pandas, Google Colab, GitHub\
Primary focus: Data quality, project status, geographic
> distribution, and records requiring verification



 1. Project Overview

Public project dashboards can help residents, researchers, journalists,
civil society organisations, and decision-makers understand what
government projects are listed, where they are located, and what
progress is reported.

This project examines public project records published through the
[Anambra State Government Solution Lens
portal](https://lens.anambrastate.gov.ng/insights). It uses Python to
audit the available data, summarise project statuses and locations,
identify missing information, and flag records that may require
follow-up.

The aim is not to assume that missing information proves poor
performance. Instead, the project distinguishes between what the
dataset shows, what it does not show, and what should be verified before
drawing conclusions.

 2. Problem Statement

Public project information is more useful when records are complete,
consistent, and updated. However, a project register may contain gaps in
fields such as approved cost, responsible government agency, progress,
schedule, and update date.

Without checking these gaps, a reader could mistake incomplete reporting
for evidence of project failure---or interpret a status label as proof
of delivery without supporting details.

This project applies a structured data-audit approach to help answer:

-   How many projects are listed, and what statuses are recorded?
-   How are listed projects distributed across Local Government Areas
    (LGAs)?
-   Which important fields are missing or incomplete?
-   Are there records whose reported status and progress should be
    checked?
-   What additional information would make public project reporting more
    useful?

3. Dataset

The dataset was downloaded from the [Solution Lens public project
register](https://lens.anambrastate.gov.ng/insights).

The initial extract contains 201 records and 14 columns:

  -----------------------------------------------------------------------
  Field                               Description
  ----------------------------------- -----------------------------------
  `Code`                              Project reference code

  `Title`                             Project title

  `Status`                            Recorded project status

  `Schedule`                          Schedule or delivery label, where
                                      available

  `LGA`                               Local Government Area

  `Location`                          Recorded project location

  `Responsible MDA`                   Responsible ministry, department,
                                      or agency, where available

  `Sector`                            Project sector, where available

  `Progress (%)`                      Reported progress percentage, where
                                      available

  `Approved cost (NGN)`               Approved cost in Nigerian naira,
                                      where available

  `Started`                           Recorded start date, where
                                      available

  `Target completion`                 Target completion date, where
                                      available

  `Completed`                         Completion field, where available

  `Last update`                       Date of the latest recorded update,
                                      where available
  -----------------------------------------------------------------------

Data-use note: This analysis describes the downloaded extract, not
necessarily the current state of every project. The portal may change
over time. The original source should be checked again before publishing
time-sensitive conclusions. Confirm the portal's terms and any
applicable reuse conditions before redistributing the raw data.

4. Tools and Methods

-   Python: analysis and reproducible checks.
-   pandas: data loading, missing-value assessment, grouping, and
    record-level checks.
-   Google Colab: cloud-based notebook environment; no local Python
    installation required.
-   GitHub: version control and project documentation.

The initial workflow includes:

1.  Load the CSV file and inspect the number of records, columns, and
    data types.
2.  Assess missing values in each field.
3.  Summarise project statuses and geographic distribution.
4.  Check for duplicate project codes and titles.
5.  Inspect available progress values and compare them with recorded
    status.
6.  Add review flags to an audit copy of the data.
7.  Export the audit and flagged records for further review.

The audit copy preserves the original data. Missing values are not
automatically replaced with zero, and records are not deleted simply
because they are incomplete.

 5. Initial Findings

The following findings are based on the initial dataset audit performed
in Google Colab.

 Dataset summary

  Measure                            Initial result
  -------------------------------- ----------------
  Project records                               201
  Columns                                        14
  Records marked `In progress`                  123
  Records marked `Completed`                     78
  Records with a project code                   201
  Unique project codes                          201
  Duplicate project titles found                  0

 Reporting completeness

Several important fields are incomplete in the initial extract:

  Field                     Missing records
  ----------------------- -----------------
  `Target completion`                   201
  `Sector`                              201
  `Completed`                           201
  `Approved cost (NGN)`                 200
  `Started`                             200
  `Responsible MDA`                     154
  `Progress (%)`                        154
  `Schedule`                            123
  `Last update`                          47
  `LGA`                                   1
  `Location`                              1

These gaps limit the questions that can be answered confidently. For
example, with no target completion dates in the extract, this analysis
cannot reliably determine which projects are late. With only one
approved-cost value, it cannot support a meaningful budget or
cost-overrun analysis.

Recorded project status

-   123 projects are labelled `In progress`.
-   78 projects are labelled `Completed`.

These figures describe the status labels in the dataset. They do not
independently verify whether a project is physically complete or
operational.

 Geographic distribution

Awka South has the largest number of records in the extract, with 70
projects. Other comparatively high counts include Aguata (18), Nnewi
North (13), and Anaocha (11).

A higher count means that more records in this dataset are associated
with that LGA. It does not establish that the area receives more
funding, has better services, or has more completed projects. Those
conclusions would require additional reliable data and appropriate
comparisons.

 Progress values requiring context

Progress was populated for 47 records. The reported values ranged from
0% to 100%, with a median of 65%.

One record---`PRJ-2026-000085`, titled *Reclamation/rechannelization and
remediation o...* in Njikoka---was recorded as `In progress` with 100%
progress. This is a verification flag, not proof of an error: the
reporting rules may permit a project to remain in progress after
reaching 100% reported progress.

Seven records had a reported progress value of 0%. These records may
merit review, but the available extract does not provide enough
consistent start-date and update history to establish how long they have
remained at that level.

 6. Data Quality and Interpretation

A central lesson from this project is that data completeness and
project performance are different things.

-   A missing progress value does not mean progress is 0%.
-   A missing cost does not mean a project has no cost.
-   A status of `Completed` is a recorded label, not independent
    verification of delivery.
-   A 100% progress value alongside `In progress` is a reason to check
    the reporting definition, not automatically a contradiction.
-   A missing update date limits the ability to assess how current a
    record is.

For these reasons, the review flags are intended to support
investigation and data-quality improvement---not to label projects as
failed, fraudulent, or mismanaged.

 7. Reproducibility

The analysis was carried out in Google Colab using Python and pandas.

To reproduce the work:

1.  Download the dataset from the [Solution Lens
    portal](https://lens.anambrastate.gov.ng/insights), subject to the
    portal's terms.
2.  Open the notebook in Google Colab.
3.  Upload the CSV file when prompted, or update the notebook's file
    path.
4.  Run the cells in order.
5.  Review the audit summary and flagged records.
6.  Export the resulting audit files for further analysis.

Recommended repository structure

``` text
nigeria-public-project-accountability/
├── notebooks/
│   └── anambra_project_analysis.ipynb
├── outputs/
│   ├── anambra_project_audit.csv
│   └── anambra_flagged_projects.csv
├── data/
│   └── README.md
└── README.md
```

The filenames above are a suggested structure. Include only files that
you have actually created. If the raw dataset is not redistributed, use
`data/README.md` to document its source and retrieval date instead of
committing the CSV.

 8. Limitations

The initial extract has substantial missingness in several fields,
especially sector, target completion, completion date, approved cost,
responsible MDA, and progress. This restricts the analysis.

This first stage does not independently verify project sites,
expenditure, physical delivery, procurement records, or service
outcomes. It also does not establish why information is missing.

Any findings should be revisited if a more complete or updated dataset
becomes available.

 9. Next Steps

Planned improvements include:

-   Build clearer charts for status distribution and project counts by
    LGA.
-   Create a field-completeness scorecard to show where reporting gaps
    are concentrated.
-   Analyse available progress values without treating missing values as
    zero.
-   Develop SQL queries for status, location, and data-quality checks.
-   Add a Power BI dashboard once the analysis and definitions are
    validated.
-   Compare future data extracts to monitor changes in reporting
    completeness.
-   Where reliable source material is available, verify selected records
    against official project updates and clearly document the evidence.

These are proposed next steps, not features that should be considered
completed until they have been implemented and tested.

 10. What This Project Demonstrates

This project demonstrates an applied approach to data analytics:

-   Data inspection and quality assessment
-   Missing-value analysis
-   Descriptive statistics and group-by summaries
-   Duplicate checks
-   Rule-based record flagging
-   Exporting analysis-ready outputs
-   Responsible interpretation of public-sector data
-   Communicating limitations and actionable follow-up questions

 11. Source

Anambra State Government --- Solution Lens public project register\
https://lens.anambrastate.gov.ng/insights

The dataset and all findings should be interpreted in the context of the
source, the date the data was retrieved, and the limitations described
above.

