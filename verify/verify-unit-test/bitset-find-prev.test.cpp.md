---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: misc/bitset-find-prev.hpp
    title: bitset::find_prev
  - icon: ':heavy_check_mark:'
    path: template/bitop.hpp
    title: template/bitop.hpp
  - icon: ':heavy_check_mark:'
    path: template/debug.hpp
    title: template/debug.hpp
  - icon: ':heavy_check_mark:'
    path: template/inout.hpp
    title: template/inout.hpp
  - icon: ':heavy_check_mark:'
    path: template/macro.hpp
    title: template/macro.hpp
  - icon: ':heavy_check_mark:'
    path: template/template.hpp
    title: template/template.hpp
  - icon: ':heavy_check_mark:'
    path: template/util.hpp
    title: template/util.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/aplusb
    links:
    - https://judge.yosupo.jp/problem/aplusb
  bundledCode: "#line 1 \"verify/verify-unit-test/bitset-find-prev.test.cpp\"\n#define\
    \ PROBLEM \"https://judge.yosupo.jp/problem/aplusb\"\n//\n#line 2 \"template/template.hpp\"\
    \nusing namespace std;\n\n// intrinstic\n#include <immintrin.h>\n\n#include <algorithm>\n\
    #include <array>\n#include <bitset>\n#include <cassert>\n#include <cctype>\n#include\
    \ <cfenv>\n#include <cfloat>\n#include <chrono>\n#include <cinttypes>\n#include\
    \ <climits>\n#include <cmath>\n#include <complex>\n#include <csetjmp>\n#include\
    \ <csignal>\n#include <cstdarg>\n#include <cstddef>\n#include <cstdint>\n#include\
    \ <cstdio>\n#include <cstdlib>\n#include <cstring>\n#include <ctime>\n#include\
    \ <deque>\n#include <exception>\n#include <forward_list>\n#include <fstream>\n\
    #include <functional>\n#include <initializer_list>\n#include <iomanip>\n#include\
    \ <ios>\n#include <iosfwd>\n#include <iostream>\n#include <istream>\n#include\
    \ <iterator>\n#include <limits>\n#include <list>\n#include <locale>\n#include\
    \ <map>\n#include <memory>\n#include <new>\n#include <numeric>\n#include <ostream>\n\
    #include <queue>\n#include <random>\n#include <ratio>\n#include <regex>\n#include\
    \ <set>\n#include <sstream>\n#include <stack>\n#include <stdexcept>\n#include\
    \ <streambuf>\n#include <string>\n#include <system_error>\n#include <tuple>\n\
    #include <type_traits>\n#include <typeinfo>\n#include <unordered_map>\n#include\
    \ <unordered_set>\n#include <utility>\n#include <valarray>\n#include <vector>\n\
    \n// utility\n#line 1 \"template/util.hpp\"\nnamespace Nyaan {\nusing ll = long\
    \ long;\nusing i64 = long long;\nusing u64 = unsigned long long;\nusing i128 =\
    \ __int128_t;\nusing u128 = __uint128_t;\n\ntemplate <typename T>\nusing V = vector<T>;\n\
    template <typename T>\nusing VV = vector<vector<T>>;\nusing vi = vector<int>;\n\
    using vl = vector<long long>;\nusing vd = V<double>;\nusing vs = V<string>;\n\
    using vvi = vector<vector<int>>;\nusing vvl = vector<vector<long long>>;\n\ntemplate\
    \ <typename T, typename U>\nstruct P : pair<T, U> {\n  template <typename... Args>\n\
    \  P(Args... args) : pair<T, U>(args...) {}\n\n  using pair<T, U>::first;\n  using\
    \ pair<T, U>::second;\n\n  T &x() { return first; }\n  const T &x() const { return\
    \ first; }\n  U &y() { return second; }\n  const U &y() const { return second;\
    \ }\n\n  P &operator+=(const P &r) {\n    first += r.first;\n    second += r.second;\n\
    \    return *this;\n  }\n  P &operator-=(const P &r) {\n    first -= r.first;\n\
    \    second -= r.second;\n    return *this;\n  }\n  P &operator*=(const P &r)\
    \ {\n    first *= r.first;\n    second *= r.second;\n    return *this;\n  }\n\
    \  P operator+(const P &r) const { return P(*this) += r; }\n  P operator-(const\
    \ P &r) const { return P(*this) -= r; }\n  P operator*(const P &r) const { return\
    \ P(*this) *= r; }\n};\n\nusing pl = P<ll, ll>;\nusing pi = P<int, int>;\nusing\
    \ vp = V<pl>;\n\nconstexpr int inf = 1001001001;\nconstexpr long long infLL =\
    \ 4004004004004004004LL;\n\ntemplate <typename T>\nint sz(const T &t) {\n  return\
    \ t.size();\n}\ntemplate <typename T, size_t N>\nvoid mem(T (&a)[N], int c) {\n\
    \  memset(a, c, sizeof(T) * N);\n}\n\ntemplate <typename T, typename U>\ninline\
    \ bool amin(T &x, U y) {\n  return (y < x) ? (x = y, true) : false;\n}\ntemplate\
    \ <typename T, typename U>\ninline bool amax(T &x, U y) {\n  return (x < y) ?\
    \ (x = y, true) : false;\n}\n\ntemplate <typename T>\nint lb(const vector<T> &v,\
    \ const T &a) {\n  return lower_bound(begin(v), end(v), a) - begin(v);\n}\ntemplate\
    \ <typename T>\nint ub(const vector<T> &v, const T &a) {\n  return upper_bound(begin(v),\
    \ end(v), a) - begin(v);\n}\n\nconstexpr long long TEN(int n) {\n  long long ret\
    \ = 1, x = 10;\n  for (; n; x *= x, n >>= 1) ret *= (n & 1 ? x : 1);\n  return\
    \ ret;\n}\n\ntemplate <typename T, typename U>\npair<T, U> mkp(const T &t, const\
    \ U &u) {\n  return make_pair(t, u);\n}\n\ntemplate <typename T>\nvector<T> mkrui(const\
    \ vector<T> &v, bool rev = false) {\n  vector<T> ret(v.size() + 1);\n  if (rev)\
    \ {\n    for (int i = int(v.size()) - 1; i >= 0; i--) ret[i] = v[i] + ret[i +\
    \ 1];\n  } else {\n    for (int i = 0; i < int(v.size()); i++) ret[i + 1] = ret[i]\
    \ + v[i];\n  }\n  return ret;\n};\n\ntemplate <typename T>\nvector<T> mkuni(const\
    \ vector<T> &v) {\n  vector<T> ret(v);\n  sort(ret.begin(), ret.end());\n  ret.erase(unique(ret.begin(),\
    \ ret.end()), ret.end());\n  return ret;\n}\n\ntemplate <typename F>\nvector<int>\
    \ mkord(int N, F f) {\n  vector<int> ord(N);\n  iota(begin(ord), end(ord), 0);\n\
    \  sort(begin(ord), end(ord), f);\n  return ord;\n}\n\ntemplate <typename T>\n\
    vector<T> reord(const vector<T> &v, const vector<T> &ord) {\n  int N = v.size();\n\
    \  vector<T> ret(N);\n  for (int i = 0; i < N; i++) ret[i] = v[ord[i]];\n  return\
    \ ret;\n};\n\ntemplate <typename T = int>\nvector<T> mkiota(int N) {\n  vector<T>\
    \ ret(N);\n  iota(begin(ret), end(ret), 0);\n  return ret;\n}\n\ntemplate <typename\
    \ T>\nvector<int> mkinv(vector<T> &v, int max_val = -1) {\n  if (max_val < (int)v.size())\
    \ max_val = v.size() - 1;\n  vector<int> inv(max_val + 1, -1);\n  for (int i =\
    \ 0; i < (int)v.size(); i++) inv[v[i]] = i;\n  return inv;\n}\n\n}  // namespace\
    \ Nyaan\n#line 70 \"template/template.hpp\"\n\n// bit operation\n#line 1 \"template/bitop.hpp\"\
    \nnamespace Nyaan {\n\n__attribute__((target(\"popcnt\"))) inline int popcnt(const\
    \ u64 &a) {\n  return _mm_popcnt_u64(a);\n}\n\n__attribute__((target(\"bmi\")))\
    \ inline int lsb(const u64 &a) {\n  return _tzcnt_u64(a);\n}\n__attribute__((target(\"\
    bmi\"))) inline int ctz(const u64 &a) {\n  return _tzcnt_u64(a);\n}\n\n__attribute__((target(\"\
    lzcnt\"))) inline int msb(const u64 &a) {\n  return 63 - _lzcnt_u64(a);\n}\n__attribute__((target(\"\
    lzcnt\"))) inline int clz64(const u64 &a) {\n  return _lzcnt_u64(a);\n}\n\ntemplate\
    \ <typename T>\ninline int gbit(const T &a, int i) {\n  return (a >> i) & 1;\n\
    }\ntemplate <typename T>\ninline void sbit(T &a, int i, bool b) {\n  a ^= (gbit(a,\
    \ i) == b ? 0 : (T(b) << i));\n}\n\nconstexpr long long PW(int n) { return 1LL\
    \ << n; }\n\nconstexpr long long MSK(int n) { return (1LL << n) - 1; }\n\n}  //\
    \ namespace Nyaan\n#line 73 \"template/template.hpp\"\n\n// inout\n#line 1 \"\
    template/inout.hpp\"\nnamespace Nyaan {\n\ntemplate <typename T, typename U>\n\
    ostream &operator<<(ostream &os, const pair<T, U> &p) {\n  os << p.first << \"\
    \ \" << p.second;\n  return os;\n}\ntemplate <typename T, typename U>\nistream\
    \ &operator>>(istream &is, pair<T, U> &p) {\n  is >> p.first >> p.second;\n  return\
    \ is;\n}\n\ntemplate <typename T>\nostream &operator<<(ostream &os, const vector<T>\
    \ &v) {\n  int s = (int)v.size();\n  for (int i = 0; i < s; i++) os << (i ? \"\
    \ \" : \"\") << v[i];\n  return os;\n}\ntemplate <typename T>\nistream &operator>>(istream\
    \ &is, vector<T> &v) {\n  for (auto &x : v) is >> x;\n  return is;\n}\n\nvoid\
    \ in() {}\ntemplate <typename T, class... U>\nvoid in(T &t, U &... u) {\n  cin\
    \ >> t;\n  in(u...);\n}\n\nvoid out() { cout << \"\\n\"; }\ntemplate <typename\
    \ T, class... U, char sep = ' '>\nvoid out(const T &t, const U &... u) {\n  cout\
    \ << t;\n  if (sizeof...(u)) cout << sep;\n  out(u...);\n}\n\nvoid outr() {}\n\
    template <typename T, class... U, char sep = ' '>\nvoid outr(const T &t, const\
    \ U &... u) {\n  cout << t;\n  outr(u...);\n}\n\nstruct IoSetupNya {\n  IoSetupNya()\
    \ {\n    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed\
    \ << setprecision(15);\n    cerr << fixed << setprecision(7);\n  }\n} iosetupnya;\n\
    \n}  // namespace Nyaan\n#line 76 \"template/template.hpp\"\n\n// debug\n#line\
    \ 1 \"template/debug.hpp\"\nnamespace DebugImpl {\n\ntemplate <typename U, typename\
    \ = void>\nstruct is_specialize : false_type {};\ntemplate <typename U>\nstruct\
    \ is_specialize<\n    U, typename conditional<false, typename U::iterator, void>::type>\n\
    \    : true_type {};\ntemplate <typename U>\nstruct is_specialize<\n    U, typename\
    \ conditional<false, decltype(U::first), void>::type>\n    : true_type {};\ntemplate\
    \ <typename U>\nstruct is_specialize<U, enable_if_t<is_integral<U>::value, void>>\
    \ : true_type {\n};\n\nvoid dump(const char& t) { cerr << t; }\n\nvoid dump(const\
    \ string& t) { cerr << t; }\n\ntemplate <typename U,\n          enable_if_t<!is_specialize<U>::value,\
    \ nullptr_t> = nullptr>\nvoid dump(const U& t) {\n  cerr << t;\n}\n\ntemplate\
    \ <typename T>\nvoid dump(const T& t, enable_if_t<is_integral<T>::value>* = nullptr)\
    \ {\n  string res;\n  if (t == Nyaan::inf) res = \"inf\";\n  if (is_signed<T>::value)\n\
    \    if (t == -Nyaan::inf) res = \"-inf\";\n  if (sizeof(T) == 8) {\n    if (t\
    \ == Nyaan::infLL) res = \"inf\";\n    if (is_signed<T>::value)\n      if (t ==\
    \ -Nyaan::infLL) res = \"-inf\";\n  }\n  if (res.empty()) res = to_string(t);\n\
    \  cerr << res;\n}\n\ntemplate <typename T, typename U>\nvoid dump(const pair<T,\
    \ U>&);\ntemplate <typename T>\nvoid dump(const pair<T*, int>&);\n\ntemplate <typename\
    \ T>\nvoid dump(const T& t,\n          enable_if_t<!is_void<typename T::iterator>::value>*\
    \ = nullptr) {\n  cerr << \"[ \";\n  for (auto it = t.begin(); it != t.end();)\
    \ {\n    dump(*it);\n    cerr << (++it == t.end() ? \"\" : \", \");\n  }\n  cerr\
    \ << \" ]\";\n}\n\ntemplate <typename T, typename U>\nvoid dump(const pair<T,\
    \ U>& t) {\n  cerr << \"( \";\n  dump(t.first);\n  cerr << \", \";\n  dump(t.second);\n\
    \  cerr << \" )\";\n}\n\ntemplate <typename T>\nvoid dump(const pair<T*, int>&\
    \ t) {\n  cerr << \"[ \";\n  for (int i = 0; i < t.second; i++) {\n    dump(t.first[i]);\n\
    \    cerr << (i == t.second - 1 ? \"\" : \", \");\n  }\n  cerr << \" ]\";\n}\n\
    \nvoid trace() { cerr << endl; }\ntemplate <typename Head, typename... Tail>\n\
    void trace(Head&& head, Tail&&... tail) {\n  cerr << \" \";\n  dump(head);\n \
    \ if (sizeof...(tail) != 0) cerr << \",\";\n  trace(forward<Tail>(tail)...);\n\
    }\n\n}  // namespace DebugImpl\n\n#ifdef NyaanDebug\n#define trc(...)        \
    \                    \\\n  do {                                      \\\n    cerr\
    \ << \"## \" << #__VA_ARGS__ << \" = \"; \\\n    DebugImpl::trace(__VA_ARGS__);\
    \          \\\n  } while (0)\n#else\n#define trc(...)\n#endif\n#line 79 \"template/template.hpp\"\
    \n\n// macro\n#line 1 \"template/macro.hpp\"\n#define each(x, v) for (auto&& x\
    \ : v)\n#define each2(x, y, v) for (auto&& [x, y] : v)\n#define all(v) (v).begin(),\
    \ (v).end()\n#define rep(i, N) for (long long i = 0; i < (long long)(N); i++)\n\
    #define repr(i, N) for (long long i = (long long)(N)-1; i >= 0; i--)\n#define\
    \ rep1(i, N) for (long long i = 1; i <= (long long)(N); i++)\n#define repr1(i,\
    \ N) for (long long i = (N); (long long)(i) > 0; i--)\n#define reg(i, a, b) for\
    \ (long long i = (a); i < (b); i++)\n#define regr(i, a, b) for (long long i =\
    \ (b)-1; i >= (a); i--)\n#define repc(i, a, cond) for (long long i = (a); (cond);\
    \ i++)\n#define enm(i, val, vec)                                  \\\n  for (long\
    \ long i = 0; i < (long long)(vec).size(); i++) \\\n    if (auto& val = vec[i];\
    \ false)                        \\\n      ;                                  \
    \                 \\\n    else\n\n#define ini(...)   \\\n  int __VA_ARGS__; \\\
    \n  in(__VA_ARGS__)\n#define inl(...)         \\\n  long long __VA_ARGS__; \\\n\
    \  in(__VA_ARGS__)\n#define ins(...)      \\\n  string __VA_ARGS__; \\\n  in(__VA_ARGS__)\n\
    #define inc(...)    \\\n  char __VA_ARGS__; \\\n  in(__VA_ARGS__)\n#define in2(s,\
    \ t)                           \\\n  for (int i = 0; i < (int)s.size(); i++) {\
    \ \\\n    in(s[i], t[i]);                         \\\n  }\n#define in3(s, t, u)\
    \                        \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\n\
    \    in(s[i], t[i], u[i]);                   \\\n  }\n#define in4(s, t, u, v)\
    \                     \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\n   \
    \ in(s[i], t[i], u[i], v[i]);             \\\n  }\n\n#define die(...)        \
    \     \\\n  do {                       \\\n    Nyaan::out(__VA_ARGS__); \\\n \
    \   return;                  \\\n  } while (0)\n#line 82 \"template/template.hpp\"\
    \n\nnamespace Nyaan {\nvoid solve();\n}\nint main() { Nyaan::solve(); }\n#line\
    \ 4 \"verify/verify-unit-test/bitset-find-prev.test.cpp\"\n//\n#line 2 \"misc/bitset-find-prev.hpp\"\
    \n\n// \u53C2\u8003\uFF1Ahttps://github.com/gcc-mirror/gcc/blob/master/libstdc%2B%2B-v3/include/std/bitset\n\
    template <size_t Nb>\nstruct Bitset : bitset<Nb> {\n  template <typename... Args>\n\
    \  Bitset(Args... args) : bitset<Nb>(args...) {}\n\n  static constexpr int N =\
    \ Nb;\n  static constexpr int array_size = (Nb + 63) / 64;\n\n  union raw_cast\
    \ {\n    array<uint64_t, array_size> a;\n    Bitset b;\n  };\n\n  int _Find_prev(size_t\
    \ i) const {\n    if (i == 0) return -1;\n    if ((*this)[--i] == true) return\
    \ i;\n    size_t M = i / 64;\n    const auto& a = ((raw_cast*)(this))->a;\n  \
    \  uint64_t buf = a[M] & ((1ull << (i & 63)) - 1);\n    if (buf != 0) return M\
    \ * 64 + 63 - __builtin_clzll(buf);\n    while (M--) {\n      if (a[M] != 0) return\
    \ M * 64 + 63 - __builtin_clzll(a[M]);\n    }\n    return -1;\n  }\n\n  inline\
    \ int _Find_last() const { return _Find_prev(N); }\n};\n\n/**\n * @brief bitset::find_prev\n\
    \ */\n#line 6 \"verify/verify-unit-test/bitset-find-prev.test.cpp\"\n\nusing namespace\
    \ Nyaan;\n\ntemplate <int N>\nvoid verify(int seed) {\n  Bitset<N> bs;\n  int\
    \ rng = seed;\n  rep(i, N) bs[i] = (rng >> 1) & 1, rng = rng * 1928373 % 10203913;\n\
    \n  int last = N;\n  while (true) {\n    int i = bs._Find_prev(last);\n    if\
    \ (i == -1) break;\n    assert(0 <= i and i < N);\n    assert(bs[i] == 1);\n \
    \   assert(i < last);\n    bs[i].flip();\n    last = i;\n  }\n  assert(bs.any()\
    \ == false);\n}\n\n/*\n\n// for time measurement\n\n#include \"../../misc/timer.hpp\"\
    \nvoid test() {\n  constexpr int N = 100000000;\n  int loop = 100;\n  Bitset<N>\
    \ *p = new Bitset<N>;\n  Bitset<N> &bs = *p;\n\n  Timer timer;\n  auto init =\
    \ [&]() {\n    int rng = 10;\n    while (rng < N) bs[rng] = 1, rng += 20;\n  };\n\
    \n  // prev_naive\n  {\n    timer.reset();\n    rep(_, loop / 10) {\n      init();\n\
    \      int last = N;\n      while (true) {\n        int i = last - 1;\n      \
    \  while (i != -1 and bs[i] == 0) i--;\n        if (i == -1) break;\n        bs[i].flip();\n\
    \        last = i;\n      }\n    }\n    out(\"naive\", timer.elapsed());\n   \
    \ assert(bs.any() == false);\n  }\n\n  // prev\n  {\n    timer.reset();\n    rep(i,\
    \ loop) {\n      init();\n      int last = N;\n      while (true) {\n        int\
    \ i = bs._Find_prev(last);\n        if (i == -1) break;\n        bs[i].flip();\n\
    \        last = i;\n      }\n    }\n    out(\"prev\", timer.elapsed());\n    assert(bs.any()\
    \ == false);\n  }\n\n  // next\n  {\n    timer.reset();\n    rep(i, loop) {\n\
    \      init();\n      int last = bs._Find_first();\n      bs[last].flip();\n \
    \     while (true) {\n        int i = bs._Find_next(last);\n        if (i == N)\
    \ break;\n        bs[i].flip();\n        last = i;\n      }\n    }\n    out(\"\
    next\", timer.elapsed());\n    assert(bs.any() == false);\n  }\n}\n*/\n\nBitset<TEN(7)>\
    \ bs;\n\nvoid Nyaan::solve() {\n  // test();\n  rep(i, 1000) verify<8191>(i);\n\
    \  rep(i, 1000) verify<8192>(i);\n  rep(i, 1000) verify<8193>(i);\n\n  int a,\
    \ b;\n  cin >> a >> b;\n  cout << (a + b) << endl;\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/aplusb\"\n//\n#include\
    \ \"../../template/template.hpp\"\n//\n#include \"../../misc/bitset-find-prev.hpp\"\
    \n\nusing namespace Nyaan;\n\ntemplate <int N>\nvoid verify(int seed) {\n  Bitset<N>\
    \ bs;\n  int rng = seed;\n  rep(i, N) bs[i] = (rng >> 1) & 1, rng = rng * 1928373\
    \ % 10203913;\n\n  int last = N;\n  while (true) {\n    int i = bs._Find_prev(last);\n\
    \    if (i == -1) break;\n    assert(0 <= i and i < N);\n    assert(bs[i] == 1);\n\
    \    assert(i < last);\n    bs[i].flip();\n    last = i;\n  }\n  assert(bs.any()\
    \ == false);\n}\n\n/*\n\n// for time measurement\n\n#include \"../../misc/timer.hpp\"\
    \nvoid test() {\n  constexpr int N = 100000000;\n  int loop = 100;\n  Bitset<N>\
    \ *p = new Bitset<N>;\n  Bitset<N> &bs = *p;\n\n  Timer timer;\n  auto init =\
    \ [&]() {\n    int rng = 10;\n    while (rng < N) bs[rng] = 1, rng += 20;\n  };\n\
    \n  // prev_naive\n  {\n    timer.reset();\n    rep(_, loop / 10) {\n      init();\n\
    \      int last = N;\n      while (true) {\n        int i = last - 1;\n      \
    \  while (i != -1 and bs[i] == 0) i--;\n        if (i == -1) break;\n        bs[i].flip();\n\
    \        last = i;\n      }\n    }\n    out(\"naive\", timer.elapsed());\n   \
    \ assert(bs.any() == false);\n  }\n\n  // prev\n  {\n    timer.reset();\n    rep(i,\
    \ loop) {\n      init();\n      int last = N;\n      while (true) {\n        int\
    \ i = bs._Find_prev(last);\n        if (i == -1) break;\n        bs[i].flip();\n\
    \        last = i;\n      }\n    }\n    out(\"prev\", timer.elapsed());\n    assert(bs.any()\
    \ == false);\n  }\n\n  // next\n  {\n    timer.reset();\n    rep(i, loop) {\n\
    \      init();\n      int last = bs._Find_first();\n      bs[last].flip();\n \
    \     while (true) {\n        int i = bs._Find_next(last);\n        if (i == N)\
    \ break;\n        bs[i].flip();\n        last = i;\n      }\n    }\n    out(\"\
    next\", timer.elapsed());\n    assert(bs.any() == false);\n  }\n}\n*/\n\nBitset<TEN(7)>\
    \ bs;\n\nvoid Nyaan::solve() {\n  // test();\n  rep(i, 1000) verify<8191>(i);\n\
    \  rep(i, 1000) verify<8192>(i);\n  rep(i, 1000) verify<8193>(i);\n\n  int a,\
    \ b;\n  cin >> a >> b;\n  cout << (a + b) << endl;\n}\n"
  dependsOn:
  - template/template.hpp
  - template/util.hpp
  - template/bitop.hpp
  - template/inout.hpp
  - template/debug.hpp
  - template/macro.hpp
  - misc/bitset-find-prev.hpp
  isVerificationFile: true
  path: verify/verify-unit-test/bitset-find-prev.test.cpp
  requiredBy: []
  timestamp: '2021-04-19 21:35:56+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: verify/verify-unit-test/bitset-find-prev.test.cpp
layout: document
redirect_from:
- /verify/verify/verify-unit-test/bitset-find-prev.test.cpp
- /verify/verify/verify-unit-test/bitset-find-prev.test.cpp.html
title: verify/verify-unit-test/bitset-find-prev.test.cpp
---