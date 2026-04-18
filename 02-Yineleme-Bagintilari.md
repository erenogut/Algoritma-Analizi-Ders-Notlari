# 2. Yineleme Bağıntıları (Recurrence Relations)

Özyinelemeli (recursive) algoritmaların çalışma zamanı asimptotik notasyonlarla doğrudan ifade edilemez. Bu algoritmaların zaman karmaşıklığını ($T(n)$) bulmak için yineleme bağıntılarının çözülmesi gerekir. Bu bölümde en yaygın iki çözüm yöntemini inceleyeceğiz: Telescoping (Yerine Koyma/Genişletme) ve Master Theorem (Ana Teorem).

## 2.1. Telescoping Yöntemi (Substitution / Expansion Method)

Telescoping yöntemi, yineleme bağıntısını adım adım açarak ve fonksiyonun önceki değerlerini yerine koyarak bir örüntü yakalama ve bu örüntüyü genel bir toplama formülüne dönüştürme işlemidir. Genellikle her adımda problemin boyutunun sabit bir miktar azaldığı durumlarda kullanılır.

**Çözüm Adımları:**
1. Bağıntı $T(n)$ cinsinden yazılır.
2. $T(n-1)$, $T(n-2)$ vb. terimler denklemde yerine konarak genişletilir.
3. Denklem temel duruma (base case, genellikle $T(1)$) ulaşana kadar $k$ adım için genelleştirilir.
4. Elde edilen seri toplamı asimptotik olarak ifade edilir.

**Örnek Çözüm:**
Algoritmamızın yineleme bağıntısı şu olsun: $T(n) = T(n-1) + c$ ve $T(1) = 1$

Genişletme adımları:
$T(n) = T(n-1) + c$
$T(n) = [T(n-2) + c] + c = T(n-2) + 2c$
$T(n) = [T(n-3) + c] + 2c = T(n-3) + 3c$

$k$ adım sonrası genel form:
$T(n) = T(n-k) + k \cdot c$

Temel duruma ulaşmak için $n-k = 1 \implies k = n-1$ seçilir:
$T(n) = T(1) + (n-1) \cdot c$
$T(n) = 1 + cn - c$

En büyük dereceli terim $n$ olduğu için sonuç:
$T(n) = \Theta(n)$

---

## 2.2. Master Theorem (Ana Teorem)

Master Theorem, problemin her adımda belirli bir oranda alt problemlere bölündüğü "Böl ve Fethet" (Divide and Conquer) algoritmalarının karmaşıklığını çözmek için kullanılan hazır bir formüldür.

**Standart Form:**
$$T(n) = aT\left(\frac{n}{b}\right) + f(n)$$

Burada:
- $n$: Problemin giriş boyutu.
- $a$: Her adımda oluşan alt problem sayısı ($a \ge 1$).
- $b$: Her bir alt problemin orijinal probleme göre ne oranda küçüldüğü ($b > 1$).
- $f(n)$: Problemi bölmek ve alt çözümleri birleştirmek için gereken maliyet.

### Master Theorem'in 3 Temel Durumu (Cases)

Teorem, $f(n)$ fonksiyonunun büyüme hızını, $n^{\log_b a}$ (alt problemlerin toplam maliyeti) değeri ile karşılaştırarak üç farklı durum tanımlar.

**Durum 1: Alt problemlerin maliyeti baskınsa**
Eğer bir $\epsilon > 0$ sabiti için $f(n) = O\left(n^{\log_b a - \epsilon}\right)$ ise:
$$T(n) = \Theta\left(n^{\log_b a}\right)$$
*Örnek:* $T(n) = 9T(n/3) + n$. Burada $a=9, b=3, f(n)=n$. $n^{\log_3 9} = n^2$. $n < n^2$ olduğu için Durum 1 geçerlidir ve sonuç $\Theta(n^2)$ olur.

**Durum 2: Bölme/Birleştirme maliyeti ile alt problem maliyeti eşitse**
Eğer $f(n) = \Theta\left(n^{\log_b a}\right)$ ise:
$$T(n) = \Theta\left(n^{\log_b a} \log n\right)$$
*Örnek:* $T(n) = 2T(n/2) + O(n)$ (Merge Sort). Burada $a=2, b=2, f(n)=n$. $n^{\log_2 2} = n^1$. İki taraf eşit olduğu için Durum 2 geçerlidir ve sonuç $\Theta(n \log n)$ olur.

**Durum 3: Bölme/Birleştirme maliyeti baskınsa**
Eğer bir $\epsilon > 0$ sabiti için $f(n) = \Omega\left(n^{\log_b a + \epsilon}\right)$ ve düzenlilik şartı ($a \cdot f(n/b) \le c \cdot f(n)$, $c < 1$) sağlanıyorsa:
$$T(n) = \Theta(f(n))$$
*Örnek:* $T(n) = 3T(n/4) + n \log n$. Burada $a=3, b=4, f(n)=n \log n$. $n^{\log_4 3} \approx n^{0.79}$. $n \log n$ fonksiyonu daha hızlı büyüdüğü için Durum 3 geçerlidir ve sonuç $\Theta(n \log n)$ olur.
