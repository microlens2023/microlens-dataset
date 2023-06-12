# A Content-Driven Micro-Video Recommendation Dataset at Scale

# Dataset

Download link: 

For review purpose, we release a part of our Microlens dataset temporarily. 

We upload a MicroLens-TOY folder, which contains 100 videos sampled randomly from MicroLens. The folder contains covers, audio files, video content as well as the textual caption of all 100 videos.

We also upload a MicroLens-100K folder, which contains the interaction pair MicroLens-100K_pairs.tsv (each row indicates a user as well as the videos s/he interacted, sorted by the interaction timestamp), the audio files, the textual captions, and the corresponding cover files of all videos in MicroLens-100K (we add watermark for each image temporarily). Please note that the video content for MicroLens-100K is not provided at this time.

For different types of modal data and the interaction pairs of MicroLen-100K, MicroLen-1M and MicroLen, we will release all of them once accepted.

# Code

We release codes of all algorithms, including VideoRec (all 15 video models are implemented in this project), IDRec and VIDRec (each folder contains multiple subfolders, each of which is the codes of a baseline), please see the the paths "Code/VideoRec", "Code/IDRec" and "Code/VIDRec" for details.

## Special instructions on VideoRec
In VideoRec, please run the python scripts "run_id.py", "run_text.py", "run_image.py" and "run_video.py" if you want to switch to a different training mode, and run "run_id_test.py", "run_text_test.py", "run_image_test.py" and "run_video_test.py" for testing, respectively.

Please modify the dataset path, the item encoder, the pretrained model path, gpu devices, gpu numbers and hyper-parameters before you run the training script, and fill in the best validation checkpoint (e.g., "epoch-30.pt") before running the test script.

Note that you need to prepare lmdb file and specify it in the scripts before you run image-based or video-based VideoRec. To solve this, we have prepared a python script for lmdb generation, please see "Data Generation/generate_cover_frames_lmdb.py" for details.

## Environments
```
python==3.8.12
Pytorch==1.8.0
cudatoolkit==11.1
torchvision==0.9.0
transformers==4.23.1
```

# Baseline Evaluation

<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/main/Results/baseline_evaluation.png"/></div>

# Video Understanding Meets Recommender Systems

<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/main/Results/video_meets_rs.png"/></div>
