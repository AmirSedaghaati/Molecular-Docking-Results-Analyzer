# vina-docking-filter

Python scripts to parse, filter, and rank AutoDock Vina docking results.

---

## Context

The code below will handle only the first stage which is converting the raw docking output into a list of screened and ordered compounds.
A small fake dataset is provided to allow testing and checking of the pipeline.


## The Problem

After each docking run I had to:
1. Open up each of the Vina output files (one by one)
2. Copy the binding affinity number by hand into a spreadsheet
3. Go through each compound and determine if they violated Lipinski's criteria (by hand)
4. Sort and determine which hits to include in subsequent screens
This process was taking multiple hours to complete by hand for each batch (120+ compounds) and resulted in transcription errors.

---

## The Solution

Parseandfilter.py performs the following:
1. Reads the docking results from a properly structured CSV file
2. Filters the compounds which do not follow Lipinski Rule of Five
3. Ranks compounds by binding energy (the lowest value of kcal/mol has the tightest binding energy).
4. Marks the hits compounds with an affinity threshold value (below this threshold value the compounds are considered to be hit)
5. Writes a ranking table as well as a bar graph representation of the result to a file.
Mock data (data/mockdata/dockingresults.csv) represents the output of the real data which is in my thesis, these are natural compounds with known docking energies to serve as a reference.

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

## Related

- Thesis topic: In silico screening of natural compounds as enzyme inhibitors
- Published work: [Aesculin as pectate lyase Pel3 inhibitor — BBR 2025](https://doi.org/10.1016/j.bbrep.2025.102171)
- Contact: amirbio1996@gmail.com
