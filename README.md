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

```
#plot NIfT1 slice 11
image(1:d[1], 1:d[2], nii_T1[,,11],
  col = gray(0:64/64),
  xlab = "",
  ylab= "",
  main = "DICOM T1 Slice 11 Grayscale")
```
### DICOM T2 Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_03/DICOM_T2_Slice_11.png" width="400" />

```
#plot NIfT2 slice 11
image(1:d[1], 1:d[2], nii_T2[,,11],
  col = gray(0:64/64),
  xlab = "",
  ylab= "",
  main = "DICOM T2 Slice 11 Grayscale")
```
### NIfTI nii T1 Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Grayscale.png" width="400" />

```
#read without reorientation
nii_T1 <- readNIfTI(fname, reorient = FALSE)

#slice using custom x and y axes, grayscale, for slice 11
png("NIfTI_nii_T1_Slice_11_Grayscale.png", width = 800, height = 800)
image(1:d[1], 1:d[2], nii_T1[,,11], xlab = "", ylab = "", col = gray(0:64/64), main = "NIfTI nii T1 Slice 11 Grayscale")
dev.off()
```
### NIfTI nii T1 Slice 11 Heat
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Heat.png" width="400" />

```
#read without reorientation
nii_T1 <- readNIfTI(fname, reorient = FALSE)

#slice using custom x and y axes, default colors of heat color orange, for slice 11
png("NIfTI_nii_T1_Slice_11_Heat.png", width = 800, height = 800)
image(1:d[1], 1:d[2], nii_T1[,,11], xlab = "", ylab = "", col = heat.colors(12), main = "NIfTI nii T1 Slice 11 Heat")
dev.off()
```
### NIfTI nii T1 Slice 11 Oro
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Oro.png" width="400" />

```
#read without reorientation
nii_T1 <- readNIfTI(fname, reorient = FALSE)

#slice using oro.nifti package for slice 11
png("NIfTI_nii_T1_Slice_11_Oro.png", width = 800, height = 800)
image(nii_T1, z=11,plot.type="single")
dev.off()
```
### NIfTI nii T1 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_nii_T1_Slice_11_Orthographic.png" width="400" />

```
#read without reorientation
nii_T1 <- readNIfTI(fname, reorient = FALSE)

#slice orthographic all planes of coronal, sagittal, and axial for slice 11, text
png("NIfTI_nii_T1_Slice_11_Orthographic.png", width = 800, height = 800)
orthographic(nii_T1, xyz = c(200, 220, 11))  
mtext("NIfTI nii T1 Slice 11 Orthographic", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T1 Slice 11 Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_T1_Slice_11_Histogram.png" width="700" />

```
#plot area
par(mfrow=c(1,2))
o<-par(mar=c(4,4,4,2))

#slice selection for slice 11
slice_data_11 <- nii_T1[,,11]

#histogram with density and intensities for all in slice 11
hist(slice_data_11, breaks = 75, prob = TRUE, xlab = "T1 Intensities", col = rgb(0,0,1,0.5), main = "NIfTI nii T1 Slice 11 Histogram", cex.main = 1)

#histogram with density and intensities for < 20 in slice 11
hist(slice_data_11[slice_data_11 > 20], breaks = 75, prob = TRUE, xlab = "T1 Intensities > 20", col = rgb(0,0,1,0.5), main = "NIfTI nii T1 Slice 11 Histogram (>20)", cex.main = 1)

dev.off()
```
### NIfTI nii T2 Slice 11 Grayscale
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Grayscale.png" width="400" />

```
#read without reorientation
nii_T2 <- readNIfTI(fname, reorient = FALSE)

#slice using custom x and y axes, grayscale, for slice 11
png("NIfTI_nii_T2_Slice_11_Grayscale.png", width = 800, height = 800)
image(1:d[1], 1:d[2], nii_T2[,,11], xlab = "", ylab = "", col = gray(0:64/64), main = "NIfTI nii T2 Slice 11 Grayscale")
dev.off()
```
### NIfTI nii T2 Slice 11 Heat
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Heat.png" width="400" />

```
#read without reorientation
nii_T2 <- readNIfTI(fname, reorient = FALSE)

#slice using custom x and y axes, default colors of heat color orange, for slice 11
png("NIfTI_nii_T2_Slice_11_Heat.png", width = 800, height = 800)
image(1:d[1], 1:d[2], nii_T2[,,11], xlab = "", ylab = "", col = heat.colors(12), main = "NIfTI nii T2 Slice 11 Heat")
dev.off()
```
### NIfTI nii T2 Slice 11 Oro
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Oro.png" width="400" />

```
#read without reorientation
nii_T2 <- readNIfTI(fname, reorient = FALSE)

