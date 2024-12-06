# Lineer Regresyona Giriş ve Uygulama Rehberi

Bu repo, temel bir lineer regresyon modelinin ne olduğunu, nasıl kurulduğunu ve Python ile nasıl uygulanabileceğini anlatan bir rehber niteliğindedir. Hem teorik arka plan hem de pratik örnekler sunularak lineer regresyona yeni başlayanların bu konuyu anlamasına yardımcı olmayı amaçlamaktadır.

## İçindekiler

- [Lineer Regresyon Nedir?](#lineer-regresyon-nedir)
- [Matematiksel Temel](#matematiksel-temel)
- [Varsayımlar](#varsayımlar)
- [Python Örneği](#python-örneği)
- [İleri Okumalar ve Kaynaklar](#ileri-okumalar-ve-kaynaklar)
- [GitHub Üzerinde Projenizi Geliştirme İpuçları](#github-üzerinde-projenizi-geliştirme-ipuçları)

---

## Lineer Regresyon Nedir?

**Lineer regresyon**, bir bağımlı değişken (çıktı) ile bir veya birden fazla bağımsız değişken (girdi) arasındaki ilişkiyi doğrusal bir modelle açıklamaya çalışan istatistiksel bir tekniktir. Temel hali olan **Basit Doğrusal Regresyon**, tek bir bağımsız değişkenin (x) bağımlı değişken (y) üzerindeki etkisini modelleyerek şu formu alır:

\[
y \approx \beta_0 + \beta_1 x
\]

Burada:
- \(\beta_0\): Sabit terim (intercept),
- \(\beta_1\): Eğim (slope),
- \(y\): Çıktı değeri,
- \(x\): Giriş değeri.

Amaç, veri noktalarına (x,y) en iyi uyan doğruyu bulmaktır.

## Matematiksel Temel

Veri kümesi \((x_1, y_1), (x_2, y_2), \dots, (x_n, y_n)\) olsun. Amaç, hata terimlerinin karelerinin toplamını minimize etmektir:

\[
S(\beta_0,\beta_1) = \sum_{i=1}^{n}(y_i - (\beta_0+\beta_1x_i))^2.
\]

Bu fonksiyonu minimize etmek için türevler alınır ve sıfıra eşitlenir. Sonuçta elde edilen kapalı form çözümler:

\[
\beta_1 = \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^n (x_i - \bar{x})^2}, \quad \beta_0 = \bar{y} - \beta_1\bar{x}.
\]

Burada \(\bar{x}\) ve \(\bar{y}\) sırasıyla x ve y verilerinin ortalamalarıdır.

## Varsayımlar

Lineer regresyon modeli için bazı temel varsayımlar vardır:

1. **Doğrusallık:** Y ile X arasında doğrusal bir ilişki.
2. **Hataların Normal Dağılımı:** Hata terimlerinin ortalamalarının 0 olması ve yaklaşık normal dağılması.
3. **Sabit Varyans (Homoskedastisite):** Hata terimlerinin varyansının sabit olması.
4. **Bağımsızlık:** Hataların birbirinden bağımsız olması.

Bu varsayımların büyük ölçüde sağlanması modelin güvenilirliğini arttırır.

## Python Örneği

Aşağıdaki örnek, basit bir veri seti oluşturarak lineer regresyon katsayılarını hesaplamaktadır.

```python
import numpy as np
import matplotlib.pyplot as plt

# Örnek veri oluşturma
x = np.linspace(0, 10, 20)
y = 3*x + 2 + np.random.randn(20)*2  # Gerçek model y = 3x + 2 + gürültü

# Parametrelerin hesaplanması
x_mean = np.mean(x)
y_mean = np.mean(y)

beta_1 = np.sum((x - x_mean)*(y - y_mean)) / np.sum((x - x_mean)**2)
beta_0 = y_mean - beta_1*x_mean

# Tahmin edilen model
y_pred = beta_0 + beta_1*x

# Sonuçların görselleştirilmesi
plt.scatter(x, y, label='Veri Noktaları')
plt.plot(x, y_pred, color='red', label='Lineer Model')
plt.xlabel('x')
plt.ylabel('y')
plt.title('Basit Doğrusal Regresyon Örneği')
plt.legend()
plt.grid(True)
plt.show()

print("Beta_0:", beta_0)
print("Beta_1:", beta_1)
