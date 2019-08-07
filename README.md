# GDP MKR

This repository is the implementation of MKR ([arXiv](https://arxiv.org/abs/1901.08907)):

> Multi-Task Feature Learning for Knowledge Graph Enhanced Recommendation  
Hongwei Wang, Fuzheng Zhang, Miao Zhao, Wenjie Li, Xing Xie, and Minyi Guo.  
In Proceedings of The 2019 Web Conference (WWW 2019)

![](https://github.com/hwwang55/MKR/blob/master/framework.png)

MKR is a **M**ulti-task learning approach for **K**nowledge graph enhanced **R**ecommendation.
MKR consists of two parts: the recommender system (RS) module and the knowledge graph embedding (KGE) module. 
The two modules are bridged by *cross&compress* units, which can automatically learn high-order interactions of item and entity features and transfer knowledge between the two tasks.


## Files in the folder

- `data/`
  - `book/`
    - `BX-Book-Ratings.csv`: raw rating file of Book-Crossing dataset;
    - `item_index2entity_id.txt`: the mapping from item indices in the raw rating file to entity IDs in the KG;
    - `kg.txt`: knowledge graph file;
  - `movie/`
    - `item_index2entity_id.txt`: the mapping from item indices in the raw rating file to entity IDs in the KG;
    - `kg.txt`: knowledge graph file;
    - `ratrings.dat`: raw rating file of MovieLens-1M;
  - `music/`
    - `item_index2entity_id.txt`: the mapping from item indices in the raw rating file to entity IDs in the KG;
    - `kg.txt`: knowledge graph file;
    - `user_artists.dat`: raw rating file of Last.FM;
  - `intersect-14m/`
    - `ratings_re2.csv` : rating file of MovieLens-14M;
    - `triples_idx2.txt` : KG obtained from DBpedia
- `src/`: implementations of MKR.
- `log/` : log of every training and model saved from every epoch
- `test/` : evaluation of the model 

## Where to download the dataset
You can download the intersect-20m dataset [here](https://github.com/Jessinra/GDP-KG-Dataset). Copy all items inside and put into `/movie` folder **except the Preprocess.ipynb**.

## Preparing 
### Installing dependencies 
    pip3 install -r requirements.txt
### Preprocess the data 
1. To create missing `kg_final.txt` & `ratings_final.txt` files:
- use this [jupyter notebook](./data/intersect-14m/Preprocess.ipynb) (`Preprocess.ipynb` inside the `./data/intersect-14m`).

### How to run
1. Make sure `kg_final.txt` & `ratings_final.txt` exist. If not, run the preprocessing first.
2. Train the data (this command  will train the data using default hyperparameter)
    ~~~
    python3 src/main.py --dataset intersect-14m
    ~~~

## **! Caching warning !**
To start using new dataset, or if dataset changed, those file need to be deleted, and re preprocess it, otherwise it will use old dataset:
- `data/movie/ratings_final.npy`
- `data/movie/kg_final.npy`

# Training

## How to change hyper parameter
There are several ways to do this :
1. Open `src/main.py` and change the args parser default value
2. run `src/main.py` with arguments required.