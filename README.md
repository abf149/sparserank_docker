# Due date: Feb 28, 2022 at 11:59 P.M.

# Lab 2: The Neural Network Training Competition

Now that we have seen how to run simple networks using PyTorch, our next goal will be to train our own network for a classic computer vision task. The task we will focus on is based on the CIFAR-10 dataset. Our goal is to come up with the simplest network to correctly classify the supplied images into one of 10 classes.

We will be running this assignment as a competition on Kaggle. [Kaggle](https://www.kaggle.com) offers a platform where companies and researchers can post data for the community to compute to produce the best model that explains the provided data. Please use this URL to join the in-class competition for this lab: https://www.kaggle.com/t/d818dc63f8f14bfea7acb1d1ccb69819.

This lab can be broken down into two large parts: 1) train your neural network that satisfies the constraints, and 2) estimate the energy and latency of processing inference using your neural network with Timeloop/Accelergy tools. The first part of this lab will require GPU support, and we outline GPU options below. The second part will be using the Docker same as in Lab 1. Please refer to [./workspace/lab2/README.md](./workspace/lab2/README.md) for details. The neural network training and Timeloop/Accelergy profiling both take **multiple hours to finish**, so please start this lab early.

## Update Docker

Before starting this lab, please update the Docker image. This step has to be done only once. 
```
cd <your-git-repo-for-lab2>
docker-compose pull
```
After downloading the new Docker image, please start the Docker (and the Jupyter server) same as in Lab 1, with `docker-compose up`. 

## GPU Platform

This lab requires GPU support. The starter codes will outline basic training and utility functions you can use for this lab, depending on your GPU platform. We recommend using Google Colab, which offers free GPU acceleration (NVIDIA K80), for the training purpose. However, if you have a personal GPU platform that you have been already using (e.g., GPU Laptops, AWS or Google Cloud Platform), please feel free to use it. 

1. Personal GPU Available

If you have a personal GPU that can be used for this lab, please install [PyTorch](https://pytorch.org/) with GPU support. The docker we are using does not support GPU, and you can separately install PyTorch for GPU using virtual environments (e.g., Ananconda) on your personal computer. For the starter code for training your neural network, please refer to [./workspace/lab2/starter-code-gpu.ipynb](./workspace/lab2/starter-code-gpu.ipynb).

2. Google Colab (Recommended)

Google Colab offers free GPU acceleration. You can copy the starter code in [./workspace/lab2/starter-code-colab.ipynb](./workspace/lab2/starter-code-colab.ipynb) to your Google Drive, and follow instructions in the starter code to start using Google Colab. You don't have to install any other programs locally to your personal computer in this case! The GPU types in Colab vary over time, including Nvidia K80s, T4s, P4s and P100s.

## Grading Rubric

In this lab, you can design your own neural network, aiming for high accuracy while achieving low energy and latency. With this is mind, you need to construct the a single neural network to maximize your grade on the assignment. All error rates below are on the test set. 

- Hard constraints (violation of any of these conditions will result in 0 point)
    - The peak activation size (sum of both the input activation size and the output activation size to any given layer) should be smaller than 1MB.
    - Error rate on the test set should be less than 50%. 
    
- Base Points (Maximum: 120 Points)
    - Error rate
    
    | Error rate  | 40%~49%  |  30%~39% |  20%~29% |  10%~19% |  5%~9%   |  < 5%    | 
    | :---------: | :------: | :------: | :------: | :------: | :------: | :------: |
    | Point       | 30       | 40       | 50       | 60       | 70       | 80       |
    
    - Energy
    
    | Energy  | < 2mJ   | < 1.5mJ  | < 1mJ    | < 0.5mJ  |
    | :-----: | :-----: | :-----:  | :-----:  | :-----:  |
    | Point   | 5       | 10       | 15       | 20       |
    
    - Latency
    
    | Latency  | < 1M cycles | < 0.5M cycles | < 0.25M cycles | < 0.1M cycles |
    | :-----:  | :---------: | :-----------: | :------------: | :-----------: |
    | Point    | 5           | 10            | 15             | 20            |
    
- Bonus Points from the Competition (Maximum: 10 Points)

In addition to the base points, you can earn bonus points based on your competition ranking. The competition ranking will be determined by both the error rate and the latency. The metric for the ranking will be: 

`metric = error_rate_in_percent/12 + num_cycles/300000`

Your goal is to minimize this metric. The competition ranking you can check from the Kaggle page will only show you the ranking based on the error rate. After the competition ends, we will compute the new ranking using both the error rate and the latency. 

Depending on your final ranking, you will get bonus points:

- Top 1~5: +10 points
- Top 6~10: +5 points
    
    
## Rules

1. Please do not use or reverse-engineer the test set to improve the performance of your model. You can only use the training set (and choose a subsample of it as the validation set) to train the model and choose pre-processing and hyperparameters.
2. Please do not use any pre-trained models that were trained using other datasets, such as ImageNet.
3. Please commit and push your training code and the pytorch model description to this repository. If we cannot reasonably reproduce your error rate, we will not award the competition bonus points. Specify your hyperparameters and random seed numbers as well.
4. Please do not change Timeloop/Accelergy settings in `./workspace/lab2/simple_weight_stationary` and `./workspace/lab2/profiler.py`.
5. Finally, sign this agreement form: 
https://forms.gle/GQ7Rzsa4kZM8ZU4j9
