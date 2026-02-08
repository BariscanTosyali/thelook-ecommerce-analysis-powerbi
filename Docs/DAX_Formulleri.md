# Projede Kullanılan DAX Formülleri

Bu raporun dinamik hesaplamaları aşağıdaki temel ölçüler (measures) ve hesaplanmış sütunlar (calculated columns) ile yapılmıştır:

### 1. Müşteri Segmentasyonu (Yeni Sütun)
Müşterileri toplam harcamalarına göre kategorize eder:
```dax
Müşteri Segmenti = 
VAR MusteriHarcamasi = SUMX(RELATEDTABLE('order_items'), 'order_items'[sale_price])
RETURN
    IF(MusteriHarcamasi < 100, "Bronz (Düşük)",
        IF(MusteriHarcamasi >= 100 && MusteriHarcamasi < 500, "Gümüş (Orta)", 
            "Altın (Yüksek Değerli)"))


İade Oranı = 
DIVIDE(
    COUNTROWS(FILTER('order_items', 'order_items'[status] = "Returned")),
    COUNTROWS('order_items'),
    0
)


Toplam Harcama = SUM('order_items'[sale_price])
