# StyleGAN2-ADA for Hand-written Molecule Image Generation

- Latest update: 11 April 2023


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
python train.py --outdir=./training-runs --data=./datasets/DECIMER.zip --gpus=1 --cfg=auto --kimg=2000 --batch=32
```


Generate new molecule images using the checkpoints 1400 & 1600
----
- The two checkpoints had the lowest FID scores (see the log.txt)
```
mkdir generating-runs
python generate.py --outdir=generating-runs --trunc=1 --seeds=2023-2522 --network=training-runs/00000-DECIMER-auto1-kimg2000-batch32/network-snapshot-001400.pkl
python generate.py --outdir=generating-runs --trunc=1 --seeds=3023-3522 --network=training-runs/00000-DECIMER-auto1-kimg2000-batch32/network-snapshot-001600.pkl
```