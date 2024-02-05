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

## Related Datasets

**Table 1: Dataset comparison. "p-Image" refers to pre-extracted visual features from pre-trained visual encoders (such as ResNet), while "r-Image" refers to images with raw image pixels. "Audio" and "Video" refer to the original full-length audio and video content. Note that MicroLens is the first recommendation dataset that contains raw micro-video data.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/dataset-comparison.png"/></div>

## Video Model Details in Video Understanding and Recommendation

**Table 2: Performance of VideoRec with 15 video encoders. "Pretrain Settings" are the adopted frame length and sample rate from the pre-trained checkpoint. ACC@5 is the accuracy of the video classification task.**

<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/video-details.png"/></div>

## Hyper-parameter Settings for Baselines

**Table 3: Hyper-parameters settings for baselines. The "finetuning rate" denotes the learning rate applied to the video encoder during the finetuning process.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/baseline-settings.png"/></div>

## Details of the Applied Image Encoders

**Table 4: Network architecture, parameter size, and download URL of the vision encoders for image baselines. L: number of Transformer blocks, H: number of multi-head attention, C: channel number of the hidden layers in the first stage, B: number of layers in each block.**

<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/image-details.png"/></div>

## Recommendation with Side Features

We investigate the impact of other features on recommendation performance using the MicroLens-100K dataset. We introduce two types of side features: item popularity level (Pop) and tag categories (Tag). For popularity features, we divide the item popularity into 10 uniform bins. The first bin represents the top 10% of popular items, while the last bin represents the bottom 10%. We assign a Pop ID to each item according to its popularity level. Regarding the tag features, we also handle them as categorical features with a category of 15,580. We conducted experiments on SASRec_{ID} (ID) with different feature combinations: SASRec_ID, SASRec_{ID+Pop}, SASRec_{ID+Tag}, and SASRec_{ID+Pop+Tag}. The "+" symbol denotes feature combinations achieved by summing and averaging them. We report the results in Table 5.

We found that incorporating item popularity level and tag categories as side features did not clearly improve the algorithm's performance. One possible reason is that in typical recommendation scenarios, item ID embeddings have already been extensively trained, implicitly learning latent factors including similarity and popularity. For instance, we observed that many videos recommended in the top-10 recommendation list share similar categories and have relatively high popularity, indicating that ID-based methods can already capture popularity and category information. In such scenarios, incorporating many unimportant features  may have a negative impact on overall performance. It is worth noting that in the very cold-start setting, the item ID feature is very weak and adding other features is necessary for better performance.

**Table 5: Recommendation results with side features on MicroLens-100K.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/side-features.png"/></div>

## Baseline Evaluation and Warm-up Recommendation on MicroLens-1M

**Table 6: Benchmark results on MicroLens-1M.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/benchmark-1m.png"/></div>

**Table 7: Comparison of VideoRec and IDRec in regular and warm-start settings using SASRec as the user backbone. Warm-20 denotes that items with less than 20 interactions were removed from the original MicroLens-1M.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/warm-1m.png"/></div>

## Comparison between Textual Features and Video Content

We used [BERT](https://huggingface.co/prajjwal1/bert-small) as the text encoder and SlowFast16x8-r101 as the video encoder and perform end-to-end training. We fixed the learning rate of recommender model as 1e-4, and searched for the optimal learning rates for the text encoder and video encoder from {1e-3, 1e-4}. The comparison results are reported in Table 8. Our results demonstrate that using only text features yields similar performance to the itemID feature. By analyzing the data, we have observed that some short videos have only a few words in their descriptions, which may contribute to the performance not being particularly competitive. On the other hand, the amount of information contained in the original videos far exceeds that of the video titles. Therefore, we believe that in the future, utilizing more powerful video understanding techniques can lead to better recommendation results.

**Table 8: Comparison results of ID, textual features and video content on MicroLens-100K.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/text-video.png"/></div>

## Computation Cost

**Table 9. The computation cost information for IDRec and VideoRec on the MicroLens-100K dataset, where SASRec is taken as the recommender backbone and top1-block fine-tuning strategy used in this paper is applied for VideoRec. #Param: the size of tunable parameters, FLOPs: computational complexity, Time/E: averaged training time for one epoch, BE: the best epoch in terms of optimal validation results, MU: GPU memory usage, and the GPU configuration used, e.g., ’A40-48G(4)’ denotes that we used 4 A40s with 48G memory. Note that although VideoRec by E2E learning is more expensive than IDRec, it also shows improved performance. The main finding is that there is still much room for improvement in recommendation models by properly leveraging video features. We believe that more effective and efficient VideoRec models, even beyond the VideoRec paradigm, can be developed in the future inspired by MicroLens.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/computation-cost.png"/></div>


## Recommendation Scenario of Collected Platform

Figure 1 below illustrates the recommendation scenario of the micro-video platform from which our MicroLens collected data. In this example, a user is recommended a video about trucks. After watching a short segment, the user swipes up to the next video. All these videos allow user engagement through buttons for liking, sharing, and commenting, which are visible on the right side of the videos. On this platform, there are multiple ways to define positive and negative examples. For instance, the duration of video views, presence of likes, comments, or shares can all be considered as different levels of user feedback.  However, among these behaviors, only comment behaviors are public without any access restrictions. Also,  note that the videos and comments are publicly accessible both on the mobile app and the web. In the mobile app, users navigate to the next video by swiping gestures, while on the web, users use mouse scrolling to move to the next video. The web scene is displayed in the same way as the mobile app scene.

In the micro-video application, users are typically presented with a continuous stream of videos. The recommendation process continues uninterrupted through the user swiping up or mouse scrolling, ensuring a seamless flow of video recommendations.

**Figure 1: An illustration of the recommendation scenario in MicroLens. Videos a, b, and c are displayed in landscape format, while videos d, e, and f are displayed in portrait format. Please note that the format of the next video is random and can be either landscape or portrait. The English translation is provided for all video titles**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/recommendation-scenario.png"/></div>
