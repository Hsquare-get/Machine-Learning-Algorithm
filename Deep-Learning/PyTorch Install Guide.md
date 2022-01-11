# PyTorch Install Guide

## 1. 설치 환경

- Windows10
- NVIDIA GeForce GTX 1050
- 참고 설치가이드: https://blog.daum.net/geoscience/1565

<br/>

## 2.사전 설치

### 2.1 Anaconda

### 2.2 MS Visual Studio Community 2019

- 다운로드 링크: https://docs.microsoft.com/ko-kr/visualstudio/releases/2019/release-notes

- 다운로드 후 로그인하여 새 프로젝트 템플릿에 `CUDA 11.5 Runtime` 있는지만 확인

### 2.3 CUDA

- GPU 환경에서 연산하려면 CUDA 플랫폼 설치
- 서버PC의 그래픽카드가 CUDA가 지원해주는 그래픽카드인지 확인 (https://developer.nvidia.com/cuda-gpus)
- 운영체제에 맞게 CUDA Toolkit(11.5) 설치 (https://developer.nvidia.com/cuda-toolkit)

<br/>

## 3. 가상환경에 PyTorch 설치

```bash
# 가상환경 생성 (Anaconda Prompt)
(base) conda create -n pytorchtest python=3.8
(base) conda activate pytorchtest

# Pytorch Install (https://pytorch.kr/get-started/locally/)
(pytorchtest) conda install pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch
```



```bash
# python shell에서 pytorch 테스트
(pytorchtest) python
>>> import torch
>>> torch.__version__
>>> import torchvision
>>> torchvision.__version__
>>> torch.rand(5,3)					# 텐서 생성
>>> torch.cuda.is_available()		# CUDA 플랫폼 사용 가능 여부
>>> torch.cuda.device_count()		# 디바이스 개수
>>> torch.cuda.current_device()		# 현재 디바이스 ID
>>> torch.cuda.get_device_name(0)	# 디바이스 명칭 (그래픽카드명)
```