# SO-HandNet
[SO-HandNet: Self-Organizing Network for 3D Hand Pose Estimation with Semi-supervised Learning](http://openaccess.thecvf.com/content_ICCV_2019/papers/Chen_SO-HandNet_Self-Organizing_Network_for_3D_Hand_Pose_Estimation_With_Semi-Supervised_ICCV_2019_paper.pdf)

ICCV 2019

## Installation
	
	conda create -n sohand python=3.6
	source activate sohand
	conda install pytorch torchvision cudatoolkit=8.0 -c pytorch
	conda install faiss-gpu -c pytorch
	pip install --upgrade pip
requirements: numba matplotlib h5py scipy dominate visdom horovod libnccl2 libnccl-dev tqdm
## Usage
### Data Preprocessing
Download ICVL dataset, and use matlab scripts to process the data (transfrom depth map into point cloud).
	
	matlab ICVL_train_process.m
	matlab ICVL_test_process.m
	
Or directly download the processed data. [Google Drive Link](https://drive.google.com/open?id=1jdEIcS6WM3v6lwirBEzU1Aw-z0TXa2xX) or [BaiduNetDesk Link](https://pan.baidu.com/s/1V8hLca_OBv5fGeR0iqhQEw)

Put data into /data as /data/ICVL/process_out/
### Train and evaluation

#### Evaluation 
pretrained models: [Google Drive Link](https://drive.google.com/open?id=1QM9U-3RH8m1Dy1-zKpVyeKuFASDa1sK_)   [BaiduNetDesk Link](https://pan.baidu.com/s/1AhDSa_G39tcEssLhABff1g)
Put data into /checkpoints
	
	python ICVL_Get_test_result.py

#### Fully-supervised Training：
	python ICVL_en_de.py
	
set "pretrain_encoder" "pretrain_decoder" as the saved model in last stage.
	
	python ICVL_en_es.py
	
set "pretrain_encoder" "pretrain_decoder" "pretrain_estimater" as the saved model in last stage.
	
	python ICVL_train_all.py
	
#### Semi-supervised training:
Change "train_label_ratio" as the ratio of labeled frames used for training, and the "trainlist" and "testlist" can be generated by "datalist.ipynb", we provide them along with the processed data.
	
	python ICVL_semi_en_de.py
	python ICVL_semi_en_es.py
	python ICVL_semi_train_all.py

## References
Here are some great resources we benefit:

[Hand PointNet](https://sites.google.com/site/geliuhaontu/home/cvpr2018)

[SO-Net](https://github.com/lijx10/SO-Net)

[PointNet](https://github.com/charlesq34/pointnet)
