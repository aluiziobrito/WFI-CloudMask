# 🌥️ Cloud Detection Model for WFI Sensors 🌥️ 

This repository contains a methodology for cloud detection using RGB-NIR images from the WFI (Wide Field Imager) camera onboard Brazilian satellites, including Amazonia-1, CBERS-4, and CBERS-4A. The model was developed with a focus on creating a simple, dynamic, and operationalizable cloud masking routine tailored for Brazilian satellite missions.

# 🌎 Overview
Cloud cover in optical remote sensing imagery poses a recurring challenge in data processing and analysis. This model addresses this challenge by providing an efficient preprocessing step to detect and mask clouds, specifically leveraging images from RGB-NIR bands.

# ✨ Key Features
- 🔁 Dynamic and Replicable: The model can be easily applied to other RGB-NIR datasets from WFI sensors.
- 🚀 High Performance: Achieves robust results, with minimal accuracy loss across different satellites and regions.
- 🛠️ Simplified Workflow: Designed for ease of use and operational applicability.
- 🌗 A novel indice that detects both clouds and shadows in images named NIR-SCD.

# 📊 Applications

 This methodology is particularly useful for:

- Preprocessing optical remote sensing data for cloud-free analyses.
- Supporting Brazilian remote sensing missions by providing a tailored cloud masking solution.
- Enhancing the usability of WFI sensor imagery for environmental monitoring and geospatial analysis.

# 🔧 How to Use
 - Clone the repository and ensure the required dependencies are installed.
- Follow the provided scripts to preprocess WFI images and apply the cloud detection model.
- Adjust parameters as needed for specific datasets or regions.
- 
# Results and Validation
The results validate the model's robustness across different satellites and study areas. While accuracy decreases slightly for some cases, the method remains reliable and operationally viable.

# 🫶 Collaboration is Welcome!
This is a project by a beginner enthusiast 🚶‍♂️ learning remote sensing and geospatial data processing. If you’re interested in improving the code or suggesting better practices, feel free to contribute or open issues! Your feedback is highly appreciated. 😊

# Citation
If you use this model or methodology in your research, please cite this work.

MAIA, Aluizio Brito et al.. A CLOUD DETECTION MODEL FOR MULTISPECTRAL SENSORS: APPLICATIONS TO WFI CAMERA ON AMAZONIA-1, CBERS-4 AND CBERS-4A SATELLITES... In: Anais do Simpósio Internacional Selper: Além do dossel – Tecnologias e Aplicações de Sensoriamento Remoto. Anais...Belém(PA) UFPA, 2024. Disponível em: https//www.even3.com.br/anais/xxi-selper-2024/869872-A-CLOUD-DETECTION-MODEL-FOR-MULTISPECTRAL-SENSORS--APPLICATIONS-TO-WFI-CAMERA-ON-AMAZONIA-1-CBERS-4-AND-CBERS-4A. 

## Installation 
To install all of the required packages, run in your R environment:

```R
# List of required packages
neededPackages = c("viridis", "terra", "raster", "stats", "sf", "ggplot2", "sp", "dplyr", "tidyr", "ROCR",
                   "reshape2", "randomForest", "caret", "caTools", "geobr", "prettymapr", 
                   "tidyselect", "rpart", "rpart.plot", "partykit")

# Function to check if the package is installed. If not, it will be installed and loaded.
pkgTest = function(x) {
  if (!x %in% rownames(installed.packages())) { 
    install.packages(x, dependencies = TRUE) 
  }
  library(x, character.only = TRUE)
}
for (package in neededPackages) {
  pkgTest(package)
}
