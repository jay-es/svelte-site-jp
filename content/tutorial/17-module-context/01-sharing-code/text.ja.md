---
title: Sharing code
---

これまで見てきたすべての例では、`<script>` ブロックには各コンポーネントのインスタンスが初期化されたときに実行されるコードが含まれています。大部分のコンポーネントでは、これだけで十分です。

ごく稀に、個々のコンポーネントのインスタンスの外でコードを実行する必要があることがあります。例えば、5つのオーディオプレーヤーを同時に再生することができますが、1つを再生すると他のすべてのオーディオプレーヤーが停止した方がより良いでしょう。

これを実現するには、`<script context="module">` ブロックを宣言します。ここに含まれるコードは、コンポーネントがインスタンス化されたときではなく、モジュールが最初に評価されたときに一度だけ実行されます。

これを `AudioPlayer.svelte` の先頭に配置してください。

```html
<script context="module">
	let current;
</script>
```

これで状態を管理することなく、コンポーネント同士がお互いに「話す」ことが可能になりました。

```js
function stopOthers() {
	if (current && current !== audio) current.pause();
	current = audio;
}
```