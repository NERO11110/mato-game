# 🎯 的あてゲーム (Target Shot Game)

Python の物理演算（斜方投射・反発バウンド）と `matplotlib.animation` を組み合わせた 2D シューティングゲームです。

## 📖 概要
初速度と打ち出し角度を直感的に入力し、ランダムに配置されるターゲットを狙う放物線シミュレーションゲームです。
重力加速度（$g = 9.8 \text{ m/s}^2$）や反発係数（$e = 0.6$）を考慮した物理計算を行っており、ユーザーが入力した値に応じて球の軌道がリアルタイムに計算・描画されます。

---

## 📸 画面・機能一覧 (Screenshots)

### 1. 難易度選択画面
<img width="279" height="111" alt="hard" src="https://github.com/user-attachments/assets/0d093cc2-ceeb-4cba-bc29-e6a1200448ef" />

- **Easy (🟢) / Normal (🟡) / Hard (🔴)** の 3 段階から難易度を選択できます。
- 難易度に応じてターゲットのサイズが変わり、位置も毎回ランダムに再生成されます。

### 2. 数値入力と鉄壁のエラーガード
<img width="233" height="212" alt="guard" src="https://github.com/user-attachments/assets/a512b406-56c5-4f12-a0a2-ab2e1ef3bf03" />

- 初速度 (m/s) と打ち出し角度 (0°〜90°) を入力します。
- 全角入力、文字列、範囲外の数値が入力されてもプログラムが強制終了せず、正しく再入力を促す多重の例外処理（`try-except`）を搭載しています。

### 3. 放物線アニメーション ＆ HIT 演出
<img width="232" height="171" alt="hit" src="https://github.com/user-attachments/assets/3971098a-e2b7-46eb-ada6-d99d46bd4c87" />

- 計算された座標データをもとに、コマ送りアニメーション（`matplotlib.animation`）で球の軌道をリアルタイム表示します。
- ターゲットの領域内に球が入ると「✨ HIT!! ✨」と大きく表示されます。

### 4. バウンド物理計算 ＆ MISS / リトライ機能
<img width="225" height="161" alt="bound" src="https://github.com/user-attachments/assets/a518fcdf-ec8f-4598-8503-6b1af0460aff" />

<img width="237" height="166" alt="miss" src="https://github.com/user-attachments/assets/5c2d0963-412d-4ec9-95b5-c67904466df3" />

- 地面との接触時に反発係数を計算し、最大 3 回まで跳ね返る物理挙動を再現しています。
- ターゲットを外した場合は「💦 MISS... 💦」と表示され、ゲーム終了後にそのまま再チャレンジ（y/n）を選択可能です。

---

## 🛠️ 技術的な工夫点・こだわり

1. **堅牢なエラーハンドリング（例外処理）**
   - ユーザーの予期せぬ入力（文字入力やマイナス数値など）に対しても、プログラムが破綻せずにゲームを継続できる設計にしました。

2. **Pythonのスコープ制約の回避**
   - アニメーションの更新関数内でフラグ（命中判定）を書き換える際、要素数 1 のリスト構造（`already_hit = [False]`）を用いることで、可変オブジェクトの参照を保持して状態を更新する工夫を自力で実装しました。

3. **描画メモリとパフォーマンスの最適化**
   - 連続実行時にアニメーションが重くならないよう、`IPython.display.clear_output(wait=True)` や `plt.close()` を適切なタイミングで挿入し、描画負荷を最小限に抑えました。

---

## 💻 動作環境・使用ライブラリ
- **Language:** Python
- **Environment:** Google Colab
- **Libraries:** `matplotlib`, `math`, `random`, `IPython`
