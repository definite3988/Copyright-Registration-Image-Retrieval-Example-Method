# 📜 Copyright Registration Image Retrieval  

## 🔍 Problem Statement  
The dataset (`/content/copyright_records.csv`) contains **test data** related to copyright registrations.  
🛑 **Important Note:** The image files in `/content/sample copyright` are **for reference only** and should **not** be used for actual validation.  

## 🎯 Goal  
Develop a **scalable method** to retrieve **copyright registration images** based on **metadata matching**, using AI or other suitable technologies.  
Since images are **reference files**, the approach focuses on **text-based validation** rather than direct image verification.  

## ⚡ Approach  
The retrieval process follows **five key steps**:  

### 🔹 **1. Extract Metadata** 🗂️  
- Load `copyright_records.csv` using **Pandas**.  
- Identify fields such as **Registration Number, Title, Claimant**, etc.  

### 🔹 **2. Scan Reference Images** 🖼️  
- List available images from `/content/sample copyright`.  
- Extract file names and metadata for matching.  

### 🔹 **3. Apply AI-based OCR** 🧠  
- Use **Tesseract OCR** to extract text from images.  
- Convert image text into structured data for comparison.  

### 🔹 **4. Fuzzy Text Matching** 🔍  
- Compare extracted text against **metadata fields** using **fuzzy logic** (`fuzzywuzzy`).  
- Rank matches based on **confidence scores**.  

### 🔹 **5. Display Results** 🎨  
- Showcase matched images **(reference only)** in a **grid format**.  
- Label each image with **title, extracted text, and confidence score**.  

## 🛠️ Implementation  

```python
import os
import pandas as pd
import pytesseract
from fuzzywuzzy import process
from PIL import Image
import matplotlib.pyplot as plt

# 🛑 IMPORTANT: Images are for REFERENCE ONLY!

# Define paths
metadata_file = "/content/copyright_records.csv"
image_folder = "/content/sample copyright"

# Load metadata
df = pd.read_csv(metadata_file)
titles = df["Title"].tolist()

# List image files
image_files = [f for f in os.listdir(image_folder) if f.endswith(('.png', '.jpg', '.jpeg', '.webp'))]

# Extract text from images using OCR (FOR REFERENCE ONLY)
def extract_text(image_path):
    img = Image.open(image_path)
    return pytesseract.image_to_string(img).strip()

# Match extracted text to metadata
matches = {img: process.extractOne(extract_text(os.path.join(image_folder, img)), titles) for img in image_files}

# Display images one by one (FOR REFERENCE ONLY)
for img_name in random.sample(image_files, min(6, len(image_files))):
    img_path = os.path.join(image_folder, img_name)
    img = Image.open(img_path)

    plt.figure(figsize=(6, 6))
    plt.imshow(img)
    plt.title(f"🖼️ {img_name} (REFERENCE ONLY)\n📜 Matched: {matches[img_name][0]}\n🔍 Confidence: {matches[img_name][1]}%", fontsize=10)
    plt.axis("off")
    plt.show()
```

# 📜 Deliverables  

✅ **Proposed Method** – A metadata-based retrieval approach ensuring efficient image matching.  
✅ **Sample Reference Images** – Images provided **for reference only** (not for actual validation).  
✅ **Code Snippet** – Demonstrates **OCR-based text extraction** and **fuzzy matching** for metadata alignment.  
