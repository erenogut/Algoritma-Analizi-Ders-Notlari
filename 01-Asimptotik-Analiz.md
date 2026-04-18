# 1. Asimptotik Analiz ve Fonksiyonlar

Asimptotik analiz, bir algoritmanın çalışma süresinin veya bellek kullanımının, girdi boyutu ($n$) sonsuza yaklaşırken nasıl bir büyüme eğilimi gösterdiğini matematiksel olarak ifade etme yöntemidir. Bu analiz, donanım veya programlama dilinden bağımsız olarak algoritmaları karşılaştırmamızı sağlar.

## 1.1. Big O ($O$) Notasyonu - Üst Sınır (Upper Bound)

Big O notasyonu, bir fonksiyonun büyüme hızının alabileceği maksimum değeri (en kötü durum - worst case) tanımlar. Algoritmanın çalışma süresinin belirli bir noktadan sonra bir $g(n)$ fonksiyonunun sabit bir katını geçemeyeceğini belirtir.

**Matematiksel Tanım:**
Eğer $f(n) = O(g(n))$ ise, öyle pozitif $c$ ve $n_0$ sabitleri vardır ki; tüm $n \ge n_0$ değerleri için:
$0 \le f(n) \le c \cdot g(n)$ eşitsizliği sağlanır.

**Örnek:** $f(n) = 3n^2 + 5n + 2$ fonksiyonu için en büyük dereceli terim $n^2$'dir. Katsayılar ve küçük dereceli terimler $n$ büyüdükçe önemsizleşeceği için $f(n) = O(n^2)$ olarak ifade edilir.

## 1.2. Omega ($\Omega$) Notasyonu - Alt Sınır (Lower Bound)

Omega notasyonu, bir algoritmanın alabileceği minimum zamanı (en iyi durum - best case) ifade eder. Algoritmanın belirli bir noktadan sonra en az ne kadar süreceğini gösterir.

**Matematiksel Tanım:**
Eğer $f(n) = \Omega(g(n))$ ise, öyle pozitif $c$ ve $n_0$ sabitleri vardır ki; tüm $n \ge n_0$ değerleri için:
$0 \le c \cdot g(n) \le f(n)$ eşitsizliği sağlanır.

**Örnek:**
Bir dizide eleman ararken, aradığımız elemanın dizinin ilk elemanı olması durumu $\Omega(1)$ çalışma zamanını ifade eder.

## 1.3. Theta ($\Theta$) Notasyonu - Sıkı Sınır (Tight Bound)

Theta notasyonu, bir algoritmanın büyüme hızının hem alt hem de üst sınırdan aynı fonksiyonla sınırlandığı durumu ifade eder. Bu, ortalama durumu veya kesin çalışma zamanını belirtmek için kullanılır.

**Matematiksel Tanım:**
Eğer $f(n) = \Theta(g(n))$ ise, öyle pozitif $c_1, c_2$ ve $n_0$ sabitleri vardır ki; tüm $n \ge n_0$ değerleri için:
$0 \le c_1 \cdot g(n) \le f(n) \le c_2 \cdot g(n)$ eşitsizliği sağlanır.

**Önemli Kural:** Bir f(n) fonksiyonu ancak ve ancak hem $O(g(n))$ hem de $\Omega(g(n))$ ise $\Theta(g(n))$ olabilir.

## 1.4. Little o ($o$) Notasyonu - Kesin Üst Sınır (Strict Upper Bound)

Big O notasyonunda $\le$ (küçük eşittir) durumu varken, Little o notasyonunda $<$ (kesin küçüktür) durumu vardır. $f(n)$ fonksiyonunun büyüme hızının, $g(n)$'den kesinlikle daha yavaş olduğunu ifade eder.

**Matematiksel Tanım:**
Her $c > 0$ sabiti için, öyle bir $n_0 > 0$ vardır ki; tüm $n \ge n_0$ için:
$0 \le f(n) < c \cdot g(n)$ eşitsizliği sağlanır.

Limit ile tanımı:
$$\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0$$

**Örnek Karşılaştırma:**
- $2n = O(n)$ doğrudur.
- $2n = o(n)$ yanlıştır (çünkü asimptotik olarak aynı hızda büyürler, kesin küçüklük yoktur).
- $2n = o(n^2)$ doğrudur.

---

## 2. Temel Büyüme Fonksiyonları (Growth Functions)

Algoritmaların karmaşıklık sınıfları, yavaştan hızlı büyüyene (yani iyi performanstan kötü performansa) doğru şu şekilde sıralanır:

1. **$O(1)$ - Sabit Zamanlı (Constant Time):** Girdi boyutundan bağımsızdır. (Örn: Bir dizinin indeksine erişmek).
2. **$O(\log n)$ - Logaritmik Zaman:** Veri setinin her adımda belirli bir oranda (genellikle yarı yarıya) bölündüğü algoritmalardır. (Örn: Binary Search).
3. **$O(n)$ - Doğrusal Zaman (Linear Time):** Girdi boyutuyla doğru orantılıdır. (Örn: Bir döngü ile diziyi taramak).
4. **$O(n \log n)$ - Doğrusal Logaritmik (Linearithmic):** Genellikle en verimli genel amaçlı sıralama algoritmalarının sınırıdır. (Örn: Merge Sort, Quick Sort).
5. **$O(n^2)$ - Karesel Zaman (Quadratic Time):** İç içe iki döngü barındıran algoritmalardır. Büyük veri setlerinde performans sorunları yaratır. (Örn: Bubble Sort, Selection Sort).
6. **$O(n^3)$ - Kübik Zaman (Cubic Time):** İç içe üç döngü barındırır. (Örn: Standart matris çarpımı).
7. **$O(2^n)$ - Üstel Zaman (Exponential Time):** Her adımda problem boyutunun katlandığı, genellikle brute-force (kaba kuvvet) yaklaşımlarıdır.
8. **$O(n!)$ - Faktöriyel Zaman (Factorial Time):** Tüm permütasyonları deneyen en yavaş algoritma sınıfıdır. (Örn: Gezgin Satıcı Probleminin kaba kuvvet çözümü).
