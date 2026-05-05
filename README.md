# HOGRL
A Financial Fraud Detection Framework.
- `HOGRL`: Effective High-order Graph Representation Learning for Credit Card Fraud Detection, published in [IJCAI 2024](https://arxiv.org/pdf/2503.01556).



## Usage

### Data processing

1. Run `unzip /data/Amazon.zip` and `unzip /data/YelpChi.zip` to unzip the datasets; 
2. Run `python feature_engineering/data_process.py` to pre-process all datasets needed in this repo.
3. Run `python feature_engineering/get_matrix.py` to generate the adjacency matrix of the high-order transaction graph.Please note that this will require approximately 280GB of storage space. Please be aware that if you intend to run `HOGRL` , you should first execute the `get_matrix.py` script.


### Training & Evalutaion
<!-- 
To use fraud detection baselines including GBDT, LSTM, etc., simply run

```
python main.py --method LSTM
python main.py  --method GBDT
```
You may change relevant configurations in `config/base_cfg.yaml`. -->



Model in `HOGRL` can be run via:

```
python main.py --method hogrl
```
For specification of hyperparameters, please refer to `config/hogrl_cfg.yaml`.



### Data Description

There are three datasets, YelpChi, Amazon and S-FFSD, utilized for model experiments in this repository.

<!-- YelpChi and Amazon can be downloaded from [here](https://github.com/YingtongDou/CARE-GNN/tree/master/data) or [dgl.data.FraudDataset](https://docs.dgl.ai/api/python/dgl.data.html#fraud-dataset).

Put them in `/data` directory and run `unzip /data/Amazon.zip` and `unzip /data/YelpChi.zip` to unzip the datasets. -->

YelpChi and Amazon datasets are from [CARE-GNN](https://dl.acm.org/doi/abs/10.1145/3340531.3411903), whose original source data can be found in [this repository](https://github.com/YingtongDou/CARE-GNN/tree/master/data).

S-FFSD is a simulated & small version of finacial fraud semi-supervised dataset. Description of S-FFSD are listed as follows:
|Name|Type|Range|Note|
|--|--|--|--|
|Time|np.int32|from $\mathbf{0}$ to $\mathbf{N}$|$\mathbf{N}$ denotes the number of trasactions.  |
|Source|string|from $\mathbf{S_0}$ to $\mathbf{S}_{ns}$|$ns$ denotes the number of transaction senders.|
|Target|string|from $\mathbf{T_0}$  to $\mathbf{T}_{nt}$ | $nt$ denotes the number of transaction reveicers.|
|Amount|np.float32|from **0.00** to **np.inf**|The amount of each transaction. |
|Location|string|from $\mathbf{L_0}$  to $\mathbf{L}_{nl}$ |$nl$ denotes the number of transacation locations.|
|Type|string|from $\mathbf{TP_0}$ to $\mathbf{TP}_{np}$|$np$ denotes the number of different transaction types. |
|Labels|np.int32|from **0** to **2**|**2** denotes **unlabeled**||


> We are looking for interesting public datasets! If you have any suggestions, please let us know!

## Test Result
The performance of five models tested on three datasets are listed as follows:
| |YelpChi| | |Amazon| | |S-FFSD| | |
|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|
| |AUC|F1|AP|AUC|F1|AP|AUC|F1|AP|
|HOGRL|0.9808|0.8595|-|0.9800|0.9198|-|-|-|-|

>
> `HOGRL` is presently not applicable to S-FFSD dataset.

## Repo Structure
The repository is organized as follows:
- `models/`: the pre-trained models for each method. The readers could either train the models by themselves or directly use our pre-trained models;
- `data/`: dataset files;
- `config/`: configuration files for different models;
- `feature_engineering/`: data processing;
- `methods/`: implementations of models;
- `main.py`: organize all models;
- `requirements.txt`: package dependencies;

    
## Requirements
```
python           3.7
scikit-learn     1.0.2
pandas           1.3.5
numpy            1.21.6
networkx         2.6.3
scipy            1.7.3
torch            1.12.1+cu113
dgl-cu113        0.8.1
```



### Citing

If you find *HOGRL* is useful for your research, please consider citing the following papers:
    

    @inproceedings{zou2024effective,
      title={Effective High-order Graph Representation Learning for Credit Card Fraud Detection.},
      author={Zou, Yao and Cheng, Dawei},
      booktitle={International Joint Conference on Artificial Intelligence},
      year={2024}
    }
