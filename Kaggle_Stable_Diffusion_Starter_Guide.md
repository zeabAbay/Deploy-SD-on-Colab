# Stable Diffusion on Kaggle: Starter Guide

This guide will help you set up and use Stable Diffusion (SD) on [Kaggle Notebooks](https://www.kaggle.com/code). 
It’s tailored for content creators using Google Drive and GitHub, with a focus on AUTOMATIC1111’s WebUI (most popular and user-friendly).

---

## **Step 1: Create a Kaggle Account and Start a Notebook**

1. Go to [Kaggle](https://www.kaggle.com/).
2. Sign up (or log in) with your Google/Email account.
3. Click **Code** in the left sidebar, then **New Notebook**.

---

## **Step 2: Enable the GPU Accelerator**

1. Click the **Settings** (gear icon) on the right sidebar.
2. Under **Accelerator**, select **GPU** (usually a T4 or P100).
3. Confirm changes.

---

## **Step 3: Mount Google Drive (Optional but Recommended)**

> Kaggle does not natively support mounting Google Drive like Colab.  
> Use the [`kaggle_gdrive`](https://github.com/shubhamjn1/kaggle-gdrive) workaround, or download/upload models manually.

### **Option A: Use Kaggle Datasets for Storage**
- Upload your SD models/checkpoints as a Kaggle Dataset.
- Add them to your notebook via the “Add Data” sidebar.

### **Option B: Use a Third-Party Drive Mount Script**
- See: https://github.com/shubhamjn1/kaggle-gdrive  
  (Note: This method is unofficial and may require entering your Google credentials.)

---

## **Step 4: Clone the AUTOMATIC1111 WebUI Repository**

```python
!git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
%cd stable-diffusion-webui
```

---

## **Step 5: Install Dependencies**

> Kaggle Notebooks come with many preinstalled packages, but you may need to force (re)install compatible versions.

```python
!pip install torch==2.1.0 torchvision==0.16.0 --upgrade --quiet
!pip install xformers==0.0.20 --quiet
!pip install -r requirements.txt --quiet
```

---

## **Step 6: Add Your SD Model Checkpoint**

### **Option A: Via Kaggle Dataset**
- Upload your `.ckpt` or `.safetensors` SD model to a Kaggle Dataset.
- Add the dataset via “Add Data” sidebar.
- Copy the model to the WebUI models folder:
  ```python
  !cp /kaggle/input/YOUR_DATASET_NAME/YOUR_MODEL.ckpt /kaggle/working/stable-diffusion-webui/models/Stable-diffusion/
  ```

### **Option B: Download from URL**
- If you have a direct download link (e.g., HuggingFace), use:
  ```python
  !wget -O models/Stable-diffusion/model.ckpt "YOUR_DIRECT_MODEL_URL"
  ```

---

## **Step 7: Launch the WebUI**

> Kaggle does NOT allow you to open a public web server, but you can generate images with scripts or use Gradio tunneled via [ngrok](https://ngrok.com/) for very short sessions.

### **Example: Generate Images via Script**

```python
!python launch.py --exit
# Now use scripts to generate images, e.g.:
!python scripts/txt2img.py --prompt "a fantasy landscape, vivid colors" --n_samples 1 --n_iter 1 --plms
```

### **Optional: Use Gradio + NGROK (Advanced)**
- See [this guide](https://www.kaggle.com/code/sergeykonovalov/sd-webui-on-kaggle-with-ngrok) for exposing WebUI via ngrok.

---

## **Step 8: Save Outputs**

- Save generated images to `/kaggle/working/` to download easily.
- If using Kaggle Datasets, you can write outputs there for later sessions.

---

## **Step 9: Version Control Your Workflow**

- Save your notebook to a GitHub repo by downloading and uploading, or by using the Kaggle “Download” button.

---

## **Best Practices**

- **Pin versions** of torch, xformers, etc. for reproducibility.
- **Store models and outputs** in Kaggle Datasets or download after each session.
- **Document** your workflow in the notebook.
- **Be mindful of GPU time limits** (30 hours/week).

---

## **References and Useful Links**

- [AUTOMATIC1111 WebUI GitHub](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
- [Kaggle Notebooks](https://www.kaggle.com/code)
- [Kaggle Datasets](https://www.kaggle.com/datasets)
- [Kaggle gdrive workaround](https://github.com/shubhamjn1/kaggle-gdrive)
- [SD WebUI on Kaggle (ngrok method)](https://www.kaggle.com/code/sergeykonovalov/sd-webui-on-kaggle-with-ngrok)

---

## **Troubleshooting**

- **Out of memory?** Reduce image size or batch size.
- **Dependency errors?** Reinstall with pinned versions as shown.
- **Need more storage?** Use Kaggle Datasets or download results frequently.

---

**Happy creating!**