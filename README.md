## Introduction

https://github.com/zlzeng/DeepFloorplan を、python3.6で動くように変更したリポジトリです

## Requirements

Our code has been tested by using tensorflow-gpu==1.15.1 & OpenCV==3.3.1. We used Nvidia Geforce GTX1060 with CUDA 10.0 installed.

```bash
conda env create -f=requirements.yml
```

## Data

We share all our annotations and train-test split file [here](https://mycuhk-my.sharepoint.com/:f:/g/personal/1155052510_link_cuhk_edu_hk/EgyJhisy04hNnxKncWl5zksBf9zDKDpMJ7c0V-q53_pxuA?e=P0BjZd). Or download the annotation using the link in file "dataset/download_links.txt". The additional round plan is included in the annotations.

Our annotations are saved as png format. The name with suffixes "\_wall.png", "\_close.png" and "\_room.png" are denoted "wall", "door & window" and "room types" label, respectively. We used these labels to train our multi-task network.

The name with suffixes "\_close_wall.png" is the combination of "wall", "door & window" label. We don't use this label in our paper, but maybe useful for other tasks.

The name with suffixes "\_multi.png" is the combination of all the labels. We used this kind of label to retrain the general segmentation network.

We also provide our training data on R3D dataset in "tfrecord" format, which can improve the loading speed during training.

To create the "tfrecord" training set, please refer to the example code in "utils/create_tfrecord.py"

All the raw floor plan image please refer to the following two links:

- R2V: <https://github.com/art-programmer/FloorplanTransformation.git>
- R3D: <http://www.cs.toronto.edu/~fidler/projects/rent3D.html>

## Usage

To use our demo code, please first download the pretrained model, find the link in "pretrained/download_links.txt" file, unzip and put it into "pretrained" folder, then run

```bash
python demo.py --im_path=./demo/45719584.jpg 
```

To train the network, simply run

```bash
python main.py --phase=Train
```

Run the following command to generate network outputs, all results are saved as png format.

```bash
python main.py --phase=Test
```

To compute the evaluation metrics, please first inference the results, then simply run

```bash
python scores.py --dataset=R3D
```

To use our post-processing method, please first inference the results, then simply run

```bash
python postprocess.py
```

or 

```bash
python postprocess.py --result_dir=./[result_folder_path]
```

## Citation

If you find our work useful in your research, please consider citing:

---

	@InProceedings{zlzeng2019deepfloor,
		author = {Zhiliang ZENG, Xianzhi LI, Ying Kin Yu, and Chi-Wing Fu},
		title = {Deep Floor Plan Recognition using a Multi-task Network with Room-boundary-Guided Attention},
		booktitle = {IEEE International Conference on Computer Vision (ICCV)},
		year = {2019}
	}

---
