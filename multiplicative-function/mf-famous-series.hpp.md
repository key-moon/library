---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: multiplicative-function/divisor-multiple-transform.hpp
    title: "\u500D\u6570\u5909\u63DB\u30FB\u7D04\u6570\u5909\u63DB"
  - icon: ':heavy_check_mark:'
    path: prime/prime-enumerate.hpp
    title: prime/prime-enumerate.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: hpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 2 \"multiplicative-function/mf-famous-series.hpp\"\n#include\
    \ <bits/stdc++.h>\nusing namespace std;\n\n#line 3 \"multiplicative-function/divisor-multiple-transform.hpp\"\
    \nusing namespace std;\n\n#line 3 \"prime/prime-enumerate.hpp\"\nusing namespace\
    \ std;\n\n// Prime Sieve {2, 3, 5, 7, 11, 13, 17, ...}\nvector<int> prime_enumerate(int\
    \ N) {\n  vector<bool> sieve(N / 3 + 1, 1);\n  for (int p = 5, d = 4, i = 1, sqn\
    \ = sqrt(N); p <= sqn; p += d = 6 - d, i++) {\n    if (!sieve[i]) continue;\n\
    \    for (int q = p * p / 3, r = d * p / 3 + (d * p % 3 == 2), s = 2 * p,\n  \
    \           qe = sieve.size();\n         q < qe; q += r = s - r)\n      sieve[q]\
    \ = 0;\n  }\n  vector<int> ret{2, 3};\n  for (int p = 5, d = 4, i = 1; p <= N;\
    \ p += d = 6 - d, i++)\n    if (sieve[i]) ret.push_back(p);\n  while (!ret.empty()\
    \ && ret.back() > N) ret.pop_back();\n  return ret;\n}\n#line 6 \"multiplicative-function/divisor-multiple-transform.hpp\"\
    \n\nstruct divisor_transform {\n  template <typename T>\n  static void zeta_transform(vector<T>\
    \ &a) {\n    int N = a.size() - 1;\n    auto sieve = prime_enumerate(N);\n   \
    \ for (auto &p : sieve)\n      for (int k = 1; k * p <= N; ++k) a[k * p] += a[k];\n\
    \  }\n  template <typename T>\n  static void mobius_transform(T &a) {\n    int\
    \ N = a.size() - 1;\n    auto sieve = prime_enumerate(N);\n    for (auto &p :\
    \ sieve)\n      for (int k = N / p; k > 0; --k) a[k * p] -= a[k];\n  }\n\n  template\
    \ <typename T>\n  static void zeta_transform(map<long long, T> &a) {\n    for\
    \ (auto p = rbegin(a); p != rend(a); p++)\n      for (auto &x : a) {\n       \
    \ if (p->first == x.first) break;\n        if (p->first % x.first == 0) p->second\
    \ += x.second;\n      }\n  }\n  template <typename T>\n  static void mobius_transform(map<long\
    \ long, T> &a) {\n    for (auto &x : a)\n      for (auto p = rbegin(a); p != rend(a);\
    \ p++) {\n        if (x.first == p->first) break;\n        if (p->first % x.first\
    \ == 0) p->second -= x.second;\n      }\n  }\n};\n\nstruct multiple_transform\
    \ {\n  template <typename T>\n  static void zeta_transform(vector<T> &a) {\n \
    \   int N = a.size() - 1;\n    auto sieve = prime_enumerate(N);\n    for (auto\
    \ &p : sieve)\n      for (int k = N / p; k > 0; --k) a[k] += a[k * p];\n  }\n\
    \  template <typename T>\n  static void mobius_transform(vector<T> &a) {\n   \
    \ int N = a.size() - 1;\n    auto sieve = prime_enumerate(N);\n    for (auto &p\
    \ : sieve)\n      for (int k = 1; k * p <= N; ++k) a[k] -= a[k * p];\n  }\n\n\
    \  template <typename T>\n  static void zeta_transform(map<long long, T> &a) {\n\
    \    for (auto p1 = rbegin(a); p1 != rend(a); p1++)\n      for (auto p2 = rbegin(a);\
    \ p2 != p1; p2++)\n        if (p2->first % p1->first == 0) p1->second += p2->second;\n\
    \  }\n  template <typename T>\n  static void mobius_transform(map<long long, T>\
    \ &a) {\n    for (auto p1 = rbegin(a); p1 != rend(a); p1++)\n      for (auto p2\
    \ = rbegin(a); p2 != p1; p2++)\n        if (p2->first % p1->first == 0) p1->second\
    \ -= p2->second;\n  }\n};\n\n/**\n * @brief \u500D\u6570\u5909\u63DB\u30FB\u7D04\
    \u6570\u5909\u63DB\n */\n#line 6 \"multiplicative-function/mf-famous-series.hpp\"\
    \n\ntemplate <typename T>\nstatic constexpr vector<T> mobius_function(int N) {\n\
    \  vector<T> a(N + 1, 0);\n  a[1] = 1;\n  divisor_transform::mobius_transform(a);\n\
    \  return a;\n}\n"
  code: "#pragma once\n#include <bits/stdc++.h>\nusing namespace std;\n\n#include\
    \ \"divisor-multiple-transform.hpp\"\n\ntemplate <typename T>\nstatic constexpr\
    \ vector<T> mobius_function(int N) {\n  vector<T> a(N + 1, 0);\n  a[1] = 1;\n\
    \  divisor_transform::mobius_transform(a);\n  return a;\n}\n"
  dependsOn:
  - multiplicative-function/divisor-multiple-transform.hpp
  - prime/prime-enumerate.hpp
  isVerificationFile: false
  path: multiplicative-function/mf-famous-series.hpp
  requiredBy: []
  timestamp: '2020-12-02 14:41:33+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: multiplicative-function/mf-famous-series.hpp
layout: document
redirect_from:
- /library/multiplicative-function/mf-famous-series.hpp
- /library/multiplicative-function/mf-famous-series.hpp.html
title: multiplicative-function/mf-famous-series.hpp
---