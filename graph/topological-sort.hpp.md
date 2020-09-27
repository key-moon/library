---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/graph-template.hpp
    title: graph/graph-template.hpp
  _extendedRequiredBy:
  - icon: ':warning:'
    path: math/grundy-number.hpp
    title: math/grundy-number.hpp
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: verify/verify-aoj-grl/aoj-grl-4-b.test.cpp
    title: verify/verify-aoj-grl/aoj-grl-4-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: verify/verify-aoj-grl/aoj-grl-4-a.test.cpp
    title: verify/verify-aoj-grl/aoj-grl-4-a.test.cpp
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 2 \"graph/topological-sort.hpp\"\n#include <bits/stdc++.h>\n\
    using namespace std;\n\n#line 3 \"graph/graph-template.hpp\"\nusing namespace\
    \ std;\n\ntemplate <typename T>\nstruct edge {\n  int src, to;\n  T cost;\n\n\
    \  edge(int to, T cost) : src(-1), to(to), cost(cost) {}\n  edge(int src, int\
    \ to, T cost) : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const int\
    \ &x) {\n    to = x;\n    return *this;\n  }\n\n  operator int() const { return\
    \ to; }\n};\ntemplate <typename T>\nusing Edges = vector<edge<T>>;\ntemplate <typename\
    \ T>\nusing WeightedGraph = vector<Edges<T>>;\nusing UnweightedGraph = vector<vector<int>>;\n\
    \n// Input of (Unweighted) Graph\nUnweightedGraph graph(int N, int M = -1, bool\
    \ is_directed = false,\n                      bool is_1origin = true) {\n  UnweightedGraph\
    \ g(N);\n  if (M == -1) M = N - 1;\n  for (int _ = 0; _ < M; _++) {\n    int x,\
    \ y;\n    cin >> x >> y;\n    if (is_1origin) x--, y--;\n    g[x].push_back(y);\n\
    \    if (!is_directed) g[y].push_back(x);\n  }\n  return g;\n}\n\n// Input of\
    \ Weighted Graph\ntemplate <typename T>\nWeightedGraph<T> wgraph(int N, int M\
    \ = -1, bool is_directed = false,\n                        bool is_1origin = true)\
    \ {\n  WeightedGraph<T> g(N);\n  if (M == -1) M = N - 1;\n  for (int _ = 0; _\
    \ < M; _++) {\n    int x, y;\n    cin >> x >> y;\n    T c;\n    cin >> c;\n  \
    \  if (is_1origin) x--, y--;\n    g[x].eb(x, y, c);\n    if (!is_directed) g[y].eb(y,\
    \ x, c);\n  }\n  return g;\n}\n\n// Input of Edges\ntemplate <typename T>\nEdges<T>\
    \ esgraph(int N, int M, int is_weighted = true, bool is_1origin = true) {\n  Edges<T>\
    \ es;\n  for (int _ = 0; _ < M; _++) {\n    int x, y;\n    cin >> x >> y;\n  \
    \  T c;\n    if (is_weighted)\n      cin >> c;\n    else\n      c = 1;\n    if\
    \ (is_1origin) x--, y--;\n    es.emplace_back(x, y, c);\n  }\n  return es;\n}\n\
    \n// Input of Adjacency Matrix\ntemplate <typename T>\nvector<vector<T>> adjgraph(int\
    \ N, int M, T INF, int is_weighted = true,\n                           bool is_directed\
    \ = false, bool is_1origin = true) {\n  vector<vector<T>> d(N, vector<T>(N, INF));\n\
    \  for (int _ = 0; _ < M; _++) {\n    int x, y;\n    cin >> x >> y;\n    T c;\n\
    \    if (is_weighted)\n      cin >> c;\n    else\n      c = 1;\n    if (is_1origin)\
    \ x--, y--;\n    d[x][y] = c;\n    if (!is_directed) d[y][x] = c;\n  }\n  return\
    \ d;\n}\n#line 6 \"graph/topological-sort.hpp\"\n\n// if the graph is not DAG,\
    \ return empty vector\ntemplate <typename T>\nvector<int> TopologicalSort(T &g)\
    \ {\n  int N = g.size();\n  vector<int> marked(N, 0), temp(N, 0), v;\n  auto visit\
    \ = [&](auto f, int i) -> bool {\n    if (temp[i] == 1) return false;\n    if\
    \ (marked[i] == 0) {\n      temp[i] = 1;\n      for (auto &e : g[i]) {\n     \
    \   if (f(f, e) == false) return false;\n      }\n      marked[i] = 1;\n     \
    \ v.push_back(i);\n      temp[i] = 0;\n    }\n    return true;\n  };\n\n  for\
    \ (int i = 0; i < N; i++) {\n    if (marked[i] == 0) {\n      if (visit(visit,\
    \ i) == false) return vector<int>();\n    }\n  }\n  reverse(v.begin(), v.end());\n\
    \  return v;\n}\n"
  code: "#pragma once\n#include <bits/stdc++.h>\nusing namespace std;\n\n#include\
    \ \"./graph-template.hpp\"\n\n// if the graph is not DAG, return empty vector\n\
    template <typename T>\nvector<int> TopologicalSort(T &g) {\n  int N = g.size();\n\
    \  vector<int> marked(N, 0), temp(N, 0), v;\n  auto visit = [&](auto f, int i)\
    \ -> bool {\n    if (temp[i] == 1) return false;\n    if (marked[i] == 0) {\n\
    \      temp[i] = 1;\n      for (auto &e : g[i]) {\n        if (f(f, e) == false)\
    \ return false;\n      }\n      marked[i] = 1;\n      v.push_back(i);\n      temp[i]\
    \ = 0;\n    }\n    return true;\n  };\n\n  for (int i = 0; i < N; i++) {\n   \
    \ if (marked[i] == 0) {\n      if (visit(visit, i) == false) return vector<int>();\n\
    \    }\n  }\n  reverse(v.begin(), v.end());\n  return v;\n}"
  dependsOn:
  - graph/graph-template.hpp
  isVerificationFile: false
  path: graph/topological-sort.hpp
  requiredBy:
  - math/grundy-number.hpp
  timestamp: '2020-07-28 11:29:32+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - verify/verify-aoj-grl/aoj-grl-4-b.test.cpp
  - verify/verify-aoj-grl/aoj-grl-4-a.test.cpp
documentation_of: graph/topological-sort.hpp
layout: document
redirect_from:
- /library/graph/topological-sort.hpp
- /library/graph/topological-sort.hpp.html
title: graph/topological-sort.hpp
---