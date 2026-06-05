# vina-docking-filter

Python scripts to parse, filter, and rank AutoDock Vina docking results.
Written as part of my MSc thesis in biochemistry.

---

## Context

This repository contains scripts I wrote during my master's thesis research
on enzyme inhibition using natural compounds. The docking experiments were
carried out using AutoDock Vina as part of a larger virtual screening workflow.

The code here covers one specific step: taking the raw docking output and
turning it into a filtered, ranked list of candidate compounds.

The original dataset is not included because the experimental results are
part of an ongoing study and have not yet been published in full.
A small mock dataset is provided instead so the pipeline can be tested and reviewed.

---

## The Problem

After each docking batch, I had to:
1. Open every Vina output file individually
2. Copy the binding affinity score into a spreadsheet by hand
3. Manually check each compound against Lipinski criteria
4. Sort the list and decide which hits to carry forward

With 120+ compounds per batch and multiple rounds of screening, this took
several hours of manual work and introduced transcription errors.

---

## The Solution

`parse_and_filter.py` does the following:

1. Reads docking results from a structured CSV file
2. Filters out compounds that fail Lipinski Rule of Five
3. Ranks the remaining compounds by binding affinity (lowest kcal/mol = tightest binding)
4. Flags compounds below a defined affinity threshold as hits
5. Saves a ranked summary table and a bar chart of the results

The mock data in `data/mock_data/docking_results.csv` simulates the format
of the real output from my thesis. It uses known natural compounds with
publicly available docking values for reference.

---

## File Structure

```
vina-docking-filter/
│
├── data/
│   └── mock_data/
│       └── docking_results.csv     # simulated docking results for testing
│
├── results/                        # output folder (created on first run)
│   ├── ranked_hits.csv
│   └── affinity_chart.png
│
├── scripts/
│   └── parse_and_filter.py         # main pipeline script
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/AmirSedaghaati/vina-docking-filter.git
cd vina-docking-filter

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run with mock data (default)
python scripts/parse_and_filter.py

# 4. Or specify a different input file
python scripts/parse_and_filter.py --input data/mock_data/docking_results.csv --results results/
```

Expected output:
- `results/ranked_hits.csv` — filtered and ranked compound list
- `results/affinity_chart.png` — bar chart of binding affinities with hit threshold marked

---

## Example Output

From the mock dataset (10 compounds), after Lipinski filtering and ranking:

| Rank | Compound   | Affinity (kcal/mol) | Hit? |
|------|------------|----------------------|------|
| 1    | Kaempferol | −7.33                | ✓    |
| 2    | Quercetin  | −7.12                | ✓    |
| 3    | Berberine  | −6.74                | ✓    |
| 4    | Apigenin   | −6.58                | ✓    |
| 5    | Aesculin   | −6.39                | ✓    |

---

## Honest Skill Disclaimer

I am a biochemist who uses computational tools to advance my research and
am still learning more advanced programming concepts.

This code was written to solve a specific problem in my thesis workflow —
not to be a general-purpose software package. The structure is intentionally
simple: plain functions, pandas for data handling, matplotlib for plotting.
I prioritized clarity and correctness over software engineering conventions.

If you find a bug or have a suggestion, feel free to open an issue.
I'm still learning and I welcome feedback.

---

## Related

- Thesis topic: In silico screening of natural compounds as enzyme inhibitors
- Published work: [Aesculin as pectate lyase Pel3 inhibitor — BBR 2025](https://doi.org/10.1016/j.bbrep.2025.102171)
- Contact: amirbio1996@gmail.com
