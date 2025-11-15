[WSL安装](开发环境/WSL)
## ROCm

### 安装

[快速入门安装指南 — ROCm 安装 （Linux）](https://rocm.docs.amd.com/projects/install-on-linux/en/latest/install/quick-start.html)

[Install Radeon software for WSL with ROCm — Use ROCm on Radeon and Ryzen](https://rocm.docs.amd.com/projects/radeon-ryzen/en/latest/docs/install/installrad/wsl/install-radeon.html)

Windows 需要安装 `Radeon™ Software for Windows`

```
wget https://repo.radeon.com/amdgpu-install/6.4.2.1/ubuntu/jammy/amdgpu-install_6.4.60402-1_all.deb

sudo apt install ./amdgpu-install_6.4.60402-1_all.deb

sudo apt update

sudo amdgpu-install --list-usecase

amdgpu-install -y --usecase=wsl,rocm --no-dkms

rocminfo
```

### 卸载

```
sudo amdgpu-uninstall
```

### 升级

先卸载再安装

## pytorch

[安装 PyTorch for ROCm — 在 Radeon 和 Ryzen 上使用 ROCm](https://rocm.docs.amd.com/projects/radeon-ryzen/en/latest/docs/install/installrad/wsl/install-pytorch.html)

[AMD Repo](https://repo.radeon.com/rocm/manylinux/)

```
wget https://repo.radeon.com/rocm/manylinux/rocm-rel-6.4.2/torch-2.6.0%2Brocm6.4.2.git76481f7c-cp312-cp312-linux_x86_64.whl
wget https://repo.radeon.com/rocm/manylinux/rocm-rel-6.4.2/torchvision-0.21.0%2Brocm6.4.2.git4040d51f-cp312-cp312-linux_x86_64.whl
wget https://repo.radeon.com/rocm/manylinux/rocm-rel-6.4.2/pytorch_triton_rocm-3.2.0%2Brocm6.4.2.git7e948ebf-cp312-cp312-linux_x86_64.whl
wget https://repo.radeon.com/rocm/manylinux/rocm-rel-6.4.2/torchaudio-2.6.0%2Brocm6.4.2.gitd8831425-cp312-cp312-linux_x86_64.whl
pip3 uninstall torch torchvision pytorch-triton-rocm
pip3 install torch-2.6.0+rocm6.4.2.git76481f7c-cp312-cp312-linux_x86_64.whl torchvision-0.21.0+rocm6.4.2.git4040d51f-cp312-cp312-linux_x86_64.whl torchaudio-2.6.0+rocm6.4.2.gitd8831425-cp312-cp312-linux_x86_64.whl pytorch_triton_rocm-3.2.0+rocm6.4.2.git7e948ebf-cp312-cp312-linux_x86_64.whl
```

```
location=`pip show torch | grep Location | awk -F ": " '{print $2}'`

cd ${location}/torch/lib/

rm libhsa-runtime64.so*

conda install -c conda-forge gcc=12.1.0
```

```
python3 -c 'import torch' 2> /dev/null && echo 'Success' || echo 'Failure'

python3 -c 'import torch; print(torch.cuda.is_available())'

python3 -c "import torch; print(f'device name [0]:', torch.cuda.get_device_name(0))"

python3 -m torch.utils.collect_env
```

## LLaMA Factory（AMD）

[hiyouga/LLaMA-Factory: Unified Efficient Fine-Tuning of 100+ LLMs & VLMs (ACL 2024)](https://github.com/hiyouga/LLaMA-Factory?tab=readme-ov-file#build-docker)

### 下载代码

```
git clone https://github.com/hiyouga/LLaMA-Factory.git
```

```
pip install -e ".[metrics]" --no-build-isolation
```

