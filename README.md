# Urdu OCR Project | Code Saviours SI-26 | Uswa Fatima

## Research Task

### 1. What is OCR (Optical Character Recognition)?
Optical Character Recognition (OCR) is a technology that scans printed or handwritten text from images, PDFs, or documents and converts it into editable and searchable digital text. Instead of manually typing the content, OCR automatically recognizes the characters and extracts the text. OCR is widely used for digitizing books, forms, invoices, historical documents, and other paper-based records.

### 2. Why is Urdu OCR harder than English OCR?
Urdu OCR is more challenging than English OCR because Urdu is written in a cursive script where most letters are connected to each other. Many Urdu letters have very similar shapes and differ only by the number or position of dots, making them difficult to recognize accurately. In addition, different fonts, handwriting styles, image quality, and complex document layouts make Urdu OCR more difficult than English OCR. To improve recognition accuracy, Urdu OCR systems usually perform preprocessing, segmentation, and character recognition before extracting the final text.

### 3. What are 2 real-world situations where Urdu OCR would be useful?
Urdu OCR is very useful for visually impaired people because it can extract text from books or documents and convert it into speech using text-to-speech technology. It is also useful for government offices, libraries, and legal organizations where thousands of Urdu documents, gazettes, and official records need to be digitized and stored in searchable electronic form. This saves time, reduces manual work, and makes documents easier to search and manage. 

## Why We Need a Better Model

We tested baseline Tesseract OCR on 5 processed Urdu images and found:

- On clean, synthetic (typed) Urdu text, Tesseract performed very well — 
  sometimes with 100% accuracy.
- On real-world scanned/photographed images, Tesseract output was almost 
  completely gibberish.
- Common errors included confusion between visually similar characters 
  (e.g. پ vs ب), incorrect extra characters (e.g. extra hamza), and 
  complete breakdown on noisy/real images.

**Tesseract fails on Urdu because it struggles with cursive, joined 
characters, and performs drastically worse on real-world scanned or 
photographed images compared to clean synthetic text.** This confirms 
the need for a custom-trained OCR model built specifically for 
real-world Urdu documents.
