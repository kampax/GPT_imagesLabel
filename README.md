# GPT Images Label - Cultural Ecosystem Services Classification
Author: Carlos Javier Navarro
mail: carlosnavarro@ugr.es

## Overview

This repository contains an automated image classification system using GPT-4.1 Vision to categorize photographs according to **Cultural Ecosystem Services (CES)**. The system analyzes images and automatically classifies them into specific categories related to the cultural ecosystems services.

## What does it do exactly?

The project implements an image classifier that:

1. **Reads a CSV file** (`inputs.csv`) containing:
   - Image IDs
   - URLs or file paths of the images

2. **Processes images in batches** using OpenAI GPT-4 Vision API to classify them into **7 specific categories**:
   - **Spiritual Services**: Sacred or religious inspiration derived from ecosystems
   - **Inspiration**: Use of natural motifs or artifacts in art, folklore, etc.
   - **Recreation and Tourism**: Activities like hiking, fishing, and visiting natural sites
   - **Heritage Values**: Cultural and historical significance of ecosystems and natural features
   - **Cultural Identity**: Sense of belonging and connection to an area's natural environment
   - **Aesthetic Appreciation**: Enjoyment of natural landscapes and the beauty of ecosystems
   - **Not Relevant**: Images not relevant for Cultural Ecosystem Services studies (blurry photos, memes, selfies, etc.)

3. **Automatically generates results** in CSV files organized by batches in folders:
   - `results_local/` (for local images)
   - `results_url/` (for images from URLs)

## Available Notebooks

### `GPT_Label_local_files.ipynb`
- Processes images stored **locally** in the `img/` folder
- Reads the `inputs.csv` file and builds local paths
- Converts images to base64 to send them to the API

### `GPT_Label_using_url.ipynb`
- Processes images from **remote URLs**
- Uses URLs directly from the `inputs.csv` file
- Ideal for images hosted in remote repositories or web servers

## Technical Features

- **Batch processing**: Handles large volumes of images by dividing work into batches of 100 images
- **Error handling**: Captures and logs processing errors
- **Rate control**: Implements delays to respect OpenAI API limits
- **Incremental results**: Saves results by batches to avoid data loss
- **Low temperature (0.2)**: Ensures consistent and accurate model responses

## Requirements

### OpenAI API
- **Valid API key** for OpenAI with access to GPT-4 Vision
- **Active paid subscription** (GPT-4 models are not available on the free plan)
- **Sufficient credits** to process images (each image consumes tokens)

### Python Dependencies
```python
openai>=1.0.0
pandas
IPython
base64 (included in Python standard library)
```

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/kampax/GPT_imagesLabel.git
   cd GPT_imagesLabel
   ```

2. **Install dependencies**:
   ```bash
   pip install openai pandas ipython
   ```

3. **Configure your API key**:
   - Edit the notebook file you plan to use
   - Replace `'your-API-key-here'` with your actual OpenAI API key

## Usage

### Data Preparation
1. **Prepare your CSV file** (`inputs.csv`) with columns:
   - `id`: Unique identifier for the image
   - `url`: Complete URL of the image (for the URLs notebook)

2. **For local images**: Place images in the `img/` folder

### Execution
1. **Open the appropriate notebook** in Jupyter Lab/Notebook:
   - `GPT_Label_local_files.ipynb` for local images
   - `GPT_Label_using_url.ipynb` for remote images

2. **Execute cells sequentially**:
   - Cell 1: Configuration and data loading
   - Cell 2: Classification prompt definition
   - Cell 3: Processing function
   - Cell 4: Batch processing and results saving

3. **Review results** in folders:
   - `results_local/captions_output_batch_X.csv`
   - `results_url/captions_output_batch_X.csv`

## Output Structure

Result CSV files contain:
- `id`: Image identifier
- `path/url`: Image path or URL
- `caption`: Category assigned by GPT-4 Vision

## Cost Considerations

- **GPT-4 Vision**: ~$0.01-0.02 per image (depending on resolution)
- **Rate limits**: Code includes delays to respect rate limits
- **Batch processing**: Allows pausing and resuming work without losing progress

## Use Cases

This system is especially useful for:
- **Academic research** in cultural ecosystem services
- **Content analysis** on social media about tourism and nature
- **Automatic cataloging** of landscape and outdoor activity photographs
- **Cultural perception studies** of the environment

