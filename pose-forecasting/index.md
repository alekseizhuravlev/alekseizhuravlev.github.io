---
title: Human Pose Forecasting
# subtitle: Human Pose Forecasting
# type: project
summary: • A human pose prediction model based on temporal convolution. Performs inference in autoregressive way over time intervals of up to 2 seconds.
date: '2023-10-31T00:00:00Z'

links:
- name: Project Page
  url: 'https://alekseizhuravlev.github.io/project/pose_forecasting/'
- name: PDF
  url: 'https://drive.google.com/file/d/1uFtFNbG0R6z7cEVWbDfxI2-yMyg_wJ5K/view?usp=sharing'
- name: Code
  url: 'https://github.com/AlekseiZhuravlev/MotionMixerConv/'


slides: ""

image:
  preview_only: true


# Page settings
show_title: false

show_date: false
reading_time: false
share: false
profile: false
commentable: true
editable: false
pager: false
show_related: false
show_breadcrumb: false

header:
  navbar:
    enable: false
---

<div align="center">
  <b>Aleksei Zhuravlev and Valentin von Bornhaupt</b><br>
  <b><i>University of Bonn</i></b>
</div>


<table>
  <tr>
    <td><img src="visualization/best_model_h36m/walking_1_10.gif" width="320" height="240"><br />Prediction on Human3.6m dataset</td>
    <td><img src="visualization/best_model_ais_local/2021-08-04-singlePerson_001_20_10.gif" width="320" height="240"><br />Prediction on our dataset</td>
    </tr>
</table>


## Abstract

<div style="text-align: justify"> 
In this work we address the problem of 3D human pose forecasting. Given a pose representation, our model, Convolutional Mixer, first applies the convolution in temporal dimension, learning the dependency between the target joint position at previous and future time frames. Then, it performs convolution in pose dimension to assess the relation between adjacent joints. We perform experiments on Human3.6m dataset and evaluate the importance of each parameter of our model.  We also evaluate it on the custom dataset recorded in the AIS lab. Finally, we extend it to perform predictions in an autoregressive fashion, which allows us to perform inference over long time intervals. Our results show that the model performs well on various motion sequences, and generalizes to novel datasets and long predictions.
</div>


## Method


![Model architecture](visualization/Model_architecture.png)

- We build upon MotionMixer, which applied MLPs to an encoded pose vector. We replaced MLPs with convolutional layers and experimented with kernel sizes, number of layers, and ways to encode the pose vector
- Our model can work with different methods of human pose representation, such as axis-angle or coordinate-based formats. We consider both local motion with respect to pelvis joint as well as global. 
- We use 10 seed frames for prediction and output 10 subsequent frames. To generalize to longer sequences, we additionally consider autoregressive prediction with a sliding window for a total of 25 frames.
- We test our model on Human3.6m dataset and custom data captured by our tutor, which has a slightly different skeleton model

## Results on Human3.6m dataset: 

### 10 seed frames + 10 frames prediction

<table>
  <tr>
    <td><img src="visualization/best_model_h36m/directions_1_10.gif" width="320" height="240"><br />directions</td>
    <td><img src="visualization/best_model_h36m/discussion_1_10.gif" width="320" height="240"><br />discussion</td>
  </tr>
    <tr>
        <td><img src="visualization/best_model_h36m/smoking_1_10.gif" width="320" height="240"><br />smoking</td>
        <td><img src="visualization/best_model_h36m/waiting_1_10.gif" width="320" height="240"><br />waiting</td>
    </tr>
    <tr>
        <td><img src="visualization/best_model_h36m/walking_1_10.gif" width="320" height="240"><br />walking</td>
        <td><img src="visualization/best_model_h36m/walkingtogether_1_10.gif" width="320" height="240"><br />walkingtogether</td>
    </tr>
</table>

### Autoregressive: 10 seed frames + 25 frames prediction

<table>
  <tr>
    <td><img src="visualization/best_model_h36m_autoregressive/directions_1_10.gif" width="320" height="240"><br />directions</td>
    <td><img src="visualization/best_model_h36m_autoregressive/discussion_1_10.gif" width="320" height="240"><br />discussion</td>
  </tr>
    <tr>
        <td><img src="visualization/best_model_h36m_autoregressive/smoking_1_10.gif" width="320" height="240"><br />smoking</td>
        <td><img src="visualization/best_model_h36m_autoregressive/waiting_1_10.gif" width="320" height="240"><br />waiting</td>
    </tr>
    <tr>
        <td><img src="visualization/best_model_h36m_autoregressive/walking_1_10.gif" width="320" height="240"><br />walking</td>
        <td><img src="visualization/best_model_h36m_autoregressive/walkingtogether_1_10.gif" width="320" height="240"><br />walkingtogether</td>
    </tr>
</table>


## Results on custom dataset:

### 10 seed frames + 10 frames prediction

<table>
  <tr>
    <td><img src="visualization/best_model_ais_local/2021-08-04-singlePerson_000_20_10.gif" width="320" height="240"><br />singlePerson_000</td>
    <td><img src="visualization/best_model_ais_local/2021-08-04-singlePerson_001_20_10.gif" width="320" height="240"><br />singlePerson_001</td>
    </tr>
    <tr>
        <td><img src="visualization/best_model_ais_local/2022-05-26_2persons_001_30_10.gif" width="320" height="240"><br />2persons_001</td>
        <td><img src="visualization/best_model_ais_local/2022-05-26_2persons_002_30_10.gif" width="320" height="240"><br />2persons_002</td>
    </tr>
</table>

### Global movement: 10 seed frames + 10 frames prediction

<table>
  <tr>
    <td><img src="visualization/best_model_ais_global/2021-08-04-singlePerson_000_10_10.gif" width="320" height="240"><br />singlePerson_000</td>
    <td><img src="visualization/best_model_ais_global/2021-08-04-singlePerson_001_10_10.gif" width="320" height="240"><br />singlePerson_001</td>
    </tr>
    <tr>
        <td><img src="visualization/best_model_ais_global/2022-05-26_2persons_001_10_10.gif" width="320" height="240"><br />2persons_001</td>
        <td><img src="visualization/best_model_ais_global/2022-05-26_2persons_002_10_10.gif" width="320" height="240"><br />2persons_002</td>
    </tr>
</table>

### Autoregressive: 10 seed frames + 25 frames prediction

<table>
  <tr>
    <td><img src="visualization/best_model_ais_autoregressive/2021-08-04-singlePerson_000_20_10.gif" width="320" height="240"><br />singlePerson_000</td>
    <td><img src="visualization/best_model_ais_autoregressive/2021-08-04-singlePerson_001_20_10.gif" width="320" height="240"><br />singlePerson_001</td>
    </tr>
    <tr>
        <td><img src="visualization/best_model_ais_autoregressive/2022-05-26_2persons_001_30_10.gif" width="320" height="240"><br />2persons_001</td>
        <td><img src="visualization/best_model_ais_autoregressive/2022-05-26_2persons_002_30_10.gif" width="320" height="240"><br />2persons_002</td>
    </tr>
</table>

---
