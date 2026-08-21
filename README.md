Urdu OCR

Extracts text from Urdu document images using a fine-tuned TrOCR model.

Why this matters

Urdu is read by over 300 million people across Pakistan, India, and Bangladesh, but Urdu OCR is far less mature than OCR for Latin-script languages — the cursive, joined script and near-identical letter shapes (differing only by dot placement) trip up general-purpose tools like Tesseract, which we tested and found broke down almost completely on real scanned/photographed Urdu text. A working Urdu OCR model matters for two concrete reasons: it can make printed Urdu material accessible to visually impaired users via text-to-speech, and it can help digitize the huge backlog of Urdu records sitting in government offices, libraries, and legal archives.

Live Demo

https://huggingface.co/spaces/122Uswa/urdu-ocr-codesaviours-si26-Uswa

Upload an image containing Urdu text and the app will attempt to extract it.

How it works

TrOCR pairs a vision encoder (a Vision Transformer that "reads" the image) with a text decoder (a language model that turns what it saw into text, one token at a time). This project takes microsoft/trocr-base-printed — a checkpoint originally trained on printed English — and fine-tunes it on a custom dataset of Urdu text images for 10 epochs, so it gradually adapts from English to Urdu script instead of starting from scratch.

Results

Training loss dropped from 9.00 to 3.50 over 10 epochs, but the model did not reach usable accuracy: exact-match accuracy was 0%, with a character error rate around 200% (meaning predictions were, on average, longer and more different from the correct text than the ground truth itself is).

Likely causes: the training set (~200 images) was probably too small and not varied enough in fonts/handwriting/backgrounds; starting from an English-only printed-text checkpoint may not transfer well to cursive, right-to-left Urdu without a much larger fine-tuning set; and 10 epochs likely wasn't enough for the model to meaningfully adapt to a new script.

Next steps: collect a much larger and more diverse Urdu image dataset, try a base model with stronger multilingual/Urdu pretraining, tune learning rate and epoch count, add data augmentation (rotation, noise, contrast), and evaluate on a held-out set throughout training rather than only at the end.

How to run locally
bash
git clone https://github.com/codewithUswaFatima/urdu-ocr-codesaviours-si26-Uswa
cd urdu-ocr-codesaviours-si26-Uswa
pip install gradio transformers torch pillow
python app.py

Open the local URL shown in your terminal (usually http://127.0.0.1:7860). The app pulls the fine-tuned model automatically from the Hugging Face Hub (122Uswa/urdu-ocr-codesaviours-si26-uswa) on first run.

Demo Video

Loom walkthrough

Built by: Uswa Fatima | Code Saviours SI-26 | 2026
