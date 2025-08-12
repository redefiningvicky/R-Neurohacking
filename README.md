# 🔬 R Neurohacking Part 1
## 🎯 Objective <br>
This project uses the R programming language and its neuroimaging packages to manipulate, process, and analyze structural brain MRI data in the NIfTI (Neuroimaging Informatics Technology Initiative) format. It focuses on performing inhomogeneity correction, brain extraction, image registration, and visualization to enable comprehensive exploration of neuroimaging data. <p>
## 🛠️ Tools <br>
• <b>Language:</b> R <p>
## 🖼️ Images Brainix DICOM FLAIR <br>
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
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/951f629a1bbc2550b4d2b12ea8a01228f2862280/R_Neurohacking_Results_Part_01/DICOM_FLAIR_Slice_11_Histogram.png" width="375" />

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
## 🖼️ Images Brainix NIfTI nii <br>
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
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_04/NIfTI_T1_Slice_11_Histogram.png" width="750" />

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
<img src="https://github.com/redefiningvicky/R-Neurohacking/blob/86908aca3a9cbb611c04c1fc4e4c7191795ae103/R_Neurohacking_Results_Part_05/NIfTI_T2_Slice_11_Histogram.png" width="750" />

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
## 🖼️ Images Brainix NIfTI nii <br>
### NIfTI nii T1 Log-Scale Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/355e40279b3d93a0ccb5c99be26608424ccf9467/R_Neurohacking_Results_Part_11/NIfTI_nii_T1_Log_Scale_Histogram.png" width="600" />

```
T1_numeric <- as.numeric(T1_img)

x <- T1_numeric[is.finite(T1_numeric)]

print(length(x))
print(head(x))

if (length(unique(x)) < 2) x <- jitter(x)

im_hist <- hist(x, breaks = 20, plot = FALSE)
counts_log <- ifelse(im_hist$counts > 0, im_hist$counts, NA)

par(mar = c(5, 4, 4, 4) + 0.3)
col1 <- rgb(0, 0, 1, 0.5)
plot(im_hist$mids, counts_log, log = "y", type = "h", lwd = 10, lend = 2,
     col = col1, xlab = "Intensity Values", ylab = "Count (Log Scale)",
     main = "NIfTI nii T1 Log-Scale Histogram")

dev.off()
```
### NIfTI nii T1 Log-Scale Histogram with Linear Transfer Function
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/355e40279b3d93a0ccb5c99be26608424ccf9467/R_Neurohacking_Results_Part_11/NIfTI_nii_T1_Log_Scale_Histogram_Linear_Transfer_Function.png" width="600" />

```
#create base plot
plot(im_hist$mids, counts_log, log = "y", type = "h", lwd = 10, lend = 2,
     col = col1, xlab = "Intensity Values", ylab = "Count (Log Scale)",
     main = "NIfTI nii T1 Log-Scale Histogram with Linear Transfer Function")

#scaling factor
l <- 1

#add the curve on the same plot
curve(x * l, from = min(im_hist$mids), to = max(im_hist$mids),
      col = "red", lwd = 3, add = TRUE)

#add secondary axis on right side to show original intensity scale
ticks <- pretty(im_hist$mids)
max_val <- max(x)
ticks_norm <- ticks / max_val

axis(side = 4, at = ticks_norm, labels = ticks)

#add label for right axis
mtext("Original Intensity", side = 4, line = 2)

dev.off()
```
### Log-Scale Histogram with Spline Transfer Function
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/355e40279b3d93a0ccb5c99be26608424ccf9467/R_Neurohacking_Results_Part_11/NIfTI_nii_T1_Log_Scale_Histogram_Spline_Transfer_Function.png" width="600" />

