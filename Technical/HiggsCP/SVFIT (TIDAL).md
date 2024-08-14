Link to repo: https://github.com/Ksavva1021/TIDAL


## Install Instructions

Clone recursively: 
```shell
git clone --recurse-submodules git@github.com:Ksavva1021/TIDAL.git
```

Mamba environment install:
```shell
mamba env create -f environment.yml
```

Source SVFIT:
```shell
source setup_svfit.sh
```

Interactive testing:
```python
from TauAnalysis.ClassicSVfit.wrapper.pybind_wrapper import FastMTT
x = FastMTT()
```

## Running Instructions

Source environment
```shell
conda activate TIDAL
```

Load ROOT and SVFIT - Select **option 2**:
```shell
source load_package.sh
```

To calculate mass for all outputs in a given directory:

``` python
python3 scripts/run_svfit.py --source_dir /vols/cms/lcr119/offline/HiggsCP/HiggsDNA/output/Run3_2022/ --use_condor
```

Output file is called `svfit.parquet` and contains `run, lumi, event, svfit mass, svfit error` (saved in the directory where the merged.parquet file is found)