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


# :heavy_check_mark: graph/strongly-connected-components.hpp

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#f8b0b924ebd7046dbfa85a856e4682c8">graph</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/strongly-connected-components.hpp">View this file on GitHub</a>
    - Last commit date: 2020-08-02 19:22:09+09:00




## Depends on

* :question: <a href="graph-template.hpp.html">graph/graph-template.hpp</a>


## Verified with

* :heavy_check_mark: <a href="../../verify/verify/verify-aoj-grl/aoj-grl-3-c.test.cpp.html">verify/verify-aoj-grl/aoj-grl-3-c.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/verify/verify-yosupo-graph/yosupo-strongly-connected-components.test.cpp.html">verify/verify-yosupo-graph/yosupo-strongly-connected-components.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#pragma once
#include <bits/stdc++.h>
using namespace std;

#include "./graph-template.hpp"

// Strongly Connected Components
// DAG of SC graph   ... scc.dag (including multiedges)
// new node of k     ... scc[k]
// inv of scc[k] = i ... scc.belong(i)
template <typename G>
struct StronglyConnectedComponents {
 private:
  const G &g;
  vector<vector<int>> rg;
  vector<int> comp, order;
  vector<char> used;
  vector<vector<int>> blng;

 public:
  vector<vector<int>> dag;
  StronglyConnectedComponents(G &g) : g(g), used(g.size(), 0) { build(); }

  int operator[](int k) { return comp[k]; }

  vector<int> &belong(int i) { return blng[i]; }

 private:
  void dfs(int idx) {
    if (used[idx]) return;
    used[idx] = true;
    for (auto to : g[idx]) dfs(int(to));
    order.push_back(idx);
  }

  void rdfs(int idx, int cnt) {
    if (comp[idx] != -1) return;
    comp[idx] = cnt;
    for (int to : rg[idx]) rdfs(to, cnt);
  }

  void build() {
    for (int i = 0; i < (int)g.size(); i++) dfs(i);
    reverse(begin(order), end(order));
    used.clear();
    used.shrink_to_fit();

    comp.resize(g.size(), -1);

    rg.resize(g.size());
    for (int i = 0; i < (int)g.size(); i++) {
      for (auto e : g[i]) {
        rg[(int)e].emplace_back(i);
      }
    }
    int ptr = 0;
    for (int i : order)
      if (comp[i] == -1) rdfs(i, ptr), ptr++;
    rg.clear();
    rg.shrink_to_fit();
    order.clear();
    order.shrink_to_fit();

    dag.resize(ptr);
    blng.resize(ptr);
    for (int i = 0; i < (int)g.size(); i++) {
      blng[comp[i]].push_back(i);
      for (auto &to : g[i]) {
        int x = comp[i], y = comp[to];
        if (x == y) continue;
        dag[x].push_back(y);
      }
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 2 "graph/strongly-connected-components.hpp"
#include <bits/stdc++.h>
using namespace std;

#line 3 "graph/graph-template.hpp"
using namespace std;

template <typename T>
struct edge {
  int src, to;
  T cost;

  edge(int to, T cost) : src(-1), to(to), cost(cost) {}
  edge(int src, int to, T cost) : src(src), to(to), cost(cost) {}

  edge &operator=(const int &x) {
    to = x;
    return *this;
  }

  operator int() const { return to; }
};
template <typename T>
using Edges = vector<edge<T>>;
template <typename T>
using WeightedGraph = vector<Edges<T>>;
using UnweightedGraph = vector<vector<int>>;

// Input of (Unweighted) Graph
UnweightedGraph graph(int N, int M = -1, bool is_directed = false,
                      bool is_1origin = true) {
  UnweightedGraph g(N);
  if (M == -1) M = N - 1;
  for (int _ = 0; _ < M; _++) {
    int x, y;
    cin >> x >> y;
    if (is_1origin) x--, y--;
    g[x].push_back(y);
    if (!is_directed) g[y].push_back(x);
  }
  return g;
}

// Input of Weighted Graph
template <typename T>
WeightedGraph<T> wgraph(int N, int M = -1, bool is_directed = false,
                        bool is_1origin = true) {
  WeightedGraph<T> g(N);
  if (M == -1) M = N - 1;
  for (int _ = 0; _ < M; _++) {
    int x, y;
    cin >> x >> y;
    T c;
    cin >> c;
    if (is_1origin) x--, y--;
    g[x].eb(x, y, c);
    if (!is_directed) g[y].eb(y, x, c);
  }
  return g;
}

// Input of Edges
template <typename T>
Edges<T> esgraph(int N, int M, int is_weighted = true, bool is_1origin = true) {
  Edges<T> es;
  for (int _ = 0; _ < M; _++) {
    int x, y;
    cin >> x >> y;
    T c;
    if (is_weighted)
      cin >> c;
    else
      c = 1;
    if (is_1origin) x--, y--;
    es.emplace_back(x, y, c);
  }
  return es;
}

// Input of Adjacency Matrix
template <typename T>
vector<vector<T>> adjgraph(int N, int M, T INF, int is_weighted = true,
                           bool is_directed = false, bool is_1origin = true) {
  vector<vector<T>> d(N, vector<T>(N, INF));
  for (int _ = 0; _ < M; _++) {
    int x, y;
    cin >> x >> y;
    T c;
    if (is_weighted)
      cin >> c;
    else
      c = 1;
    if (is_1origin) x--, y--;
    d[x][y] = c;
    if (!is_directed) d[y][x] = c;
  }
  return d;
}
#line 6 "graph/strongly-connected-components.hpp"

// Strongly Connected Components
// DAG of SC graph   ... scc.dag (including multiedges)
// new node of k     ... scc[k]
// inv of scc[k] = i ... scc.belong(i)
template <typename G>
struct StronglyConnectedComponents {
 private:
  const G &g;
  vector<vector<int>> rg;
  vector<int> comp, order;
  vector<char> used;
  vector<vector<int>> blng;

 public:
  vector<vector<int>> dag;
  StronglyConnectedComponents(G &g) : g(g), used(g.size(), 0) { build(); }

  int operator[](int k) { return comp[k]; }

  vector<int> &belong(int i) { return blng[i]; }

 private:
  void dfs(int idx) {
    if (used[idx]) return;
    used[idx] = true;
    for (auto to : g[idx]) dfs(int(to));
    order.push_back(idx);
  }

  void rdfs(int idx, int cnt) {
    if (comp[idx] != -1) return;
    comp[idx] = cnt;
    for (int to : rg[idx]) rdfs(to, cnt);
  }

  void build() {
    for (int i = 0; i < (int)g.size(); i++) dfs(i);
    reverse(begin(order), end(order));
    used.clear();
    used.shrink_to_fit();

    comp.resize(g.size(), -1);

    rg.resize(g.size());
    for (int i = 0; i < (int)g.size(); i++) {
      for (auto e : g[i]) {
        rg[(int)e].emplace_back(i);
      }
    }
    int ptr = 0;
    for (int i : order)
      if (comp[i] == -1) rdfs(i, ptr), ptr++;
    rg.clear();
    rg.shrink_to_fit();
    order.clear();
    order.shrink_to_fit();

    dag.resize(ptr);
    blng.resize(ptr);
    for (int i = 0; i < (int)g.size(); i++) {
      blng[comp[i]].push_back(i);
      for (auto &to : g[i]) {
        int x = comp[i], y = comp[to];
        if (x == y) continue;
        dag[x].push_back(y);
      }
    }
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>