```
#correct variable names
knots.vals <- c(0.3, 0.6)
slp.vals <- c(1, 0.5, 0.25)

#x as numeric intensity vector, im_hist as histogram object
max_x <- max(x)

#plot a base plot
plot(im_hist$mids, counts_log, log = "y", type = "h", lwd = 10, lend = 2,
     col = rgb(0,0,1,0.5), xlab = "Intensity Values", ylab = "Count (Log Scale)",
     main = "NIfTI nii T1 Log-Scale Histogram with Spline Transfer Function")

#overlay the spline transfer function curve
curve(lin.sp(x, knots.vals * max_x, slp.vals),
      from = min(im_hist$mids), to = max(im_hist$mids),
      axes = FALSE, xlab = "", ylab = "", col = 2, lwd = 3, add = TRUE)

#add secondary axis on the right side
ticks <- pretty(im_hist$mids)
ticks_norm <- ticks / max_x
axis(side = 4, at = ticks_norm, labels = ticks)
mtext("Transformed Intensity", side = 4, line = 2)

#apply spline transfer to numeric data x
trans_T1 <- lin.sp(x, knots.vals * max_x, slp.vals)
```

### NIfTI nii T1 Slice 11 Original
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/355e40279b3d93a0ccb5c99be26608424ccf9467/R_Neurohacking_Results_Part_11/NIfTI_nii_T1_Slice_11_Original.png" width="400" />

### NIfTI nii T1 Slice 11 Smoothed
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/355e40279b3d93a0ccb5c99be26608424ccf9467/R_Neurohacking_Results_Part_11/NIfTI_nii_T1_Slice_11_Smoothed.png" width="400" />

```
#smooth image with Gaussian smoother (~1 minute)
smooth.T1 <- GaussSmoothArray(T1_img@.Data, voxdim = c(1,1,1),
                             ksize = 11, sigma = diag(3,3),
                             mask = NULL, var.norm = FALSE)

#convert back to nifti object
smooth_nifti <- nifti(smooth.T1)

#visualize smoothed volume
orthographic(smooth_nifti)

num_slices <- dim(T1_img@.Data)[3]

for(slice_index in 1:num_slices) {
  #extract original slice from raw image
  original_slice <- T1_img@.Data[, , slice_index]
  
  #extract corresponding slice from smoothed data
  smoothed_slice <- smooth_nifti@.Data[, , slice_index]
```
### NIfTI nii T1 Slice 11 Transformed
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/355e40279b3d93a0ccb5c99be26608424ccf9467/R_Neurohacking_Results_Part_11/NIfTI_nii_T1_Slice_11_Transformed.png" width="400" />

```
#calculate start and end indices for transformed slice vector
  slice_size <- nrow(original_slice) * ncol(original_slice)
  start_idx <- (slice_index - 1) * slice_size + 1
  end_idx <- slice_index * slice_size
  #extract transformed slice and reshape to matrix
  transformed_slice <- matrix(trans_T1[start_idx:end_idx],
                              nrow = nrow(original_slice),
                              ncol = ncol(original_slice))
```
### NIfTI nii T2 Log-Scale Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/9a36451e89327cfd0ad3daa0e51584349552c16b/R_Neurohacking_Results_Part_12/NIfTI_nii_T2_Log_Scale_Histogram.png" width="600" />

```
T2_numeric <- as.numeric(T2_img)

x <- T2_numeric[is.finite(T2_numeric)]

print(length(x))
print(head(x))

if (length(unique(x)) < 2) x <- jitter(x)

im_hist <- hist(x, breaks = 20, plot = FALSE)
counts_log <- ifelse(im_hist$counts > 0, im_hist$counts, NA)

par(mar = c(5, 4, 4, 4) + 0.3)
col1 <- rgb(0, 0, 1, 0.5)
plot(im_hist$mids, counts_log, log = "y", type = "h", lwd = 10, lend = 2,
     col = col1, xlab = "Intensity Values", ylab = "Count (Log Scale)",
     main = "NIfTI nii T2 Log-Scale Histogram")

dev.off()
```
### NIfTI nii T2 Log-Scale Histogram with Linear Transfer Function
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/9a36451e89327cfd0ad3daa0e51584349552c16b/R_Neurohacking_Results_Part_12/NIfTI_nii_T2_Log_Scale_Histogram_Linear_Transfer_Function.png" width="600" />

