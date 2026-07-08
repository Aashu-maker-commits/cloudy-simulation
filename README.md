# cloudy-simulation

Simulations and analysis for radiative-transfer / emission spectra produced with Cloudy-style input models. Includes blackbody and supernova model input files, generated spectra/continuum output data, and Jupyter notebooks used to build and visualize the models and results.

Authors: Prof Arkaprabha Sarangi and Anwesha Barman

---

## Quick overview
This repository contains model input files, output data, and analysis notebooks for producing and inspecting simulated spectra and continuum for two main model families:
- Blackbody — models and transmission spectra built from blackbody sources and layered model inputs.
- Supernova — model inputs and produced spectra for supernova-like conditions.

The repo stores raw model input files (.in), precomputed output data (.dat), and notebooks that generate/visualize results.

### What you will find (top-level)
- Blackbody/
  - datafiles/            Large output tables (.dat) — continuum and spectra
  - models/               Model input files (.in) and analysis notebooks (Jupyter)
  - transmission files/   transmission-related outputs and supporting files
- supernova/
  - datafiles/            Spectra output tables (.dat)
  - input files/          Input files used for supernova model runs
  - models/               Model definitions and notebooks
- README.md               (this file)

---

## How it’s organized (annotated)

```
Blackbody/
  datafiles/                output continuum/spectra (.dat)
  models/
    blackbody model/        multiple model_*.in files + notebooks (MakeModelwithdiffTemp.ipynb, Simulation with different temperatures.ipynb)
    Transmission model/     model_1.in .. model_5.in + transmission notebooks
  transmission files/       (supporting transmission outputs)

supernova/
  datafiles/                spectra_h*.dat (simulated spectra files for different parameter sets)
  input files/              input files used to run supernova simulations
  models/                   (model descriptions / notebooks)
README.md
```

How it fits together:
- The .in files in each models/ directory define physical setups (density, temperature, radiation source, geometry, etc.). Those inputs are intended to be executed by Cloudy (or an equivalent radiative-transfer code) to produce the .dat spectra/continuum outputs stored in the datafiles/ directories.
- The Jupyter notebooks read those .dat outputs (or run processing steps) and produce plots/analysis to inspect continuum, line strengths, or transmission as functions of model parameters (temperature, density, optical depth, etc.).

---

## Prerequisites
- Cloudy (or the radiative-transfer code used to run the .in model inputs). Use the same Cloudy major version you used when producing the stored outputs to ensure identical outputs.
- Python 3.8+ for the notebooks and plotting.
- Typical Python packages used in the notebooks: jupyter / jupyterlab, numpy, matplotlib, pandas (install as needed).

Suggested Python install:
```bash
python -m venv .venv
source .venv/bin/activate       # or .venv\Scripts\activate on Windows
pip install jupyterlab numpy matplotlib pandas
```

---

## How to reproduce results / run models

1. Run a model input with Cloudy
- From a terminal, run Cloudy with an input file from Blackbody/models/... or supernova/input files/....
- Replace `cloudy` below with the Cloudy executable name/command used on your system.

Example (replace with your Cloudy invocation):
```bash
# example: run the blackbody model_h10_t10000 input
cloudy < "Blackbody/models/blackbody model/model_h10_t10000.in"
```

Cloudy will produce output files (continuum/spectra) in the working directory; you can copy/move them into the repository's `datafiles/` folder or point the analysis notebooks to the generated output.

2. Open and run the notebooks
- Start a Jupyter server:
```bash
jupyter lab
```
- Open notebooks:
  - Blackbody/models/Simulation with different temperatures.ipynb
  - Blackbody/models/MakeModelwithdiffTemp.ipynb
  - Blackbody/models/Transmission model/*.ipynb
- Run cells to load .dat outputs and generate the plots/tables in the notebooks.

3. Analyze precomputed data
- Many output files are already present in Blackbody/datafiles/ and supernova/datafiles/ (large .dat files). The notebooks expect these files; open them directly to reproduce the figures and numbers without rerunning Cloudy.

---

## Notable files (examples)
- Blackbody/models/Simulation with different temperatures.ipynb — notebook for building and comparing blackbody-based models at different temperatures.
- Blackbody/models/MakeModelwithdiffTemp.ipynb — notebook to prepare models with differing temperatures.
- Blackbody/models/Transmission model/model_1.in ... model_5.in — example transmission input files.
- supernova/datafiles/spectra_h10_L6.dat, spectra_h11_L5.dat, etc. — precomputed spectra for different parameter sets.
- Blackbody/datafiles/last_cont_h*.dat — precomputed continuum output files for a range of model parameters.

---

## Notes, tips and caveats
- Many of the .dat output files are large; keep that in mind if cloning the repo or moving files.
- The notebooks assume a CSV/space-delimited format typical of Cloudy output tables. If you re-run Cloudy with different version/options, verify column layout and adjust the notebook parsing cells if necessary.
- If you plan to reproduce results exactly, confirm the Cloudy version and any command-line options used originally.

---

## Contribution and contact
- If you want to add new models, please:
  - add your .in model to the appropriate models/ folder,
  - run Cloudy and place the produced outputs into datafiles/,
  - add or update a notebook showing how the new model is analyzed.
- For questions or to propose changes, open an issue or submit a pull request.

Authors: Prof Arkaprabha Sarangi and Anwesha Barman

---

## Suggested follow-ups
- Add a small requirements.txt or environment.yml capturing exact Python packages used by the notebooks.
- Add a short script (e.g., run_model.sh) that standardizes the Cloudy invocation used for these inputs.
- Record the Cloudy version and exact run commands used to generate the committed data so others can reproduce outputs exactly.
