# 3. Veri Yapıları ve Amortize Analiz

## 3.1. Soyut Veri Tipleri (Abstract Data Types - ADTs)
Soyut Veri Tipi, verilerin nasıl saklandığından ziyade, hangi operasyonların yapılabileceğini ve bu operasyonların davranışlarını tanımlayan matematiksel bir modeldir. Bir ADT, sadece "ne yapılacağını" söyler; veri yapısı ise bunu "nasıl yapılacağını" (implementasyon) belirler.

## 3.2. Liste, Yığın (Stack), Kuyruk (Queue) ve Dequeue

Bu yapılar hem dizi (array) tabanlı hem de işaretçi (pointer/linked list) tabanlı olarak uygulanabilir.

### 3.2.1. Dizi Tabanlı (Array-based) Uygulama
Veriler bellekte ardışık (contiguous) bloklar halinde saklanır.
- **Avantajlar:** İndeksleme sayesinde rastgele erişim (random access) $O(1)$ sürede yapılır. Bellek yerelliği (cache locality) avantajı sağlar.
- **Dezavantajlar:** Boyut başlangıçta sabittir. Kapasite dolduğunda yeniden boyutlandırma (resizing) gerekir. Araya eleman ekleme veya silme işlemi elemanların kaydırılmasını gerektirdiği için $O(n)$ maliyetlidir.

### 3.2.2. İşaretçi Tabanlı (Pointer-based / Linked List) Uygulama
Her veri elemanı (node), bir sonraki elemanın bellek adresini tutan bir işaretçi barındırır.
- **Avantajlar:** Dinamik bir yapıya sahiptir; eleman eklendikçe büyür. İşaretçi adresi biliniyorsa araya ekleme ve silme işlemleri $O(1)$ sürede tamamlanır.
- **Dezavantajlar:** Rastgele erişim yoktur; $k$. elemana ulaşmak için $O(k)$ tarama yapılmalıdır. Her düğüm için fazladan işaretçi belleği harcanır.

### 3.2.3. Operasyonel Karşılaştırma (Zaman Karmaşıklığı)

| Yapı | Operasyon | Dizi (Amortize) | Bağlı Liste |
| :--- | :--- | :--- | :--- |
| **Stack** | Push / Pop | $O(1)$ | $O(1)$ |
| **Queue** | Enqueue / Dequeue | $O(1)$ | $O(1)$ |
| **List** | İndeksle Erişim | $O(1)$ | $O(n)$ |
| **List** | Başa Ekleme | $O(n)$ | $O(1)$ |

*Not: Kuyruk yapısında dizi kullanılırken "Circular Array" mantığı uygulanarak $O(1)$ verimlilik sağlanır.*

## 3.3. Amortize Analiz (Amortized Cost)

Amortize analiz, bir algoritmanın bir dizi (sequence) işlem boyunca gösterdiği ortalama maliyeti hesaplar. Sık yapılan ucuz işlemler ile nadiren yapılan pahalı işlemlerin maliyetini dengeler.

### Dinamik Dizi Resizing Örneği
Bir dinamik dizi (örneğin Java'daki ArrayList veya C++'daki std::vector) dolduğunda kapasitesini iki katına çıkarır.
1. Normal Ekleme: $O(1)$ maliyetlidir.
2. Kapasite Dolduğunda: Yeni bir yer açılır ve mevcut $n$ eleman buraya kopyalanır. Bu işlem $O(n)$ maliyetlidir.

**Analiz:**
$n$ adet ekleme yapıldığında gerçekleşen kopyalama işlemleri: $1 + 2 + 4 + 8 + \dots + n/2$ serisini izler. Bu serinin toplamı yaklaşık $n$ değerine eşittir.
- Toplam maliyet = $n$ (normal eklemeler) + $n$ (tüm kopyalamalar) = $2n$.
- İşlem başına düşen maliyet = $2n / n = 2 \implies O(1)$.

Sonuç olarak, dinamik bir diziye eleman eklemenin **amortize maliyeti** $O(1)$'dir.
