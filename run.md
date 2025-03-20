record how to run the pipeline

## unzip input zip file
cd inputs
unzip [filename].zip
unzip 'chebi-*.zip'

## install CMDL conda env
conda env create -f environment.yml
conda activate CMDL

if fail the conda env creation, install the package manually

## convert ipynb to py
pip install notebook
jupyter nbconvert --to script [filename].ipynb
python [filename].py

## build up snorkel environment
