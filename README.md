# [Ubuntu22.04] CUDA + cuDNN + Pytorch 環境構築

## 0. 前準備
- Ubuntu 22.04  
- CPU：Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz  
- GPU：GeForce GTX 1080  

## 1. Nvidiaドライバのインストール
既に入っているNvidiaドライバ及びCUDAドライバを削除しておく(推奨)  
```
$ sudo apt-get --purge remove nvidia-*
$ sudo apt-get --purge remove cuda-*
$ sudo apt update
$ sudo apt install ubunt-drivers-common
```
ハードウェアに適したNvidiaドライバを確認する  
```
$ ubuntu-drivers devices
```
recommendと記載されているNvidiaドライバ名をインストールする  
```
$ sudo apt install nvidia-driver-*
$ reboot
```
任意の仮想環境へ戻り, Nvidiaドライバのインストールを確認する  
```
$ conda activate *
$ nvidia-smi
```
## 2. CUDAのインストール

## 3. cuDNNのインストール

## 4. Pytorchのインストール