```
#create base plot
plot(im_hist$mids, counts_log, log = "y", type = "h", lwd = 10, lend = 2,
     col = col1, xlab = "Intensity Values", ylab = "Count (Log Scale)",
     main = "NIfTI nii T2 Log-Scale Histogram with Linear Transfer Function")

#scaling factor
l <- 1

#add the curve on the same plot
curve(x * l, from = min(im_hist$mids), to = max(im_hist$mids),
      col = "red", lwd = 3, add = TRUE)

#add secondary axis on right side to show original intensity scale
ticks <- pretty(im_hist$mids)
max_val <- max(x)
ticks_norm <- ticks / max_val

axis(side = 4, at = ticks_norm, labels = ticks)

#add label for right axis
mtext("Original Intensity", side = 4, line = 2)

dev.off()
```
### NIfTI nii T2 Log-Scale Histogram with Spline Transfer Function
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/9a36451e89327cfd0ad3daa0e51584349552c16b/R_Neurohacking_Results_Part_12/NIfTI_nii_T2_Log_Scale_Histogram_Spline_Transfer_Function.png" width="600" />

```
#correct variable names
knots.vals <- c(0.3, 0.6)
slp.vals <- c(1, 0.5, 0.25)

#x as numeric intensity vector, im_hist as histogram object
max_x <- max(x)

#plot a base plot
plot(im_hist$mids, counts_log, log = "y", type = "h", lwd = 10, lend = 2,
     col = rgb(0,0,1,0.5), xlab = "Intensity Values", ylab = "Count (Log Scale)",
     main = "NIfTI nii T2 Log-Scale Histogram with Spline Transfer Function")

#overlay the spline transfer function curve
curve(lin.sp(x, knots.vals * max_x, slp.vals),
      from = min(im_hist$mids), to = max(im_hist$mids),
      axes = FALSE, xlab = "", ylab = "", col = 2, lwd = 3, add = TRUE)

#add secondary axis on the right side
ticks <- pretty(im_hist$mids)
ticks_norm <- ticks / max_x
axis(side = 4, at = ticks_norm, labels = ticks)
mtext("Transformed Intensity", side = 4, line = 2)

#apply spline transfer to numeric data x
trans_T2 <- lin.sp(x, knots.vals * max_x, slp.vals)
```

### NIfTI nii T2 Slice 12 Original
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/9a36451e89327cfd0ad3daa0e51584349552c16b/R_Neurohacking_Results_Part_12/NIfTI_nii_T2_Slice_11_Original.png" width="400" />

### NIfTI nii T2 Slice 12 Smoothed
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/9a36451e89327cfd0ad3daa0e51584349552c16b/R_Neurohacking_Results_Part_12/NIfTI_nii_T2_Slice_11_Smoothed.png" width="400" />

```
#smooth image with Gaussian smoother (~1 minute)
smooth.T2 <- GaussSmoothArray(T2_img@.Data, voxdim = c(1,1,1),
                             ksize = 11, sigma = diag(3,3),
                             mask = NULL, var.norm = FALSE)

#convert back to nifti object
smooth_nifti <- nifti(smooth.T2)

#visualize smoothed volume
orthographic(smooth_nifti)

num_slices <- dim(T2_img@.Data)[3]

for(slice_index in 1:num_slices) {
  #extract original slice from raw image
  original_slice <- T2_img@.Data[, , slice_index]
  
  #extract corresponding slice from smoothed data
  smoothed_slice <- smooth_nifti@.Data[, , slice_index]
```
### NIfTI nii T2 Slice 12 Transformed
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-1/blob/9a36451e89327cfd0ad3daa0e51584349552c16b/R_Neurohacking_Results_Part_12/NIfTI_nii_T2_Slice_11_Transformed.png" width="400" />

```
#calculate start and end indices for transformed slice vector
  slice_size <- nrow(original_slice) * ncol(original_slice)
  start_idx <- (slice_index - 1) * slice_size + 1
  end_idx <- slice_index * slice_size
  #extract transformed slice and reshape to matrix
  transformed_slice <- matrix(trans_T2[start_idx:end_idx],
                              nrow = nrow(original_slice),
                              ncol = ncol(original_slice))
