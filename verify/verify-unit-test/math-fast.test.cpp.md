---
data:
  _extendedDependsOn:
  - icon: ':x:'
    path: math-fast/gcd.hpp
    title: binary GCD
  - icon: ':question:'
    path: template/bitop.hpp
    title: template/bitop.hpp
  - icon: ':question:'
    path: template/debug.hpp
    title: template/debug.hpp
  - icon: ':question:'
    path: template/inout.hpp
    title: template/inout.hpp
  - icon: ':question:'
    path: template/macro.hpp
    title: template/macro.hpp
  - icon: ':question:'
    path: template/template.hpp
    title: template/template.hpp
  - icon: ':question:'
    path: template/util.hpp
    title: template/util.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/aplusb
    links:
    - https://judge.yosupo.jp/problem/aplusb
  bundledCode: "#line 1 \"verify/verify-unit-test/math-fast.test.cpp\"\n#define PROBLEM\
    \ \"https://judge.yosupo.jp/problem/aplusb\"\n\n#line 2 \"template/template.hpp\"\
    \nusing namespace std;\n\n// intrinstic\n#include <immintrin.h>\n\n#include <algorithm>\n\
    #include <array>\n#include <bitset>\n#include <cassert>\n#include <cctype>\n#include\
    \ <cfenv>\n#include <cfloat>\n#include <chrono>\n#include <cinttypes>\n#include\
    \ <climits>\n#include <cmath>\n#include <complex>\n#include <cstdarg>\n#include\
    \ <cstddef>\n#include <cstdint>\n#include <cstdio>\n#include <cstdlib>\n#include\
    \ <cstring>\n#include <deque>\n#include <fstream>\n#include <functional>\n#include\
    \ <initializer_list>\n#include <iomanip>\n#include <ios>\n#include <iostream>\n\
    #include <istream>\n#include <iterator>\n#include <limits>\n#include <list>\n\
    #include <map>\n#include <memory>\n#include <new>\n#include <numeric>\n#include\
    \ <ostream>\n#include <queue>\n#include <random>\n#include <set>\n#include <sstream>\n\
    #include <stack>\n#include <streambuf>\n#include <string>\n#include <tuple>\n\
    #include <type_traits>\n#include <typeinfo>\n#include <unordered_map>\n#include\
    \ <unordered_set>\n#include <utility>\n#include <vector>\n\n// utility\n#line\
    \ 1 \"template/util.hpp\"\nnamespace Nyaan {\nusing ll = long long;\nusing i64\
    \ = long long;\nusing u64 = unsigned long long;\nusing i128 = __int128_t;\nusing\
    \ u128 = __uint128_t;\n\ntemplate <typename T>\nusing V = vector<T>;\ntemplate\
    \ <typename T>\nusing VV = vector<vector<T>>;\nusing vi = vector<int>;\nusing\
    \ vl = vector<long long>;\nusing vd = V<double>;\nusing vs = V<string>;\nusing\
    \ vvi = vector<vector<int>>;\nusing vvl = vector<vector<long long>>;\n\ntemplate\
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
    \ t.size();\n}\n\ntemplate <typename T, typename U>\ninline bool amin(T &x, U\
    \ y) {\n  return (y < x) ? (x = y, true) : false;\n}\ntemplate <typename T, typename\
    \ U>\ninline bool amax(T &x, U y) {\n  return (x < y) ? (x = y, true) : false;\n\
    }\n\ntemplate <typename T>\ninline T Max(const vector<T> &v) {\n  return *max_element(begin(v),\
    \ end(v));\n}\ntemplate <typename T>\ninline T Min(const vector<T> &v) {\n  return\
    \ *min_element(begin(v), end(v));\n}\ntemplate <typename T>\ninline long long\
    \ Sum(const vector<T> &v) {\n  return accumulate(begin(v), end(v), 0LL);\n}\n\n\
    template <typename T>\nint lb(const vector<T> &v, const T &a) {\n  return lower_bound(begin(v),\
    \ end(v), a) - begin(v);\n}\ntemplate <typename T>\nint ub(const vector<T> &v,\
    \ const T &a) {\n  return upper_bound(begin(v), end(v), a) - begin(v);\n}\n\n\
    constexpr long long TEN(int n) {\n  long long ret = 1, x = 10;\n  for (; n; x\
    \ *= x, n >>= 1) ret *= (n & 1 ? x : 1);\n  return ret;\n}\n\ntemplate <typename\
    \ T, typename U>\npair<T, U> mkp(const T &t, const U &u) {\n  return make_pair(t,\
    \ u);\n}\n\ntemplate <typename T>\nvector<T> mkrui(const vector<T> &v, bool rev\
    \ = false) {\n  vector<T> ret(v.size() + 1);\n  if (rev) {\n    for (int i = int(v.size())\
    \ - 1; i >= 0; i--) ret[i] = v[i] + ret[i + 1];\n  } else {\n    for (int i =\
    \ 0; i < int(v.size()); i++) ret[i + 1] = ret[i] + v[i];\n  }\n  return ret;\n\
    };\n\ntemplate <typename T>\nvector<T> mkuni(const vector<T> &v) {\n  vector<T>\
    \ ret(v);\n  sort(ret.begin(), ret.end());\n  ret.erase(unique(ret.begin(), ret.end()),\
    \ ret.end());\n  return ret;\n}\n\ntemplate <typename F>\nvector<int> mkord(int\
    \ N, F f) {\n  vector<int> ord(N);\n  iota(begin(ord), end(ord), 0);\n  sort(begin(ord),\
    \ end(ord), f);\n  return ord;\n}\n\ntemplate <typename T>\nvector<int> mkinv(vector<T>\
    \ &v) {\n  int max_val = *max_element(begin(v), end(v));\n  vector<int> inv(max_val\
    \ + 1, -1);\n  for (int i = 0; i < (int)v.size(); i++) inv[v[i]] = i;\n  return\
    \ inv;\n}\n\n}  // namespace Nyaan\n#line 58 \"template/template.hpp\"\n\n// bit\
    \ operation\n#line 1 \"template/bitop.hpp\"\nnamespace Nyaan {\n__attribute__((target(\"\
    popcnt\"))) inline int popcnt(const u64 &a) {\n  return _mm_popcnt_u64(a);\n}\n\
    inline int lsb(const u64 &a) { return a ? __builtin_ctzll(a) : 64; }\ninline int\
    \ ctz(const u64 &a) { return a ? __builtin_ctzll(a) : 64; }\ninline int msb(const\
    \ u64 &a) { return a ? 63 - __builtin_clzll(a) : -1; }\ntemplate <typename T>\n\
    inline int gbit(const T &a, int i) {\n  return (a >> i) & 1;\n}\ntemplate <typename\
    \ T>\ninline void sbit(T &a, int i, bool b) {\n  if (gbit(a, i) != b) a ^= T(1)\
    \ << i;\n}\nconstexpr long long PW(int n) { return 1LL << n; }\nconstexpr long\
    \ long MSK(int n) { return (1LL << n) - 1; }\n}  // namespace Nyaan\n#line 61\
    \ \"template/template.hpp\"\n\n// inout\n#line 1 \"template/inout.hpp\"\nnamespace\
    \ Nyaan {\n\ntemplate <typename T, typename U>\nostream &operator<<(ostream &os,\
    \ const pair<T, U> &p) {\n  os << p.first << \" \" << p.second;\n  return os;\n\
    }\ntemplate <typename T, typename U>\nistream &operator>>(istream &is, pair<T,\
    \ U> &p) {\n  is >> p.first >> p.second;\n  return is;\n}\n\ntemplate <typename\
    \ T>\nostream &operator<<(ostream &os, const vector<T> &v) {\n  int s = (int)v.size();\n\
    \  for (int i = 0; i < s; i++) os << (i ? \" \" : \"\") << v[i];\n  return os;\n\
    }\ntemplate <typename T>\nistream &operator>>(istream &is, vector<T> &v) {\n \
    \ for (auto &x : v) is >> x;\n  return is;\n}\n\nvoid in() {}\ntemplate <typename\
    \ T, class... U>\nvoid in(T &t, U &... u) {\n  cin >> t;\n  in(u...);\n}\n\nvoid\
    \ out() { cout << \"\\n\"; }\ntemplate <typename T, class... U, char sep = ' '>\n\
    void out(const T &t, const U &... u) {\n  cout << t;\n  if (sizeof...(u)) cout\
    \ << sep;\n  out(u...);\n}\n\nvoid outr() {}\ntemplate <typename T, class... U,\
    \ char sep = ' '>\nvoid outr(const T &t, const U &... u) {\n  cout << t;\n  outr(u...);\n\
    }\n\nstruct IoSetupNya {\n  IoSetupNya() {\n    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n\
    \    cout << fixed << setprecision(15);\n    cerr << fixed << setprecision(7);\n\
    \  }\n} iosetupnya;\n\n}  // namespace Nyaan\n#line 64 \"template/template.hpp\"\
    \n\n// debug\n#line 1 \"template/debug.hpp\"\nnamespace DebugImpl {\n\ntemplate\
    \ <typename U, typename = void>\nstruct is_specialize : false_type {};\ntemplate\
    \ <typename U>\nstruct is_specialize<\n    U, typename conditional<false, typename\
    \ U::iterator, void>::type>\n    : true_type {};\ntemplate <typename U>\nstruct\
    \ is_specialize<\n    U, typename conditional<false, decltype(U::first), void>::type>\n\
    \    : true_type {};\ntemplate <typename U>\nstruct is_specialize<U, enable_if_t<is_integral<U>::value,\
    \ void>> : true_type {\n};\n\nvoid dump(const char& t) { cerr << t; }\n\nvoid\
    \ dump(const string& t) { cerr << t; }\n\nvoid dump(const bool& t) { cerr << (t\
    \ ? \"true\" : \"false\"); }\n\ntemplate <typename U,\n          enable_if_t<!is_specialize<U>::value,\
    \ nullptr_t> = nullptr>\nvoid dump(const U& t) {\n  cerr << t;\n}\n\ntemplate\
    \ <typename T>\nvoid dump(const T& t, enable_if_t<is_integral<T>::value>* = nullptr)\
    \ {\n  string res;\n  if (t == Nyaan::inf) res = \"inf\";\n  if constexpr (is_signed<T>::value)\
    \ {\n    if (t == -Nyaan::inf) res = \"-inf\";\n  }\n  if constexpr (sizeof(T)\
    \ == 8) {\n    if (t == Nyaan::infLL) res = \"inf\";\n    if constexpr (is_signed<T>::value)\
    \ {\n      if (t == -Nyaan::infLL) res = \"-inf\";\n    }\n  }\n  if (res.empty())\
    \ res = to_string(t);\n  cerr << res;\n}\n\ntemplate <typename T, typename U>\n\
    void dump(const pair<T, U>&);\ntemplate <typename T>\nvoid dump(const pair<T*,\
    \ int>&);\n\ntemplate <typename T>\nvoid dump(const T& t,\n          enable_if_t<!is_void<typename\
    \ T::iterator>::value>* = nullptr) {\n  cerr << \"[ \";\n  for (auto it = t.begin();\
    \ it != t.end();) {\n    dump(*it);\n    cerr << (++it == t.end() ? \"\" : \"\
    , \");\n  }\n  cerr << \" ]\";\n}\n\ntemplate <typename T, typename U>\nvoid dump(const\
    \ pair<T, U>& t) {\n  cerr << \"( \";\n  dump(t.first);\n  cerr << \", \";\n \
    \ dump(t.second);\n  cerr << \" )\";\n}\n\ntemplate <typename T>\nvoid dump(const\
    \ pair<T*, int>& t) {\n  cerr << \"[ \";\n  for (int i = 0; i < t.second; i++)\
    \ {\n    dump(t.first[i]);\n    cerr << (i == t.second - 1 ? \"\" : \", \");\n\
    \  }\n  cerr << \" ]\";\n}\n\nvoid trace() { cerr << endl; }\ntemplate <typename\
    \ Head, typename... Tail>\nvoid trace(Head&& head, Tail&&... tail) {\n  cerr <<\
    \ \" \";\n  dump(head);\n  if (sizeof...(tail) != 0) cerr << \",\";\n  trace(forward<Tail>(tail)...);\n\
    }\n\n}  // namespace DebugImpl\n\n#ifdef NyaanDebug\n#define trc(...)        \
    \                    \\\n  do {                                      \\\n    cerr\
    \ << \"## \" << #__VA_ARGS__ << \" = \"; \\\n    DebugImpl::trace(__VA_ARGS__);\
    \          \\\n  } while (0)\n#else\n#define trc(...) (void(0))\n#endif\n#line\
    \ 67 \"template/template.hpp\"\n\n// macro\n#line 1 \"template/macro.hpp\"\n#define\
    \ each(x, v) for (auto&& x : v)\n#define each2(x, y, v) for (auto&& [x, y] : v)\n\
    #define all(v) (v).begin(), (v).end()\n#define rep(i, N) for (long long i = 0;\
    \ i < (long long)(N); i++)\n#define repr(i, N) for (long long i = (long long)(N)-1;\
    \ i >= 0; i--)\n#define rep1(i, N) for (long long i = 1; i <= (long long)(N);\
    \ i++)\n#define repr1(i, N) for (long long i = (N); (long long)(i) > 0; i--)\n\
    #define reg(i, a, b) for (long long i = (a); i < (b); i++)\n#define regr(i, a,\
    \ b) for (long long i = (b)-1; i >= (a); i--)\n#define fi first\n#define se second\n\
    #define ini(...)   \\\n  int __VA_ARGS__; \\\n  in(__VA_ARGS__)\n#define inl(...)\
    \         \\\n  long long __VA_ARGS__; \\\n  in(__VA_ARGS__)\n#define ins(...)\
    \      \\\n  string __VA_ARGS__; \\\n  in(__VA_ARGS__)\n#define in2(s, t)    \
    \                       \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\n \
    \   in(s[i], t[i]);                         \\\n  }\n#define in3(s, t, u)    \
    \                    \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\n    in(s[i],\
    \ t[i], u[i]);                   \\\n  }\n#define in4(s, t, u, v)            \
    \         \\\n  for (int i = 0; i < (int)s.size(); i++) { \\\n    in(s[i], t[i],\
    \ u[i], v[i]);             \\\n  }\n#define die(...)             \\\n  do {  \
    \                     \\\n    Nyaan::out(__VA_ARGS__); \\\n    return;       \
    \           \\\n  } while (0)\n#line 70 \"template/template.hpp\"\n\nnamespace\
    \ Nyaan {\nvoid solve();\n}\nint main() { Nyaan::solve(); }\n#line 4 \"verify/verify-unit-test/math-fast.test.cpp\"\
    \n//\n#line 2 \"math-fast/gcd.hpp\"\n\n#line 4 \"math-fast/gcd.hpp\"\nusing namespace\
    \ std;\n\nnamespace BinaryGCDImpl {\nusing u64 = unsigned long long;\nusing i8\
    \ = char;\n\ninline u64 binary_gcd(u64 a, u64 b) {\n  if (a == 0 || b == 0) return\
    \ a + b;\n  i8 n = __builtin_ctzll(a);\n  i8 m = __builtin_ctzll(b);\n  a >>=\
    \ n;\n  b >>= m;\n  n = min(n, m);\n  while (a != b) {\n    u64 d = a - b;\n \
    \   i8 s = __builtin_ctzll(d);\n    bool f = a > b;\n    b = f ? b : a;\n    a\
    \ = (f ? d : -d) >> s;\n  }\n  return a << n;\n}\n}  // namespace BinaryGCDImpl\n\
    \nlong long gcd(long long a, long long b) {\n  return BinaryGCDImpl::binary_gcd(abs(a),\
    \ abs(b));\n}\nlong long lcm(long long a, long long b) { return a / gcd(a, b)\
    \ * b; }\n\n/**\n * @brief binary GCD\n */\n#line 6 \"verify/verify-unit-test/math-fast.test.cpp\"\
    \n\nnamespace fast_gcd_verify {\n\nusing i64 = long long;\n\ni64 naive_gcd(i64\
    \ a, i64 b) {\n  while (b) swap(a %= b, b);\n  return a;\n}\n\ni64 x_;\nvoid rng_init()\
    \ { x_ = 88172645463325252ULL; }\ni64 rng() { return x_ = x_ ^ (x_ << 7), x_ =\
    \ x_ ^ (x_ >> 9); }\n\nvoid unit_test() {\n  using P = pair<i64, i64>;\n  using\
    \ F = i64 (*)(i64, i64);\n\n  vector<P> testcase{P(2, 4),\n                  \
    \   P(100000, 10000),\n                     P(998244353, 1000000007),\n      \
    \               P(1LL << 40, 1LL << 60),\n                     P((1LL << 61) -\
    \ 1, 11111111111111111),\n                     P((1LL << 60) + 1, (1LL << 59)\
    \ + 1),\n                     P(1LL << 62, 1LL << 62),\n                     P(1LL\
    \ << 62, 1LL << 61),\n                     P(3LL << 61, 9LL << 60),\n        \
    \             P((1uLL << 63) - 1, (1LL << 62)),\n                     P(0, 1),\n\
    \                     P(1, 0),\n                     P(0, 0),\n              \
    \       P(0, -1),\n                     P(-1, 0),\n                     P(-1,\
    \ -1)};\n  for (i64 i = 1000; i--;)\n    for (i64 j = 1000; j--;) testcase.emplace_back(i,\
    \ j);\n  rng_init();\n  for (i64 n = 10000; n--;) {\n    i64 i = rng(), j = rng();\n\
    \    testcase.emplace_back(i, j);\n  }\n\n  vector<F> functions{std::__gcd<int64_t>,\
    \ naive_gcd, gcd};\n\n  for (auto p : testcase) {\n    unordered_set<i64> s;\n\
    \    for (auto &f : functions) {\n      s.insert(abs(f(p.first, p.second)));\n\
    \    }\n    if (s.size() != 1u) {\n      cerr << \"verify failed.\" << endl;\n\
    \      cerr << \"case : \" << p.first << \" \" << p.second << endl;\n      cerr\
    \ << \"output : \";\n      for (auto &f : functions) cerr << f(p.first, p.second)\
    \ << \", \";\n      cerr << endl;\n      exit(1);\n    }\n  }\n  cerr << \"verify\
    \ passed.\" << endl;\n}\n}  // namespace fast_gcd_verify\n\nusing namespace Nyaan;\n\
    \nvoid Nyaan::solve() {\n  fast_gcd_verify::unit_test();\n\n  int a, b;\n  cin\
    \ >> a >> b;\n  cout << a + b << endl;\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/aplusb\"\n\n#include \"\
    ../../template/template.hpp\"\n//\n#include \"../../math-fast/gcd.hpp\"\n\nnamespace\
    \ fast_gcd_verify {\n\nusing i64 = long long;\n\ni64 naive_gcd(i64 a, i64 b) {\n\
    \  while (b) swap(a %= b, b);\n  return a;\n}\n\ni64 x_;\nvoid rng_init() { x_\
    \ = 88172645463325252ULL; }\ni64 rng() { return x_ = x_ ^ (x_ << 7), x_ = x_ ^\
    \ (x_ >> 9); }\n\nvoid unit_test() {\n  using P = pair<i64, i64>;\n  using F =\
    \ i64 (*)(i64, i64);\n\n  vector<P> testcase{P(2, 4),\n                     P(100000,\
    \ 10000),\n                     P(998244353, 1000000007),\n                  \
    \   P(1LL << 40, 1LL << 60),\n                     P((1LL << 61) - 1, 11111111111111111),\n\
    \                     P((1LL << 60) + 1, (1LL << 59) + 1),\n                 \
    \    P(1LL << 62, 1LL << 62),\n                     P(1LL << 62, 1LL << 61),\n\
    \                     P(3LL << 61, 9LL << 60),\n                     P((1uLL <<\
    \ 63) - 1, (1LL << 62)),\n                     P(0, 1),\n                    \
    \ P(1, 0),\n                     P(0, 0),\n                     P(0, -1),\n  \
    \                   P(-1, 0),\n                     P(-1, -1)};\n  for (i64 i\
    \ = 1000; i--;)\n    for (i64 j = 1000; j--;) testcase.emplace_back(i, j);\n \
    \ rng_init();\n  for (i64 n = 10000; n--;) {\n    i64 i = rng(), j = rng();\n\
    \    testcase.emplace_back(i, j);\n  }\n\n  vector<F> functions{std::__gcd<int64_t>,\
    \ naive_gcd, gcd};\n\n  for (auto p : testcase) {\n    unordered_set<i64> s;\n\
    \    for (auto &f : functions) {\n      s.insert(abs(f(p.first, p.second)));\n\
    \    }\n    if (s.size() != 1u) {\n      cerr << \"verify failed.\" << endl;\n\
    \      cerr << \"case : \" << p.first << \" \" << p.second << endl;\n      cerr\
    \ << \"output : \";\n      for (auto &f : functions) cerr << f(p.first, p.second)\
    \ << \", \";\n      cerr << endl;\n      exit(1);\n    }\n  }\n  cerr << \"verify\
    \ passed.\" << endl;\n}\n}  // namespace fast_gcd_verify\n\nusing namespace Nyaan;\n\
    \nvoid Nyaan::solve() {\n  fast_gcd_verify::unit_test();\n\n  int a, b;\n  cin\
    \ >> a >> b;\n  cout << a + b << endl;\n}\n"
  dependsOn:
  - template/template.hpp
  - template/util.hpp
  - template/bitop.hpp
  - template/inout.hpp
  - template/debug.hpp
  - template/macro.hpp
  - math-fast/gcd.hpp
  isVerificationFile: true
  path: verify/verify-unit-test/math-fast.test.cpp
  requiredBy: []
  timestamp: '2021-05-15 01:48:03+09:00'
  verificationStatus: TEST_WRONG_ANSWER
  verifiedWith: []
documentation_of: verify/verify-unit-test/math-fast.test.cpp
layout: document
redirect_from:
- /verify/verify/verify-unit-test/math-fast.test.cpp
- /verify/verify/verify-unit-test/math-fast.test.cpp.html
title: verify/verify-unit-test/math-fast.test.cpp
---