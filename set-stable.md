# Stable Diffusion Web UI（AUTOMATIC1111）

## Recommended Specs

* CPU: 6core
* memory: 16gb~
* GPU(VRAM): 8gb~
* storage: 512gb~

## Python

```
sudo apt update
sudo apt upgrade

sudo apt install wget git python3 python3-pip python3-venv
```

## CUDA Toolkit

```
// CUDA apt_preference
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600

// To Local deb
wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda-repo-ubuntu2204-11-7-local_11.7.1-515.65.01-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-11-7-local_11.7.1-515.65.01-1_amd64.deb

// cp key-info
sudo cp /var/cuda-repo-ubuntu2204-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/

// install
sudo apt update
sudo apt install cuda-11-7

```

## Write Path

```
vim ~/.zshrc
```


```
# Setting CUDA PATH

export PATH=”/usr/local/cuda-11.7/bin:$PATH”

export LD_LIBRARY_PATH=”/usr/local/cuda-11.7/lib64:$LD_LIBRARY_PATH”

export PATH=$PATH:/home/glkt/.local/bin

export PATH="$HOME/.nodenv/bin:$PATH"
eval "$(nodenv init -)"
```

## Clone Stable Diffusion WebUi

```
git clone –depth=1 –branch v1.2.1 https://github.com/AUTOMATIC1111/stable-diffusion-webui
cd stable-diffusion-webui
```

```
vim webui-user.sh

### if u clone other dir
install_dir="/home/$(whiami)"

### if u are version v1.2.1
vim ./requirements_versions.txt
 httpx==0.24.1
```

```
chmod 755 webui-user.sh
zsh ./webui-user.sh
zsh ./webui.sh
```