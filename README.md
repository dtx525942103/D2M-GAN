# D2M-GAN: Music Generation for Dance Videos.
This is the official Pytorch implementation for **D2M-GAN**, a VQ-GAN based complex music generative model for dance videos.

[Paper](https://arxiv.org/abs/2204.00604) | [Samples](https://l-yezhu.github.io/D2M-GAN/) 

### Updates:

- [X] I provided the pre-processed AIST++ visual, motion and music audio data in 2-seconds to facilitate the training experiments. They can be downloaded here if needed: [video](https://drive.google.com/file/d/1Wb5HVJW3oP9Q2WTu_rqaTIOAFoxPoLTI/view?usp=sharing), [motion](https://drive.google.com/file/d/138rM85CDbSRTsHaLOEXdqqzDyS0vt_sT/view?usp=sharing), [audio](https://drive.google.com/file/d/1YVDvHqg3Tw7gxzdt8fSNtuDPFru9rgxa/view?usp=sharing)
- [ ] I will provide the script to calculate the beats scores between the GT and generated music later.
- [ ] The TikTok Dance-Music dataset release.
- [ ] Pre-trained models release.


## 1. Project Overview
In our paper Quantized GAN for Complex Music Generation from Dance Videos, we present Dance2Music-GAN (D2M-GAN), a novel adversarial multi-modal framework that generates complex musical samples conditioned on dance videos.

<p align="center">
	<img src="assets/d2m.png" width="700">


## 2. Environment Setup

The envirunment can be set up following the instructions below.
Since our proposed **D2M-GAN** utilizes the VQ-VAE decoder of JukeBox for synthesizing the music, part of the code for loading the pre-trained VQ-VAE are adapted from the [JukeBox repo](https://github.com/openai/jukebox).

 
```
conda create --name d2m python=3.8
source activate d2m
conda install mpi4py==3.0.3
# install the pytorch and cudatoolkit based on your machine env.
conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=11.0 -c pytorch
git clone https://github.com/L-YeZhu/D2M-GAN.git
cd D2M-GAN
pip install -r requirements.txt
pip install -e .
```


## 3. Data

We conduct experiments on the following two datasets.

### 3.1 AIST++ Dataset
The AIST++ dataset is a subset of AIST dataset, which can be downloaded from [here](https://google.github.io/aistplusplus_dataset/download.html). We use the cross-modality data split for training and testing. We also provide our preprocessed [motion](https://drive.google.com/file/d/138rM85CDbSRTsHaLOEXdqqzDyS0vt_sT/view?usp=sharing), [vision](https://drive.google.com/file/d/1Wb5HVJW3oP9Q2WTu_rqaTIOAFoxPoLTI/view?usp=sharing), and [music audio](https://drive.google.com/file/d/1YVDvHqg3Tw7gxzdt8fSNtuDPFru9rgxa/view?usp=sharing) data.


### 3.2 TikTok Dance-Music Dataset
We build a TikTok Dance-Music dataset, which contains the "in-the-wild" dance videos. The current dataset has 445 dance videos with an average length of 12.5 seconds. 
The dataset will be released later.
<!-- This dataset can be downloaded from our [project page](). -->




## 4. Training

### 4.1 Training on the AIST++
To train the D2M-GAN on the AIST++ dataset.

```
python d2m_aist.py --model=5b --save_sample_path=./samples --model_level=high
```

### 4.2 Training on the TikTok Dance-Music
To train the D2M-GAN on the TikTok Dance-Music dataset. 

```
python d2m_tiktok.py --model=5b --save_sample_path=./samples --model_level=high
```


## 5. Generation

After finish training the **D2M-GAN**, run the following command to generate the music samples.

For the AIST++ dataset.

```
python generate_aist.py --model=5b --load_path=./logs_aist_high --result_path=./audio_result_aist --model_level=high
```

For the TikTok dance-music dataset.

```
python generate_tiktok.py --model=5b --load_path=./logs_tiktok_high --result_path=./audio_result_tiktok --model_level=high
```



## 6. Citation
Please consider citing our paper if you find it useful. 
```
@article{yezhu2022quantizedgan,
  title={Quantized GAN for Complex Music Generation from Dance Videos},
  author={Zhu, Ye and Olszewski, Kyle and Wu, Yu and Achlioptas, Panos and Chai, Menglei and Yan, Yan and Tulyakov, Sergey},
  journal={arXiv preprint arXiv:2204.00604},
  year={2022}
}
```


