---
title: Setting Up Virtual Environment for PyTorch
date: 2021-09-01 14:04:31
categories:
- Python
- PyTorch
tags:
- Python
- PyTorch
- Machine Learning
- Deep Learning
---
{% gdemo_terminal 'activate pytorch_env' '60px' 'Zerohertz' '300' '>' 'terminal' 'applescript' %}
{% endgdemo_terminal %}

<!-- More -->

+ 시작하기 전 필수 설치
  + Python
  + Anaconda

# Setting Up Virtual Environment

{% gdemo_terminal 'conda create --name pytorch_env python=3' '60px' 'Zerohertz' '300' '>' 'terminal1' 'applescript' %}
{% endgdemo_terminal %}

</br>

> To activate environment

~~~python
conda activate pytorch_env
~~~

> To deactivate an active environment

~~~python
conda deactivate
~~~

***

# Installing PyTorch and Package

~~~python
conda install -y pytorch-cpu torchvision-cpu -c pytorch
pip install torchtext
conda install -y scikit-learn
conda install -y matplotlib
conda install -y pandas
~~~