# Content-Aware Image Compression System

### DCT-Based Frequency Analysis and Edge-Preserving Adaptive Quantization

## Overview

Content-Aware Image Compression System is an image processing project designed to reduce image storage requirements while preserving important visual information and image quality.

The project implements Discrete Cosine Transform (DCT), Sobel Edge Detection, and Adaptive Quantization to analyze image frequency components and identify regions containing important visual details.

Unlike conventional image compression techniques that apply uniform compression across all image regions, this system uses an adaptive approach that adjusts compression strength according to the local complexity and edge density of different image blocks.

The system divides images into 8×8 pixel blocks, performs frequency-domain transformation, and classifies image regions into high-detail, medium-detail, and low-detail categories. More frequency coefficients are retained in detailed regions, while fewer coefficients are retained in smoother regions.

The project includes a Python-based interactive Streamlit dashboard and a MATLAB-based image compression and analysis implementation.

The primary goal is to demonstrate how frequency-domain image processing and adaptive quantization can improve the balance between compression efficiency and reconstructed image quality.

## Features

- **DCT-Based Compression:** Converts image information into frequency-domain coefficients using Discrete Cosine Transform.
- **8×8 Block Processing:** Divides images into smaller blocks for localized frequency analysis.
- **Sobel Edge Detection:** Identifies important edges and structural details within images.
- **Adaptive Quantization:** Dynamically adjusts the number of retained frequency coefficients according to image complexity.
- **Detail Classification:** Categorizes image blocks into high-detail, medium-detail, and low-detail regions.
- **Standard DCT Compression:** Implements conventional uniform frequency coefficient retention for comparison.
- **Adaptive DCT Compression:** Preserves more frequency information in visually important regions.
- **Inverse DCT Reconstruction:** Reconstructs compressed images from their retained frequency coefficients.
- **Compression Quality Control:** Allows users to adjust compression quality through interactive controls.
- **Performance Evaluation:** Measures image quality using MSE, PSNR, and SSIM.
- **Compression Comparison:** Compares Standard DCT and Adaptive DCT results.
- **Interactive Dashboard:** Provides image upload, visualization, compression analysis, and performance statistics.
- **MATLAB Visualization:** Provides a dedicated dashboard for frequency analysis, edge detection, image reconstruction, and performance comparison.

## System Architecture

The project follows a structured image processing and compression pipeline:

```text
             INPUT IMAGE
                  |
                  v
          IMAGE PREPROCESSING
                  |
                  v
          DIVIDE INTO 8x8 BLOCKS
                  |
                  v
          DISCRETE COSINE
             TRANSFORM
                  |
                  v
          FREQUENCY ANALYSIS
                  |
                  v
           SOBEL EDGE DETECTION
                  |
                  v
          EDGE DENSITY ANALYSIS
                  |
                  v
          ADAPTIVE CLASSIFICATION
                  |
          +-------+-------+
          |       |       |
          v       v       v
         HIGH   MEDIUM   LOW
        DETAIL  DETAIL  DETAIL
          |       |       |
          v       v       v
       MORE    MODERATE  FEWER
     COEFFICIENTS         COEFFICIENTS
          |       |       |
          +-------+-------+
                  |
                  v
          ADAPTIVE QUANTIZATION
                  |
                  v
             DEQUANTIZATION
                  |
                  v
              INVERSE DCT
                  |
                  v
          RECONSTRUCTED IMAGE
                  |
                  v
          QUALITY EVALUATION
                  |
                  v
          MSE | PSNR | SSIM
                  |
                  v
          PERFORMANCE DASHBOARD
```

## System Modules

### 1. Image Input and Preprocessing

The system accepts RGB images in common image formats, including:

- PNG
- JPG
- JPEG
- BMP
- TIFF

The uploaded image is converted into RGB format and prepared for block-based processing.

The image dimensions are adjusted to ensure compatibility with 8×8 block processing.

### 2. Discrete Cosine Transform (DCT)

DCT converts spatial image information into frequency-domain coefficients.

Each 8×8 image block is transformed into frequency components.

These components represent:

- Low-frequency information: General image structure and smooth variations.
- High-frequency information: Fine details, edges, and rapid intensity changes.

