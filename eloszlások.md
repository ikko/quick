### Mi az eloszlás?

Az **eloszlás** a statisztikában és a valószínűségszámításban azt írja le, hogy egy véletlenszerű változó milyen módon oszlik meg a lehetséges értékei között. Az eloszlás tehát a valószínűségeket vagy sűrűségfüggvényeket jelenti, amelyek meghatározzák, hogy egy változó adott intervallumban milyen eséllyel vesz fel egy-egy értéket. Az eloszlások segítenek abban, hogy megértsük, hogyan viselkednek a véletlenszerű folyamatok és események.

Az eloszlások lehetnek **diszkrétek**, ahol a véletlenszerű változó csak meghatározott, számolható értékeket vehet fel (pl. dobókocka eredményei), vagy **folytonosak**, ahol a változó egy intervallum bármely értékét felveheti (pl. testhőmérséklet, idő).

### A legfontosabb eloszlások

1. **Normál eloszlás (Gaussian eloszlás)**
2. **Poisson-eloszlás**
3. **Exponenciális eloszlás**
4. **Binomiális eloszlás**
5. **Gamma-eloszlás**

Most részletesebben bemutatom ezeket az eloszlásokat és a Python-ban való implementálásuk legfontosabb részleteit.

---

### 1. **Normál eloszlás (Gauss-eloszlás)**

A **normál eloszlás** az egyik legelterjedtebb és legfontosabb eloszlás, amelyet széles körben használnak a statisztikában. A normál eloszlás sűrűségfüggvénye haranggörbét (bell curve) alkot, és az alábbi tulajdonságokkal rendelkezik:
- **Paraméterek**: A normál eloszlásnak két paramétere van:
  - **µ (mu)**: A középérték (vagy átlag), amely meghatározza a görbe középpontját.
  - **σ (sigma)**: A szórás, amely a görbe szélességét jelzi, azaz azt, hogy mennyire szóródnak az adatok a középértéktől.

A normál eloszlás akkor alkalmazható, ha a mérési hibák, a fizikai jelenségek, vagy az emberi populációs jellemzők (pl. magasság) követik ezt az eloszlást.

**Matematikai képlet**:
\[
f(x) = \frac{1}{\sigma \sqrt{2\pi}} \exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)
\]

**Python implementáció** (SciPy könyvtár):

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Paraméterek
mu = 0      # Középérték
sigma = 1   # Szórás

# Adatok generálása a normál eloszlás alapján
x = np.linspace(-5, 5, 1000)
pdf = norm.pdf(x, mu, sigma)

# Ábrázolás
plt.plot(x, pdf, label='Normál eloszlás')
plt.title('Normál eloszlás (µ=0, σ=1)')
plt.xlabel('x')
plt.ylabel('sűrűség')
plt.grid(True)
plt.legend()
plt.show()
```

#### Fontos SciPy funkciók:
- `norm.pdf(x, mu, sigma)`: A normál eloszlás sűrűségfüggvénye (PDF) \(x\) pontban.
- `norm.cdf(x, mu, sigma)`: A normál eloszlás kumulatív eloszlásfüggvénye (CDF) \(x\) pontban.
- `norm.rvs(mu, sigma, size=n)`: Véletlen mintát generál a normál eloszlásból.

---

### 2. **Poisson-eloszlás**

A **Poisson-eloszlás** egy diszkrét eloszlás, amely a ritka események számát modellezi egy adott időintervallumban. Ezt az eloszlást gyakran használják például balesetek, telefonhívások vagy egyéb események előrejelzésére, amelyek függetlenek és egyenletes eloszlásúak egy meghatározott időszak alatt.

**Matematikai képlet**:
\[
P(k;\lambda) = \frac{\lambda^k e^{-\lambda}}{k!}
\]
ahol \(\lambda\) az események várható száma egy időszakban, és \(k\) az események tényleges száma.

**Python implementáció** (SciPy könyvtár):

```python
from scipy.stats import poisson

# Paraméterek
lambda_poisson = 3  # Várható események száma

# Diszkrét Poisson-eloszlás
k = np.arange(0, 10)
pmf = poisson.pmf(k, lambda_poisson)

# Ábrázolás
plt.vlines(k, 0, pmf, colors='b', label="Poisson PMF")
plt.plot(k, pmf, 'bo', ms=8)
plt.title('Poisson-eloszlás (λ=3)')
plt.xlabel('Események száma (k)')
plt.ylabel('Valószínűség')
plt.grid(True)
plt.legend()
plt.show()
```

#### Fontos SciPy funkciók:
- `poisson.pmf(k, mu)`: A Poisson-eloszlás valószínűségi tömegfüggvénye (PMF) \(k\)-ra.
- `poisson.cdf(k, mu)`: A Poisson-eloszlás kumulatív eloszlásfüggvénye (CDF) \(k\)-ra.
- `poisson.rvs(mu, size=n)`: Véletlen mintát generál a Poisson-eloszlásból.

---

### 3. **Exponenciális eloszlás**

Az **exponenciális eloszlás** egy folytonos eloszlás, amely gyakran alkalmazható a "várakozási idők" modellezésére, például telefonhívások közötti idő, vagy az első baleset várható ideje.

**Matematikai képlet**:
\[
f(x;\lambda) = \lambda e^{-\lambda x}
\]
ahol \(\lambda\) az események gyakorisága.

**Python implementáció** (SciPy könyvtár):

```python
from scipy.stats import expon

