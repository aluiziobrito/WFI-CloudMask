Cloud cover is one of the primary challenges in acquiring remote sensing imagery. Several methods have been developed to create cloud and shadow masks. The method proposed in this study aims to generate cloud and shadow masks specifically tailored for flood events, focusing on a straightforward processing approach that balances cloud and shadow detection while minimizing false positives, particularly those caused by surface water.

Define, in a preliminary study, the selected attributes for creating your cloud and shadow mask. It is recommended to individually threshold the attributes to analyze their separability and respective potential. Additionally, the use of the Boruta algorithm is suggested to evaluate the importance of each attribute in a more robust manner.

Below is an example of how the Boruta package can be used in R to assess attribute importance:

```R
# Install and load the Boruta package
if (!require("Boruta")) install.packages("Boruta")
library(Boruta)

# Example dataset: Assume `data` is your dataframe with attributes and `target` is your images
# Replace 'attribute1', 'attribute2', ..., 'attributeN' with your actual spectral attributes
set.seed(1)  
boruta_result <- Boruta(target ~ ., data = data, doTrace = 2)

# Print the importance of attributes
print(boruta_result)

# Plot the results for better visualization
plot(boruta_result, main = "Boruta Attribute Importance")
final_boruta <- TentativeRoughFix(boruta_result)
important_attributes <- getSelectedAttributes(final_boruta, withTentative = FALSE)

# Print the selected attributes
cat("Important attributes identified by Boruta:\n", important_attributes, "\n")
```

The attributes were generated in a GIS environment. It is important to mention that bands with differing nominal spatial resolutions must be resampled to ensure consistency in analysis. A simple example of a resampling process can be performed using the following code in R

```r
target_resolution <- 60  # Resolution
B9 <- resample(B4, B1, method="bilinear")

```

As an alternative to the generation of the attribute by a GIS software, the script below calculates each of the attributes.

```r

# Loading the bands that will be used, in the example, the MUX/CBERS-4A bands.

B05 <- rast("path-B5.tif")
B06 <- rast("path-B6.tif")
B07 <- rast("path-B7.tif")
B08 <- rast("path-B8.tif")

# Calculating the spectral attributes. 

HOT <- B05 - (0.45 * B07) - 0.08
M <- (0.25 * B05) + (0.375 * B06) + (0.375 * B07)
WI <- ( (B05 - M) / M ) + ( (B06 - M) / M ) + ( (B07 - M) / M )
Cloud Index  <- (3 * B08) / (B05 + B06 + B07)
NIR-SCD <- B05− (0,45 * B07) − (0,16 * B08)
NDWI <- B07 - B08 / B07 + B08

# Saving the results 
writeRaster(HOT, "HOT.tif", overwrite=TRUE)
writeRaster(M, "M.tif", overwrite=TRUE)
writeRaster(WI, "WI.tif", overwrite=TRUE)
writeRaster(Cloud_Index_Alternativo, "Cloud_Index_Alternativo.tif", overwrite=TRUE)
writeRaster(NIR_SCD, "NIR_SCD.tif", overwrite=TRUE)
writeRaster(NDWI, "NDWI.tif", overwrite=TRUE)

```



# Important Bibliography
GÓMEZ-CHOVA, L. et al. Cloud-screening algorithm for envisat/meris multispectral images. IEEE Transactions on Geoscience and Remote Sensing, v. 45, n. 12, p. 4105–4118, 2007. 8

ZHAI, H.; ZHANG, H.; ZHANG, L.; LI, P. Cloud/shadow detection based on spectral indices for multi/hyperspectral optical remote sensing imagery. ISPRS Journal of Photogrammetry and Remote Sensing, v. 144, p. 235–253, 2018.

ZHANG, Y.; HANG, Y.; GUINDON, B.; CIHLAR, J. An image transform to characterize and compensate for spatial variations in thin cloud contamination of landsat images. Remote Sensing of Environment, v. 82, n. 2-3, p. 173–187, 2002. 7, 8, 21




