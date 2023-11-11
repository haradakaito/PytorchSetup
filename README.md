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
※この時表示されるステータス画面の右上に記載されているCUDAのバージョンは, インストールしたNvidiaドライバで対応しているCUDAの最新バージョンのことであり, インストールされているCUDAのバージョンではない  
## 2. CUDAのインストール
CUDAは11.7, 11.8, 12.1を推奨する(今回は11.7をインストールする)  
CUDA11.7のアーカイブ  
https://developer.nvidia.com/cuda-11-7-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_network  
にアクセスし, Linux > x86_64 > Ubuntu > 22.04 > deb(local)を順に選択  
表示されるコマンド(下記)に従って, 入力していく  
※ この時, keyコードは自分で確認して変更することと, インストールコマンドの際にCUDAのバージョンを指定することに注意！  
```
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
$ sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.7.0/local_installers/cuda-repo-ubuntu2204-11-7-local_11.7.0-515.43.04-1_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu2204-11-7-local_11.7.0-515.43.04-1_amd64.deb
$ sudo cp /var/cuda-repo-ubuntu2204-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/
$ sudo apt-get update
$ sudo apt-get -y install cuda-11-7
$ reboot
```
任意の仮想環境へ戻り, パスを通す    
```
$ conda activate *
$ nano ~/.bashrc
```
末尾に以下を追加する  
```
export PATH=/usr/local/cuda:/usr/local/cuda-11.7/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/lib:/usr/local/cuda-11.7/lib64:$LD_LIBRARY_PATH
```
sourceした後, インストールを確認する  
```
$ source ~/.bashrc
$ conda activate *
$ nvcc -V
```
CUDAが複数入っている場合は, 優先順位をCUDA11.7が一番高くなるように変更しておく  
```
$ sudo update-alternatives --config cuda
```
## 3. cuDNNのインストール

## 4. Pytorchのインストール
