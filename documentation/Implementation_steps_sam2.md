# **SAM2 Model for Lumbar Paraspinal Muscle Segmentation**

This repository implements **SAM2** for **lumbar paraspinal muscle segmentation** using **Linux (Ubuntu 18.04)** with an **RTX 3060 GPU (12GB VRAM)**. The implementation is based on [Facebook Research's SAM2 repository](https://github.com/facebookresearch/sam2).

---

## **Environment Setup**

Before using SAM2, ensure that Python and PyTorch are installed. The model requires:

- **Python**: `>=3.10`
- **PyTorch**: `>=2.5.1`
- **Torchvision**: `>=0.20.1`

### **Installation Steps**
```bash
# Step 1: Create and activate the conda environment
conda create -n sam2 python=3.10
conda activate sam2

# Step 2: Install Jupyter Notebook
conda install notebook>=5.3 jupyter_server

# Step 3: Install PyTorch and dependencies
conda install pytorch==2.3.1 torchvision==0.18.1 torchaudio==2.3.1 pytorch-cuda=11.8 -c pytorch -c nvidia

# Step 4: Clone the SAM2 repository
git clone https://github.com/facebookresearch/sam2.git && cd sam2

# Step 5: Install required packages
pip3 install -e .

# Step6: Run the SAM2 video segmentation example to confirm that the environment and file structure are correctly set up:
notebooks/video_predictor_example.ipynb

# Step7: Replace the following files in the original SAM2 repository to output iou_score:

sam2_video_predictor.py → sam2/sam2_video_predictor.py
sam2_base.py → sam2/modeling/sam2_base.py  

# Step8: Run SAM2 for LPM segmentation on T1-weighted (T1W) and T2-weighted (T2W) MRI images in a training-free manner.
# We have not re-trained SAM2 but instead use its original weights and implementation code with our LPM dataset.
Github_SAM2seg_LPM_T1W.ipynb
Github_SAM2seg_LPM_T2W.ipynb

```

To **remove** the environment if needed:
```bash
conda remove -n sam2 --all
```

---

## **Data Download**
Download the dataset and extract the files into the following directories. The dataset is provided in both JPG and PNG formats (.zip) within this GitHub repository:

```
notebook/videos/MRI515_T1

notebook/videos/MRI515_T2
```

---
