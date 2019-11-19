# Video Person Re-ID: Fantastic Techniques and Where to Find Them
Official Pytorch Implementation of the paper:  
**Video Person Re-ID: Fantastic Techniques and Where to Find Them** *(Submitted in AAAI'20)*  
*Priyank Pathak,  Amir Erfan Eshratifar,  Michael Gormish*   
*(Work done in collaboration of NYU and Clarifai)*



Extension of Work done for Videos 
* [Revisiting Temporal Modeling for Video-based Person ReID](https://github.com/jiyanggao/Video-Person-ReID) [paper](https://arxiv.org/pdf/1805.02104.pdf)
* [Bag of Tricks and A Strong ReID Baseline](https://github.com/michuanhaohao/reid-strong-baseline)[paper](http://openaccess.thecvf.com/content_CVPRW_2019/papers/TRMTMCT/Luo_Bag_of_Tricks_and_a_Strong_Baseline_for_Deep_Person_CVPRW_2019_paper.pdf) 
* [Online-Soft-Mining-and-Class-Aware-Attention](https://github.com/ppriyank/-Online-Soft-Mining-and-Class-Aware-Attention-Pytorch)[paper](https://arxiv.org/pdf/1811.01459v2.pdf)

## MODEL

<img src="https://github.com/ppriyank/Video-Person-Re-ID-Fantastic-Techniques-and-Where-to-Find-Them/blob/master/images/diag.png" width="900">


## RESULTS




### LOSS

```
loss = ide_loss + (1 - beta_ratio)*triplet_loss + center_loss * cetner_loss_weight + beta_ratio * osm_caa_loss + attention_loss
```

### Performance

   
Use `59` configuration in `cl_centers.conf` and `vals.conf` for **MARS DATASET** and `27` and `24` configuration in `prid.conf` for **prid DATASET**


**MARS DATASET** 

| Model            | mAP (re-rank)  | CMC-1 (re-rank) | CMC-5 (re-rank)| CMC-20 (re-rank)|
| :--------------- | -------------: | -------------: | -------------: | ------------: | 
| SOTA (w/o re-rank) (Fu et al.)[1]     |   81.2 (-)  | 86.2 (-) | 95.7 (-) |  - (-)   |
| SOTA (with re-rank) (Fu et al.)[1]   |   80.8 (87.7)  | 86.3(87.2) | 95.7(96.2) | 98.1(98.6) |
| Baseline     |  76.7 (84.5) | 83.3 (85.0) | 93.8 (94.7) | 97.4 (97.7)|
| Baseline + BOT    |    81.3 (88.4) | 87.1 (87.6) | 95.9 (96.0) | 98.2 (98.4) |
|  Baseline + BOT + OSM Loss    |  |   |   |   |
| (Proposed) Baseline + BOT + OSM Loss + CL Centers    |  82(88.1)  | 87.3(87.3)  | 96.2(95.8)  | 97.9(98.4) |
| (Proposed) B-BOT + Attn-CL loss    | 82.9(87.8)   | 88.6(88.0)  | 96.2(95.4)  | 98.0(98.3) |


**PRID DATASET**   

| Model            | CMC-1 | CMC-5 | CMC-20 |
| :--------------- | ----------: | ----------: | ----------: | ----------: | 
| SOTA  (Zeng, Tian, and Wu)[2]     |  96.1%  | 99.5  | -  |  
| Baseline + BOT + OSM Loss + CL Centers    |  93.1  |  88.8 | 97.8  | 100.0 |
| Baseline + BOT + OSM Loss + CL Centers (pretrained on MARS)   |  96.6  | 100  | 100  | 
 


## DATASET

MARS dataset: 

<img src="https://github.com/ppriyank/Video-Person-Re-ID-Fantastic-Techniques-and-Where-to-Find-Them/blob/master/images/data.jpg" width="400">





## bag of tricks   
`args.arch = "ResNet50ta_bt"`

`python bagoftricks.py --name="_CL_CENTERS_" --validation-training --cl-centers --opt=8`  
`python bagoftricks.py --name="_triplet_OSM_only_" --validation-training --use-OSMCAA --opt=8`  
`python bagoftricks.py --name="_triplet_only_" --validation-training --opt=8`   
`python bagoftricks.py --name="_ilidsvid_" --validation-training --opt=8`   
`python bagoftricks.py --name="_prid_" --validation-training --opt=24`   

## hyper parameter optimization   

`python hyper_supervise_validation.py --focus="map" --opt=8`       
`python hyper_supervise_validation.py --focus="rerank_map" --opt=8`      
`python hyper_supervise_validation.py --focus="map" --sampling="inteliigi" --opt=8`      
`python hyper_supervise_validation.py --focus="rerank_map" --sampling="inteliigi" --opt=8`    



Ref: 

[1] STA:  Spatial-Temporal Attention for Large-Scale Video-based Person Re-Identification  
[2] Person Re-identification with Hierarchical Deep Learning Feature and efficient XQDA Metric
