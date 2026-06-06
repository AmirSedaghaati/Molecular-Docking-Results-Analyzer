# Vina Docking Filter

> An automated pipeline to parse, filter, and rank AutoDock Vina results for virtual screening.

---

## Background

For the analysis of AutoDock Vina outputs of large libraries of compounds, it is necessary to extract the binding affinities from each log file, assess adherence to Rule of 5 of Lipinski, and rank hits. When doing this manually for hundreds of compounds, bottlenecks in data manipulation occur and transcriptional errors arise, impeding the lead identification step.

---

## Implementation

A Python script (parseandfilter.py) is provided here to automate the post-docking work. The workflow consists of:
1. Parsing the docking results from the formatted Vina CSV outputs.
2. Applying Lipinski's rules to remove compounds that are not drug-like.
3. Ranking the remaining compounds by their binding energy, where smaller numbers indicate better affinity (lower kcal/mol is tighter binding).
4. Marking "hits" according to an affinity threshold that can be easily adjusted.
5. Outputting both a tabular ranking of ranked compounds and a bar chart of the filtered compounds.

In my thesis, a subset of the data represented the set of natural compounds that were tested. A sample dataset that mimics my natural compound set can be found in data/mock_data/, and can be run by the pipeline, saving time if the original raw data is unavailable.

---

## Technical Stack

| Component | Function |
| :--- | :--- |
| **Python 3.10+** | Core data processing |
| **pandas** | Tabular data manipulation and ranking |
| **matplotlib** | Visualization of binding affinities |

---

## File Structure

```text
vina-docking-filter/
│
├── data/
│   └── mock_data/
│       └── docking_results.csv     # Simulated docking results for testing
│
├── results/                        # Output folder (generated on execution)
│   ├── ranked_hits.csv
│   └── affinity_chart.png
│
├── scripts/
│   └── parse_and_filter.py         # Main pipeline script
│
├── .gitignore
├── requirements.txt
└── README.md
