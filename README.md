📘 AIDev Mining Challenge – RQ1 & RQ2 Analysis

This repository contains two analysis notebooks (RQ1.ipynb and RQ2.ipynb) for the AIDev Mining Challenge (MSR 2026).
Both notebooks explore different aspects of AI-generated pull requests using the official AIDev dataset hosted on HuggingFace.

🧪 Research Questions
RQ1 – AI Agent Usage Across Repositories

Research Question
Do different AI coding agents get used in different types of repositories

This notebook analyzes whether AI PRs created by different agents appear more frequently in repositories with different levels of

popularity (measured by stars)

activity (measured by forks)

It uses repository metadata to group repos into tiers and compares agent distributions across those groups.

RQ2 – PR Size, File Type, and ReviewMerge Outcomes

Research Question
How do the size and dominant file type of AI pull requests relate to merge outcomes and review effort

This notebook studies how AI PR characteristics influence

merge rate

time to merge  close

volume of review comments

PRs are grouped into size buckets and dominant file types, and metrics are compared.

📂 Dataset

Both notebooks use tables from the AIDev dataset

all_pull_request.parquet

all_repository.parquet

all_user.parquet (RQ1)

pr_commit_details.parquet (RQ2)

pr_review_comments.parquet (RQ2)

Data is loaded directly via HuggingFace paths

hfdatasetshao-liAIDevall_pull_request.parquet

📄 Notebook Summaries
### 🔎 RQ1.ipynb – Agent Usage Across Popularity & Activity Levels
Main Steps

Load PR, repository, and user tables

Filter to AI-generated PRs

Non-null agent

Final state (merged or closed)

Merge repository metadata

Compute repository groups

Popularity tiers via stars (Low, Medium, High)

Activity tiers via forks (Low, Medium, High)

Compute agent distribution metrics

Visualize

Agent usage across popularity groups

Agent usage across activity groups

Outputs

Distribution plots by agent × popularityactivity

Tables showing agent percentages in each bucket

🔎 RQ2.ipynb – PR Size, File Type, and Outcomes
Main Steps

Load PR, repository, commit details, and review comments tables

Filter to AI-generated PRs and compute

merge flag

time to merge  close

Compute PR size

Aggregate additions + deletions + total lines changed

Identify dominant file type per PR

Based on max line changes by file type

Count review comments

Extract PR numbers from URLs

Merge all metrics into a unified PR table

Create size buckets

Tertiles Small, Medium, Large

Group and compare metrics

merge rate

median time to merge

average review comments

PR count per category

Visualizations

Size vs merge rate

File type vs review comments

Size × file type heatmaps  bar charts

Outputs

Summary tables by size_bucket × main_file_type

Merge rate and review comment visualizations

📁 Repository Structure
.
├── RQ1.ipynb
├── RQ2.ipynb
├── README.md
└── figures        # (optional) saved plots from notebooks

🛠️ Environment & Dependencies

These Python packages are required

pip install pandas numpy matplotlib seaborn pyarrow fastparquet fsspec huggingface_hub


Python 3.10+ is recommended.

▶️ How to Run

Ensure environment supports HuggingFace hf file system.

Launch Jupyter

jupyter lab


Run

RQ1.ipynb for repository-popularityagent analysis

RQ2.ipynb for PR-size and file-type outcome analysis

Export figures if needed (recommended for reports)

plt.savefig(figuresplot_name.png)
