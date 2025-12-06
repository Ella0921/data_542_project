# Data 542 Project - Group 20

## Yin-Wen Tsai, Haozhong Ji

This repository contains two analysis notebooks (`RQ1.ipynb` and
`RQ2.ipynb`) for the **AIDev Mining Challenge (MSR 2026)**.\
Both notebooks explore different aspects of AI-generated pull requests
using the official AIDev dataset hosted on HuggingFace.

------------------------------------------------------------------------

## 🧪 Research Questions

### **RQ1 – AI Agent Usage Across Repositories**

**Research Question:**\
*Do different AI coding agents get used in different types of
repositories?*

This notebook analyzes whether AI PRs created by different agents appear
more frequently in repositories with different levels of:

-   popularity (measured by stars)

-   activity (measured by forks)

-   It uses repository metadata to group repos into tiers and compares
    agent distributions across those groups.

### **RQ2 – PR Size, File Type, and Review/Merge Outcomes**

**Research Question:**\
*How do the size and dominant file type of AI pull requests relate to
merge outcomes and review effort?*

This notebook studies how AI PR characteristics influence:

-   merge rate

-   time to merge / close

-   volume of review comments

PRs are grouped into **size buckets** and **dominant file types**, and
metrics are compared.

## 📂 Dataset

Both notebooks use tables from the **AIDev dataset**:

-   `all_pull_request.parquet`

-   `all_repository.parquet`

-   `all_user.parquet` (RQ1)

-   `pr_commit_details.parquet` (RQ2)

-   `pr_review_comments.parquet` (RQ2)

Data is loaded directly via HuggingFace paths:

`{"hf://datasets/hao-li/AIDev/all_pull_request.parquet"}`

------------------------------------------------------------------------

## 📄 Notebook Summaries

### **🔎 RQ1.ipynb – Agent Usage Across Popularity & Activity Levels**

#### **Main Steps**

1.  **Load PR, repository, and user tables**

2.  **Filter to AI-generated PRs**

    -   Non-null `agent`

    -   Final state (`merged` or `closed`)

3.  **Merge repository metadata**

4.  **Compute repository groups**

    -   Popularity tiers via stars (`Low`, `Medium`, `High`)

    -   Activity tiers via forks (`Low`, `Medium`, `High`)

5.  **Compute agent distribution metrics**

6.  **Visualize**

    -   Agent usage across popularity groups

    -   Agent usage across activity groups

#### **Outputs**

-   Distribution plots by agent × popularity/activity

-   Tables showing agent percentages in each bucket

### **🔎 RQ2.ipynb – PR Size, File Type, and Outcomes**

#### **Main Steps**

1.  **Load PR, repository, commit details, and review comments tables**

2.  **Filter to AI-generated PRs** and compute:

    -   merge flag

    -   time to merge / close

3.  **Compute PR size**

    -   Aggregate additions + deletions + total lines changed

4.  **Identify dominant file type per PR**

    -   Based on max line changes by file type

5.  **Count review comments**

    -   Extract PR numbers from URLs

6.  **Merge all metrics into a unified PR table**

7.  **Create size buckets**

    -   Tertiles: `Small`, `Medium`, `Large`

8.  **Group and compare metrics**

    -   merge rate

    -   median time to merge

    -   average review comments

    -   PR count per category

9.  **Visualizations**

    -   Size vs merge rate

    -   File type vs review comments

Size × file type heatmaps / bar charts

**Outputs**

-   Summary tables by `size_bucket` × `main_file_type`

-   Merge rate and review comment visualizations

------------------------------------------------------------------------

## 📁 Repository Structure

```{bash}
├── RQ1.ipynb 
├── RQ2.ipynb 
├── RQ3.ipynb 
└── README.md 
```

------------------------------------------------------------------------

## 🛠️ Environment & Dependencies

These Python packages are required:

```{python}
pip install pandas numpy matplotlib seaborn pyarrow fastparquet fsspec huggingface_hub 
```

Python 3.10+ is recommended.
