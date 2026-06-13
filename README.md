# Vina Docking Pipeline

An automated pipeline to parse, filter, and rank AutoDock Vina docking results for virtual screening.

## Background

The post-processing of AutoDock Vina output for large compound libraries requires retrieving binding affinities, assessing Lipinski Rule of Five, and sorting of hits. Manual verification over hundreds of compounds takes time and errors are easily committed, thus creating an bottleneck at the lead identification process.

## Implementation

The script `parse_and_filter.py` automates this workflow:

1. Parses docking results from a formatted CSV (binding affinities, Lipinski properties).
2. Applies a pre-calculated Lipinski Rule of Five flag to remove non-drug-like compounds.
3. Ranks the remaining compounds by binding affinity (more negative = tighter binding).
4. Flags "hits" against a configurable affinity threshold.
5. Outputs a ranked summary table and a bar chart of binding affinities.

## Technical Stack

| Component | Function |
|---|---|
| Python 3.10+ | Core data processing |
| pandas | Tabular data manipulation and ranking |
| matplotlib | Visualization of binding affinities |

## Usage

Run from the repository root:

```bash
pip install -r requirements.txt

python parse_and_filter.py --input data/mock_data/docking_results.csv --results results/
```

## Mock Data

`data/mock_data/docking_results.csv` is an illustrative dataset for testing the pipeline. It does not reproduce the exact rankings or compound set from the published screening study (Biochemical and Biophysical Reports,[doi.org/10.1016/j.bbrep.2025.102171]) — it is provided so the pipeline can be run end-to-end without access to the original raw data.

## File Structure

```
vina-docking-pipeline/
│
├── data/
│   └── mock_data/
│       └── docking_results.csv     # Illustrative docking results for testing
│
├── results/                        # Output folder (generated on execution)
│   ├── ranked_hits.csv
│   └── affinity_chart.png
│
├── parse_and_filter.py             # Main pipeline script
├── .gitignore
├── requirements.txt
└── README.md
```
