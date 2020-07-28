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


# :heavy_check_mark: data-structure/2d-cumulative-sum.hpp

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#36397fe12f935090ad150c6ce0c258d4">data-structure</a>
* <a href="{{ site.github.repository_url }}/blob/master/data-structure/2d-cumulative-sum.hpp">View this file on GitHub</a>
    - Last commit date: 2020-07-28 11:29:32+09:00




## Verified with

* :heavy_check_mark: <a href="../../verify/verify-aoj-dsl/aoj-dsl-5-b.test.cpp.html">verify-aoj-dsl/aoj-dsl-5-b.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#pragma once
#include <bits/stdc++.h>
using namespace std;

// Don't Forget to call build() !!!!!
template <class T>
struct CumulativeSum2D {
  vector<vector<T> > data;

  CumulativeSum2D(int H, int W) : data(H + 3, vector<int>(W + 3, 0)) {}

  void add(int i, int j, T z) {
    ++i, ++j;
    if (i >= (int)data.size() || j >= (int)data[0].size()) return;
    data[i][j] += z;
  }

  // add [ [i1,j1], [i2,j2] )
  void imos(int i1, int j1, int i2, int j2, T z) {
    add(i1, j1, 1);
    add(i1, j2, -1);
    add(i2, j1, -1);
    add(i2, j2, 1);
  }

  void build() {
    for (int i = 1; i < (int)data.size(); i++) {
      for (int j = 1; j < (int)data[i].size(); j++) {
        data[i][j] += data[i][j - 1] + data[i - 1][j] - data[i - 1][j - 1];
      }
    }
  }

  T query(int i1, int j1, int i2, int j2) {
    return (data[i2][j2] - data[i1][j2] - data[i2][j1] + data[i1][j1]);
  }
};
```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 2 "data-structure/2d-cumulative-sum.hpp"
#include <bits/stdc++.h>
using namespace std;

// Don't Forget to call build() !!!!!
template <class T>
struct CumulativeSum2D {
  vector<vector<T> > data;

  CumulativeSum2D(int H, int W) : data(H + 3, vector<int>(W + 3, 0)) {}

  void add(int i, int j, T z) {
    ++i, ++j;
    if (i >= (int)data.size() || j >= (int)data[0].size()) return;
    data[i][j] += z;
  }

  // add [ [i1,j1], [i2,j2] )
  void imos(int i1, int j1, int i2, int j2, T z) {
    add(i1, j1, 1);
    add(i1, j2, -1);
    add(i2, j1, -1);
    add(i2, j2, 1);
  }

  void build() {
    for (int i = 1; i < (int)data.size(); i++) {
      for (int j = 1; j < (int)data[i].size(); j++) {
        data[i][j] += data[i][j - 1] + data[i - 1][j] - data[i - 1][j - 1];
      }
    }
  }

  T query(int i1, int j1, int i2, int j2) {
    return (data[i2][j2] - data[i1][j2] - data[i2][j1] + data[i1][j1]);
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>