The frequency coefficients are used to determine which image information should be retained during compression.

### 3. Sobel Edge Detection

The system implements Sobel edge detection to identify important visual structures.

Horizontal and vertical edge information is calculated using Sobel operators.

The resulting edge strength map helps determine the amount of detail present in each 8×8 image block.

### 4. Adaptive Block Classification

Based on the calculated edge density, each image block is classified into three categories:

| Classification | Edge Density | Compression Strategy |
|---|---|---|
| High Detail | > 0.08 | Retains more frequency coefficients |
| Medium Detail | 0.03–0.08 | Retains a moderate number of coefficients |
| Low Detail | ≤ 0.03 | Retains fewer frequency coefficients |

This classification allows the system to allocate frequency information according to local image complexity.

### 5. Quantization

Quantization reduces the precision of frequency coefficients using a JPEG-like quantization matrix.

The system adjusts the quantization matrix according to the selected compression quality.

Adaptive quantization further determines how many frequency coefficients should be retained in each image block.

### 6. Standard DCT Compression

Standard DCT applies uniform compression across all image blocks.

The same frequency-retention strategy is applied regardless of the local image detail.

This implementation serves as a baseline for evaluating the adaptive compression technique.

### 7. Adaptive DCT Compression

Adaptive DCT applies different compression strengths according to the edge density of individual image blocks.

- High-detail regions preserve more frequency information.
- Medium-detail regions retain a moderate amount of information.
- Low-detail regions retain fewer frequency coefficients.

This approach aims to preserve important visual structures while reducing unnecessary frequency information.

### 8. Image Reconstruction

The compressed frequency coefficients are dequantized and processed using Inverse Discrete Cosine Transform (IDCT).

The reconstructed blocks are combined to produce the final compressed image.

### 9. Image Quality Evaluation

The system evaluates reconstructed image quality using three performance metrics:

| Metric | Purpose |
|---|---|
| MSE (Mean Squared Error) | Measures the average pixel-level reconstruction error. |
| PSNR (Peak Signal-to-Noise Ratio) | Measures reconstruction quality in decibels. |
| SSIM (Structural Similarity Index) | Evaluates structural similarity between original and reconstructed images. |

These metrics help evaluate the effectiveness of Standard DCT and Adaptive DCT compression.

## Dashboard Modules

The Python Streamlit dashboard provides the following sections:

| Module | Functionality |
|---|---|
| Image Upload | Uploads images for compression analysis. |
| Experiment Controls | Adjusts compression quality. |
| Image Information | Displays image name, resolution, format, and size. |
| Frequency Analysis | Processes image frequency components. |
| Edge Detection | Displays edge information and detail classification. |
| Standard DCT | Displays the conventionally compressed image. |
| Adaptive DCT | Displays the content-aware reconstructed image. |
| Performance Comparison | Compares compression metrics. |
| Adaptive Advantage | Displays improvements in compression and reconstruction quality. |
| Block Distribution | Displays high-detail, medium-detail, and low-detail block statistics. |

The MATLAB dashboard additionally provides visualizations of the original image, frequency spectrum, edge strength map, reconstructed images, and compression performance.

## Technology Stack

**Programming Languages**
- Python
- MATLAB

**Image Processing and Numerical Computing**
- NumPy
- Pillow
- MATLAB Image Processing Functions

**Algorithms**
- Discrete Cosine Transform (DCT)
- Inverse Discrete Cosine Transform (IDCT)
- Sobel Edge Detection
- Adaptive Quantization
- Frequency Domain Analysis

**Frontend and Visualization**
- Streamlit
- Matplotlib
- MATLAB App Designer UI Components
- HTML and CSS (Streamlit Dashboard Styling)

**Performance Evaluation**
- Mean Squared Error (MSE)
- Peak Signal-to-Noise Ratio (PSNR)
- Structural Similarity Index (SSIM)

## Project Structure

