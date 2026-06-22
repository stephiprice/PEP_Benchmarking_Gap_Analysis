# Dutch PEP Benchmark and OpenSanctions Coverage Assessment

## Project purpose

This repository contains the code and input files used to construct and evaluate a Dutch Politically Exposed Person (PEP) benchmark.

The project has two main aims:

1. construct an independently sourced benchmark of current Dutch PEPs using official Dutch sources;
2. assess the coverage of Dutch PEPs in the OpenSanctions dataset.

OpenSanctions is treated as the dataset being evaluated, not as ground truth.

The benchmark is structured using an EU-aligned taxonomy of PEP functions. The current extended benchmark includes Category C political party board members. Category H, senior functions in international organisations, is currently outside the scope of the final benchmark version.

## Repository structure

```text
Code_clean/
│
├── data/
│   ├── input/        # Manually prepared source lists and taxonomy files
│   ├── external/     # External datasets, including OpenSanctions
│   ├── output/       # Generated benchmark and matching outputs
│   ├── raw_html/     # Archived official source HTML pages
│   └── raw_text/     # Cleaned source text files
│
├── notebooks/
│   ├── 00_setup.ipynb
│   ├── 01_data_collection_scraper.ipynb
│   ├── 02_clean_build_benchmark.ipynb
│   ├── 03_match_opensanctions.ipynb
│   └── 04_validate_benchmark_completeness.ipynb
│
├── requirements.txt
└── README.md
```

## Notebooks

### `00_setup.ipynb`

Checks the Python environment, project folders, required input files, and package versions.

### `01_data_collection_scraper.ipynb`

Collects and archives official Dutch source material. It saves raw HTML, cleaned source text, and fetch logs.

### `02_clean_build_benchmark.ipynb`

Cleans extracted and manually coded records, standardises names, combines benchmark components, checks data quality, and creates the final Dutch PEP benchmark.

### `03_match_opensanctions.ipynb`

Matches the final benchmark against OpenSanctions using staged record linkage:

* normalised exact matching;
* cleaned exact matching;
* fuzzy candidate matching;
* manual review outputs;
* category-level coverage analysis.

### `04_validate_benchmark_completeness.ipynb`

Performs reverse validation by identifying Dutch-relevant OpenSanctions records that are not represented in the benchmark. This is used as a triangulation and completeness check; OpenSanctions is not treated as ground truth.

````markdown

## Environment setup

Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
````

Install the required packages:

```powershell
python -m pip install -r requirements.txt
```

When opening the notebooks in VS Code or Jupyter, select the Python interpreter from this virtual environment:

```text
.venv
```

In VS Code, open any notebook, click the kernel selector in the top-right corner, and choose:

```text
Python Environments → .venv
```

No separately registered Jupyter kernel is required.

```
```

## Required external data

The OpenSanctions input file is not stored in this repository because it may be large and changes over time.

Place the file below before running the matching and validation notebooks:

```text
data/external/opensanctions_targets.simple.csv
```

## Running order

Run the notebooks in this order:

```text
00_setup.ipynb
01_data_collection_scraper.ipynb
02_clean_build_benchmark.ipynb
03_match_opensanctions.ipynb
04_validate_benchmark_completeness.ipynb
```

## Reproducibility approach

The project separates source collection, benchmark construction, matching, and validation.

Official source URLs, archived source text, fetch logs, manual coding decisions, cleaning checks, and matching outputs are retained where possible to support transparency and reproducibility.
