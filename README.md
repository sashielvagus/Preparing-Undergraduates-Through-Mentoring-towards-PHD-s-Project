# Semi-Automated Image Quantification of Cell Proliferation in Gilt Uterus Tissue

This repository contains two MATLAB scripts developed for image-based segmentation and quantification of cell proliferation in gilt uterus tissue, using histological images stained with Ki67. This project was completed under the mentorship of **Dr. Uduak George** at **San Diego State University**, in collaboration with colleagues at **Purdue University**.

---

## Project Overview

The purpose of this project was to automate the quantification of proliferating versus non-proliferating cells in gilt uterus tissue, collected during a study on postnatal colostrum intake. Two MATLAB algorithms were developed:

1. **Image Segmentation**
   Segments tissue into mucosa, connective, and muscle regions using hand-drawn ROIs.

2. **Cell Area Quantification** 
   Applies color thresholding to Ki67-stained images to calculate the area of proliferating and non-proliferating cells.

This research was part of a broader effort to understand how early colostrum intake (10% vs 20% of body weight) affects postnatal tissue growth and potential fertility in gilts.

---

## Scientific Background

- **Sample source**: Gilt uteri from Purdue University's swine research farm  
- **Staining**: Ki67 for proliferating cells, H&E as visual reference  
- **Treatment groups**: COL10 and COL20, based on % body weight in colostrum intake  
- **Analysis**: Boxplots, t-tests, and random forest classification used to assess impact  
- **Findings**: No statistically significant difference in proliferation between groups, but biological trends and other significant indicators (e.g., immunocrit, TEMP-24H) were revealed


---

## Technologies Used

- MATLAB (R2020b - Version 9.9.0.1467703)
- Image Processing Toolbox (Version 11.2)
- Color Thresholder App (HSV-based masking)
- Adobe Photoshop (for panorama assembly)

---


## How to Use
Requirements: MATLAB R2020b or later with the Image Processing Toolbox installed.

Step 1: ROI-Based Tissue Segmentation
Navigate to the folder:
1) Image Segmentation - ROI Dissection
Run the script inside to manually draw Regions of Interest (ROIs) that segment the tissue image into:

Mucosa

Connective

Muscle

Segmented images will be saved and used for the next step.

Use the H&E-stained image as a guide when drawing ROIs to ensure anatomical accuracy.

Step 2: Tissue Area Masking and Cell Quantification
Navigate to the folder:

2) Tissue Area Masking
Run the following MATLAB scripts in this order:

areaMain.m – Main driver script for initializing analysis

colorAreaCalculator.m – Applies HSV-based color thresholding

proliferationMask.m – Identifies and masks proliferating (brown) cells

nonproliferationMask.m – Identifies and masks non-proliferating (blue) cells

totalTissueAreaMask.m – Captures and calculates total tissue area

Output
Segmented tissue images (mucosa, connective, muscle)

Binary masks of cell populations

An Excel file summarizing:

Proliferating cell area

Non-proliferating cell area

Total tissue area for each classification


---

## Poster Presentation

This project was presented at the 2021 SDSU Student Research Symposium (SRS).
[Click here to view the full research poster (PDF)](SRS_Poster_2021.pdf)

---

## Attribution & Acknowledgments

- **Images provided by**:
  - Dr. Theresa Casey, Department of Animal Sciences, Purdue University
  - Dr. Ariany Suarez-Trujillo & Kelsey Teeple

- **Mentor**: Dr. Uduak George (SDSU)

- **Authors**:  
  - Brooke Tyler  
  - Sashiel Vagus ([GitHub Profile](https://github.com/sashielvagus))

- **Funding**: Supported by NSF PUMP Research Grant No. DMS-1916494

---

## Citation

> Tyler, B., & Vagus, S. et al. (2021). *Predictive Multi-Scale Modeling of Postnatal Regulation of Protein Synthesis in Gilts*. The PUMP Journal of Undergraduate Research.

---

## Contact

**Sashiel Vagus**  
San Diego State University  
Email: svagus@sdsu.edu  
GitHub: [@sashielvagus](https://github.com/sashielvagus)

---

## License

This repository is shared under an academic research license. For permission to reuse or cite the work, please contact the author(s).


