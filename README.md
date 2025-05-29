# OCR Text Detection

A comprehensive comparison of three popular OCR (Optical Character Recognition) tools to evaluate their text extraction performance on various image types.

## Overview

This project compares the accuracy and performance of three different OCR engines:
- **Tesseract OCR** (pytesseract)
- **EasyOCR**
- **AWS Textract**

The comparison is performed using Jaccard similarity coefficient to measure how well each OCR tool extracts text from images compared to ground truth labels.

## Features

- **Multi-OCR Support**: Implements three different OCR engines for comprehensive comparison
- **Performance Evaluation**: Uses Jaccard similarity for quantitative assessment
- **Batch Processing**: Processes multiple images from a dataset
- **Google Colab Integration**: Designed to work seamlessly with Google Colab environment

## Prerequisites

### System Requirements
- Python 3.7+
- Google Colab (recommended) or local Python environment
- Internet connection for AWS Textract

### Dependencies

```bash
# System packages (for Ubuntu/Debian)
apt install tesseract-ocr
apt install libtesseract-dev

# Python packages
pip install pytesseract
pip install Pillow
pip install easyocr
pip install boto3
```

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/WafaaFadlelmula/text-detection.git
   cd text-detection
   ```

2. **Install dependencies:**
   ```bash
   # Install system packages
   !apt install tesseract-ocr libtesseract-dev
   
   # Install Python packages
   !pip install pytesseract Pillow easyocr boto3
   ```

3. **Set up AWS credentials** (for Textract):
   - Create an AWS account and get access keys
   - Update the credentials in the code:
   ```python
   access_key = 'your_aws_access_key'
   secret_access_key = 'your_secret_key'
   region_name = 'your_region'  # e.g., 'us-east-1'
   ```

## Usage

### Basic Usage

1. **Prepare your dataset:**
   - Place images in the `txt_data` folder
   - Ensure image filenames reflect their content (used as ground truth)

2. **Run individual OCR functions:**

   ```python
   # Tesseract OCR
   text = read_text_tesseract('path/to/image.jpg')
   
   # EasyOCR
   text = read_text_easyocr('path/to/image.jpg')
   
   # AWS Textract
   text = read_text_textract('path/to/image.jpg')
   ```

3. **Run performance comparison:**
   ```python
   # The script will automatically process all images and calculate scores
   python text_detection.py
   ```

### Google Colab Usage

1. **Mount Google Drive:**
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

2. **Copy dataset:**
   ```python
   !cp -r "/content/drive/My Drive/txt_data" "/content/"
   ```

3. **Run the comparison script**

## Dataset Structure

```
txt_data/
├── journal.jpg
├── car.jpg
├── phone.jpg
├── paper.jpg
└── ... (other images)
```

**Note**: Image filenames should reflect their content as they're used as ground truth for comparison.

## Functions

### `read_text_tesseract(image_path)`
Extracts text using Google's Tesseract OCR engine.

**Parameters:**
- `image_path`: Path to the input image

**Returns:**
- Extracted text as string

### `read_text_easyocr(image_path)`
Extracts text using EasyOCR library with English language support.

**Parameters:**
- `image_path`: Path to the input image

**Returns:**
- Extracted text as string

### `read_text_textract(image_path)`
Extracts text using AWS Textract service.

**Parameters:**
- `image_path`: Path to the input image

**Returns:**
- Extracted text as string

### `jaccard_similarity(sentence1, sentence2)`
Calculates Jaccard similarity coefficient between two text strings.

**Parameters:**
- `sentence1`: First text string
- `sentence2`: Second text string

**Returns:**
- Similarity score (0-1)

## Performance Metrics

The project uses **Jaccard Similarity** to evaluate OCR performance:

```
Jaccard Similarity = |A ∩ B| / |A ∪ B|
```

Where A and B are sets of words from ground truth and extracted text respectively.

## Results

The script outputs average scores for each OCR tool:
- `score_tesseract`: Average Tesseract performance
- `score_easyocr`: Average EasyOCR performance  
- `score_textract`: Average AWS Textract performance

## Known Issues

- **EasyOCR Warning**: "Neither CUDA nor MPS are available - defaulting to CPU" - This is normal for CPU-only environments
- **AWS Credentials**: Ensure proper AWS setup for Textract functionality
- **Image Quality**: OCR performance heavily depends on image quality and text clarity

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgments

- Google Tesseract OCR team
- EasyOCR developers
- AWS Textract service
- Google Colab platform

