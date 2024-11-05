<h1 align="center"> Analisis Sentimen menggunakan Caikit dan Hugging Face </h1> 
<p align="center"> Selamat datang di proyek Analisis Sentimen menggunakan Caikit dan Hugging Face! Proyek ini bertujuan untuk menganalisis sentimen teks dengan memanfaatkan kekuatan Caikit dan Transformer dari Hugging Face. Dengan menggabungkan kedua alat ini, kami menyediakan solusi yang efisien dan akurat untuk memahami emosi dan opini dalam teks.</p>

<div align="center">
   
<img src="https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white">
<img src="https://img.shields.io/badge/Hugging%20Face-Transformer-yellow?logo=huggingface&logoColor=white">
<img src="https://img.shields.io/badge/Caikit-Analisis%20Sentimen-blueviolet">
<img src="https://img.shields.io/badge/Linux-x86__64-important?logo=linux">
</div>

---

# Analisis Sentimen Teks menggunakan Caikit dan Hugging Face
Author: Cognitive Class AI

---

## 🚀 Fitur Utama
- **Model Sentimen Terbaru**: Menggunakan model transformer terbaru dari Hugging Face untuk analisis sentimen yang akurat.
- **Integrasi Caikit**: Memanfaatkan kerangka kerja Caikit untuk pengembangan AI yang modular dan skalabel.
- **Antarmuka Pengguna yang Mudah**: Menyediakan antarmuka yang intuitif dan ramah pengguna.
- **Dukungan Multi-Bahasa**: Mampu melakukan analisis sentimen dalam beberapa bahasa utama.
- **Visualisasi Data**: Menampilkan hasil analisis untuk memberikan wawasan yang lebih mendalam.

## 📦 Instalasi
Ikuti langkah-langkah berikut untuk menginstal dan menjalankan proyek ini di lingkungan lokal Anda.

## ✨ Teknologi yang Digunakan:
- Python

## 📝 Persyaratan:
1. Linux/MacOS x86_64
2. Caikit (v0.9.2)
3. Python (v3.8+)
4. pip (v23.0+)

##  Dokumentasi:
1. Instal virtualenv <br>
   <code>pip install --user virtualenv</code>
2. Buat virtualenv <br>
   <code>virtualenv -p python3 env</code>
3. Aktifkan virtualenv <br>
   <code>source env/bin/activate</code>
4. Instalasi paket yang diperlukan <br>
   <code>pip install -r requirements.txt</code>
5. Mulai runtime <br>
   <code>python start_runtime.py</code>
6. Jalankan klien <br>
   <code>python client.py</code>

## Prosedur 🛠️
<p align="justify">
Selesaikan tugas-tugas berikut untuk mengkonfigurasi runtime Caikit dan model AI, kemudian uji dari aplikasi klien:
</p>

1. **Buat Proyek**: 
   - Siapkan direktori dan file yang diperlukan untuk proyek Anda.
     ```bash
     pip install --user virtualenv  
     mkdir -p /home/project/text-sentiment/text_sentiment  
     cd /home/project/text-sentiment/text_sentiment
     ```

2. **Buat Spesifikasi Model Data**: 
   - Definisikan format data yang digunakan oleh modul Caikit.
     ```bash
     mkdir data_model
     cd data_model
     touch classification.py
     ```

3. **Buat Pembungkus Model**: 
   - Implementasikan pembungkus yang mengintegrasikan model AI dengan kerangka kerja Caikit.
     ```bash
     mkdir -p models/text_sentiment
     cd models/text_sentiment
     touch config.yml
     mkdir runtime_model
     cd runtime_model
     touch hf_module.py
     touch __init__.py
     cd ../../..  # Kembali ke direktori proyek
     ```

4. **Sertakan Modul dan Ketergantungan Paket**: 
   - Tentukan ketergantungan yang diperlukan dalam konfigurasi proyek Anda.
     ```bash
     touch requirements.txt
     virtualenv -p python3 env
     source env/bin/activate
     pip install -r requirements.txt
     ```

5. **Mulai Runtime Caikit**: 
   - Luncurkan runtime Caikit untuk melayani model untuk inferensi.
     ```bash
     touch start_runtime.py
     python start_runtime.py
     ```

6. **Uji Analisis Sentimen**: 
   - Jalankan tes untuk memvalidasi fungsi model analisis sentimen melalui aplikasi klien.
     ```bash
     touch client.py
     python client.py
     ```


##  Penggunaan
Setelah aplikasi berjalan, Anda dapat memasukkan teks untuk menganalisis sentimennya melalui antarmuka pengguna. Hasil analisis akan menampilkan sentimen—positif, negatif, atau netral.

## 💻 Kode Utama
Berikut adalah kode utama yang digunakan dalam proyek ini untuk menjalankan analisis sentimen:

```python
# Hak Cipta Penulis Caikit
#
# Berlisensi di bawah Lisensi Apache, Versi 2.0 (the "License");
# Anda tidak diperbolehkan menggunakan file ini kecuali sesuai dengan License.
# Anda dapat memperoleh salinan License di
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Kecuali diatur oleh hukum yang berlaku atau disepakati secara tertulis,
# perangkat lunak ini didistribusikan dalam kondisi "APA ADANYA",
# tanpa jaminan atau kondisi apapun, baik tersurat maupun tersirat.
# Lihat License untuk informasi lebih lanjut.

# Standar
import os

# Pihak Ketiga
import grpc

# Lokal
from caikit.runtime.service_factory import ServicePackageFactory
from text_sentiment.data_model import TextInput

inference_service = ServicePackageFactory().get_service_package(
    ServicePackageFactory.ServiceType.INFERENCE,
)

port = 8085

# Konfigurasi klien
channel = grpc.insecure_channel(f"localhost:{port}")
client_stub = inference_service.stub_class(channel)

# Menjalankan inferensi untuk dua contoh teks
for text in ["The sunset was beautiful", "yet I felt sad to see it go."]:
    input_text_proto = TextInput(text=text).to_proto()
    request = inference_service.messages.HuggingFaceSentimentTaskRequest(
        text_input=input_text_proto
    )
    response = client_stub.HuggingFaceSentimentTaskPredict(
        request, metadata=[("mm-model-id", "text_sentiment")]
    )
    print("Text:", text)
    print("RESPONSE:", response)

## 📊 Hasil Akhir
Berikut adalah contoh hasil dari analisis sentimen menggunakan dua kalimat sampel.

### Contoh Output
```plaintext
Text: The sunset was beautiful
RESPONSE: [Positif]

Text: yet I felt sad to see it go.
RESPONSE: [Negatif]

