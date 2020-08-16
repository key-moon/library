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


# :heavy_check_mark: modint/simd-montgomery.hpp

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#fb97f878c938d7517d3d9f7de68146e9">modint</a>
* <a href="{{ site.github.repository_url }}/blob/master/modint/simd-montgomery.hpp">View this file on GitHub</a>
    - Last commit date: 2020-07-28 11:29:32+09:00




## Required by

* :heavy_check_mark: <a href="../fps/arbitrary-fps.hpp.html">fps/arbitrary-fps.hpp</a>
* :heavy_check_mark: <a href="../fps/ntt-friendly-fps.hpp.html">fps/ntt-friendly-fps.hpp</a>
* :heavy_check_mark: <a href="../modulo/gauss-elimination.hpp.html">modulo/gauss-elimination.hpp</a>
* :heavy_check_mark: <a href="../ntt/arbitrary-ntt.hpp.html">ntt/arbitrary-ntt.hpp</a>
* :heavy_check_mark: <a href="../ntt/ntt-avx2.hpp.html">ntt/ntt-avx2.hpp</a>
* :heavy_check_mark: <a href="../ntt/ntt-sse42.hpp.html">ntt/ntt-sse42.hpp</a>
* :heavy_check_mark: <a href="../tree/frequency-table-of-tree-distance.hpp.html">tree/frequency-table-of-tree-distance.hpp</a>


## Verified with

* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-composition.test.cpp.html">verify/verify-yosupo-fps/yosupo-composition.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-exp-arb.test.cpp.html">verify/verify-yosupo-fps/yosupo-exp-arb.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-exp.test.cpp.html">verify/verify-yosupo-fps/yosupo-exp.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-interpolation.test.cpp.html">verify/verify-yosupo-fps/yosupo-interpolation.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-inv-arb.test.cpp.html">verify/verify-yosupo-fps/yosupo-inv-arb.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-inv.test.cpp.html">verify/verify-yosupo-fps/yosupo-inv.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-log-arb.test.cpp.html">verify/verify-yosupo-fps/yosupo-log-arb.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-log.test.cpp.html">verify/verify-yosupo-fps/yosupo-log.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-multieval.test.cpp.html">verify/verify-yosupo-fps/yosupo-multieval.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-pow-arb.test.cpp.html">verify/verify-yosupo-fps/yosupo-pow-arb.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-pow.test.cpp.html">verify/verify-yosupo-fps/yosupo-pow.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-sqrt.test.cpp.html">verify/verify-yosupo-fps/yosupo-sqrt.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-fps/yosupo-taylor-shift.test.cpp.html">verify/verify-yosupo-fps/yosupo-taylor-shift.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-graph/yosupo-frequency-table-of-tree-distance.test.cpp.html">verify/verify-yosupo-graph/yosupo-frequency-table-of-tree-distance.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-math/yosupo-determinant.test.cpp.html">verify/verify-yosupo-math/yosupo-determinant.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-math/yosupo-linear-equation.test.cpp.html">verify/verify-yosupo-math/yosupo-linear-equation.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-math/yosupo-sparse-determinant.test.cpp.html">verify/verify-yosupo-math/yosupo-sparse-determinant.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-ntt/yosupo-convolution-arbitraryntt-arbitrarymodint.test.cpp.html">verify/verify-yosupo-ntt/yosupo-convolution-arbitraryntt-arbitrarymodint.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-ntt/yosupo-convolution-arbitraryntt-arbitraryprimemodint.test.cpp.html">verify/verify-yosupo-ntt/yosupo-convolution-arbitraryntt-arbitraryprimemodint.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-ntt/yosupo-convolution-arbitraryntt.test.cpp.html">verify/verify-yosupo-ntt/yosupo-convolution-arbitraryntt.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-ntt/yosupo-convolution-ntt-avx2.test.cpp.html">verify/verify-yosupo-ntt/yosupo-convolution-ntt-avx2.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-ntt/yosupo-convolution-ntt-sse42.test.cpp.html">verify/verify-yosupo-ntt/yosupo-convolution-ntt-sse42.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-ntt/yosupo-inliner-multiply.test.cpp.html">verify/verify-yosupo-ntt/yosupo-inliner-multiply.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yuki/yuki-0214.test.cpp.html">verify/verify-yuki/yuki-0214.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yuki/yuki-0215.test.cpp.html">verify/verify-yuki/yuki-0215.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yuki/yuki-0963-circular.test.cpp.html">verify/verify-yuki/yuki-0963-circular.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yuki/yuki-0963.test.cpp.html">verify/verify-yuki/yuki-0963.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yuki/yuki-1080.test.cpp.html">verify/verify-yuki/yuki-1080.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yuki/yuki-1145.test.cpp.html">verify/verify-yuki/yuki-1145.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#pragma once
#include <bits/stdc++.h>
using namespace std;
#include <immintrin.h>

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
my128_mullo_epu32(const __m128i &a, const __m128i &b) {
  return _mm_mullo_epi32(a, b);
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
my128_mulhi_epu32(const __m128i &a, const __m128i &b) {
  __m128i a13 = _mm_shuffle_epi32(a, 0xF5);
  __m128i b13 = _mm_shuffle_epi32(b, 0xF5);
  __m128i prod02 = _mm_mul_epu32(a, b);
  __m128i prod13 = _mm_mul_epu32(a13, b13);
  __m128i prod = _mm_unpackhi_epi64(_mm_unpacklo_epi32(prod02, prod13),
                                    _mm_unpackhi_epi32(prod02, prod13));
  return prod;
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
montgomery_mul_128(const __m128i &a, const __m128i &b, const __m128i &r,
                   const __m128i &m1) {
  return _mm_sub_epi32(
      _mm_add_epi32(my128_mulhi_epu32(a, b), m1),
      my128_mulhi_epu32(my128_mullo_epu32(my128_mullo_epu32(a, b), r), m1));
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
montgomery_add_128(const __m128i &a, const __m128i &b, const __m128i &m2,
                   const __m128i &m0) {
  __m128i ret = _mm_sub_epi32(_mm_add_epi32(a, b), m2);
  return _mm_add_epi32(_mm_and_si128(_mm_cmpgt_epi32(m0, ret), m2), ret);
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
montgomery_sub_128(const __m128i &a, const __m128i &b, const __m128i &m2,
                   const __m128i &m0) {
  __m128i ret = _mm_sub_epi32(a, b);
  return _mm_add_epi32(_mm_and_si128(_mm_cmpgt_epi32(m0, ret), m2), ret);
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
my256_mullo_epu32(const __m256i &a, const __m256i &b) {
  return _mm256_mullo_epi32(a, b);
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
my256_mulhi_epu32(const __m256i &a, const __m256i &b) {
  __m256i a13 = _mm256_shuffle_epi32(a, 0xF5);
  __m256i b13 = _mm256_shuffle_epi32(b, 0xF5);
  __m256i prod02 = _mm256_mul_epu32(a, b);
  __m256i prod13 = _mm256_mul_epu32(a13, b13);
  __m256i prod = _mm256_unpackhi_epi64(_mm256_unpacklo_epi32(prod02, prod13),
                                       _mm256_unpackhi_epi32(prod02, prod13));
  return prod;
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
montgomery_mul_256(const __m256i &a, const __m256i &b, const __m256i &r,
                   const __m256i &m1) {
  return _mm256_sub_epi32(
      _mm256_add_epi32(my256_mulhi_epu32(a, b), m1),
      my256_mulhi_epu32(my256_mullo_epu32(my256_mullo_epu32(a, b), r), m1));
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
montgomery_add_256(const __m256i &a, const __m256i &b, const __m256i &m2,
                   const __m256i &m0) {
  __m256i ret = _mm256_sub_epi32(_mm256_add_epi32(a, b), m2);
  return _mm256_add_epi32(_mm256_and_si256(_mm256_cmpgt_epi32(m0, ret), m2),
                          ret);
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
montgomery_sub_256(const __m256i &a, const __m256i &b, const __m256i &m2,
                   const __m256i &m0) {
  __m256i ret = _mm256_sub_epi32(a, b);
  return _mm256_add_epi32(_mm256_and_si256(_mm256_cmpgt_epi32(m0, ret), m2),
                          ret);
}
```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 2 "modint/simd-montgomery.hpp"
#include <bits/stdc++.h>
using namespace std;
#line 5 "modint/simd-montgomery.hpp"

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
my128_mullo_epu32(const __m128i &a, const __m128i &b) {
  return _mm_mullo_epi32(a, b);
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
my128_mulhi_epu32(const __m128i &a, const __m128i &b) {
  __m128i a13 = _mm_shuffle_epi32(a, 0xF5);
  __m128i b13 = _mm_shuffle_epi32(b, 0xF5);
  __m128i prod02 = _mm_mul_epu32(a, b);
  __m128i prod13 = _mm_mul_epu32(a13, b13);
  __m128i prod = _mm_unpackhi_epi64(_mm_unpacklo_epi32(prod02, prod13),
                                    _mm_unpackhi_epi32(prod02, prod13));
  return prod;
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
montgomery_mul_128(const __m128i &a, const __m128i &b, const __m128i &r,
                   const __m128i &m1) {
  return _mm_sub_epi32(
      _mm_add_epi32(my128_mulhi_epu32(a, b), m1),
      my128_mulhi_epu32(my128_mullo_epu32(my128_mullo_epu32(a, b), r), m1));
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
montgomery_add_128(const __m128i &a, const __m128i &b, const __m128i &m2,
                   const __m128i &m0) {
  __m128i ret = _mm_sub_epi32(_mm_add_epi32(a, b), m2);
  return _mm_add_epi32(_mm_and_si128(_mm_cmpgt_epi32(m0, ret), m2), ret);
}

__attribute__((target("sse4.2"))) __attribute__((always_inline)) __m128i
montgomery_sub_128(const __m128i &a, const __m128i &b, const __m128i &m2,
                   const __m128i &m0) {
  __m128i ret = _mm_sub_epi32(a, b);
  return _mm_add_epi32(_mm_and_si128(_mm_cmpgt_epi32(m0, ret), m2), ret);
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
my256_mullo_epu32(const __m256i &a, const __m256i &b) {
  return _mm256_mullo_epi32(a, b);
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
my256_mulhi_epu32(const __m256i &a, const __m256i &b) {
  __m256i a13 = _mm256_shuffle_epi32(a, 0xF5);
  __m256i b13 = _mm256_shuffle_epi32(b, 0xF5);
  __m256i prod02 = _mm256_mul_epu32(a, b);
  __m256i prod13 = _mm256_mul_epu32(a13, b13);
  __m256i prod = _mm256_unpackhi_epi64(_mm256_unpacklo_epi32(prod02, prod13),
                                       _mm256_unpackhi_epi32(prod02, prod13));
  return prod;
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
montgomery_mul_256(const __m256i &a, const __m256i &b, const __m256i &r,
                   const __m256i &m1) {
  return _mm256_sub_epi32(
      _mm256_add_epi32(my256_mulhi_epu32(a, b), m1),
      my256_mulhi_epu32(my256_mullo_epu32(my256_mullo_epu32(a, b), r), m1));
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
montgomery_add_256(const __m256i &a, const __m256i &b, const __m256i &m2,
                   const __m256i &m0) {
  __m256i ret = _mm256_sub_epi32(_mm256_add_epi32(a, b), m2);
  return _mm256_add_epi32(_mm256_and_si256(_mm256_cmpgt_epi32(m0, ret), m2),
                          ret);
}

__attribute__((target("avx2"))) __attribute__((always_inline)) __m256i
montgomery_sub_256(const __m256i &a, const __m256i &b, const __m256i &m2,
                   const __m256i &m0) {
  __m256i ret = _mm256_sub_epi32(a, b);
  return _mm256_add_epi32(_mm256_and_si256(_mm256_cmpgt_epi32(m0, ret), m2),
                          ret);
}

```
{% endraw %}

<a href="../../index.html">Back to top page</a>
