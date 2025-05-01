# Preparing Undergraduates Through Mentoring Towards PhD's – Image-Based Quantification
Created two MATLAB codes using ROI and image-based processing to quantify the area of proliferation cells in three different types of tissues for numerous piglet uteri. Automated quantification of proliferating cell area, reducing analysis time from days to hours for biologists. Used image J for image analysis.

This repository contains two MATLAB scripts developed to support image-based quantification of proliferation areas using Regions of Interest (ROI). The work was completed by **Sashiel Vagus** as part of a mentoring project aimed at preparing undergraduates for Ph.D. programs.

## 🧠 Project Summary

These scripts were designed to assist in analyzing cellular proliferation through image processing. They take microscopy images and use ROI-based segmentation and thresholding to calculate the total proliferation area.

## 🛠 Technologies

- MATLAB
- Image Processing Toolbox

## 📁 File Structure


## 📦 Requirements

- MATLAB R2020b or later
- Image Processing Toolbox

## 🚀 How to Use

1. Clone or download this repository.
2. Open `proliferation_analysis_roi.m` in MATLAB.
3. Place your microscopy images into the `sample_images/` folder.
4. Run the script. The output files (e.g., area measurements, processed images) will be saved in the `results/` directory.

## 📌 Notes

- ROI masks can be defined manually or generated using `roi_mask_generation.m`.
- Thresholding parameters are adjustable depending on image quality.

## 👤 Author

**Sashiel Vagus**  
[GitHub Profile →](https://github.com/sashielvagus)

---

This project was completed under the supervision of **Dr. George** as part of a mentoring program preparing undergraduates for Ph.D. research pathways.
