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

## install es
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.17.3-linux-x86_64.tar.gz
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.17.3-linux-x86_64.tar.gz.sha512
shasum -a 512 -c elasticsearch-8.17.3-linux-x86_64.tar.gz.sha512 
tar -xzf elasticsearch-8.17.3-linux-x86_64.tar.gz
cd elasticsearch-8.17.3/ 
./bin/elasticsearch
./bin/elasticsearch -d -p pid # daemon
config/elasticsearch.yml: xpack.security.enabled: false # find the config term and modify to false
curl http://localhost:9200

## convert ipynb to py
pip install notebook
jupyter nbconvert --to script [filename].ipynb
python [filename].py

## run python file
python build_label_files.py
python build_features.py

## run python file
cd labeler
jupyter nbconvert --to script snorkel_labeler.ipynb
python snorkel_labeler.py

## run python file
cd trainer
jupyter nbconvert --to script column-text-joint-training.ipynb
python column-text-joint-training.py