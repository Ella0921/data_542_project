# Data 542 Project — Group 20

**Yin-Wen Tsai, Haozhong Ji**  
Repository for the *Data 542: Mining Software Repositories* group project.

This repository contains analysis notebooks and summary reports exploring AI-generated pull request (PR) characteristics and outcomes using the AIDev dataset from the MSR 2026 Mining Challenge.

---

## 📌 Overview

This project analyzes AI-generated pull requests from GitHub using the **AIDev dataset**. We investigate how AI coding agents are distributed, how PR characteristics influence review and merge outcomes, and how simple human–AI collaboration patterns relate to these outcomes.

Three research questions (RQ1–RQ3) are addressed through Jupyter Notebooks:

1. **RQ1.ipynb** — AI usage patterns across repositories  
2. **RQ2.ipynb** — PR size and file type impacts on outcomes  
3. **RQ3.ipynb** — Human follow-up commit patterns

---

## 📊 Research Questions

### **RQ1 – AI Agent Usage Across Repositories**
**Research Question:**  
How do different AI coding agents (e.g., GitHub Copilot) vary in usage across repositories with different levels of popularity and activity?  

This notebook:
- Loads PR, repository, and user tables from the AIDev dataset.
- Filters to AI-generated PRs (`agent` non-null and final state `merged` or `closed`).
- Merges repository metadata (stars, forks).
- Groups repositories into popularity and activity tiers.
- Visualizes agent distributions across these tiers.

---

### **RQ2 – PR Size, File Type, and Outcomes**
**Research Question:**  
How do the size and dominant file type of AI-generated pull requests relate to merge outcomes and review effort?  

This notebook:
- Loads PR, commit details, and review comment tables.
- Computes PR size measures (additions + deletions + total lines changed).
- Identifies dominant file type per PR based on line changes.
- Creates size buckets (`Small`, `Medium`, `Large`).
- Reports merge rate, median time to merge, and review comments per bucket × file type group.
- Visualizes results (bar charts, heatmaps).

---

### **RQ3 – Human Follow-up Commit Patterns**
**Research Question:**  
For AI-generated PRs, how do simple human–AI collaboration patterns (based on follow-up commits) relate to merge rate, time to merge, and review effort?  

This notebook:
- Builds a PR-level table only for AI PRs.
- Detects human follow-up commits in PR commit histories by excluding committer names that appear to be bots or system accounts (e.g., `GitHub`, `github-actions[bot]`) as suggested by the TA.
- Labels PRs as:
  - `agent_only` — no human follow-up commit
  - `agent_then_human` — at least one human follow-up commit
- Computes summary metrics (merge rate, median time to merge, average review comments).
- Visualizes summary comparisons.

---
## 📦 Dataset

We use the **AIDev** dataset from the MSR 2026 Mining Challenge. Relevant extracted tables include:

| Table | Description |
|-------|-------------|
| `pull_request.parquet` | Metadata of all pull requests |
| `all_repository.parquet` | Repository information (stars, forks, etc.) |
| `all_user.parquet` | User identities (for RQ1) |
| `pr_commit_details.parquet` | Commit-level details per PR |
| `pr_review_comments.parquet` | Review comments per PR |

Data is loaded in notebooks via HuggingFace dataset paths such as:

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
├── RQ1.ipynb # AI agent usage analysis
├── RQ2.ipynb # PR size/file type outcomes analysis
├── RQ3.ipynb # Human follow-up analysis
├── DATA_542__Milestone_2_Report.pdf
├── DATA_542__Milestone_3_Report.pdf
└── README.md # This file
```

------------------------------------------------------------------------

## 🛠️ Environment & Dependencies

These Python packages are required:

```{python}
pip install pandas numpy matplotlib seaborn pyarrow fastparquet fsspec huggingface_hub 
```

Python 3.10+ is recommended.

---

## ▶️ How to Run

1. Clone this repository:

```bash
git clone https://github.com/Ella0921/data_542_project.git
```

2. Navigate to the folder:

```bash
cd data_542_project
```

3. Launch Jupyter Notebook:

```bash
jupyter notebook
```

4. Open and run:

* RQ1.ipynb
* RQ2.ipynb
* RQ3.ipynb

Be sure your working directory has access to the AIDev dataset files or configure your HuggingFace authentication (`huggingface-cli login`) if needed.

---

# 📌 Citations

* MSR 2026 Mining Challenge: AIDev dataset
* HuggingFace datasets: hao-li/AIDev
