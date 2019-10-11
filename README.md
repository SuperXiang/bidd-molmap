# MolMap: A Molecule Representation Method Based on High-level Features

## MolMap
MolMap is generated by the following steps:

* Step1: Sample data 
* Step2: Feature extraction
* Step3: Calculate feature pairwise distance
* Step4: Feature 2D embedding
* Step5: Linear assignment to grid
* Step5: Gaussian smoothing
* Step6: Get MolMap


## installation

* 1. install [rdkit]('http://www.rdkit.org/docs/Install.html) first:
```bash
conda create -c rdkit -n my-rdkit-env rdkit
conda activate my-rdkit-env
```
* 2. in your "my-rdkit-env" env, install molmap by:

```bash
git clone https://github.com/shenwanxiang/bidd-molmap.git
cd bidd-molmap
pip install -r requirements.txt --user

# add molmap to PYTHONPATH
echo export PYTHONPATH="\$PYTHONPATH:`pwd`" >> ~/.bashrc
```

## Usage

```python
from molmap import MolMap, loadmap
from molmap.feature.fingerprint import Extraction as fext
from molmap.feature.descriptor import Extraction as dext
from molmap.vismap import plot_scatter, plot_alignmap
                 
f1 = dext().bitsinfo[dext().bitsinfo.Subtypes.isin(['Constitution', 'Property'])] #'MACCSFP', 'EstateFP'
flist = f1.IDs.tolist()[:]

mp = MolMap(ftype = 'descriptor' ,flist = flist)
mp = mp.fit(method = 'umap', n_neighbors = 100, verbose = 0) 

df1 = plot_alignmap(mp,htmlpath='temp/')
```

