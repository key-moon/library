---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: lct/lazy-reversible-bbst-base.hpp
    title: "\u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\u53EF\u80FD\u5E73\u8861\u4E8C\u5206\
      \u6728(\u57FA\u5E95\u30AF\u30E9\u30B9)"
  - icon: ':heavy_check_mark:'
    path: lct/link-cut-base.hpp
    title: Link/Cut Tree(base)
  - icon: ':heavy_check_mark:'
    path: lct/splay-base.hpp
    title: Splay Tree(base)
  - icon: ':heavy_check_mark:'
    path: lct/splay-lazy-reversible.hpp
    title: "\u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\u53EF\u80FDSplay Tree"
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: verify/verify-yosupo-ds/yosupo-range-add-range-sum-linkcuttree.test.cpp
    title: verify/verify-yosupo-ds/yosupo-range-add-range-sum-linkcuttree.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "\u9045\u5EF6\u4F1D\u642CLink/Cut Tree"
    links: []
  bundledCode: "#line 2 \"lct/link-cut-tree-lazy.hpp\"\n\n#line 2 \"lct/splay-lazy-reversible.hpp\"\
    \n\n#line 2 \"lct/lazy-reversible-bbst-base.hpp\"\n\ntemplate <typename Tree,\
    \ typename Node, typename T, typename E, T (*f)(T, T),\n          T (*g)(T, E),\
    \ E (*h)(E, E), T (*ts)(T)>\nstruct LazyReversibleBBST : Tree {\n  using Tree::merge;\n\
    \  using Tree::split;\n  using typename Tree::Ptr;\n\n  LazyReversibleBBST() =\
    \ default;\n\n  void toggle(Ptr t) {\n    swap(t->l, t->r);\n    t->sum = ts(t->sum);\n\
    \    t->rev ^= true;\n  }\n\n  T fold(Ptr &t, int a, int b) {\n    auto x = split(t,\
    \ a);\n    auto y = split(x.second, b - a);\n    auto ret = sum(y.first);\n  \
    \  t = merge(x.first, merge(y.first, y.second));\n    return ret;\n  }\n\n  void\
    \ reverse(Ptr &t, int a, int b) {\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    toggle(y.first);\n    t = merge(x.first, merge(y.first, y.second));\n\
    \  }\n\n  void apply(Ptr &t, int a, int b, const E &e) {\n    auto x = split(t,\
    \ a);\n    auto y = split(x.second, b - a);\n    propagate(y.first, e);\n    t\
    \ = merge(x.first, merge(y.first, y.second));\n  }\n\n protected:\n  inline T\
    \ sum(const Ptr t) { return t ? t->sum : T(); }\n\n  Ptr update(Ptr t) override\
    \ {\n    if (!t) return t;\n    t->cnt = 1;\n    t->sum = t->key;\n    if (t->l)\
    \ t->cnt += t->l->cnt, t->sum = f(t->l->sum, t->sum);\n    if (t->r) t->cnt +=\
    \ t->r->cnt, t->sum = f(t->sum, t->r->sum);\n    return t;\n  }\n\n  void push(Ptr\
    \ t) override {\n    if (!t) return;\n    if (t->rev) {\n      if (t->l) toggle(t->l);\n\
    \      if (t->r) toggle(t->r);\n      t->rev = false;\n    }\n    if (t->lazy\
    \ != E()) {\n      if (t->l) propagate(t->l, t->lazy);\n      if (t->r) propagate(t->r,\
    \ t->lazy);\n      t->lazy = E();\n    }\n  }\n\n  void propagate(Ptr t, const\
    \ E &x) {\n    t->lazy = h(t->lazy, x);\n    t->key = g(t->key, x);\n    t->sum\
    \ = g(t->sum, x);\n  }\n};\n\n/**\n * @brief \u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\
    \u53EF\u80FD\u5E73\u8861\u4E8C\u5206\u6728(\u57FA\u5E95\u30AF\u30E9\u30B9)\n */\n\
    #line 2 \"lct/splay-base.hpp\"\n\ntemplate <typename Node>\nstruct SplayTreeBase\
    \ {\n  using Ptr = Node *;\n  template <typename... Args>\n  Ptr my_new(const\
    \ Args &... args) {\n    return new Node(args...);\n  }\n  void my_del(Ptr p)\
    \ { delete p; }\n\n  bool is_root(Ptr t) { return !(t->p) || (t->p->l != t &&\
    \ t->p->r != t); }\n\n  int size(Ptr t) const { return count(t); }\n\n  virtual\
    \ void splay(Ptr t) {\n    push(t);\n    while (!is_root(t)) {\n      Ptr q =\
    \ t->p;\n      if (is_root(q)) {\n        push(q), push(t);\n        rot(t);\n\
    \      } else {\n        Ptr r = q->p;\n        push(r), push(q), push(t);\n \
    \       if (pos(q) == pos(t))\n          rot(q), rot(t);\n        else\n     \
    \     rot(t), rot(t);\n      }\n    }\n  }\n\n  Ptr get_left(Ptr t) {\n    while\
    \ (t->l) push(t), t = t->l;\n    return t;\n  }\n\n  Ptr get_right(Ptr t) {\n\
    \    while (t->r) push(t), t = t->r;\n    return t;\n  }\n\n  pair<Ptr, Ptr> split(Ptr\
    \ t, int k) {\n    if (!t) return {nullptr, nullptr};\n    if (k == 0) return\
    \ {nullptr, t};\n    if (k == count(t)) return {t, nullptr};\n    push(t);\n \
    \   if (k <= count(t->l)) {\n      auto x = split(t->l, k);\n      t->l = x.second;\n\
    \      t->p = nullptr;\n      if (x.second) x.second->p = t;\n      return {x.first,\
    \ update(t)};\n    } else {\n      auto x = split(t->r, k - count(t->l) - 1);\n\
    \      t->r = x.first;\n      t->p = nullptr;\n      if (x.first) x.first->p =\
    \ t;\n      return {update(t), x.second};\n    }\n  }\n\n  Ptr merge(Ptr l, Ptr\
    \ r) {\n    if (!l && !r) return nullptr;\n    if (!l) return splay(r), r;\n \
    \   if (!r) return splay(l), l;\n    splay(l), splay(r);\n    l = get_right(l);\n\
    \    splay(l);\n    l->r = r;\n    r->p = l;\n    update(l);\n    return l;\n\
    \  }\n\n  using Key = decltype(Node::key);\n  Ptr build(const vector<Key> &v)\
    \ { return build(0, v.size(), v); }\n  Ptr build(int l, int r, const vector<Key>\
    \ &v) {\n    if (l + 1 >= r) return my_new(v[l]);\n    return merge(build(l, (l\
    \ + r) >> 1, v), build((l + r) >> 1, r, v));\n  }\n\n  template <typename... Args>\n\
    \  void insert(Ptr &t, int k, const Args &... args) {\n    splay(t);\n    auto\
    \ x = split(t, k);\n    t = merge(merge(x.first, my_new(args...)), x.second);\n\
    \  }\n\n  void erase(Ptr &t, int k) {\n    splay(t);\n    auto x = split(t, k);\n\
    \    auto y = split(x.second, 1);\n    my_del(y.first);\n    t = merge(x.first,\
    \ y.second);\n  }\n\n  virtual Ptr update(Ptr t) = 0;\n\n protected:\n  inline\
    \ int count(Ptr t) const { return t ? t->cnt : 0; }\n\n  virtual void push(Ptr\
    \ t) = 0;\n\n  Ptr build(const vector<Ptr> &v) { return build(0, v.size(), v);\
    \ }\n\n  Ptr build(int l, int r, const vector<Ptr> &v) {\n    if (l + 1 >= r)\
    \ return v[l];\n    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1,\
    \ r, v));\n  }\n\n  inline int pos(Ptr t) {\n    if (t->p) {\n      if (t->p->l\
    \ == t) return -1;\n      if (t->p->r == t) return 1;\n    }\n    return 0;\n\
    \  }\n\n  virtual void rot(Ptr t) {\n    Ptr x = t->p, y = x->p;\n    if (pos(t)\
    \ == -1) {\n      if ((x->l = t->r)) t->r->p = x;\n      t->r = x, x->p = t;\n\
    \    } else {\n      if ((x->r = t->l)) t->l->p = x;\n      t->l = x, x->p = t;\n\
    \    }\n    update(x), update(t);\n    if ((t->p = y)) {\n      if (y->l == x)\
    \ y->l = t;\n      if (y->r == x) y->r = t;\n    }\n  }\n};\n\n/**\n * @brief\
    \ Splay Tree(base)\n */\n#line 5 \"lct/splay-lazy-reversible.hpp\"\n\ntemplate\
    \ <typename T, typename E>\nstruct LazyReversibleSplayTreeNode {\n  using Ptr\
    \ = LazyReversibleSplayTreeNode *;\n  Ptr l, r, p;\n  T key, sum;\n  E lazy;\n\
    \  int cnt;\n  bool rev;\n\n  LazyReversibleSplayTreeNode(const T &t = T(), const\
    \ E &e = E())\n      : l(), r(), p(), key(t), sum(t), lazy(e), cnt(1), rev(false)\
    \ {}\n};\n\ntemplate <typename T, typename E, T (*f)(T, T), T (*g)(T, E), E (*h)(E,\
    \ E),\n          T (*ts)(T)>\nstruct LazyReversibleSplayTree\n    : LazyReversibleBBST<SplayTreeBase<LazyReversibleSplayTreeNode<T,\
    \ E>>,\n                         LazyReversibleSplayTreeNode<T, E>, T, E, f, g,\
    \ h, ts> {\n  using Node = LazyReversibleSplayTreeNode<T, E>;\n};\n\n/**\n * @brief\
    \ \u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\u53EF\u80FDSplay Tree\n */\n#line 4 \"\
    lct/link-cut-tree-lazy.hpp\"\n\n//\n#line 2 \"lct/link-cut-base.hpp\"\n\ntemplate\
    \ <typename Splay>\nstruct LinkCutBase : Splay {\n  using Node = typename Splay::Node;\n\
    \  using Ptr = Node*;\n\n  virtual Ptr expose(Ptr t) {\n    Ptr rp = nullptr;\n\
    \    for (Ptr cur = t; cur; cur = cur->p) {\n      this->splay(cur);\n      cur->r\
    \ = rp;\n      this->update(cur);\n      rp = cur;\n    }\n    this->splay(t);\n\
    \    return rp;\n  }\n\n  virtual void link(Ptr u, Ptr v) {\n    evert(u);\n \
    \   expose(v);\n    u->p = v;\n  }\n\n  void cut(Ptr u, Ptr v) {\n    evert(u);\n\
    \    expose(v);\n    v->l = u->p = nullptr;\n    this->update(v);\n  }\n\n  void\
    \ evert(Ptr t) {\n    expose(t);\n    this->toggle(t);\n    this->push(t);\n \
    \ }\n\n  Ptr lca(Ptr u, Ptr v) {\n    if (get_root(u) != get_root(v)) return nullptr;\n\
    \    expose(u);\n    return expose(v);\n  }\n\n  Ptr get_kth(Ptr x, int k) {\n\
    \    expose(x);\n    while (x) {\n      this->push(x);\n      if (x->r && x->r->sz\
    \ > k) {\n        x = x->r;\n      } else {\n        if (x->r) k -= x->r->sz;\n\
    \        if (k == 0) return x;\n        k -= 1;\n        x = x->l;\n      }\n\
    \    }\n    return nullptr;\n  }\n\n  Ptr get_root(Ptr x) {\n    expose(x);\n\
    \    while (x->l) this->push(x), x = x->l;\n    return x;\n  }\n\n  virtual void\
    \ set_key(Ptr t, const decltype(Node::key)& key) {\n    this->splay(t);\n    t->key\
    \ = key;\n    this->update(t);\n  }\n\n  virtual decltype(Node::key) get_key(Ptr\
    \ t) { return t->key; }\n\n  decltype(Node::key) fold(Ptr u, Ptr v) {\n    evert(u);\n\
    \    expose(v);\n    return v->sum;\n  }\n};\n\n/**\n * @brief Link/Cut Tree(base)\n\
    \ * @docs docs/lct/link-cut-tree.md\n */\n#line 7 \"lct/link-cut-tree-lazy.hpp\"\
    \n\ntemplate <typename T, typename E, T (*f)(T, T), T (*g)(T, E), E (*h)(E, E),\n\
    \          T (*ts)(T)>\nstruct LazyLinkCutTree\n    : LinkCutBase<LazyReversibleSplayTree<T,\
    \ E, f, g, h, ts>> {\n  using base = LinkCutBase<LazyReversibleSplayTree<T, E,\
    \ f, g, h, ts>>;\n  using Ptr = typename base::Ptr;\n\n  void set_key(Ptr t, const\
    \ T& key) override {\n    this->evert(t);\n    t->key = key;\n    this->update(t);\n\
    \  }\n\n  T get_key(Ptr t) override {\n    this->evert(t);\n    return t->key;\n\
    \  }\n\n  void apply(Ptr u, Ptr v, const E& e) {\n    this->evert(u);\n    this->expose(v);\n\
    \    this->propagate(v, e);\n  }\n};\n\n/**\n * @brief \u9045\u5EF6\u4F1D\u642C\
    Link/Cut Tree\n */\n"
  code: "#pragma once\n\n#include \"splay-lazy-reversible.hpp\"\n\n//\n#include \"\
    link-cut-base.hpp\"\n\ntemplate <typename T, typename E, T (*f)(T, T), T (*g)(T,\
    \ E), E (*h)(E, E),\n          T (*ts)(T)>\nstruct LazyLinkCutTree\n    : LinkCutBase<LazyReversibleSplayTree<T,\
    \ E, f, g, h, ts>> {\n  using base = LinkCutBase<LazyReversibleSplayTree<T, E,\
    \ f, g, h, ts>>;\n  using Ptr = typename base::Ptr;\n\n  void set_key(Ptr t, const\
    \ T& key) override {\n    this->evert(t);\n    t->key = key;\n    this->update(t);\n\
    \  }\n\n  T get_key(Ptr t) override {\n    this->evert(t);\n    return t->key;\n\
    \  }\n\n  void apply(Ptr u, Ptr v, const E& e) {\n    this->evert(u);\n    this->expose(v);\n\
    \    this->propagate(v, e);\n  }\n};\n\n/**\n * @brief \u9045\u5EF6\u4F1D\u642C\
    Link/Cut Tree\n */\n"
  dependsOn:
  - lct/splay-lazy-reversible.hpp
  - lct/lazy-reversible-bbst-base.hpp
  - lct/splay-base.hpp
  - lct/link-cut-base.hpp
  isVerificationFile: false
  path: lct/link-cut-tree-lazy.hpp
  requiredBy: []
  timestamp: '2020-12-20 20:23:11+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - verify/verify-yosupo-ds/yosupo-range-add-range-sum-linkcuttree.test.cpp
documentation_of: lct/link-cut-tree-lazy.hpp
layout: document
redirect_from:
- /library/lct/link-cut-tree-lazy.hpp
- /library/lct/link-cut-tree-lazy.hpp.html
title: "\u9045\u5EF6\u4F1D\u642CLink/Cut Tree"
---