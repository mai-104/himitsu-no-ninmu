# 秘密の任務オールクリア（仮）

5秒の指令が次々に届く、スマホ向けミニゲーム集（制作中・まぃの箱にはまだ載せていません）。

遊ぶURL: https://mai-104.github.io/himitsu-no-ninmu/

---

## 見た目・音の差し替えかた

ゲームの中身はすべて `index.html` の1ファイルです。
**ファイルを置いて、`index.html` に「ファイル名を1行書く」だけ**で差し替わります。書いていないものは今のまま。

### 手順

1. 画像（PNG）は `images`、3Dモデル（GLB）は `models`、音（MP3）は `sounds` フォルダに入れる
   - GitHubの「Add file」→「Upload files」で、フォルダ名ごと入れられます
2. `index.html` を鉛筆マークで開いて、下の「書く場所」に1行足す（`null` の所をファイル名に書きかえる）
3. 保存（Commit changes）して、数分後にゲームを開き直す

---

### ① 面に貼る画像 … `const ASSETS = {` の中

| 名前 | 何か |
|---|---|
| `background` | 全体の背景 |
| `titleLogo` | タイトルの文字（画像にすると、文字の代わりに表示） |
| `titleDeco` | タイトル画面で回っている飾り |
| `tapCube` | 叩け！ のブロック |
| `player` / `enemy` / `floor` | よけろ！ の自分・敵の球・床 |
| `timingBar` | ここで押せ！ のバー |
| `puzzle` | はめて！ のピース |
| `ground` | 叩いて！ の地面 |
| `bombBox` / `bombBase` | 切って！ の時限装置・手元の装置 |
| `rouletteWheel` | とめて！ のルーレット盤（色と文字の並び順は `ROULETTE` と同じにする） |
| `lockBody` / `shackle` | あけて！ の南京錠の本体・つる |
| `katanukiPlate` | かたぬき！ のお菓子の板 |
| `balloon` / `pump` | いれて！ の風船・空気入れ |
| `jar` | まぜて！ の瓶 |

書きかた：`tapCube: "images/tap_cube.png",`

### ② 3Dの物 … `const MODEL_FILES = {` の中

ボール・モグラ・パフェの器などの「物」を、3Dモデルか画像に置きかえます。
大きさと位置は元の形に自動で合わせます。

```js
const MODEL_FILES = {
  mole: { png: "images/mole.png" },
  ball: { glb: "models/ball.glb" },
  bomb: { png: "images/bomb.png", size: 1.0 },   // size で高さを指定することもできる
};
```

| 名前 | 何か |
|---|---|
| `ball` `kettle` `watermelon` `plant` | 打ち返して！ のボールとダミー |
| `mole` `chick` `bomb` | 叩いて！ のモグラとダミー |
| `parfaitGlass` `puddingPlate` | 完成させて！ の器 |
| `softCream` `strawberry` `wafer` `cherry` `whip` `mikan` | 完成させて！ の盛り付けパーツ |
| `sodaBottle` | 振って！ のペットボトル |
| `suika` `suikaHalf` `blindfoldPerson` | スイカ割り！ のスイカ・割れたスイカ・目隠しの人 |

> 画像の時は、板に貼って正面を向けて置きます。正面から見るゲームがほとんどなので、画像でも自然に見えます。
> 差し替えた物は「全体の形」だけになります（ペットボトルのふたが飛ぶ等の部品の動きは見えなくなります）。

### ③ BGM・効果音 … `const SOUNDS = {` の中

| 名前 | いつ鳴るか |
|---|---|
| `bgm.title` | タイトル画面・ゲームオーバー画面（くり返し） |
| `bgm.play` | プレイ中（くり返し） |
| `se.start` | スタートした時 |
| `se.instruction` | 指令が出た時 |
| `se.tap` | プレイ中に画面をタップした時 |
| `se.clear` / `se.fail` | 1つのゲームをクリア／失敗した時 |
| `se.gameover` | ゲームオーバー |

書きかた：`bgm: { title: "sounds/bgm_title.mp3", play: "sounds/bgm_play.mp3" },`

- 音を1つでも入れると、タイトル画面に「音：ON／OFF」ボタンが出ます
- スマホのきまりで、BGMは画面を最初にタップした時から流れます
- 音量は `volume:` で変えられます（0〜1）
