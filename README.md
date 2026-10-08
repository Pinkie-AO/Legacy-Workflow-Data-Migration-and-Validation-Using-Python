# Legacy Workflow Data Migration and Validation Using Python

## Project Overview

This project demonstrates a practical **data migration and validation workflow** using Python and pandas.

The project simulates the migration of workflow/job records from a **legacy scheduling system** into a new workflow orchestration platform. The objective is to demonstrate how a Junior Data Migrations Engineer can extract, profile, transform, migrate, reconcile, and validate data while identifying potential data-quality and business-rule issues.

The project uses a publicly available Kaggle dataset as the source system and creates a simulated target-system structure based on defined migration requirements.

> **Note:** The client, source system, target system, and target schema used in this project are simulated for portfolio and learning purposes. This project is not a representation of Redwood Software's proprietary systems or actual client data.


## Project Objectives

The main objectives of this project are to:

* Profile and understand data from a legacy source system.
* Identify missing values, duplicates, invalid values, and potential business-rule exceptions.
* Define a source-to-target data mapping.
* Transform source fields into the required target structure.
* Migrate the transformed records into a simulated target system.
* Reconcile source and target records.
* Validate record counts and unique identifiers.
* Validate transformed categorical values.
* Identify business-rule exceptions.
* Build a foundation for automated migration validation and troubleshooting.



## Migration Workflow

The migration process follows the structure:

**Extract → Profile → Transform → Migrate → Validate → Reconcile → Investigate**

### 1. Extract

The source dataset is loaded into Python using pandas.

The source dataset contains **2,000 records and 11 columns** representing jobs/workflows and their scheduling and resource requirements.

### 2. Profile

The source data was examined for:

* Number of records and columns
* Data types
* Missing values
* Duplicate identifiers
* Category distributions
* Numerical ranges
* Potential business-rule violations

### 3. Transform

The source fields were mapped into a simulated target-system schema.

Examples include:

* `Job_ID` → `Workflow_ID`
* `Job_Size_MI` → `Workload_Size`
* `CPU_Required` → `CPU_Units`
* `RAM_Required_GB` → `Memory_GB`
* `Estimated_Time_Sec` → `Expected_Duration_Sec`
* `Arrival_Time` → `Scheduled_Arrival_Sec`

Categorical values were also transformed according to the target specification.

For example:

| Source Value | Target Value    |
| ------------ | --------------- |
| Priority 1   | High            |
| Priority 2   | Medium          |
| Priority 3   | Low             |
| C1           | Cluster-01      |
| C2           | Cluster-02      |
| C3           | Cluster-03      |
| C4           | Cluster-04      |
| Energy 0     | Standard        |
| Energy 1     | Efficient       |
| Energy 2     | High-Efficiency |

### 4. Migrate

The transformed records were placed into the simulated target structure.

The target dataset contains the same number of records as the source after transformation.

### 5. Validate

Validation checks were performed to determine whether the migration preserved the expected data.

Checks included:

* Record-count validation
* Missing-value validation
* Duplicate-ID validation
* Source-to-target ID reconciliation
* Categorical mapping validation
* Business-rule validation


## Source Data

The source dataset contains the following fields:

| Field                  | Description                    |
| ---------------------- | ------------------------------ |
| `Job_ID`               | Unique job identifier          |
| `Priority_Class`       | Source priority classification |
| `Job_Size_MI`          | Job workload size              |
| `CPU_Required`         | Required CPU units             |
| `RAM_Required_GB`      | Required memory                |
| `Estimated_Time_Sec`   | Estimated processing time      |
| `Deadline_Sec`         | Job deadline                   |
| `Protocol_Sensitivity` | Sensitivity classification     |
| `Arrival_Time`         | Job arrival time               |
| `Cluster_ID`           | Source execution cluster       |
| `Target_Energy_Class`  | Energy classification          |



## Initial Source Data Findings

The source profiling stage identified:

* **2,000 records**
* **11 columns**
* **0 missing values**
* **0 duplicate Job IDs**
* Priority classes: 1, 2, and 3
* Execution clusters: C1, C2, C3, and C4
* Sensitivity levels: Low, Medium, and High
* Energy classes: 0, 1, and 2

One important business-rule exception was identified:

**761 records (38.05%) had an estimated processing time greater than the recorded deadline.**

This was treated as a **validation exception rather than automatically deleting or modifying the records**.

This distinction is important in data migration: a discrepancy should first be investigated against the business requirements before the data is changed.



## Migration Validation Results

After the initial transformation, the following reconciliation results were obtained:

| Validation Check             | Result | Status         |
| ---------------------------- | -----: | -------------- |
| Source records               |  2,000 |  PASS         |
| Target records               |  2,000 |  PASS         |
| Duplicate target IDs         |      0 |  PASS         |
| Missing target values        |      0 |  PASS         |
| Source IDs missing in target |      0 |  PASS         |
| Extra target IDs             |      0 |  PASS         |
| Deadline exceptions          |    761 |  Investigate |

### Interpretation

The structural migration checks passed successfully.

All **2,000 source records were represented in the target**, with no missing IDs, extra IDs, duplicate target IDs, or missing target values.

However, the 761 deadline exceptions require further investigation because they represent a potential business-rule discrepancy.

The project therefore demonstrates an important migration principle:

> **Successful record transfer does not necessarily mean successful migration. Data must also be validated against business rules and target requirements.**




## Key Migration Concepts Demonstrated

This project focuses on practical concepts relevant to data migration engineering:

### Source-to-Target Mapping

Defining how fields from a legacy system correspond to fields in a new system.

### Data Transformation

Changing field names, formats, and categorical representations to meet target-system requirements.

### Data Reconciliation

Comparing source and target records to ensure that expected records have successfully migrated.

### Data Validation

Checking migrated data for completeness, uniqueness, valid mappings, and business-rule compliance.

### Exception Handling

Identifying records that require further investigation rather than silently modifying or removing them.

### Automation

Using Python to automate repetitive migration and validation checks.



## What I Learned

Through this project, I gained practical experience in:

* Understanding the stages of a data migration pipeline.
* Working with source and target schemas.
* Creating source-to-target mappings.
* Performing data profiling before migration.
* Applying transformations using Python.
* Reconciling source and target identifiers.
* Building automated validation checks.
* Distinguishing structural errors from business-rule exceptions.
* Investigating data-quality issues before applying corrections.
* Thinking about data from a migration and systems perspective rather than only an analytical perspective.


## Conclusion

This project demonstrates a complete foundation for a practical data migration workflow:

Profile → Map → Transform → Migrate → Reconcile → Validate → Investigate

The emphasis is on maintaining **data integrity, traceability, and validation throughout the migration process**, rather than simply moving records from one dataset to another.

