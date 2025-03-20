record how to run the pipeline

## unzip input zip file
cd inputs
unzip [filename].zip
unzip 'chebi-*.zip'

## install CMDL conda env
conda env create -f environment.yml
conda activate CMDL

if fail the conda env creation, install the package manually

## download cc.en.300.bn word embedding model
wget https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.en.300.bin.gz
gzip -d cc.en.300.bin.gz'
mkdir resources/fasttext/cc
mv cc.en.300.bin resources/fasttext/cc

## convert ipynb to py
pip install notebook
jupyter nbconvert --to script [filename].ipynb
python [filename].py

## build up snorkel environment