#slice using oro.nifti package for slice 11
png("NIfTI_nii_T2_Slice_11_Oro.png", width = 800, height = 800)
image(nii_T2, z=11,plot.type="single")
dev.off()
```
### NIfTI nii T2 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_nii_T2_Slice_11_Orthographic.png" width="400" />

```
#read without reorientation
nii_T2 <- readNIfTI(fname, reorient = FALSE)

#slice orthographic all planes of coronal, sagittal, and axial for slice 11, text
png("NIfTI_nii_T2_Slice_11_Orthographic.png", width = 800, height = 800)
orthographic(nii_T2, xyz = c(200, 220, 11))  
mtext("NIfTI nii T2 Slice 11 Orthographic", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T2 Slice 11 Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_T2_Slice_11_Histogram.png" width="700" />

```
#read without reorientation
nii_T2 <- readNIfTI(fname, reorient = FALSE)

#plot area
par(mfrow=c(1,2))
o<-par(mar=c(4,4,4,2))

#slice selection for slice 11
slice_data_11 <- nii_T2[,,11]

#histogram with density and intensities for all in slice 11
hist(slice_data_11, breaks = 75, prob = TRUE, xlab = "T2 Intensities", col = rgb(0,0,1,0.5), main = "NIfTI nii T2 Slice 11 Histogram", cex.main = 1)

#histogram with density and intensities for < 20 in slice 11
hist(slice_data_11[slice_data_11 > 20], breaks = 75, prob = TRUE, xlab = "T2 Intensities > 20", col = rgb(0,0,1,0.5), main = "NIfTI nii T2 Slice 11 Histogram (>20)", cex.main = 1)

dev.off()
```
### NIfTI nii T1 Slice 11 Oro Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_06/NIfTI_nii_T1_Slice_11_Oro_Overlay.png" width="400" />

```
#define value between 300 and 400
is_btw_300_400 <- (nii_T1 >= 300) & (nii_T1 <= 400)

#mask
nii_T1_mask <- nii_T1

#set value range to NA
nii_T1_mask[!is_btw_300_400] <- NA

#extract the 3D data array
mask_array <- nii_T1_mask[]

#slice 11
arr_11 <- array(NA, dim = dim(as.array(nii_T1_mask)))
arr_11[,,11] <- as.array(nii_T1_mask)[,,11]

nii_T1_mask_11 <- nii_T1_mask
nii_T1_mask_11@.Data <- arr_11

png("NIfTI_nii_T1_Slice_11_Oro_Overlay.png", width = 800, height = 800)
overlay(nii_T1, nii_T1_mask_11, z = 11, plot.type = "single")
mtext("NIfTI nii T1 Slice 11 Oro Overlay", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T1 Slices 01-22 Oro Overlay Grid
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_06/NIfTI_nii_T1_Slices_01_22_Oro_Overlay_Grid.png" width="400" />

```
#slices 01-22
arr_all <- array(NA, dim = dim(as.array(nii_T1_mask)))
arr_all[,,1:22] <- as.array(nii_T1_mask)[,,1:22]

nii_T1_mask_all <- nii_T1_mask
nii_T1_mask_all@.Data <- arr_all

png("NIfTI_nii_T1_Slices_01_22_Oro_Overlay_Grid.png", width = 800, height = 800)
overlay(nii_T1, nii_T1_mask_all, z = 1:22, plot.type = "single")
mtext("NIfTI nii T1 Slices 01-22 Oro Overlay Grid", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T2 Slice 11 Oro Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_07/NIfTI_nii_T2_Slice_11_Oro_Overlay.png" width="400" />

```
#define value between 300 and 400
is_btw_300_400 <- (nii_T2 >= 300) & (nii_T2 <= 400)

#mask
nii_T2_mask <- nii_T2

#set value range to NA
nii_T2_mask[!is_btw_300_400] <- NA

#extract the 3D data array
mask_array <- nii_T2_mask[]

#slice 11
arr_11 <- array(NA, dim = dim(as.array(nii_T2_mask)))
arr_11[,,11] <- as.array(nii_T2_mask)[,,11]

nii_T2_mask_11 <- nii_T2_mask
nii_T2_mask_11@.Data <- arr_11

png("NIfTI_nii_T2_Slice_11_Oro_Overlay.png", width = 800, height = 800)
overlay(nii_T2, nii_T2_mask_11, z = 11, plot.type = "single")
mtext("NIfTI nii T2 Slice 11 Oro Overlay", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T2 Slices 01-22 Oro Overlay Grid
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_07/NIfTI_nii_T2_Slices_01_22_Oro_Overlay_Grid.png" width="400" />

```
#slices 01-22
arr_all <- array(NA, dim = dim(as.array(nii_T2_mask)))
arr_all[,,1:22] <- as.array(nii_T2_mask)[,,1:22]

nii_T2_mask_all <- nii_T2_mask
nii_T2_mask_all@.Data <- arr_all

png("NIfTI_nii_T2_Slices_01_22_Oro_Overlay_Grid.png", width = 800, height = 800)
overlay(nii_T2, nii_T2_mask_all, z = 1:22, plot.type = "single")
mtext("NIfTI nii T2 Slices 01-22 Oro Overlay Grid", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T1 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_08/NIfTI_nii_T1_Slice_11_Orthographic.png" width="400" />

```
#read without reorientation
nii_T1 <- readNIfTI(fname, reorient = FALSE)

#slice orthographic all planes of coronal, sagittal, and axial for slice 11, text
png("NIfTI_nii_T1_Slice_11_Orthographic.png", width = 800, height = 800)
orthographic(nii_T1, xyz = c(200, 220, 11))  
mtext("NIfTI nii T1 Slice 11 Orthographic", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T1 Slice 11 Orthographic Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_08/NIfTI_nii_T1_Slice_11_Orthographic_Overlay.png" width="400" />

```
#define value between 300 and 400
is_btw_300_400 <- (nii_T1 >= 300) & (nii_T1 <= 400)

#mask
nii_T1_mask <- nii_T1

#set value range to NA
nii_T1_mask[!is_btw_300_400] <- NA

#extract the 3D data array
mask_array <- nii_T1_mask[]

#mask for slice 11
mask_11_array <- array(NA, dim = dim(mask_array))
mask_11_array[,,11] <- mask_array[,,11]

#overlay for slice 11
overlay(nii_T1, nii_T1_mask, z = 11, plot.type = "single")

#overlay orthographic all planes of coronal, sagittal, and axial for slice 11
orthographic(nii_T1, nii_T1_mask, xyz = c(200, 220, 11))  
mtext("NIfTI nii T1 Slice 11 Orthographic Overlay", side = 1, line = 1, adj = 1, cex = 1, col = "white")
```
### NIfTI nii T2 Slice 11 Orthographic
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_09/NIfTI_nii_T2_Slice_11_Orthographic.png" width="400" />

```
#read without reorientation
nii_T2 <- readNIfTI(fname, reorient = FALSE)

#slice orthographic all planes of coronal, sagittal, and axial for slice 11
png("NIfTI_nii_T2_Slice_11_Orthographic.png", width = 800, height = 800)
orthographic(nii_T2, xyz = c(200, 220, 11))  
mtext("NIfTI nii T2 Slice 11 Orthographic", side = 1, line = 1, adj = 1, cex = 1, col = "white")
dev.off()
```
### NIfTI nii T2 Slice 11 Orthographic Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_09/NIfTI_nii_T2_Slice_11_Orthographic_Overlay.png" width="400" />

```
#define value between 300 and 400
is_btw_300_400 <- (nii_T2 >= 300) & (nii_T2 <= 400)

#mask
nii_T2_mask <- nii_T2

#set value range to NA
nii_T2_mask[!is_btw_300_400] <- NA

#extract the 3D data array
mask_array <- nii_T2_mask[]

#mask for slice 11
mask_11_array <- array(NA, dim = dim(mask_array))
mask_11_array[,,11] <- mask_array[,,11]

#overlay for slice 11
overlay(nii_T2, nii_T2_mask, z = 11, plot.type = "single")

#overlay orthographic all planes of coronal, sagittal, and axial for slice 11
orthographic(nii_T2, nii_T2_mask, xyz = c(200, 220, 11))  
mtext("NIfTI nii T2 Slice 11 Orthographic Overlay", side = 1, line = 1, adj = 1, cex = 1, col = "white")
```
## 🖼️ Images Kirby21 <br>

### Kirby21 T1 Orthographic Original
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_10/Kirby21_T1_Orthographic_Original.png" width="400" />

```
#view the orthographic
orthographic(T1)
```
### Kirby21 T1 Orthographic Masked
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_10/Kirby21_T1_Orthographic_Masked.png" width="400" />

```
#view the binary mask
orthographic(mask)

#apply the mask to the original image
masked.T1 <- T1 * mask
orthographic(masked.T1)
```
### Kirby21 T1 Orthographic Subtract
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/702a98af6c51c1e48e7630f06a645b45a2dc1c18/R_Neurohacking_Results_Part_10/Kirby21_T1_Orthographic_Subtract.png" width="400" />

```
#subtract baseline
subtract.T1 <- T1.follow - T1

#calculate the min and max
min(subtract.T1)
max(subtract.T1)

#view the binary mask difference
orthographic(subtract.T1)
```
