[适用于 Linux 的 Windows 子系统文档 |Microsoft 学习](https://learn.microsoft.com/en-us/windows/wsl/)

## 开启windows linux 子系统

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

## 开启虚拟平台

```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

## 安装 WSL

```
wsl --list --online

wsl --install [Distro]
```


## 设置默认WSL

```
wsl --set-default [Distro]
```

## 安装 anaconda

[Advance AI with Open Source | Anaconda](https://www.anaconda.com/)

```
wget -c https://repo.anaconda.com/archive/Anaconda3-2025.06-0-Linux-x86_64.sh

bash Anaconda3-2025.06-0-Linux-x86_64.sh

printf '\n# Anaconda path\nexport PATH=~/anaconda3/bin:$PATH\n' >> ~/.bashrc

source ~/anaconda3/bin/activate
source ~/.bashrc

conda --version
```

## 创建python环境

```
conda create -n ROCm-pytorch python=3.12

conda activate ROCm-pytorch

conda env list
```

## 删除python环境

```
conda remove -n rocm --all
```