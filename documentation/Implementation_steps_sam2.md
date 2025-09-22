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

## **LPM Segmentation with SAM2**

We did not re-train SAM2 but used its original weights with our LPM datasets.  
During this stage, **IoU scores were recorded** per slice to guide pseudo-label selection.

Notebooks:
- `Github_SAM2seg_LPM_T1W.ipynb`
- `Github_SAM2seg_LPM_T2W.ipynb`

---

## **nnU-Net for Pseudo-label Refinement**

### Step 8: Install nnU-Net
```bash
pip3 install nnunet==1.7.1
```

### Step 9: Set Environment Paths

Replace the following paths with your own setup (e.g., user: `zhongyi`, repo: `/home/zhongyi/Desktop/gu-project/github_test`):

```bash
cd

export nnUNet_raw_data_base="/home/zhongyi/Desktop/gu-project/github_test/nnUNet_raw_data_base"
export nnUNet_preprocessed="/home/zhongyi/Desktop/gu-project/github_test/nnUNet_preprocessed"
export RESULTS_FOLDER="/home/zhongyi/Desktop/gu-project/github_test/nnUNet_trained_models"
```


### Step 10: Training nnU-Net Using Top-Ranking Pseudo-Labels (Optional)

Before segmenting other images, we recommend training your own nnU-Net model using pseudo-labeled data with high IoU scores.

#### 📁 Prepare Training Data

Download the training data into:
```
nnUNet_raw_data_base/nnUNet_train_data_raw/
```
(Training data provided in: `Files_for_running_github/nnUNet_train_data_raw.zip`)  
See `screenshot.png` for required folder structure.

#### ⚙️ Format the Data for nnU-Net
```bash
# Step 1: Convert filenames using Jupyter notebook
file_op_to_prepare_training_nnunet.ipynb

# Step 2: Convert segmentation into nnU-Net format
python nnunet/dataset_conversion/515_muscle_4class_seg.py
```

#### 🧠 Preprocess and Plan
```bash
python nnunet/experiment_planning/nnUNet_plan_and_preprocess.py -t 515 --verify_dataset_integrity
```

#### 🚀 Train the Model
```bash
nnUNet_train 3d_fullres nnUNetTrainerV2_noMirroring 515 1
```
This trains the **1st fold** of the five-fold cross-validation model.

---

### Step 11: Segment New Images with Trained Model

Once trained, use the model to segment new images.

#### 📥 Prepare Test Images
Download test data into:
```
nnUNet_raw_data_base/nnUNet_test_data/test_img_in_nii_raw/
```

Rename images using:
```
file_op_to_infer_by_nnunet.ipynb
```
(to ensure filenames end with `0000.nii.gz`)

#### 📦 Model Weights
If not training your own model, download pretrained weights from Google Drive:  
https://drive.google.com/file/d/1rQnBHTOlbW9yA86Xjf7PLMHpxKn0W2Ze/view?usp=drive_link

Unzip into:
```
nnUNet_trained_models/
```

#### 🧪 Run Inference
```bash
nnUNet_predict  -i $nnUNet_raw_data_base/nnUNet_test_data/test_img_in_nii/  -o $nnUNet_raw_data_base/nnUNet_test_data/test_seg_in_nii_raw/  -t 515 -m 3d_fullres -f 1  -tr nnUNetTrainerV2_noMirroring --disable_tta
```

This uses the **1st fold** of your trained nnU-Net model.
---

## **Clean Up**
```bash
conda remove -n nnsam2 --all
```

---
