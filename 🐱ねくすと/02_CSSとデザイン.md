# Next.js 入門 02 - CSSとデザイン 🎨

## 1. Tailwind CSS とは？
Next.jsの標準的なスタイリング方法（インストール時に選択）。
CSSファイルを書くのではなく、**HTML（TSX）のクラス名に直接デザインを指定する**ユーティリティファーストなフレームワーク。

* **メリット**:
    * CSSファイルを行き来しなくていい（開発が速い）。
    * クラス名を考える悩みから解放される。
    * ファイルサイズが小さくなる。

## 2. よく使うクラスの例

| クラス名 | 意味 | 通常のCSS |
| :--- | :--- | :--- |
| `flex` | フレックスボックス化 | `display: flex;` |
| `flex-col` | 縦並びにする | `flex-direction: column;` |
| `items-center` | 中央揃え (左右) | `align-items: center;` |
| `justify-center` | 中央揃え (上下) | `justify-content: center;` |
| `bg-blue-500` | 背景色 (青の濃さ500) | `background-color: #3b82f6;` |
| `text-white` | 文字色 (白) | `color: white;` |
| `p-4` | 内側の余白 (パディング) | `padding: 1rem;` |
| `m-4` | 外側の余白 (マージン) | `margin: 1rem;` |
| `rounded-lg` | 角丸 (大) | `border-radius: 0.5rem;` |
| `hover:bg-blue-700` | **マウスを乗せた時**の色 | `:hover { ... }` |

## 3. デザインの適用例
`className` 属性の中にスペース区切りで記述する。

```tsx
<div className="bg-white p-6 rounded-lg shadow-md">
  <h1 className="text-2xl font-bold text-gray-800">タイトル</h1>
  <button className="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">
    ボタン
  </button>
</div>
