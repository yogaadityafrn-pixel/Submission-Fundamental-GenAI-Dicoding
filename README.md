# 🎨 StudioAI — Stable Diffusion Image Generation & Editing

**Submission Project — Belajar Fundamental Generative AI (BFGAI)**
*Yoga Aditya Fernanda*

---

## 📌 Deskripsi Proyek

**StudioAI** adalah aplikasi berbasis AI untuk menghasilkan dan mengedit gambar menggunakan model **Stable Diffusion v1.5** dari Hugging Face. Proyek ini terdiri dari dua bagian utama:

1. **Pipeline Notebook** — Eksplorasi mendalam terhadap kemampuan Stable Diffusion secara programatik, mencakup Text-to-Image, Image-to-Image (refiner & inpainting), dan Outpainting.
2. **Streamlit App** — Antarmuka interaktif berbasis web yang memungkinkan pengguna menghasilkan dan mengedit gambar secara visual tanpa perlu menulis kode.

---

## 📁 Struktur File

```
.
├── Pipeline_submission_BFGAI_Yoga_Aditya_Fernanda_fixed.ipynb   # Pipeline eksplorasi Stable Diffusion
├── Streamlit_submission_BFGAI_Yoga_Aditya_Fernanda_fixed.ipynb  # Notebook Streamlit + deployment
├── requirements.txt                                              # Daftar dependensi Python
└── README.md
```

> **Catatan:** File `logic.py` dan `app.py` di-generate secara otomatis oleh sel `%%writefile` pada notebook Streamlit saat dijalankan di Google Colab.

---

## ⚙️ Instalasi & Menjalankan

### Prasyarat
- Python 3.9+
- GPU dengan CUDA (disarankan: Google Colab dengan GPU T4/A100)
- Akun [ngrok](https://ngrok.com/) untuk tunneling Streamlit

### 1. Install Dependensi

```bash
pip install -r requirements.txt
pip install streamlit_drawable_canvas==0.8.0 pyngrok
```

### 2. Jalankan Pipeline Notebook

Buka dan jalankan `Pipeline_submission_BFGAI_...ipynb` di Google Colab secara berurutan dari atas ke bawah. Notebook ini tidak memerlukan server tambahan.

### 3. Jalankan Aplikasi Streamlit

Buka `Streamlit_submission_BFGAI_...ipynb` di Google Colab, lalu jalankan semua sel secara berurutan. Sel `%%writefile` akan menghasilkan file `logic.py` dan `app.py`, kemudian Streamlit akan dijalankan dan diekspos melalui **ngrok**.

---

## 🚀 Fitur

### 🖼️ Pipeline Notebook

#### Kriteria 1 — Text-to-Image (Text-to-Image Generation)
- Generate gambar dari teks prompt menggunakan `StableDiffusionPipeline`
- Perbandingan **Guidance Scale** (CFG): rendah vs. tinggi
- Perbandingan **Inference Steps**: sedikit vs. banyak
- **Batch Inference**: generate beberapa gambar sekaligus dari satu prompt
- **Scheduler Comparison**: Euler A, DPM++, dan DDIM

#### Kriteria 2 — Image-to-Image
- **Base + Refiner Pipeline**: menyempurnakan gambar menggunakan `StableDiffusionImg2ImgPipeline`
- **Inpainting Manual**: mengganti area tertentu pada gambar menggunakan masker yang dibuat secara manual (koordinat NumPy array)
- **Inpainting Otomatis**: masker dihasilkan secara otomatis menggunakan model segmentasi `Mask2Former` (facebook/mask2former-swin-tiny-coco-instance)
- **Outpainting (Right Expand)**: memperluas kanvas ke kanan
- **Outpainting (Zoom Out)**: memperluas kanvas ke semua arah sekaligus

---

### 🌐 Streamlit App (StudioAI)

#### Tab ✨ GENERATE
- Input prompt dan negative prompt
- Kontrol parameter: Quality Steps, CFG Scale, Seed, Scheduler (Euler A / DPM++ / DDIM), Batch Size (1–4 gambar)
- Output grid untuk batch image, dengan tombol pilih gambar untuk diedit

#### Tab 🛠️ EDIT
- **Inpainting**: gambar mask secara bebas di atas gambar menggunakan drawable canvas, lalu masukkan prompt baru untuk mengganti area yang dipilih
- **Outpainting (Zoom Out)**: perluas kanvas gambar ke segala arah sebesar 128px menggunakan prompt deskriptif

#### Fitur Tambahan
- 🧹 **Flush RAM** button untuk membersihkan memori GPU
- Debug mode untuk melihat masker final sebelum proses inpainting

---

## 🧪 Model yang Digunakan

| Model | Kegunaan |
|---|---|
| `runwayml/stable-diffusion-v1-5` | Text-to-Image, Image-to-Image |
| `runwayml/stable-diffusion-inpainting` | Inpainting & Outpainting |
| `facebook/mask2former-swin-tiny-coco-instance` | Segmentasi otomatis untuk auto-masking |

---

## 📦 Dependensi Utama

```
diffusers
transformers
accelerate
torch
torchvision
torchaudio
streamlit
pyngrok
pillow
```

---

## 📝 Catatan Penting

- Seluruh proses inferensi menggunakan **`torch.float16`** untuk efisiensi memori GPU.
- **Seed** digunakan secara konsisten di seluruh eksperimen untuk memastikan reproducibility hasil gambar.
- Pada notebook Streamlit, **`logic.py`** adalah satu-satunya file yang perlu dimodifikasi; `app.py` sudah disediakan sebagai template final.
- Pastikan ngrok token sudah dikonfigurasi sebelum menjalankan sel deployment.

---

## 👤 Author

**Yoga Aditya Fernanda**
Submission — Belajar Fundamental Generative AI (Dicoding)
