# Online Shoppers Purchasing Intention

Bir e-ticaret sitesinin oturum verilerinden yola cikarak, kullanıcıların satın alım niyetlerine göre segmentasyonlarının yapılması ve satın alımları tahmin eden bir makine ogrenmesi projesi.

**Veri seti:** [UCI — Online Shoppers Purchasing Intention](https://archive.ics.uci.edu/ml/datasets/Online+Shoppers+Purchasing+Intention+Dataset)  
**Hedef degisken:** `Revenue` — oturumun satin alimla sonuclanip sonuclanmadigi

---

## Proje Yapisi

```
online-shoppers-intention-prediction/
│
├── data/
│   ├── online_shoppers_intention.csv
│   └── cleaned.csv
│
├── notebooks/
│   ├── 00_Preprocessing.ipynb    
│   ├── 01_EDA_and_Baseline.ipynb 
│   ├── 02_Segmentation.ipynb     
│   └── 03_Classification_and_Comparison.ipynb
│
├── requirements.txt
└── README.md
```

---

## Veri Seti

12.330 oturum, 18 degisken. Sinif dagilimi dengesizdir (%84 Revenue=False).

| Degisken Grubu | Degiskenler |
|---|---|
| Sayfa etkilesimleri | Administrative, Informational, ProductRelated ve sureleri |
| Google Analytics | BounceRates, ExitRates, PageValues |
| Zaman | Month, SpecialDay, Weekend |
| Ziyaretci | VisitorType, OperatingSystems, Browser, Region, TrafficType |
| Hedef | Revenue |

---

## Sonuclar

| Model | ROC-AUC | F1 (Revenue) |
|---|---|---|
| Logistic Regression (Baseline) | 0.9083 | 0.62 |
| Random Forest | 0.9303 | — |
| Gradient Boosting | **0.9373** | — |

Sinif dengesizligi `class_weight='balanced'` ve `compute_sample_weight` ile
ele alinmistir. 5-Fold Stratified CV sonuclari test seti performansiyla tutarlidir.

Segmentasyon analizi 3 davranissal kume ortaya koymaktadir:

| Segment | Tanim |
|---|---|
| 0 | Pasif Grup — dusuk sayfa degeri, yuksek cikis orani |
| 1 | Aktif Alicilar — yuksek PageValues, dusuk exit rate |
| 2 | Arastirmaci Grup — bilgi odakli gezinti |

---
