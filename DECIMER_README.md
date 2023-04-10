# StyleGAN2-ADA for Hand-written Molecule Image Generation

- Latest update: 10 April 2023


Environment setup
----
```
conda env create -f environment.yml
```


Preparing training dataset for DECIMER
----
```
mkdir datasets
python dataset_tool.py --source=./DECIMER_HDM_Dataset_Images.zip --dest=./datasets/DECIMER.zip --width 256 --height 256
```


Training a new network for DECIMER
----
```
mkdir training-runs
python train.py --outdir=./training-runs --data=./datasets/DECIMER.zip --gpus=1 --cfg=auto --kimg=1000 --batch=32
```