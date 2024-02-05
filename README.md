# A Content-Driven Micro-Video Recommendation Dataset at Scale

# Dataset

Dataset downloader (for Windows): https://github.com/microlens2023/microlens-dataset/blob/master/Downloader/microlens_downloader.exe

Dataset downloader (for Linux): https://github.com/microlens2023/microlens-dataset/blob/master/Downloader/microlens_downloader

For review purposes, we are temporarily releasing a portion of our Microlens dataset.

Through the download tools, you can download 500 randomly sampled videos from the Microlens dataset, including cover images, full-length videos (with audios), and textual captions (including tags) for all 100 videos.

Additionally, we also provide the interaction file for MicroLens-100k (namely "MicroLens-100k_pairs.csv"), in which the three columns are "userID", "videoID" and "timestamp".

For various types of modal data and the interaction pairs of MicroLens-100K and MicroLens, we will release all of them once the paper is accepted.

# Code

We have released the codes for all algorithms, including VideoRec (which implements all 15 video models in this project), IDRec, and VIDRec. For more details, please refer to the following paths: "Code/VideoRec", "Code/IDRec", and "Code/VIDRec". Each folder contains multiple subfolders, with each subfolder representing the code for a baseline.

## Special instructions on VideoRec

In VideoRec, if you wish to switch to a different training mode, please execute the following Python scripts: 'run_id.py', 'run_text.py', 'run_image.py', and 'run_video.py'. For testing, you can use 'run_id_test.py', 'run_text_test.py', 'run_image_test.py', and 'run_video_test.py', respectively. Please see the path "Code/VideoRec/SASRec" for more details.

Before running the training script, please make sure to modify the dataset path, item encoder, pretrained model path, GPU devices, GPU numbers, and hyperparameters. Additionally, remember to specify the best validation checkpoint (e.g., 'epoch-30.pt') before running the test script.

Note that you will need to prepare an LMDB file and specify it in the scripts before running image-based or video-based VideoRec. To assist with this, we have provided a Python script for LMDB generation. Please refer to 'Data Generation/generate_cover_frames_lmdb.py' for more details.

## Special instructions on IDRec and VIDRec

In IDRec, see `IDRec\process_data.ipynb` to process the interaction data.  Execute the following Python scripts: 'main.py'  under each folder to run the corresponding baselines. The data path, model parameters can be modified by changing the `yaml` file under each folder. 

## Environments
```
python==3.8.12
Pytorch==1.8.0
cudatoolkit==11.1
torchvision==0.9.0
transformers==4.23.1
```

# More Results on MicroLens

## Recommendation Scenario of Collected Platform

Figure 1 below illustrates the recommendation scenario of the micro-video platform from which our MicroLens collected data. In this example, a user is recommended a video about trucks. After watching a short segment, the user swipes up to the next video. All these videos allow user engagement through buttons for liking, sharing, and commenting, which are visible on the right side of the videos. On this platform, there are multiple ways to define positive and negative examples. For instance, the duration of video views, presence of likes, comments, or shares can all be considered as different levels of user feedback.  However, among these behaviors, only comment behaviors are public without any access restrictions. Also,  note that the videos and comments are publicly accessible both on the mobile app and the web. In the mobile app, users navigate to the next video by swiping gestures, while on the web, users use mouse scrolling to move to the next video. The web scene is displayed in the same way as the mobile app scene.

In the micro-video application, users are typically presented with a continuous stream of videos. The recommendation process continues uninterrupted through the user swiping up or mouse scrolling, ensuring a seamless flow of video recommendations.

**Figure 1: An illustration of the recommendation scenario in MicroLens. Videos a, b, and c are displayed in landscape format, while videos d, e, and f are displayed in portrait format. Please note that the format of the next video is random and can be either landscape or portrait.The English translation is provided for all video titles**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/main/Results/recommendation-scenario.png"/></div>
