---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: modint/montgomery-modint.hpp
    title: modint/montgomery-modint.hpp
  - icon: ':heavy_check_mark:'
    path: ntt/ntt.hpp
    title: ntt/ntt.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: verify/verify-yuki/yuki-2231.test.cpp
    title: verify/verify-yuki/yuki-2231.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: Wildcard Pattern Matching
    links: []
  bundledCode: "#line 2 \"string/wildcard-pattern-matching.hpp\"\n\n#include <vector>\n\
    using namespace std;\n\n#line 2 \"modint/montgomery-modint.hpp\"\n\n\n\ntemplate\
    \ <uint32_t mod>\nstruct LazyMontgomeryModInt {\n  using mint = LazyMontgomeryModInt;\n\
    \  using i32 = int32_t;\n  using u32 = uint32_t;\n  using u64 = uint64_t;\n\n\
    \  static constexpr u32 get_r() {\n    u32 ret = mod;\n    for (i32 i = 0; i <\
    \ 4; ++i) ret *= 2 - mod * ret;\n    return ret;\n  }\n\n  static constexpr u32\
    \ r = get_r();\n  static constexpr u32 n2 = -u64(mod) % mod;\n  static_assert(r\
    \ * mod == 1, \"invalid, r * mod != 1\");\n  static_assert(mod < (1 << 30), \"\
    invalid, mod >= 2 ^ 30\");\n  static_assert((mod & 1) == 1, \"invalid, mod % 2\
    \ == 0\");\n\n  u32 a;\n\n  constexpr LazyMontgomeryModInt() : a(0) {}\n  constexpr\
    \ LazyMontgomeryModInt(const int64_t &b)\n      : a(reduce(u64(b % mod + mod)\
    \ * n2)){};\n\n  static constexpr u32 reduce(const u64 &b) {\n    return (b +\
    \ u64(u32(b) * u32(-r)) * mod) >> 32;\n  }\n\n  constexpr mint &operator+=(const\
    \ mint &b) {\n    if (i32(a += b.a - 2 * mod) < 0) a += 2 * mod;\n    return *this;\n\
    \  }\n\n  constexpr mint &operator-=(const mint &b) {\n    if (i32(a -= b.a) <\
    \ 0) a += 2 * mod;\n    return *this;\n  }\n\n  constexpr mint &operator*=(const\
    \ mint &b) {\n    a = reduce(u64(a) * b.a);\n    return *this;\n  }\n\n  constexpr\
    \ mint &operator/=(const mint &b) {\n    *this *= b.inverse();\n    return *this;\n\
    \  }\n\n  constexpr mint operator+(const mint &b) const { return mint(*this) +=\
    \ b; }\n  constexpr mint operator-(const mint &b) const { return mint(*this) -=\
    \ b; }\n  constexpr mint operator*(const mint &b) const { return mint(*this) *=\
    \ b; }\n  constexpr mint operator/(const mint &b) const { return mint(*this) /=\
    \ b; }\n  constexpr bool operator==(const mint &b) const {\n    return (a >= mod\
    \ ? a - mod : a) == (b.a >= mod ? b.a - mod : b.a);\n  }\n  constexpr bool operator!=(const\
    \ mint &b) const {\n    return (a >= mod ? a - mod : a) != (b.a >= mod ? b.a -\
    \ mod : b.a);\n  }\n  constexpr mint operator-() const { return mint() - mint(*this);\
    \ }\n\n  constexpr mint pow(u64 n) const {\n    mint ret(1), mul(*this);\n   \
    \ while (n > 0) {\n      if (n & 1) ret *= mul;\n      mul *= mul;\n      n >>=\
    \ 1;\n    }\n    return ret;\n  }\n  \n  constexpr mint inverse() const { return\
    \ pow(mod - 2); }\n\n  friend ostream &operator<<(ostream &os, const mint &b)\
    \ {\n    return os << b.get();\n  }\n\n  friend istream &operator>>(istream &is,\
    \ mint &b) {\n    int64_t t;\n    is >> t;\n    b = LazyMontgomeryModInt<mod>(t);\n\
    \    return (is);\n  }\n  \n  constexpr u32 get() const {\n    u32 ret = reduce(a);\n\
    \    return ret >= mod ? ret - mod : ret;\n  }\n\n  static constexpr u32 get_mod()\
    \ { return mod; }\n};\n#line 2 \"ntt/ntt.hpp\"\n\ntemplate <typename mint>\nstruct\
    \ NTT {\n  static constexpr uint32_t get_pr() {\n    uint32_t _mod = mint::get_mod();\n\
    \    using u64 = uint64_t;\n    u64 ds[32] = {};\n    int idx = 0;\n    u64 m\
    \ = _mod - 1;\n    for (u64 i = 2; i * i <= m; ++i) {\n      if (m % i == 0) {\n\
    \        ds[idx++] = i;\n        while (m % i == 0) m /= i;\n      }\n    }\n\
    \    if (m != 1) ds[idx++] = m;\n\n    uint32_t _pr = 2;\n    while (1) {\n  \
    \    int flg = 1;\n      for (int i = 0; i < idx; ++i) {\n        u64 a = _pr,\
    \ b = (_mod - 1) / ds[i], r = 1;\n        while (b) {\n          if (b & 1) r\
    \ = r * a % _mod;\n          a = a * a % _mod;\n          b >>= 1;\n        }\n\
    \        if (r == 1) {\n          flg = 0;\n          break;\n        }\n    \
    \  }\n      if (flg == 1) break;\n      ++_pr;\n    }\n    return _pr;\n  };\n\
    \n  static constexpr uint32_t mod = mint::get_mod();\n  static constexpr uint32_t\
    \ pr = get_pr();\n  static constexpr int level = __builtin_ctzll(mod - 1);\n \
    \ mint dw[level], dy[level];\n\n  void setwy(int k) {\n    mint w[level], y[level];\n\
    \    w[k - 1] = mint(pr).pow((mod - 1) / (1 << k));\n    y[k - 1] = w[k - 1].inverse();\n\
    \    for (int i = k - 2; i > 0; --i)\n      w[i] = w[i + 1] * w[i + 1], y[i] =\
    \ y[i + 1] * y[i + 1];\n    dw[1] = w[1], dy[1] = y[1], dw[2] = w[2], dy[2] =\
    \ y[2];\n    for (int i = 3; i < k; ++i) {\n      dw[i] = dw[i - 1] * y[i - 2]\
    \ * w[i];\n      dy[i] = dy[i - 1] * w[i - 2] * y[i];\n    }\n  }\n\n  NTT() {\
    \ setwy(level); }\n\n  void fft4(vector<mint> &a, int k) {\n    if ((int)a.size()\
    \ <= 1) return;\n    if (k == 1) {\n      mint a1 = a[1];\n      a[1] = a[0] -\
    \ a[1];\n      a[0] = a[0] + a1;\n      return;\n    }\n    if (k & 1) {\n   \
    \   int v = 1 << (k - 1);\n      for (int j = 0; j < v; ++j) {\n        mint ajv\
    \ = a[j + v];\n        a[j + v] = a[j] - ajv;\n        a[j] += ajv;\n      }\n\
    \    }\n    int u = 1 << (2 + (k & 1));\n    int v = 1 << (k - 2 - (k & 1));\n\
    \    mint one = mint(1);\n    mint imag = dw[1];\n    while (v) {\n      // jh\
    \ = 0\n      {\n        int j0 = 0;\n        int j1 = v;\n        int j2 = j1\
    \ + v;\n        int j3 = j2 + v;\n        for (; j0 < v; ++j0, ++j1, ++j2, ++j3)\
    \ {\n          mint t0 = a[j0], t1 = a[j1], t2 = a[j2], t3 = a[j3];\n        \
    \  mint t0p2 = t0 + t2, t1p3 = t1 + t3;\n          mint t0m2 = t0 - t2, t1m3 =\
    \ (t1 - t3) * imag;\n          a[j0] = t0p2 + t1p3, a[j1] = t0p2 - t1p3;\n   \
    \       a[j2] = t0m2 + t1m3, a[j3] = t0m2 - t1m3;\n        }\n      }\n      //\
    \ jh >= 1\n      mint ww = one, xx = one * dw[2], wx = one;\n      for (int jh\
    \ = 4; jh < u;) {\n        ww = xx * xx, wx = ww * xx;\n        int j0 = jh *\
    \ v;\n        int je = j0 + v;\n        int j2 = je + v;\n        for (; j0 <\
    \ je; ++j0, ++j2) {\n          mint t0 = a[j0], t1 = a[j0 + v] * xx, t2 = a[j2]\
    \ * ww,\n               t3 = a[j2 + v] * wx;\n          mint t0p2 = t0 + t2, t1p3\
    \ = t1 + t3;\n          mint t0m2 = t0 - t2, t1m3 = (t1 - t3) * imag;\n      \
    \    a[j0] = t0p2 + t1p3, a[j0 + v] = t0p2 - t1p3;\n          a[j2] = t0m2 + t1m3,\
    \ a[j2 + v] = t0m2 - t1m3;\n        }\n        xx *= dw[__builtin_ctzll((jh +=\
    \ 4))];\n      }\n      u <<= 2;\n      v >>= 2;\n    }\n  }\n\n  void ifft4(vector<mint>\
    \ &a, int k) {\n    if ((int)a.size() <= 1) return;\n    if (k == 1) {\n     \
    \ mint a1 = a[1];\n      a[1] = a[0] - a[1];\n      a[0] = a[0] + a1;\n      return;\n\
    \    }\n    int u = 1 << (k - 2);\n    int v = 1;\n    mint one = mint(1);\n \
    \   mint imag = dy[1];\n    while (u) {\n      // jh = 0\n      {\n        int\
    \ j0 = 0;\n        int j1 = v;\n        int j2 = v + v;\n        int j3 = j2 +\
    \ v;\n        for (; j0 < v; ++j0, ++j1, ++j2, ++j3) {\n          mint t0 = a[j0],\
    \ t1 = a[j1], t2 = a[j2], t3 = a[j3];\n          mint t0p1 = t0 + t1, t2p3 = t2\
    \ + t3;\n          mint t0m1 = t0 - t1, t2m3 = (t2 - t3) * imag;\n          a[j0]\
    \ = t0p1 + t2p3, a[j2] = t0p1 - t2p3;\n          a[j1] = t0m1 + t2m3, a[j3] =\
    \ t0m1 - t2m3;\n        }\n      }\n      // jh >= 1\n      mint ww = one, xx\
    \ = one * dy[2], yy = one;\n      u <<= 2;\n      for (int jh = 4; jh < u;) {\n\
    \        ww = xx * xx, yy = xx * imag;\n        int j0 = jh * v;\n        int\
    \ je = j0 + v;\n        int j2 = je + v;\n        for (; j0 < je; ++j0, ++j2)\
    \ {\n          mint t0 = a[j0], t1 = a[j0 + v], t2 = a[j2], t3 = a[j2 + v];\n\
    \          mint t0p1 = t0 + t1, t2p3 = t2 + t3;\n          mint t0m1 = (t0 - t1)\
    \ * xx, t2m3 = (t2 - t3) * yy;\n          a[j0] = t0p1 + t2p3, a[j2] = (t0p1 -\
    \ t2p3) * ww;\n          a[j0 + v] = t0m1 + t2m3, a[j2 + v] = (t0m1 - t2m3) *\
    \ ww;\n        }\n        xx *= dy[__builtin_ctzll(jh += 4)];\n      }\n     \
    \ u >>= 4;\n      v <<= 2;\n    }\n    if (k & 1) {\n      u = 1 << (k - 1);\n\
    \      for (int j = 0; j < u; ++j) {\n        mint ajv = a[j] - a[j + u];\n  \
    \      a[j] += a[j + u];\n        a[j + u] = ajv;\n      }\n    }\n  }\n\n  void\
    \ ntt(vector<mint> &a) {\n    if ((int)a.size() <= 1) return;\n    fft4(a, __builtin_ctz(a.size()));\n\
    \  }\n\n  void intt(vector<mint> &a) {\n    if ((int)a.size() <= 1) return;\n\
    \    ifft4(a, __builtin_ctz(a.size()));\n    mint iv = mint(a.size()).inverse();\n\
    \    for (auto &x : a) x *= iv;\n  }\n\n  vector<mint> multiply(const vector<mint>\
    \ &a, const vector<mint> &b) {\n    int l = a.size() + b.size() - 1;\n    if (min<int>(a.size(),\
    \ b.size()) <= 40) {\n      vector<mint> s(l);\n      for (int i = 0; i < (int)a.size();\
    \ ++i)\n        for (int j = 0; j < (int)b.size(); ++j) s[i + j] += a[i] * b[j];\n\
    \      return s;\n    }\n    int k = 2, M = 4;\n    while (M < l) M <<= 1, ++k;\n\
    \    setwy(k);\n    vector<mint> s(M), t(M);\n    for (int i = 0; i < (int)a.size();\
    \ ++i) s[i] = a[i];\n    for (int i = 0; i < (int)b.size(); ++i) t[i] = b[i];\n\
    \    fft4(s, k);\n    fft4(t, k);\n    for (int i = 0; i < M; ++i) s[i] *= t[i];\n\
    \    ifft4(s, k);\n    s.resize(l);\n    mint invm = mint(M).inverse();\n    for\
    \ (int i = 0; i < l; ++i) s[i] *= invm;\n    return s;\n  }\n\n  void ntt_doubling(vector<mint>\
    \ &a) {\n    int M = (int)a.size();\n    auto b = a;\n    intt(b);\n    mint r\
    \ = 1, zeta = mint(pr).pow((mint::get_mod() - 1) / (M << 1));\n    for (int i\
    \ = 0; i < M; i++) b[i] *= r, r *= zeta;\n    ntt(b);\n    copy(begin(b), end(b),\
    \ back_inserter(a));\n  }\n};\n#line 8 \"string/wildcard-pattern-matching.hpp\"\
    \n\nnamespace WildcardPatternMatchingImpl {\n\ntemplate <typename Container, unsigned\
    \ int MOD>\nvector<int> inner(const Container& a, const Container& b,\n      \
    \            const typename Container::value_type& wildcard = 0) {\n  using mint\
    \ = LazyMontgomeryModInt<MOD>;\n  static NTT<mint> ntt;\n  int N = a.size(), M\
    \ = b.size();\n  vector<mint> A1(N), A2(N), A3(N), B1(M), B2(M), B3(M);\n  for\
    \ (int i = 0; i < N; i++) {\n    mint x = a[i] == wildcard ? 0 : a[i];\n    mint\
    \ y = a[i] == wildcard ? 0 : 1;\n    A1[i] = y * x * x;\n    A2[i] = y * x * (-2);\n\
    \    A3[i] = y;\n  }\n  for (int i = 0; i < M; i++) {\n    mint x = b[i] == wildcard\
    \ ? 0 : b[i];\n    mint y = b[i] == wildcard ? 0 : 1;\n    B1[M - 1 - i] = y;\n\
    \    B2[M - 1 - i] = y * x;\n    B3[M - 1 - i] = y * x * x;\n  }\n  auto AB1 =\
    \ ntt.multiply(A1, B1);\n  auto AB2 = ntt.multiply(A2, B2);\n  auto AB3 = ntt.multiply(A3,\
    \ B3);\n  vector<int> res(N - M + 1, 1);\n  for (int i = 0; i < N - M + 1; i++)\
    \ {\n    mint x = AB1[i + M - 1] + AB2[i + M - 1] + AB3[i + M - 1];\n    if (x\
    \ != 0) res[i] = 0;\n  }\n  return res;\n}\n\n// \u8FD4\u308A\u5024 : \u9577\u3055\
    \ |a| - |b| + 1 \u306E\u914D\u5217 c\n// c[i] := a[i, i+|b|) b \u3068\u30DE\u30C3\
    \u30C1\u3059\u308B\u306A\u3089\u3070 1, \u3057\u306A\u3051\u308C\u3070 0)\n//\
    \ wildcard \u306F\u5F15\u6570\u306B\u5165\u308C\u308B (default \u3067 0)\ntemplate\
    \ <typename Container>\nvector<int> wildcard_pattern_matching(\n    const Container&\
    \ a, const Container& b,\n    const typename Container::value_type& wildcard =\
    \ 0) {\n  if ((int)b.size() == 0) return vector<int>(a.size() + 1, 1);\n  if (a.size()\
    \ < b.size()) return {};\n  vector<int> res1 = inner<Container, 998244353>(a,\
    \ b, wildcard);\n  vector<int> res2 = inner<Container, 924844033>(a, b, wildcard);\n\
    \  vector<int> res3 = inner<Container, 1012924417>(a, b, wildcard);\n  for (int\
    \ i = 0; i < (int)res1.size(); i++) res1[i] &= res2[i] & res3[i];\n  return res1;\n\
    }\n\n}  // namespace WildcardPatternMatchingImpl\n\nusing WildcardPatternMatchingImpl::wildcard_pattern_matching;\n\
    \n/**\n * @brief Wildcard Pattern Matching\n */\n"
  code: "#pragma once\n\n#include <vector>\nusing namespace std;\n\n#include \"../modint/montgomery-modint.hpp\"\
    \n#include \"../ntt/ntt.hpp\"\n\nnamespace WildcardPatternMatchingImpl {\n\ntemplate\
    \ <typename Container, unsigned int MOD>\nvector<int> inner(const Container& a,\
    \ const Container& b,\n                  const typename Container::value_type&\
    \ wildcard = 0) {\n  using mint = LazyMontgomeryModInt<MOD>;\n  static NTT<mint>\
    \ ntt;\n  int N = a.size(), M = b.size();\n  vector<mint> A1(N), A2(N), A3(N),\
    \ B1(M), B2(M), B3(M);\n  for (int i = 0; i < N; i++) {\n    mint x = a[i] ==\
    \ wildcard ? 0 : a[i];\n    mint y = a[i] == wildcard ? 0 : 1;\n    A1[i] = y\
    \ * x * x;\n    A2[i] = y * x * (-2);\n    A3[i] = y;\n  }\n  for (int i = 0;\
    \ i < M; i++) {\n    mint x = b[i] == wildcard ? 0 : b[i];\n    mint y = b[i]\
    \ == wildcard ? 0 : 1;\n    B1[M - 1 - i] = y;\n    B2[M - 1 - i] = y * x;\n \
    \   B3[M - 1 - i] = y * x * x;\n  }\n  auto AB1 = ntt.multiply(A1, B1);\n  auto\
    \ AB2 = ntt.multiply(A2, B2);\n  auto AB3 = ntt.multiply(A3, B3);\n  vector<int>\
    \ res(N - M + 1, 1);\n  for (int i = 0; i < N - M + 1; i++) {\n    mint x = AB1[i\
    \ + M - 1] + AB2[i + M - 1] + AB3[i + M - 1];\n    if (x != 0) res[i] = 0;\n \
    \ }\n  return res;\n}\n\n// \u8FD4\u308A\u5024 : \u9577\u3055 |a| - |b| + 1 \u306E\
    \u914D\u5217 c\n// c[i] := a[i, i+|b|) b \u3068\u30DE\u30C3\u30C1\u3059\u308B\u306A\
    \u3089\u3070 1, \u3057\u306A\u3051\u308C\u3070 0)\n// wildcard \u306F\u5F15\u6570\
    \u306B\u5165\u308C\u308B (default \u3067 0)\ntemplate <typename Container>\nvector<int>\
    \ wildcard_pattern_matching(\n    const Container& a, const Container& b,\n  \
    \  const typename Container::value_type& wildcard = 0) {\n  if ((int)b.size()\
    \ == 0) return vector<int>(a.size() + 1, 1);\n  if (a.size() < b.size()) return\
    \ {};\n  vector<int> res1 = inner<Container, 998244353>(a, b, wildcard);\n  vector<int>\
    \ res2 = inner<Container, 924844033>(a, b, wildcard);\n  vector<int> res3 = inner<Container,\
    \ 1012924417>(a, b, wildcard);\n  for (int i = 0; i < (int)res1.size(); i++) res1[i]\
    \ &= res2[i] & res3[i];\n  return res1;\n}\n\n}  // namespace WildcardPatternMatchingImpl\n\
    \nusing WildcardPatternMatchingImpl::wildcard_pattern_matching;\n\n/**\n * @brief\
    \ Wildcard Pattern Matching\n */\n"
  dependsOn:
  - modint/montgomery-modint.hpp
  - ntt/ntt.hpp
  isVerificationFile: false
  path: string/wildcard-pattern-matching.hpp
  requiredBy: []
  timestamp: '2023-03-24 18:37:12+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - verify/verify-yuki/yuki-2231.test.cpp
documentation_of: string/wildcard-pattern-matching.hpp
layout: document
redirect_from:
- /library/string/wildcard-pattern-matching.hpp
- /library/string/wildcard-pattern-matching.hpp.html
title: Wildcard Pattern Matching
---