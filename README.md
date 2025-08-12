# 🔬 R Neurohacking
## 🎯 Objective <br>
This project uses the R programming language and its neuroimaging packages to manipulate, process, and analyze structural brain MRI data in the NIfTI (Neuroimaging Informatics Technology Initiative) format. It focuses on performing inhomogeneity correction, brain extraction, image registration, and visualization to enable comprehensive exploration of neuroimaging data. <p>
## 🛠️ Tools <br>
• <b>Language:</b> R <p>
## 🖼️ Images Brainix <br>
Of the MRI slices numbered 1 to 22, only slice 11 is shown here as representative examples. Sample R code snippets are also provided to demonstrate how to generate the images.
### DICOM FLAIR Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/951f629a1bbc2550b4d2b12ea8a01228f2862280/R_Neurohacking_Results_Part_01/DICOM_FLAIR_Slice_11_Grayscale.png" width="400" />
```
#transpose data using t(): faces "up" versus "right", grayscale
d11 <- dim(t(slice11$img[[1]])) 
image(1:d11[1], 1:d11[2], t(slice11$img[[1]]), col = gray(0:64/64), main = "DICOM FLAIR Slice 11 Grayscale")

#subset img matrix (rows 101-105, columns 121-125)
slice11$img[[1]][101:105, 121:125] <- matrix(c(
    4,   34,   36,   75,   222,
    9,   44,   33,   117,  248,
    19,  47,   54,   167,  274,
    27,  28,   98,   239,  286,
    12,  45,   170,  288,  307
), nrow = 5, byrow = TRUE)
```
### DICOM FLAIR Slice 11 Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/951f629a1bbc2550b4d2b12ea8a01228f2862280/R_Neurohacking_Results_Part_01/DICOM_FLAIR_Slice_11_Histogram.png" width="400" />
```
#create histogram in img
hist(slice11$img[[1]][,], 
     breaks = 50, 
     xlab = "FLAIR", 
     prob = TRUE, 
     col = rgb(0, 0, 1, 1/4), 
     main = "DICOM FLAIR Slice 11 Histogram")
```
### DICOM T1 Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_02/DICOM_T1_Slice_11.png" width="400" />

### DICOM T2 Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_03/DICOM_T2_Slice_11.png" width="400" />

### NIfTI nii T1 Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Grayscale.png" width="400" />

### NIfTI nii T1 Slice 11 Heat
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Heat.png" width="400" />

### NIfTI nii T1 Slice 11 Oro
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Oro.png" width="400" />

### NIfTI nii T1 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Orthographic.png" width="400" />

### NIfTI nii T1 Slice 11 Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_T1_Slice_11_Histogram.png" width="600" />

### NIfTI nii T2 Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Grayscale.png" width="400" />

### NIfTI nii T2 Slice 11 Heat
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Heat.png" width="400" />

### NIfTI nii T2 Slice 11 Oro
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Oro.png" width="400" />

### NIfTI nii T2 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Orthographic.png" width="400" />

### NIfTI nii T2 Slice 11 Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_T2_Slice_11_Histogram.png" width="600" />

### NIfTI nii T1 Slice 11 Oro Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_06/NIfTI_nii_T1_Slice_11_Oro_Overlay.png" width="400" />

### NIfTI nii T1 Slices 01-22 Oro Overlay Grid
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_06/NIfTI_nii_T1_Slices_01_22_Oro_Overlay_Grid.png" width="400" />

### NIfTI nii T2 Slice 11 Oro Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_07/NIfTI_nii_T2_Slice_11_Oro_Overlay.png" width="400" />

### NIfTI nii T2 Slices 01-22 Oro Overlay Grid
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_07/NIfTI_nii_T2_Slices_01_22_Oro_Overlay_Grid.png" width="400" />

### NIfTI nii T1 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_08/NIfTI_nii_T1_Slice_11_Orthographic.png" width="400" />

### NIfTI nii T1 Slice 11 Orthographic Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_08/NIfTI_nii_T1_Slice_11_Orthographic_Overlay.png" width="400" />

### NIfTI nii T2 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_09/NIfTI_nii_T2_Slice_11_Orthographic.png" width="400" />

### NIfTI nii T2 Slice 11 Orthographic Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_09/NIfTI_nii_T2_Slice_11_Orthographic_Overlay.png" width="400" />

## 🖼️ Images Kirby21 <br>

### Kirby21 T1 Orthographic Original
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_10/Kirby21_T1_Orthographic_Original.png" width="400" />

### Kirby21 T1 Orthographic Masked
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_10/Kirby21_T1_Orthographic_Masked.png" width="400" />

### Kirby21 T1 Orthographic Subtract
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_10/Kirby21_T1_Orthographic_Subtract.png" width="400" />
