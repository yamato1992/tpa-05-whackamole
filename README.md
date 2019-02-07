# Whack-a-mole VueJS

今週はモグラ叩きを実装してみます！これからはアプリケーションのレベルが徐々に上がります！毎日コツコツと進めていきましょう。

クライアントは VueJS を使用しているので、課題のキーワードはVueJSが中心となります。

こちらが動くアプリです：http://whackamole.thirdtape.com/

チェックポイントは５つあります。６日あるのでレビューの時間も含めて、毎日１つのチェックポイント進めるのが良いペースとなります。フィーチャーが未完成でも毎日プルリクエストを投稿してメンターと確認しながら進めてください。

## コンテンツ：

* [Git Workflow](#git-workflow)
* Checkpoints
  * [Checkpoint 1 README](#checkpoint-1)
  * [Checkpoint 2 README](#checkpoint-2)
  * [Checkpoint 3 README](#checkpoint-3)
  * [Checkpoint 4 README](#checkpoint-4)
  * [Checkpoint 5 README](#checkpoint-5)
* [Starting the App](#starting-the-app)

***

# Git Workflow

今回のレポジトリはGit ワークフローが少し変わります。詳しくは[こちら(wiki)](https://github.com/bootcamp-tpa/tpa-resources/wiki/%5B%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%95%E3%83%AD%E3%83%BC%5D-2%E3%83%B6%E6%9C%88%E7%9B%AE%E3%81%AEGit-Workflow)をご覧ください。

***

# Checkpoint-1

[_コンポーネント構造の設計ヒント_] こちらをご覧ください：

![コンポーネント構造](https://i.imgur.com/7VyUal6.png)

現在動かないHTML/CSSをコンポーネント化するのが第一のタスクとなります。データproos、またはイベントハンドリングなどはとりあえず置いといて、HTML/CSS だけをコンポーネント化してみましょう。

**タスク：**

* [ ] まずはスタートコードをしっかり読んでおこう。
* [ ] 複数のファイルを追加して、現在のアプリをコンポーネント化してみよう。
  * とりあえず必要なHTML/CSSをコピペする感じでOK
  * データ描画などの機能の実装はまだこれからです！
  * スタートコードとゲームの見た目は変わらないようにコードを移動するように！

**リンク：**

- 各コンポーネント内で、他のコンポーネントを使用したい場合、[components](https://jp.vuejs.org/v2/api/#components)シンタックスが必要となります:

```diff
// App.vue

<template>
  <div>
+   <MyComponent></MyComponent>
  </div>
</template>

<script>
+ import MyComponent from './MyComponent';

export default {
  name: 'App',
+ components: {
+   MyComponent: MyComponent,
+ }
  // ...
}
</script>

// ...
```

# Checkpoint-2

動くWhackamoleの実装するにはまずはデータ型を考えるのが大事です：

![アプリのデータ型](https://i.imgur.com/ZisHh7q.png)

**タスク：**

* [ ] `App` コンポーネントに上記のデータ型をVueJSの`data`プロパティとして定義しよう。（[コンポーネントのデータプロパティは関数でなければいけません](https://jp.vuejs.org/v2/guide/components.html#data-%E3%81%AF%E9%96%A2%E6%95%B0%E3%81%A7%E3%81%AA%E3%81%91%E3%82%8C%E3%81%B0%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%9B%E3%82%93)）
* [ ] 一つのコンポーネントにデータプロップスなどを渡して、データを変えたら違うデータが表示されるように実装しよう。
  * 一番シンプルなのは数字(high score, timer など）を表示するコンポーネントです。
* [ ] 実際データをそのコンポーネントに渡しましょう。これは`App.vue`の`<template>`内で行います。
* [ ] 試しにApp.vueから渡されているデータを変えて違う値が表示されるかを確認してください。

**リンク：**

- [プロップス/props](https://jp.vuejs.org/v2/api/#props)
- [v-bindディレクティブ](https://jp.vuejs.org/v2/api/#v-bind)

# Checkpoint-3

各モグラは`Mole`みたいなコンポーネントを使用していますでしょうか？`Mole`を上下に動かすためには、クラスネームを変えてください。下記の動画でどういうことかがわかります：

[クラスネームを変えるとモグラが出てくる](https://youtu.be/TWd-G0Py-vY)

**タスク:**

* [ ] 残りのコンポーネントをデータプロップスを渡し、値を表示するように実装しよう。
* [ ] App.vue から渡すデータを変えてみて、表示されるかを確認してください。
* [ ] `moleData` を`v-for`文で回して、`<Mole>`を4つ表示しましょう。

**リンク:**

- [クラスとスタイルのバインディング](https://jp.vuejs.org/v2/guide/class-and-style.html)
- [Computed プロップス](https://jp.vuejs.org/v2/api/#computed)
- [v-for](https://jp.vuejs.org/v2/api/#v-for)

# Checkpoint-4

ゲームっぽい動きの仕組みを実装してみましょう！

App コンポーネント内で、ゲームの動きをメソッドを作って定義しときましょう。ここはVueJSコンポーネントの`methods`プロパティに書き込みます。

下記がシンタックスとなります： 
```diff
export default {
  name: 'App',
  // components: ...
  // data: ...

+ methods: {
+   関数１: function() {
+     // ...
+   },
+   関数２: function() {
+     // ...
+   },
+ }
}
```

まずはタイマー機能から実装していきましょう。

**タスク：**

* [ ] App コンポーネントのdata関数に`time`プロパティがあるかを確認してください。なかったら足しときましょう！
* [ ] 必要な関数をメソッドオブジェクトに定義しときましょう。例えば、`startGame`, `endGame`, `startTimer`, `stopTimer` などなど。
* [ ] スタートボタンを押すと`startGame`関数を実行するイベントハンドリングを追加しましょう。
* [ ] スタートボタンを押すとタイマーが1秒ごとに下がっていく機能を実装しよう。
  * 秒数が変わるごとにタイマーコンポーネントの再描画を確認しとこう。
  * 秒数が０になったら止めることを忘れないように。
  * ここは[setInterval](https://developer.mozilla.org/ja/docs/Web/API/Window/setInterval)と[clearInterval](https://developer.mozilla.org/ja/docs/Web/API/WindowTimers/clearInterval)を使用してみよう。

# Checkpoint-5

最終チェックポイントです！

モールが叩かれるとモール配列を更新します。

それには、`Mole`にクリックハンドラーを与えないといけないが、`App`コンポーネントの`<template>`内で`Mole`の`div`にクリックハンドラーを与えられません。ここは`Mole`内で[$emit](https://jp.vuejs.org/v2/api/#vm-emit)関数を利用して親のコンポーネントにカスタムイベントを送ることになります。

**タスク：**

* [ ] `Mole`がクリックされたらカスタムイベントをトリガーしましょう
* [ ] `Moles` のwrapper component を使用している場合、`Moles`からもカスタムイベントをトリガーしましょう
* [ ] `App` でカスタムイベントにハンドラーを紐付けて、`moles`配列を更新しよう。
  * [ ] 叩かれた場合whacks数字も`+1`する
* [ ] 動的にモグラがポンポンと上がってくるメソッドも追加して、ゲームスタートにインターバルで実行されうようにしよう。
  * ポイント： 小さなヘルパー関数(補助関数)を追加しながら実装しよう。`startMoles`, `stopMoles`, `activateRandomMole`, などなど。
* [ ] ゲームが終わったらHigh Scoreも更新しとこう！
* [ ] ボーナスバグ潰し：現在、ゲームスタートを何度も押すと大変なことになってしまうのでは？ちゃんとゲームスタートは遊んでいる間には押せないようにしよう。

お疲れ様です！

***

# Starting the App

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm start
```

Building the app for production:

```bash
# build for production with minification
npm run build
```
