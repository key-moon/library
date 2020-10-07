---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: competitive-template.hpp
    title: competitive-template.hpp
  - icon: ':heavy_check_mark:'
    path: graph/graph-template.hpp
    title: graph/graph-template.hpp
  - icon: ':heavy_check_mark:'
    path: graph/graph-utility.hpp
    title: graph/graph-utility.hpp
  - icon: ':heavy_check_mark:'
    path: tree/heavy-light-decomposition.hpp
    title: tree/heavy-light-decomposition.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/lca
    links:
    - https://judge.yosupo.jp/problem/lca
  bundledCode: "#line 1 \"verify/verify-yosupo-graph/yosupo-lowest-common-ancestor.test.cpp\"\
    \n#define PROBLEM \"https://judge.yosupo.jp/problem/lca\"\n\n#line 1 \"competitive-template.hpp\"\
    \n#pragma region kyopro_template\n#define Nyaan_template\n#include <immintrin.h>\n\
    #include <bits/stdc++.h>\n#define pb push_back\n#define eb emplace_back\n#define\
    \ fi first\n#define se second\n#define each(x, v) for (auto &x : v)\n#define all(v)\
    \ (v).begin(), (v).end()\n#define sz(v) ((int)(v).size())\n#define mem(a, val)\
    \ memset(a, val, sizeof(a))\n#define ini(...)   \\\n  int __VA_ARGS__; \\\n  in(__VA_ARGS__)\n\
    #define inl(...)         \\\n  long long __VA_ARGS__; \\\n  in(__VA_ARGS__)\n\
    #define ins(...)      \\\n  string __VA_ARGS__; \\\n  in(__VA_ARGS__)\n#define\
    \ inc(...)    \\\n  char __VA_ARGS__; \\\n  in(__VA_ARGS__)\n#define in2(s, t)\
    \                           \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\
    \n    in(s[i], t[i]);                         \\\n  }\n#define in3(s, t, u)  \
    \                      \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\n  \
    \  in(s[i], t[i], u[i]);                   \\\n  }\n#define in4(s, t, u, v)  \
    \                   \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\n    in(s[i],\
    \ t[i], u[i], v[i]);             \\\n  }\n#define rep(i, N) for (long long i =\
    \ 0; i < (long long)(N); i++)\n#define repr(i, N) for (long long i = (long long)(N)-1;\
    \ i >= 0; i--)\n#define rep1(i, N) for (long long i = 1; i <= (long long)(N);\
    \ i++)\n#define repr1(i, N) for (long long i = (N); (long long)(i) > 0; i--)\n\
    #define reg(i, a, b) for (long long i = (a); i < (b); i++)\n#define die(...) \
    \     \\\n  do {                \\\n    out(__VA_ARGS__); \\\n    return;    \
    \       \\\n  } while (0)\nusing namespace std;\nusing ll = long long;\ntemplate\
    \ <class T>\nusing V = vector<T>;\nusing vi = vector<int>;\nusing vl = vector<long\
    \ long>;\nusing vvi = vector<vector<int>>;\nusing vd = V<double>;\nusing vs =\
    \ V<string>;\nusing vvl = vector<vector<long long>>;\nusing P = pair<long long,\
    \ long long>;\nusing vp = vector<P>;\nusing pii = pair<int, int>;\nusing vpi =\
    \ vector<pair<int, int>>;\nconstexpr int inf = 1001001001;\nconstexpr long long\
    \ infLL = (1LL << 61) - 1;\ntemplate <typename T, typename U>\ninline bool amin(T\
    \ &x, U y) {\n  return (y < x) ? (x = y, true) : false;\n}\ntemplate <typename\
    \ T, typename U>\ninline bool amax(T &x, U y) {\n  return (x < y) ? (x = y, true)\
    \ : false;\n}\ntemplate <typename T, typename U>\nostream &operator<<(ostream\
    \ &os, const pair<T, U> &p) {\n  os << p.first << \" \" << p.second;\n  return\
    \ os;\n}\ntemplate <typename T, typename U>\nistream &operator>>(istream &is,\
    \ pair<T, U> &p) {\n  is >> p.first >> p.second;\n  return is;\n}\ntemplate <typename\
    \ T>\nostream &operator<<(ostream &os, const vector<T> &v) {\n  int s = (int)v.size();\n\
    \  for (int i = 0; i < s; i++) os << (i ? \" \" : \"\") << v[i];\n  return os;\n\
    }\ntemplate <typename T>\nistream &operator>>(istream &is, vector<T> &v) {\n \
    \ for (auto &x : v) is >> x;\n  return is;\n}\nvoid in() {}\ntemplate <typename\
    \ T, class... U>\nvoid in(T &t, U &... u) {\n  cin >> t;\n  in(u...);\n}\nvoid\
    \ out() { cout << \"\\n\"; }\ntemplate <typename T, class... U>\nvoid out(const\
    \ T &t, const U &... u) {\n  cout << t;\n  if (sizeof...(u)) cout << \" \";\n\
    \  out(u...);\n}\n\n#ifdef NyaanDebug\n#define trc(...)                   \\\n\
    \  do {                             \\\n    cerr << #__VA_ARGS__ << \" = \"; \\\
    \n    dbg_out(__VA_ARGS__);          \\\n  } while (0)\n#define trca(v, N)   \
    \    \\\n  do {                   \\\n    cerr << #v << \" = \"; \\\n    array_out(v,\
    \ N);     \\\n  } while (0)\n#define trcc(v)                             \\\n\
    \  do {                                      \\\n    cerr << #v << \" = {\"; \
    \                  \\\n    each(x, v) { cerr << \" \" << x << \",\"; } \\\n  \
    \  cerr << \"}\" << endl;                    \\\n  } while (0)\ntemplate <typename\
    \ T>\nvoid _cout(const T &c) {\n  cerr << c;\n}\nvoid _cout(const int &c) {\n\
    \  if (c == 1001001001)\n    cerr << \"inf\";\n  else if (c == -1001001001)\n\
    \    cerr << \"-inf\";\n  else\n    cerr << c;\n}\nvoid _cout(const unsigned int\
    \ &c) {\n  if (c == 1001001001)\n    cerr << \"inf\";\n  else\n    cerr << c;\n\
    }\nvoid _cout(const long long &c) {\n  if (c == 1001001001 || c == (1LL << 61)\
    \ - 1)\n    cerr << \"inf\";\n  else if (c == -1001001001 || c == -((1LL << 61)\
    \ - 1))\n    cerr << \"-inf\";\n  else\n    cerr << c;\n}\nvoid _cout(const unsigned\
    \ long long &c) {\n  if (c == 1001001001 || c == (1LL << 61) - 1)\n    cerr <<\
    \ \"inf\";\n  else\n    cerr << c;\n}\ntemplate <typename T, typename U>\nvoid\
    \ _cout(const pair<T, U> &p) {\n  cerr << \"{ \";\n  _cout(p.fi);\n  cerr << \"\
    , \";\n  _cout(p.se);\n  cerr << \" } \";\n}\ntemplate <typename T>\nvoid _cout(const\
    \ vector<T> &v) {\n  int s = v.size();\n  cerr << \"{ \";\n  for (int i = 0; i\
    \ < s; i++) {\n    cerr << (i ? \", \" : \"\");\n    _cout(v[i]);\n  }\n  cerr\
    \ << \" } \";\n}\ntemplate <typename T>\nvoid _cout(const vector<vector<T>> &v)\
    \ {\n  cerr << \"[ \";\n  for (const auto &x : v) {\n    cerr << endl;\n    _cout(x);\n\
    \    cerr << \", \";\n  }\n  cerr << endl << \" ] \";\n}\nvoid dbg_out() { cerr\
    \ << endl; }\ntemplate <typename T, class... U>\nvoid dbg_out(const T &t, const\
    \ U &... u) {\n  _cout(t);\n  if (sizeof...(u)) cerr << \", \";\n  dbg_out(u...);\n\
    }\ntemplate <typename T>\nvoid array_out(const T &v, int s) {\n  cerr << \"{ \"\
    ;\n  for (int i = 0; i < s; i++) {\n    cerr << (i ? \", \" : \"\");\n    _cout(v[i]);\n\
    \  }\n  cerr << \" } \" << endl;\n}\ntemplate <typename T>\nvoid array_out(const\
    \ T &v, int H, int W) {\n  cerr << \"[ \";\n  for (int i = 0; i < H; i++) {\n\
    \    cerr << (i ? \", \" : \"\");\n    array_out(v[i], W);\n  }\n  cerr << \"\
    \ ] \" << endl;\n}\n#else\n#define trc(...)\n#define trca(...)\n#define trcc(...)\n\
    #endif\n\ninline int popcnt(unsigned long long a) { return __builtin_popcountll(a);\
    \ }\ninline int lsb(unsigned long long a) { return __builtin_ctzll(a); }\ninline\
    \ int msb(unsigned long long a) { return 63 - __builtin_clzll(a); }\ntemplate\
    \ <typename T>\ninline int getbit(T a, int i) {\n  return (a >> i) & 1;\n}\ntemplate\
    \ <typename T>\ninline void setbit(T &a, int i) {\n  a |= (1LL << i);\n}\ntemplate\
    \ <typename T>\ninline void delbit(T &a, int i) {\n  a &= ~(1LL << i);\n}\ntemplate\
    \ <typename T>\nint lb(const vector<T> &v, const T &a) {\n  return lower_bound(begin(v),\
    \ end(v), a) - begin(v);\n}\ntemplate <typename T>\nint ub(const vector<T> &v,\
    \ const T &a) {\n  return upper_bound(begin(v), end(v), a) - begin(v);\n}\ntemplate\
    \ <typename T>\nint btw(T a, T x, T b) {\n  return a <= x && x < b;\n}\ntemplate\
    \ <typename T, typename U>\nT ceil(T a, U b) {\n  return (a + b - 1) / b;\n}\n\
    constexpr long long TEN(int n) {\n  long long ret = 1, x = 10;\n  while (n) {\n\
    \    if (n & 1) ret *= x;\n    x *= x;\n    n >>= 1;\n  }\n  return ret;\n}\n\
    template <typename T>\nvector<T> mkrui(const vector<T> &v) {\n  vector<T> ret(v.size()\
    \ + 1);\n  for (int i = 0; i < int(v.size()); i++) ret[i + 1] = ret[i] + v[i];\n\
    \  return ret;\n};\ntemplate <typename T>\nvector<T> mkuni(const vector<T> &v)\
    \ {\n  vector<T> ret(v);\n  sort(ret.begin(), ret.end());\n  ret.erase(unique(ret.begin(),\
    \ ret.end()), ret.end());\n  return ret;\n}\ntemplate <typename F>\nvector<int>\
    \ mkord(int N, F f) {\n  vector<int> ord(N);\n  iota(begin(ord), end(ord), 0);\n\
    \  sort(begin(ord), end(ord), f);\n  return ord;\n}\ntemplate <typename T = int>\n\
    vector<T> mkiota(int N) {\n  vector<T> ret(N);\n  iota(begin(ret), end(ret), 0);\n\
    \  return ret;\n}\ntemplate <typename T>\nvector<int> mkinv(vector<T> &v) {\n\
    \  vector<int> inv(v.size());\n  for (int i = 0; i < (int)v.size(); i++) inv[v[i]]\
    \ = i;\n  return inv;\n}\n\nstruct IoSetupNya {\n  IoSetupNya() {\n    cin.tie(nullptr);\n\
    \    ios::sync_with_stdio(false);\n    cout << fixed << setprecision(15);\n  \
    \  cerr << fixed << setprecision(7);\n  }\n} iosetupnya;\n\nvoid solve();\nint\
    \ main() { solve(); }\n\n#pragma endregion\n#line 3 \"graph/graph-utility.hpp\"\
    \nusing namespace std;\n\n#line 3 \"graph/graph-template.hpp\"\nusing namespace\
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
    \ d;\n}\n#line 6 \"graph/graph-utility.hpp\"\n\n// Depth of Rooted Tree\n// unvisited\
    \ nodes : d = -1\nvector<int> Depth(const UnweightedGraph &g, int start = 0) {\n\
    \  vector<int> d(g.size(), -1);\n  auto dfs = [&](auto rec, int cur, int par =\
    \ -1) -> void {\n    d[cur] = par == -1 ? 0 : d[par] + 1;\n    for (auto &dst\
    \ : g[cur]) {\n      if (dst == par) continue;\n      rec(rec, dst, cur);\n  \
    \  }\n  };\n  dfs(dfs, start);\n  return d;\n}\n\n// Depth of Rooted Weighted\
    \ Tree\n// unvisited nodes : d = -1\ntemplate <typename T>\nvector<T> Depth(const\
    \ WeightedGraph<T> &g, int start = 0) {\n  vector<T> d(g.size(), -1);\n  auto\
    \ dfs = [&](auto rec, int cur, T val, int par = -1) -> void {\n    d[cur] = val;\n\
    \    for (auto &dst : g[cur]) {\n      if (dst == par) continue;\n      rec(rec,\
    \ dst, val + dst.cost, cur);\n    }\n  };\n  dfs(dfs, start, 0);\n  return d;\n\
    }\n\n// Diameter of Tree\n// return value : { {u, v}, length }\npair<pair<int,\
    \ int>, int> Diameter(const UnweightedGraph &g) {\n  auto d = Depth(g, 0);\n \
    \ int u = max_element(begin(d), end(d)) - begin(d);\n  d = Depth(g, u);\n  int\
    \ v = max_element(begin(d), end(d)) - begin(d);\n  return make_pair(make_pair(u,\
    \ v), d[v]);\n}\n\n// Diameter of Weighted Tree\n// return value : { {u, v}, length\
    \ }\ntemplate <typename T>\npair<pair<int, int>, T> Diameter(const WeightedGraph<T>\
    \ &g) {\n  auto d = Depth(g, 0);\n  int u = max_element(begin(d), end(d)) - begin(d);\n\
    \  d = Depth(g, u);\n  int v = max_element(begin(d), end(d)) - begin(d);\n  return\
    \ make_pair(make_pair(u, v), d[v]);\n}\n\n// nodes on the path u-v ( O(N) )\n\
    template <typename G>\nvector<int> Path(G &g, int u, int v) {\n  vi ret;\n  int\
    \ end = 0;\n  auto dfs = [&](auto rec, int cur, int par = -1) -> void {\n    ret.push_back(cur);\n\
    \    if (cur == v) {\n      end = 1;\n      return;\n    }\n    for (int dst :\
    \ g[cur]) {\n      if (dst == par) continue;\n      rec(rec, dst, cur);\n    \
    \  if (end) return;\n    }\n    if (end) return;\n    ret.pop_back();\n  };\n\
    \  dfs(dfs, u);\n  return ret;\n}\n#line 3 \"tree/heavy-light-decomposition.hpp\"\
    \nusing namespace std;\n\n#line 6 \"tree/heavy-light-decomposition.hpp\"\n\ntemplate\
    \ <typename G>\nstruct HeavyLightDecomposition {\n  G& g;\n  int idx;\n  vector<int>\
    \ size, depth, in, out, nxt, par;\n  HeavyLightDecomposition(G& g, int root =\
    \ 0)\n      : g(g),\n        idx(0),\n        size(g.size(), 0),\n        depth(g.size(),\
    \ 0),\n        in(g.size(), -1),\n        out(g.size(), -1),\n        nxt(g.size(),\
    \ root),\n        par(g.size(), root) {\n    dfs_sz(root);\n    dfs_hld(root);\n\
    \  }\n\n  void build(int root) {\n    dfs_sz(root);\n    dfs_hld(root);\n  }\n\
    \n  void dfs_sz(int cur) {\n    size[cur] = 1;\n    for (auto& dst : g[cur]) {\n\
    \      if (dst == par[cur]) {\n        if (g[cur].size() >= 2 && int(dst) == int(g[cur][0]))\n\
    \          swap(g[cur][0], g[cur][1]);\n        else\n          continue;\n  \
    \    }\n      depth[dst] = depth[cur] + 1;\n      par[dst] = cur;\n      dfs_sz(dst);\n\
    \      size[cur] += size[dst];\n      if (size[dst] > size[g[cur][0]]) {\n   \
    \     swap(dst, g[cur][0]);\n      }\n    }\n  }\n\n  void dfs_hld(int cur) {\n\
    \    in[cur] = idx++;\n    for (auto dst : g[cur]) {\n      if (dst == par[cur])\
    \ continue;\n      nxt[dst] = (int(dst) == int(g[cur][0]) ? nxt[cur] : int(dst));\n\
    \      dfs_hld(dst);\n    }\n    out[cur] = idx;\n  }\n\n  template <typename\
    \ F>\n  void edge_query(int u, int v, const F& f) {\n    while (1) {\n      if\
    \ (in[u] > in[v]) swap(u, v);\n      if (nxt[u] != nxt[v]) {\n        f(in[nxt[v]],\
    \ in[v] + 1);\n        v = par[nxt[v]];\n      } else {\n        if (u != v) f(in[u]\
    \ + 1, in[v] + 1);\n        break;\n      }\n    }\n  }\n\n  // TODO : verify\n\
    \  template <typename F>\n  void uncommutable_edge_query(int u, int v, const F&\
    \ f) {\n    while (1) {\n      if (nxt[u] != nxt[v]) {\n        if (in[u] > in[v])\
    \ {\n          f(in[u] + 1, in[nxt[u]], true);\n          u = par[nxt[u]];\n \
    \       } else {\n          f(in[nxt[v]], in[v] + 1, false);\n          v = par[nxt[v]];\n\
    \        }\n      } else {\n        if (in[u] != in[v]) {\n          if (in[u]\
    \ > in[v])\n            f(in[u] + 1, in[v] + 1, true);\n          else\n     \
    \       f(in[u] + 1, in[v] + 1, true);\n        }\n        break;\n      }\n \
    \   }\n  }\n\n  template <typename F>\n  void node_query(int u, int v, const F&\
    \ f) {\n    while (1) {\n      if (in[u] > in[v]) swap(u, v);\n      if (nxt[u]\
    \ != nxt[v]) {\n        f(in[nxt[v]], in[v] + 1);\n        v = par[nxt[v]];\n\
    \      } else {\n        f(in[u], in[v] + 1);\n        break;\n      }\n    }\n\
    \  }\n\n  template <typename F>\n  void uncommutable_node_query(int u, int v,\
    \ const F& f) {\n    while (1) {\n      if (nxt[u] != nxt[v]) {\n        if (in[u]\
    \ > in[v]) {\n          f(in[u] + 1, in[nxt[u]], true);\n          u = par[nxt[u]];\n\
    \        } else {\n          f(in[nxt[v]], in[v] + 1, false);\n          v = par[nxt[v]];\n\
    \        }\n      } else {\n        if (in[u] > in[v])\n          f(in[u] + 1,\
    \ in[v], true);\n        else\n          f(in[u], in[v] + 1, true);\n        break;\n\
    \      }\n    }\n  }\n\n  template <typename F>\n  void sub_edge_query(int u,\
    \ const F& f) {\n    f(in[u] + 1, out[u]);\n  }\n\n  template <typename F>\n \
    \ void sub_node_query(int u, const F& f) {\n    f(in[u], out[u]);\n  }\n\n  int\
    \ lca(int a, int b) {\n    while (nxt[a] != nxt[b]) {\n      if (in[a] < in[b])\
    \ swap(a, b);\n      a = par[nxt[a]];\n    }\n    return depth[a] < depth[b] ?\
    \ a : b;\n  }\n};\n#line 6 \"verify/verify-yosupo-graph/yosupo-lowest-common-ancestor.test.cpp\"\
    \n\nvoid solve(){\n  ini(N,Q);\n  vvi g(N);\n  rep1(i,N-1){\n    ini(j);\n   \
    \ g[j].pb(i);\n  }\n  HeavyLightDecomposition<vvi> hld(g);\n  rep(_,Q){\n    ini(u,v);\n\
    \    out(hld.lca(u,v));\n  }\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/lca\"\n\n#include \"../../competitive-template.hpp\"\
    \n#include \"../../graph/graph-utility.hpp\"\n#include \"../../tree/heavy-light-decomposition.hpp\"\
    \n\nvoid solve(){\n  ini(N,Q);\n  vvi g(N);\n  rep1(i,N-1){\n    ini(j);\n   \
    \ g[j].pb(i);\n  }\n  HeavyLightDecomposition<vvi> hld(g);\n  rep(_,Q){\n    ini(u,v);\n\
    \    out(hld.lca(u,v));\n  }\n}"
  dependsOn:
  - competitive-template.hpp
  - graph/graph-utility.hpp
  - graph/graph-template.hpp
  - tree/heavy-light-decomposition.hpp
  isVerificationFile: true
  path: verify/verify-yosupo-graph/yosupo-lowest-common-ancestor.test.cpp
  requiredBy: []
  timestamp: '2020-08-05 02:19:06+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: verify/verify-yosupo-graph/yosupo-lowest-common-ancestor.test.cpp
layout: document
redirect_from:
- /verify/verify/verify-yosupo-graph/yosupo-lowest-common-ancestor.test.cpp
- /verify/verify/verify-yosupo-graph/yosupo-lowest-common-ancestor.test.cpp.html
title: verify/verify-yosupo-graph/yosupo-lowest-common-ancestor.test.cpp
---