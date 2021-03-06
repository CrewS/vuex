# 中核概念

Vuex Store を作成するために `Vuex.Store` コンストラクタを使用できます。ほとんどの場合、各アプリケーション毎に単独の store だけが必要になります。各 Vuex Store は 3 種類の "構成要素" からなります:

- **ステート**: アプリケーション状態を表すプレーンなオブジェクト

- **ミューテーション**: 状態を変異させる関数。ミューテーションは**同期**必須

- **アクション**: ミューテーションをディスパッチする関数。アクションは非同期操作を含めることができ、複数のミューテーションをディスパッチすることができます

どうして、状態を操作する単純な機能よりもむしろ、*ミューテーション*と*アクション*を区別したいのでしょうか？その理由は、**ミューテーションを分離したいのと非同期**のためです。多くの複雑なアプリケーションは 2 つの組合せから成り立ちます。分離すると、それら両方を調査することが容易になり、そしてそれらのためのテストを書くこともできます。

> Flux について精通している場合、ここでの用語/概念の違いがあることに注意してください。Vuex のアクションは Flux の**アクションクリエータ (action creators)** と同等でありますが、Vuex のミューテーションは Flux の **アクション (actions)** に相当します。

### Vuex Store の作成

> **NOTE:** 残りのドキュメント向けのコード例に対して ES2015 シンタックスを使用します。それについて理解できない場合は、[ここで](https://babeljs.io/docs/learn-es2015/)で学習してください！ドキュメントは既に[大規模アプリケーションの構築](http://vuejs.org/guide/application.html)で説明した概念にに精通している前提としています。

Vuex Store を作成することは非常に簡単です。上記の構成要素を一緒に入れると下記になります:

``` js
import Vuex from 'vuex'

const store = new Vuex.Store({
  state: { ... },
  actions: { ... },
  mutations: { ... }
})
```

一度作成すると、ステートは `store.state` 経由、アクションは `store.actions` 経由でアクセスすることができます。ミューテーション関数は直接アクセスすることはできません。ミューテーション関数は、アクションによるトリガされた時だけ、もしくは `store.dispatch()` を呼び出すときにアクセスできます。次の詳細で各概念について説明します。
