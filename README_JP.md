# REINFORCEjs

**REINFORCEjs** はいくつかの共通 RL アルゴリズムを実装し、Web でも を含む教科学習ライブラリです。特に現在以下の機能を持っています。

- **ダイナミックプログラミング** 手法
- ** TD 学習**(SARSA/Q-Learning)
- ニューラルネットワークを用いた関数近似による Q学習である **Deep Q-Learning**
- 連続的な行動空間を扱うための**確率/決定方策勾配法** とActor-Critics アーキテクチャ。(*α機能で、バグが多くまた扱いにくく矛盾をはらんでいます*)

さらなる詳細、ドキュメント、デモについては、[main webpage](http://cs.stanford.edu/people/karpathy/reinforcejs)を参照してください。

# Code Sketch

ライブラリーは２つのグローバル変数('R' と 'RL')をエクスポートしています。前者('R')はグラフ表現を構築し、自動バックプロパゲーションをするためのユーティリティで、[recurrentjs](https://github.com/karpathy/recurrentjs)プロジェクトのフォークです。'RL'オブジェクトには現在以下の実装があります。

- `RL.DPAgent`:動的環境での有限状態/行動空間を扱う。
- `RL.TDAgent`:有限状態/行動空間を扱う
- `RL.DQNAgent`:連続状態機能で離散行動を扱う

基本的な使い方は以下の通りになる:

```javascript
// 環境オブジェクトを構築
var env = {};
env.getNumStates = function() { return 8; }
env.getMaxNumActions = function() { return 4; }

// DQN エージェントを作成
var spec = { alpha: 0.01 } // DQN ページの完全なオプションを参考
agent = new RL.DQNAgent(env, spec); 

setInterval(function(){ // start the learning loop
  var action = agent.act(s); // s は長さ8(状態)の配列
  //... 環境における行動を実行し、報酬を得る
  agent.learn(reward); // エージェントは自身のQ,方策,モデル等の更新をする。報酬は浮動小数
}, 0);
```

完全なドキュメントとデモは[main webpage](http://cs.stanford.edu/people/karpathy/reinforcejs)にあります。

# License

MIT.
