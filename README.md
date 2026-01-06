# Customer Churn Prediction: From Model to API

## Project Background
Customer churn merupakan permasalahan penting dalam bisnis, karena mempertahankan pelanggan lama umumnya lebih efisien dibandingkan memperoleh pelanggan baru. Dalam proyek ini, akan dibuat model prediktif sederhana menggunakan *logistic regression* untuk membantu mengidentifikasi risiko churn berdasarkan pola transaksi historis pelanggan.

Proyek ini merupakan implementasi **Customer Churn Prediction API** menggunakan model *machine learning* yang disajikan melalui **FastAPI**. API ini digunakan untuk memprediksi kemungkinan pelanggan melakukan *churn* berdasarkan perilaku transaksi. API ini dapat diakses secara publik menggunakan **ngrok** untuk kebutuhan pengembangan atau demo.

* Notebook pengolahan data dan pembuatan model: [link](https://github.com/mrnrasyad/Customer-Churn-Prediction-Model/blob/main/notebooks/customer_churn.ipynb)
* Notebook pembuatan API menggunakan **FastAPI** serta proses deployment dengan **ngrok**: [link](https://github.com/mrnrasyad/Customer-Churn-Prediction-Model/blob/main/notebooks/customer_churn_api.ipynb)
* Contoh implementasi model melalui API: [link](https://github.com/mrnrasyad/Customer-Churn-Prediction-Model/blob/main/notebooks/customer_curn_api_implementation.ipynb)

Base URL yang digunakan:
**[https://pugilistic-reva-goutily.ngrok-free.dev/](https://pugilistic-reva-goutily.ngrok-free.dev/)**


## Library Python yang Digunakan
- Python
- FastAPI
- Uvicorn
- scikit-learn
- pandas
- NumPy
- pyngrok

## Struktur Proyek
```
├── README.md
│   ├── raw/
│   │   └── data_retail.json                                 # raw data
├── notebooks/
│   └── customer_churn.ipynb                           # model development
│   └── customer_churn_api.ipynb                       # api development and deployment 
│   └── customer_churn_api_implementation.ipynb        # api implementation demo
├── model/
│   ├── customer_churn.sav                             # saved model
```

## Model Machine Learning
- Jenis model: Klasifikasi (prediksi churn biner)
- Fitur input:
  - `Average_Transaction_Amount`
  - `Count_Transaction`
  - `Year_Diff`
- Output:
  - Prediksi churn (misalnya: churn / tidak churn atau nilai biner)

### Model Evaluation

<p align="center">
  <kbd><img src="image\model_evaluation.png" width=600px> </kbd> <br>
  Model Evaluation
</p>

Model sangat baik dalam mengidentifikasi pelanggan yang akan churn (kelas 1.0) dengan recall tinggi (94%). Namun, recall untuk pelanggan yang tidak churn (kelas 0.0) rendah (41%), yang berarti banyak non-churner diprediksi sebagai churn. Model ini cenderung memprioritaskan prediksi churn.

### Feature Importance

<p align="center">
  <kbd><img src="image\feature_importance.png" width=600px> </kbd> <br>
  Feature Importance
</p>

Secara singkat, **Count_Transaction** dan **Year_Diff** merupakan fitur paling berpengaruh dalam prediksi churn; nilai yang lebih tinggi menurunkan kemungkinan pelanggan churn. Sementara itu, **Average_Transaction_Amount** memiliki pengaruh yang sangat kecil dalam model ini.


## Endpoint API

### `POST /churn_prediction`
Digunakan untuk memprediksi churn pelanggan berdasarkan fitur input.

**Request Body:**
```json
{
  'Average_Transaction_Amount'  : 1467681,	  
  'Count_Transaction'           : 22,
  'Year_Diff'                   : 2  
}
```

**Response:**
```
{
  "The customer will not churn"
}
```

## Assumptions and Caveats
Beberapa asumsi dan batasan dalam proyek ini adalah sebagai berikut:

- Model diasumsikan digunakan oleh perusahaan yang membutuhkan prediksi pelanggan berisiko churn.
- Kinerja model sangat bergantung pada kualitas data pelatihan yang digunakan.
