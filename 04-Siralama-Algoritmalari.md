# 4. Sıralama Algoritmaları (Sorting Algorithms)

Bu bölümde, temel mantığı kavramak için öğretilen ve zaman karmaşıklıkları genellikle $O(n^2)$ olan üç temel sıralama algoritmasını analiz edeceğiz. 

## 4.1. Bubble Sort (Kabarcık Sıralaması)

Bubble Sort, dizinin başından sonuna kadar yan yana duran elemanları ikili olarak karşılaştırır. Eğer soldaki eleman sağdakinden büyükse, bu iki eleman yer değiştirir (swap). Bu işlem, dizide hiçbir yer değiştirme yapılmayana kadar devam eder. Her tam turda, dizideki en büyük eleman "kabarcık" gibi dizinin sonuna yükselir.

**Algoritma Analizi:**
- **En Kötü Durum (Worst Case):** Dizi ters sıralıysa, her eleman için tüm dizinin taranması gerekir. Karmaşıklık $O(n^2)$.
- **En İyi Durum (Best Case):** Dizi zaten sıralıysa (ve algoritma ufak bir kontrol mekanizması ile optimize edilmişse), sadece bir kez üzerinden geçilir. Karmaşıklık $O(n)$.
- **Ortalama Durum (Average Case):** $O(n^2)$.
- **Yerinde Sıralama (In-place):** Evet, ekstra bellek gerektirmez ($O(1)$ alan).

## 4.2. Selection Sort (Seçmeli Sıralama)

Selection Sort, diziyi "sıralı" ve "sırasız" olmak üzere iki alt parçaya böler. Başlangıçta sıralı parça boştur. Algoritma, sırasız parça içindeki en küçük (minimum) elemanı bulur ve sırasız parçanın en başındaki eleman ile yer değiştirir. Bu işlem, tüm dizi sıralanana kadar devam eder.

**Algoritma Analizi:**
- **En Kötü Durum (Worst Case):** $O(n^2)$.
- **En İyi Durum (Best Case):** Dizi sıralı bile olsa, algoritma en küçük elemanı bulmak için tüm sırasız kısmı taramak zorundadır. Bu nedenle en iyi durumda da karmaşıklık değişmez: $\Omega(n^2)$.
- **Ortalama Durum (Average Case):** $\Theta(n^2)$.
- **Yerinde Sıralama (In-place):** Evet, $O(1)$ alan kullanır.

## 4.3. Insertion Sort (Araya Ekleme Sıralaması)

Insertion Sort, tıpkı elimizdeki iskambil kağıtlarını sıraladığımız gibi çalışır. Dizinin ikinci elemanından başlar, mevcut elemanı alır ve sol tarafındaki sıralı kısımda uygun olan pozisyona yerleştirir (gerekirse diğer elemanları sağa kaydırır).

**Algoritma Analizi:**
- **En Kötü Durum (Worst Case):** Dizi ters sıralıysa, her yeni eleman en başa kadar kaydırılmalıdır. Karmaşıklık $O(n^2)$.
- **En İyi Durum (Best Case):** Dizi zaten sıralıysa, sadece tek bir karşılaştırma yapılır ve kaydırma işlemi olmaz. Bu durumda karmaşıklık $O(n)$ olur.
- **Ortalama Durum (Average Case):** $O(n^2)$.
- **Yerinde Sıralama (In-place):** Evet, $O(1)$ alan kullanır.

**Neden Insertion Sort Önemlidir?**
Kötü asimptotik karmaşıklığına rağmen, veri seti çok küçükse ($n \le 20$) veya dizi büyük ölçüde sıralanmışsa (nearly sorted) çok hızlı çalışır. Bu nedenle Quick Sort ve Merge Sort gibi gelişmiş algoritmaların içinde, veri boyutu küçüldüğünde temel sıralayıcı olarak tercih edilir.
