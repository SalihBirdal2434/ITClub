# Genelüye Verisi İşleme ve Görselleştirme

Bu proje, kullanıcıların doldurduğu bir formun Excel çıktısını işleyerek verileri temizler, düzenler ve çeşitli analizler ile görselleştirir. Projede özellikle "Bölümün:" sütunundaki verilerde oluşabilecek farklı yazım biçimleri, kısaltmalar ve hatalı girişler, fuzzy matching kullanılarak standartlaştırılmaktadır. Ayrıca, günlük giriş sayıları ve bölüm dağılımları interaktif grafiklerle görselleştirilir.

---

## İçerik

- [Genel Bakış](#genel-bakış)
- [Özellikler](#özellikler)
- [Kurulum ve Gereksinimler](#kurulum-ve-gereksinimler)
- [Dosya Yapısı](#dosya-yapısı)
- [Kullanım](#kullanım)
- [Hata Ayıklama ve Uyarılar](#hata-ayıklama-ve-uyarılar)
- [Katkıda Bulunma](#katkıda-bulunma)
- [Lisans](#lisans)

---

## Genel Bakış

Proje, "genelüyeformu.xlsx" adlı Excel dosyasından verileri okuyarak aşağıdaki işlemleri gerçekleştirir:

1. **Veri Yükleme ve Temizlik:**
   - Excel dosyasından veriler `pandas` kullanılarak okunur.
   - Gereksiz sütunlar (ör. `Id`, `KVKK Metnini Onaylıyor musun?\n`) silinir.
   - Boş hücreler uygun şekilde doldurulur ve sütun tipleri düzenlenir.
   - "Bölümün:" sütunu, küçük harfe çevrilir ve kenar boşlukları temizlenir.

2. **Fuzzy Matching ile Bölüm Standartlaştırması:**
   - Kullanıcı tarafından girilen bölüm isimleri, tanımlı bir `departments` listesine göre karşılaştırılır.
   - `fuzzywuzzy` kütüphanesi kullanılarak en uygun eşleşme bulunur ve benzerlik skoru %40 veya üzeri ise, veri eşleşen isimle güncellenir.
   - Ek olarak, belirli kısaltmalar veya hatalı yazımlar için `abbreviation_map` kullanılarak doğrudan eşleştirme yapılır.

3. **Veri Analizi ve Görselleştirme:**
   - Tarih bazında kayıt sayıları gruplanarak günlük giriş yoğunluğu hesaplanır.
   - `plotly.express` kullanılarak interaktif çizgi grafikleri ve histogramlar oluşturulur.
   - Bölümlerin dağılımı, pasta grafiği şeklinde görselleştirilir.

---

## Özellikler

- **Veri Temizleme:** NaN değerlerin işlenmesi, gereksiz sütunların kaldırılması ve metin verilerinin düzenlenmesi.
- **Fuzzy Matching:** Farklı yazım biçimleri ve kısaltmaların standart bölüm isimlerine dönüştürülmesi.
- **Interaktif Görselleştirme:** Günlük kayıt sayıları ve bölüm dağılımlarının interaktif grafiklerle sunulması.
- **Esneklik:** Kod, farklı veri setleri için kolayca uyarlanabilir ve genişletilebilir.

---

## Kurulum ve Gereksinimler

### Gerekli Python Sürümü
- Python 3.10 veya üzeri (Python 3.11 önerilir)

### Gerekli Paketler

Projeyi çalıştırmadan önce aşağıdaki paketleri yükleyin:

```bash
pip install pandas
pip install openpyxl
pip install fuzzywuzzy
pip install python-Levenshtein  # Performans iyileştirmesi için önerilir
pip install plotly
