# Urdu OCR — A fine-tuned TrOCR model for extracting text from Urdu images

_Code Saviours ML/AI Internship — Batch SI-26_

## Research Task

### 1. What is OCR (Optical Character Recognition)?

Optical Character Recognition (OCR) is a technology that scans printed or handwritten text from images, PDFs, or documents and converts it into editable, searchable digital text. Instead of manually typing content, OCR automatically recognizes characters and extracts the text — widely used for digitizing books, forms, invoices, historical documents, and other paper-based records.

### 2. Why is Urdu OCR harder than English OCR?

Urdu is written in a cursive script where most letters connect to each other, and many letters have very similar shapes, differing only by the number or position of dots. Combined with varying fonts, handwriting styles, image quality, and complex layouts, this makes Urdu OCR considerably harder than OCR for Latin-script languages like English. To improve recognition accuracy, effective Urdu OCR systems typically need preprocessing, segmentation, and character recognition steps before extracting the final text.

### 3. What are 2 real-world situations where Urdu OCR would be useful?

- **Accessibility for visually impaired users** — Urdu OCR can extract text from books or documents and feed it into text-to-speech systems, making printed material accessible.
- **Digitizing institutional records** — government offices, libraries, and legal organizations hold thousands of Urdu documents, gazettes, and official records that could be converted into searchable, electronic form, saving time and reducing manual data entry.

## Why We Need a Better Model

Before building a custom model, we tested baseline **Tesseract OCR** on 5 processed Urdu images:

- On clean, synthetic (typed) Urdu text, Tesseract performed very well — sometimes with 100% accuracy.
- On real-world scanned/photographed images, Tesseract output was almost completely gibberish.
- Common errors included confusion between visually similar characters (e.g. پ vs ب), incorrect extra characters (e.g. extra hamza), and complete breakdown on noisy/real images.

**Tesseract fails on Urdu because it struggles with cursive, joined characters, and performs drastically worse on real-world scanned or photographed images compared to clean synthetic text.** This confirmed the need for a custom-trained OCR model built specifically for real-world Urdu documents.

## How it works

### The model: TrOCR

This project uses **TrOCR** (Transformer-based OCR), a model architecture developed by Microsoft that combines two parts:

- A **vision encoder** (based on a Vision Transformer, or ViT) that looks at the image and learns to represent what's visually on the page.
- A **text decoder** (based on RoBERTa/GPT-style transformers) that takes what the encoder "saw" and generates the corresponding text, one token at a time.

The base model (`microsoft/trocr-base-printed`) was originally trained on printed English text. **Fine-tuning** means taking that pretrained model and continuing to train it — this time on a dataset of Urdu images paired with their correct transcriptions — so the model gradually adapts its existing visual and language understanding to Urdu script instead of starting from scratch.

For this project, the model was fine-tuned for 10 epochs on a custom dataset of Urdu text images collected as part of the Week 4 assignment.

## Live demo

Try the model here: **[Urdu OCR on Hugging Face Spaces](https://huggingface.co/spaces/122Uswa/urdu-ocr-codesaviours-si26-Uswa)**

Upload an image containing Urdu text and the app will attempt to extract and display the text.

## How to run it locally

1. Clone this repository:
   ```bash
   git clone https://github.com/codewithUswaFatima/urdu-ocr-codesaviours-si26-Uswa
   cd urdu-ocr-codesaviours-si26-Uswa
   ```

2. Install dependencies:
   ```bash
   pip install gradio transformers torch pillow
   ```

3. Run the app:
   ```bash
   python app.py
   ```

4. Open the local URL shown in your terminal (usually `http://127.0.0.1:7860`) in your browser.

> Note: the app downloads the fine-tuned model automatically from the Hugging Face Model Hub (`122Uswa/urdu-ocr-codesaviours-si26-uswa`) the first time it runs.

## Dataset details



- **Number of images:** 203
- **Sources:** [e.g. self-collected handwritten samples, scanned printed text, public Urdu datasets]
- **Variety collected:** [fonts used, handwriting vs. printed, background types, image sizes/resolutions]

## Results

The model was fine-tuned for 10 epochs but did **not** achieve usable accuracy: exact-match accuracy was 0%, with a character error rate (CER) of roughly 200%, meaning the model's predictions were, on average, longer and more different from the correct text than the correct text itself.

**Likely reasons for this:**
- The training dataset was likely too small and/or lacked enough variety (fonts, handwriting styles, backgrounds) for the model to generalize.
- Starting from `trocr-base-printed`, which was trained on printed **English** text, may not transfer well to cursive, right-to-left Urdu script without a much larger fine-tuning dataset.
- Ten epochs may not have been enough training time for the model to meaningfully adapt to a new script and language.

**What I would try with more time:**
- Collect a significantly larger and more diverse Urdu dataset, including multiple fonts, handwriting styles, and backgrounds.
- Try a base model with stronger multilingual or Urdu-specific pretraining, rather than an English-only printed-text checkpoint.
- Experiment with more training epochs, learning rate tuning, and data augmentation (rotation, noise, contrast changes) to help the model generalize better.
- Evaluate on a held-out validation set throughout training to catch problems earlier instead of only at the end.

## Credit

**Uswa Fatima**
Built during the Code Saviours ML/AI Internship — Batch SI-26.
