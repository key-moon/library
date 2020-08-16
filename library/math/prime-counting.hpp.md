---
layout: default
---

<!-- mathjax config similar to math.stackexchange -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: { equationNumbers: { autoNumber: "AMS" }},
    tex2jax: {
      inlineMath: [ ['$','$'] ],
      processEscapes: true
    },
    "HTML-CSS": { matchFontHeight: false },
    displayAlign: "left",
    displayIndent: "2em"
  });
</script>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery-balloon-js@1.1.2/jquery.balloon.min.js" integrity="sha256-ZEYs9VrgAeNuPvs15E39OsyOJaIkXEEt10fzxJ20+2I=" crossorigin="anonymous"></script>
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :x: 素数カウント <small>(math/prime-counting.hpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#7e676e9e663beb40fd133f5ee24487c2">math</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/prime-counting.hpp">View this file on GitHub</a>
    - Last commit date: 2020-08-16 16:29:52+09:00




# 素数カウント

## 素数の個数$\pi(N)$を計算する

$\pi(N)$を$\mathrm{O}\left(\frac{N^{\frac{3}{4}}}{\log N}\right)$で計算するライブラリ。

#### 概要

まず初めに、$f(x,n):=$($n$以下の自然数のうち$x$以下の素数を因数に持たない数の個数)とおく。

この時、

$\pi(N) = f(\lfloor\sqrt{N}\rfloor,N) + \pi(\lfloor\sqrt{N}\rfloor) - 1$

であり、また

$f(x,n) = f(x-1,n) \ \ \ \ \ \mathrm{(if\ x\ is\ not\ prime)}$

$f(x,n) = f(x - 1, n) - \# \{i | (i \in [1, n] \wedge x|i )\}$
$= f(x-1,n)-f(x-1,\frac{n}{x}) \ \ \ \ \ \mathrm{(if\ x\ is\ prime)}$

となるので、$x$を$\sqrt{N}$以下の素数、$n =\lfloor\frac{N}{K}\rfloor$を範囲として、$x$を大きくしていくin-placeな動的計画法で$\pi(N)$を求められる。計算量は
- $\sqrt{N}$以下の素数の個数 $\ldots$ 素数定理より$\mathrm{O}\left(\frac{\sqrt{N}}{\log N}\right)$
- DPテーブルの長さ $\ldots$ $\lfloor\frac{N}{K}\rfloor$の個数なので$\mathrm{O}(\sqrt{N})$

なので掛けて$\mathrm{O}\left(\frac{N}{\log N}\right)$となる。

さらに高速化する。$g(x,n) :=f(x,n) + \pi(\min(n,x))$とおくと、$g(x,n)$は$n$以下の数に$x$以下の素数でふるいを掛けた時に残ったもの($1$を含む)となる。ここから

$g(\lfloor\sqrt{N}\rfloor,N) = \pi(N) - 1$

であり、また$f$に代入すると

$g(x,n) = g(x-1,n) \ \ \ \ \ \mathrm{if\ x\ is\ not\ prime\ or}\ n<x^2$

$g(x,n) = g(x-1,n)-g(x-1,\lfloor\frac{n}{x}\rfloor) + \pi(x) \ \ \ \ \ \mathrm{otherwise}$

を示せる。

ほしいものは$g(x,n)-1$なので$h(x,n) = g(x,n)-1$とおいて微調整すると、

$\pi(x) = h(\lfloor\sqrt{N}\rfloor,n)$

$h(x,n) = h(x-1,n) \ \ \ \ \ \mathrm{if\ x\ is\ not\ prime\ or}\ n<x^2$

$h(x,n) = h(x-1,n)-h(x-1,\lfloor\frac{n}{x}\rfloor) + \pi(x-1) \ \ \ \ \ \mathrm{otherwise}$

となる。動的計画法での更新回数は

- $2 \leq x \leq N^{\frac{1}{4}}$のとき $\ldots$ 素数は$\mathrm{O}\left(\frac{N^{\frac{1}{4}}}{\log N}\right)$個あってDPテーブルの長さは$\mathrm{O}(\sqrt{N})$なので合計$\mathrm{O}\left(\frac{N^{\frac{3}{4}}}{\log N}\right)$回
- $N^{\frac{1}{4}} \leq x \leq \sqrt{N}$のとき 各$x$についてそれぞれ$\ldots$ $x^2< n < N$を満たす部分を更新する。$\sqrt{N} < x^2$より$n$は$\mathrm{O}\left(\frac{N}{x^2}\right)$個なので、合計$\mathrm{O}\left(\frac{1}{\log N}\int_{N^{\frac{1}{4}}}^{\sqrt{N}} \frac{N}{x^2}dx\right)=\mathrm{O}\left(\frac{N^{\frac{3}{4}}}{\log N}\right)回$

以上より全体の計算量は$\mathrm{O}\left(\frac{N^{\frac{3}{4}}}{\log N}\right)$となる。


## Verified with

* :x: <a href="../../verify/verify/verify-yosupo-math/yosupo-counting-primes.test.hpp.html">verify/verify-yosupo-math/yosupo-counting-primes.test.hpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#pragma once
#include <bits/stdc++.h>
using namespace std;

pair<vector<long long>, vector<long long>> pi_table(long long N) {
  using i64 = long long;
  vector<i64> ns{0};
  for (i64 i = N; i > 0; i = N / (N / i + 1)) ns.push_back(i);
  vector<i64> h(ns);
  for (auto &x : h) --x;
  for (i64 x = 2, sq = sqrtl(N), nsz = ns.size(); x <= sq; ++x) {
    if (h[nsz - x] == h[nsz - x + 1]) continue;
    i64 x2 = x * x, pi = h[nsz - x + 1];
    for (i64 i = 1, n = ns[i]; i < nsz && n >= x2; n = ns[++i])
      h[i] -= h[i * x <= sq ? i * x : nsz - n / x] - pi;
  }
  return {ns, h};
}

long long prime_counting(long long N) {
  if (N < 2) return 0;
  return pi_table(N).second[1];
}

/**
 * @brief 素数カウント
 * @docs docs/math/prime-counting.md
 */

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 2 "math/prime-counting.hpp"
#include <bits/stdc++.h>
using namespace std;

pair<vector<long long>, vector<long long>> pi_table(long long N) {
  using i64 = long long;
  vector<i64> ns{0};
  for (i64 i = N; i > 0; i = N / (N / i + 1)) ns.push_back(i);
  vector<i64> h(ns);
  for (auto &x : h) --x;
  for (i64 x = 2, sq = sqrtl(N), nsz = ns.size(); x <= sq; ++x) {
    if (h[nsz - x] == h[nsz - x + 1]) continue;
    i64 x2 = x * x, pi = h[nsz - x + 1];
    for (i64 i = 1, n = ns[i]; i < nsz && n >= x2; n = ns[++i])
      h[i] -= h[i * x <= sq ? i * x : nsz - n / x] - pi;
  }
  return {ns, h};
}

long long prime_counting(long long N) {
  if (N < 2) return 0;
  return pi_table(N).second[1];
}

/**
 * @brief 素数カウント
 * @docs docs/math/prime-counting.md
 */

```
{% endraw %}

<a href="../../index.html">Back to top page</a>
