# Notebooks: run order and file uploads

All notebooks run in Google Colab. Run each city's notebooks in order: 01, then 02, then 03. Hubli-Dharwad and Hyderabad are separate runs, so keep their files separate.

## Run order

| Step | Notebook | What it does |
|---|---|---|
| 1 | `01_build_city.ipynb` | Builds the synthetic city: districts, restaurants, orders, config, zone distance matrix |
| 2 | `02_greedy_baseline.ipynb` | Greedy dispatch baseline |
| 3 | `03_batching.ipynb` | Batching: features, classifier, CVRP assignments, smart dispatch, P and Q variants |
| 4 | `national/environmental_impact.ipynb` | National CO2e estimate |
| 5 | `national/financial_model.ipynb` | National financial model (independent of step 4, so either order works) |

## Files to upload

| Notebook | Upload into Colab | Where the files are in this repo |
|---|---|---|
| 01 | Nothing. It writes to `/content/recon_survey` | Outputs are in `data/<city>/` |
| 02 | `city.csv`, `districts.csv`, `restaurants.csv`, `orders.csv`, `simulation_config.json`, `zone_distance_matrix.npy` (via the `files.upload()` cell) | `data/<city>/` |
| 03 | The same six files, plus `greedy_dispatch_log.csv` and `baseline_metrics.json` from step 2 (add them through the Colab file panel in the left sidebar, since there are several files) | `data/<city>/` and `results/<city>/baseline/` |
| national | Nothing. Values are typed into the code, taken from the Hubli-Dharwad and Hyderabad output files (`baseline_metrics.json`, `smart_metrics_p.json`, `smart_metrics_q.json`) | `results/<city>/` |

Notes:
- Notebook 03 reads `greedy_dispatch_log.csv` and `baseline_metrics.json` from the Colab working folder root, so move them out of `results/` before running it.
- Never mix the two cities' files in one Colab session.
- The road-network graphml is not in the repo (`.gitignore`). Notebook 01 downloads the road network from OpenStreetMap through OSMnx (`ox.graph_from_point`) and saves it as graphml in Colab, so it is rebuilt on each run.

## Outputs and where they are saved in this repo

| Notebook | Colab output | Repo location |
|---|---|---|
| 02 | `results/greedy_dispatch_log.csv`, `results/baseline_metrics.json` | `results/<city>/baseline/` |
| 03 | `results/dispatch_featured.csv`, `dispatch_labeled.csv`, `cvrp_assignments.csv`, `smart_dispatch_log.csv`, `smart_dispatch_log_p.csv`, `smart_metrics.json`, `smart_metrics_p.json`, `smart_metrics_q.json` | `results/<city>/batching/` |
| 03 | `results/classifier.pkl` | `models/<city>_classifier.pkl` (renamed) |
| national | `environmental_metrics.json` | `results/national/` |

## Versions

Pinned in `requirements.txt` to match the Colab runtime used. The national notebooks need only matplotlib, numpy and pandas.