# Paraméterek
lambda_expon = 1  # Az események gyakorisága

# Exponenciális eloszlás
x = np.linspace(0, 5, 1000)
pdf = expon.pdf(x, scale=1/lambda_expon)

# Ábrázolás
plt.plot(x, pdf, label='Exponenciális eloszlás')
plt.title('Exponenciális eloszlás (λ=1)')
plt.xlabel('x')
plt.ylabel('sűrűség')
plt.grid(True)
plt.legend()
plt.show()
```

#### Fontos SciPy funkciók:
- `expon.pdf(x, scale)`: Az exponenciális eloszlás sűrűségfüggvénye (PDF).
- `expon.cdf(x, scale)`: Az exponenciális eloszlás kumulatív eloszlásfüggvénye (CDF).
- `expon.rvs(scale, size=n)`: Véletlen mintát generál az exponenciális eloszlásból.

---

### 4. **Binomiális eloszlás**

A **binomiális eloszlás** diszkrét eloszlás, amely a sikeres események számát modellezi egy meghatározott számú próbálkozás esetén. Két paramétert igényel:
- **n**: A próbálkozások száma.
- **p**: A sikeres események valószínűsége.

**Matematikai képlet**:
\[
P(X = k) = \binom{n}{k} p^k (1 - p)^{n-k}
\]

**Python implementáció** (SciPy könyvtár):

```python
from scipy.stats import binom

# Paraméterek
n = 10  # Próbálkozások száma
p = 0.5  # Siker valószínűsége

# Binomiális eloszlás
k = np.arange(0, n+1)
pmf = binom.pmf(k, n, p)

# Ábrázolás
plt.vlines(k, 0, pmf, colors='g', label="Binomiális PMF")
plt.plot(k, pmf, 'go', ms=8)
plt.title('Binomiális eloszlás (n=10, p=0.5)')
plt.xlabel('Sikeres próbálkozások (k)')
plt.ylabel('Valószínűség')
plt.grid(True)
plt.legend()
plt.show()
```

#### Fontos SciPy funkciók:
- `binom.pmf(k, n, p)`: A binomiális eloszlás PMF-jét számítja ki.
- `binom.cdf(k, n, p)`: A binomiális eloszlás CDF-jét számítja ki.
- `binom.rvs(n, p, size=n)`: Véletlen mintát generál a binomiális eloszlásból.

---

### 5. **Gamma-eloszlás**

A **Gamma-eloszlás** egy folytonos eloszlás, amely a Poisson-eloszlás és az exponenciális eloszlás általánosítása. Két paraméterrel rendelkezik:
- **α (alpha)**: A formátum paraméter.
- **β (beta)**: A skálázási paraméter.

**Matematikai képlet**:
\[
f(x; \alpha, \beta) = \frac{x^{\alpha-1} e^{-x/\beta}}{\beta^\alpha \Gamma(\alpha)}
\]

**Python implementáció** (SciPy könyvtár):

```python
from scipy.stats import gamma

# Paraméterek
alpha = 2  # Forma paraméter
beta = 2   # Skála paraméter

# Gamma-eloszlás
x = np.linspace(0, 10, 1000)
pdf = gamma.pdf(x, alpha, scale=beta)

# Ábrázolás
plt.plot(x, pdf, label='Gamma eloszlás')
plt.title('Gamma-eloszlás (α=2, β=2)')
plt.xlabel('x')
plt.ylabel('sűrűség')
plt.grid(True)
plt.legend()
plt.show()
```

#### Fontos SciPy funkciók:
- `gamma.pdf(x, alpha, scale)`: A Gamma-eloszlás sűrűségfüggvénye.
- `gamma.cdf(x, alpha, scale)`: A Gamma-eloszlás kumulatív eloszlásfüggvénye.
- `gamma.rvs(alpha, scale, size=n)`: Véletlen mintát generál a Gamma-eloszlásból.

---

### Összegzés

A fenti eloszlások mind fontos szerepet játszanak különböző statisztikai elemzésekben és valószínűségi modellekben. A **SciPy** könyvtár segítségével könnyen implementálhatók és vizualizálhatók Python-ban. Az egyes eloszlások és azok paramétereinek helyes használata segít megérteni a valószínűségi folyamatokat és segít a különböző gyakorlati problémák modellezésében.
