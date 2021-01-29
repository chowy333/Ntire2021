# Ntire2021
# Ntire2021

## Updated

I downloaded every dataset to "/home/wooyeong/Burst/burstsr_dataset/" (21.01.27)

## Data Configuration

**Zurich** : dir = "/home/wooyeong/Burst/burstsr_dataset/Zurich_Public/" , train = 46839, test = 1204 rgb_image

* �츮�� �ؾ��� task :  "/home/wooyeong/Burst/burstsr_dataset/syn_burst_val/"�� �ִ� 300 ������ ���� validation�� ������� 
* (LR burst = 14, size = 48 x 48 x 4) * 300 => (HR size = 384 x 384 x 3) 300��

## Dates
* 2021.01.26 Release of train and validation data  
* 2021.02.01 Validation server online  
* 2021.03.01 Final test data release (inputs only)  
* 2021.03.08 Test output results submission deadline  
* 2021.03.09 Fact sheets and code/executable submission deadline  
* 2021.03.11 Preliminary test results released to the participants  
* 2021.03.28 Paper submission deadline for entries from the challenge  
* 2021.06.15 NTIRE workshop and challenges, results and award ceremony (CVPR 2021, Online)  


## Introduction

* The task of this challenge is to generate a denoised, demosaicked, higher-resolution image, given a RAW burst as input

* The challenge uses a new dataset and has 2 tracks, namely Track 1: Synthetic and Track 2: Real-world.

## Dataset

* 300���� GT RGB, ���� 14���� sequenced bayer Raw image(RGGB)�� �����Ǿ��ִ�.
* The images in the burst have unknown offsets with respect to each other, and are corrupted by noise.
* The goal is to exploit the information from the multiple input images to predict a denoised, demosaicked RGB image having a 4 times higher resolution, compared to the input. (scale 4���� ������ ���� ���� ��ǥ)
* test split of the Zurich RAW�� ���� 

## Track 1 - Synthetic

* HR RGB �̹��� ���� LR input burst�� ������ pipeline

**Data generation** : sRGB �̹����� inverse ISP�ϰ�, Random tranlation�� rotation���� LR burst�� ���� �� , Bilinear downsampling��. �� ����, mosaic ���ְ� noise ÷��

**Training set** : synthetic burst����� �ڵ� ����, Zurich dataset���� �� ���밡��

**Validation set** : The bursts in the validation set have been pre-generated with the data generation code, using the RGB images from the test split of the Zurich RAW to RGB dataset.

## Evaluation

*  the PSNR computation will be computed in the linear sensor space, before post-processing steps such as color correction, white-balancing, gamma correction etc.

## Submission

**Validation set** : Colab server, 2�� 1�� open. save_results_synburst_val.py Ȯ���ؼ� ����

---

## Track2 - Real-world

**BurstSR dataset** : 14 sequence�� handheld smartphone camera. crop�� ����. detailed specific ���� �� �ö�� Deep Burst Super-Resolution ����.

**Challenges** : Burst �̹������� mis-alignment�� ���ߴ� ���� keypoint.

**Evaluation** : AlignedPSNR => AlignedPSNR first spatially aligns the network prediction to the ground truth, using pixel-wise optical flow estimated using PWC-Net. A linear color mapping between the input burst and the ground truth, modeled as a 3x3 color correction matrix, is then estimated and used to transform the spatially aligned network prediction to the same color space as the ground truth. Finally, PSNR is computed between the spatially aligned and color corrected network prediction and the ground truth. More description of the AlignedPSNR metric is available in the paper "Deep Burst Super-Resolution" (link will be posted soon).

**User Study** : original�� �ִ��� �� �����ϴ� ���� ��ǥ�̴�.

## Submission

* No evaluation server. validation set�� GT�� �� ��ǥ �������ٲ���