```text
Content-Aware-Image-Compression/
│
├── app(2).py
│
├── compressionDashboard.m
│
├── decompressAdaptiveImage.m
│
├── main.m
│
├── requirements.txt
│
├── README.md
│
└── MATLAB Project Dependencies/
    ├── src/
    │   ├── frequencyCompression.m
    │   ├── actualCompression.m
    │   ├── actualAdaptiveCompression.m
    │   ├── decompressImage.m
    │   └── other supporting functions
    │
    ├── test_images/
    │   └── peppers.png
    │
    └── results/
        └── Generated compression results
```

*Note: The MATLAB supporting files shown above are dependencies referenced by the supplied MATLAB scripts. Include their actual implementations in the repository if you want the MATLAB workflow to run independently.*

## Installation and Setup

### 1. Clone the Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

### 2. Navigate to the Project Directory

```bash
cd Content-Aware-Image-Compression
```

### 3. Create a Virtual Environment

```bash
python -m venv venv
```

### 4. Activate the Virtual Environment

For Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

If script execution is blocked:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Activate the environment again:

```powershell
.\venv\Scripts\Activate.ps1
```

### 5. Install Dependencies

```bash
pip install -r requirements.txt
```

## How to Run the Project

### Python Streamlit Implementation

**Step 1: Open the project directory**

Open the project folder in VS Code or your preferred Python IDE.

**Step 2: Activate the virtual environment**

```powershell
.\venv\Scripts\Activate.ps1
```

**Step 3: Install the required packages**

```bash
pip install -r requirements.txt
```

**Step 4: Launch the Streamlit Application**

```bash
streamlit run app(2).py
```

**Step 5: Open the Dashboard**

Open the browser at the local address displayed in the terminal.

```text
http://localhost:8501
```

**Step 6: Upload an Image**

1. Upload an RGB image.
2. Adjust the compression quality using the sidebar.
3. Allow the system to perform frequency and edge analysis.
4. View the Standard DCT reconstruction.
5. View the Adaptive DCT reconstruction.
6. Compare compression performance and image quality metrics.

### MATLAB Implementation

**Step 1:** Open the project folder in MATLAB.

**Step 2:** Ensure the supporting source functions and test image are available.

**Step 3:** Execute the main script:

```matlab
main
```

**Step 4:** To launch the MATLAB comparison dashboard, execute:

```matlab
compressionDashboard
```

The MATLAB implementation performs compression, image reconstruction, frequency analysis, and performance comparison.

## Performance Comparison

The project evaluates two compression approaches:

| Parameter | Standard DCT | Adaptive DCT |
|---|---|---|
| Compression Strategy | Uniform | Content-aware |
| Block Processing | 8×8 | 8×8 |
| Edge Detection | Not used for allocation | Sobel-based |
| Frequency Retention | Uniform | Variable |
| Quantization | Standard | Adaptive |
| Image Reconstruction | Inverse DCT | Inverse DCT |
| Quality Evaluation | MSE, PSNR, SSIM | MSE, PSNR, SSIM |

The comparison helps determine how adaptive frequency retention affects storage efficiency and reconstructed image quality.

## Project Objective

The objective of this project is to develop a content-aware image compression technique that improves compression efficiency while preserving visually important image details.

By combining Discrete Cosine Transform, Sobel Edge Detection, and Adaptive Quantization, the system analyzes image complexity and dynamically allocates frequency information to different image regions.

The project demonstrates the application of Digital Signal Processing, frequency-domain analysis, and image processing techniques through Python and MATLAB implementations.

## Future Enhancements

- Implementation of actual encoded binary compression formats.
- Support for additional image formats.
- Optimization of adaptive quantization thresholds.
- Advanced edge detection algorithms.
- Integration of alternative compression algorithms.
- Improved compression performance for high-resolution images.
- Real-time image compression and reconstruction.
- Further optimization of storage efficiency and reconstruction quality.

## Important Note

This project is an academic implementation of DCT-based image compression and adaptive frequency coefficient retention.

The Python dashboard estimates compressed representation size based on retained frequency coefficients. These estimated values should not be interpreted as the size of an actual encoded image file.

The MATLAB implementation includes a separate compression and decompression workflow using stored compressed representations.

## Author

**Abhi Raksha**

B.Tech – Electronics and Computer Science  
Specialization: Artificial Intelligence and Machine Learning

LinkedIn: https://www.linkedin.com/in/abhi-raksha-9b3b80369/
