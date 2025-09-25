# **SAM2 Model for Lumbar Paraspinal Muscle Segmentation**

The implementation is based on [Facebook Research's SAM2](https://github.com/facebookresearch/sam2).

---

## **Environment Setup**

Before using SAM2, ensure that Python and PyTorch are installed. The model requires:

- **Python**: `>=3.10`
- **PyTorch**: `>=2.5.1`
- **Torchvision**: `>=0.20.1`

### **Installation Steps**
```bash
# Step 1: Create and activate the conda environment
conda create -n nnsam2 python=3.10
conda activate nnsam2

# Step 2: Install Jupyter Notebook
conda install notebook>=5.3 jupyter_server

# Step 3: Install PyTorch and dependencies
conda install pytorch==2.3.1 torchvision==0.18.1 torchaudio==2.3.1 pytorch-cuda=11.8 -c pytorch -c nvidia

# Step 4: Clone the SAM2 repository
git clone https://github.com/facebookresearch/sam2.git && cd sam2

# Step 5: Install required packages
pip3 install -e .

# Step 6: Run the SAM2 video segmentation example
notebooks/video_predictor_example.ipynb

# Step 7: Replace the following files to output IoU scores
# (replace original files in the repo)
notebooks/sam2_video_predictor.py → sam2/sam2_video_predictor.py
notebooks/sam2_base.py → sam2/modeling/sam2_base.py
```

---


## **Clean Up**
```bash
conda remove -n nnsam2 --all
```

---
