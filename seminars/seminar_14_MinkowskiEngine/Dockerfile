FROM nvidia/cuda:11.7.1-cudnn8-devel-ubuntu22.04

ENV DEBIAN_FRONTEND=noninteractive \
    VIRTUAL_ENV=/opt/me-venv \
    PATH=/opt/me-venv/bin:/usr/local/cuda/bin:$PATH \
    CUDA_HOME=/usr/local/cuda \
    TORCH_CUDA_ARCH_LIST=7.5 \
    MAX_JOBS=2

WORKDIR /work

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    git \
    libopenblas-dev \
    ninja-build \
    python3 \
    python3-dev \
    python3-venv \
    wget \
    && rm -rf /var/lib/apt/lists/*

RUN python3 -m venv "$VIRTUAL_ENV" \
    && pip install --upgrade "pip==22.3.1" "setuptools==69.5.1" wheel \
    && pip install \
        "numpy<2" \
        torch==1.13.1 \
        torchvision==0.14.1 \
        h5py \
        scikit-learn \
        tqdm \
        notebook \
        ipykernel \
    && pip install -U git+https://github.com/NVIDIA/MinkowskiEngine -v --no-deps \
        --install-option="--force_cuda" \
        --install-option="--blas=openblas" \
    && python -m ipykernel install --sys-prefix --name minkowski --display-name "Python (MinkowskiEngine)"

CMD ["bash"]
