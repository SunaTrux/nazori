# nazori
指でなぞって何もしないをするアプリ

画面をなぞると光の軌跡が描けるリラックスアプリです。

- アプリ:https://sunatrux.github.io/nazori/
- 更新履歴:[CHANGELOG.md](CHANGELOG.md)

## 更新のしかた

1. `index.html` の `APP_VERSION` と `APP_RELEASE_DATE` を上げる
2. `RELEASE_NOTES` に、その版のお知らせを1行以上追加する
3. `CHANGELOG.md` に同じ版を追加する

`sw.js` は変更しなくて大丈夫です。

## 注意:セキュリティ設定のハッシュ

`index.html` の先頭にある Content Security Policy は、ページ内の `<script>` の中身から計算した sha256 の値だけを実行できるようにしています。`<script>` の中を書き換えたら、必ず値を計算し直してください。合わないと、アプリがまったく動かなくなります。

```sh
python3 - <<'PY'
import re, hashlib, base64
p = 'index.html'
s = open(p, encoding='utf-8').read()
js = re.search(r'<script>(.*?)</script>', s, re.S).group(1)
h = base64.b64encode(hashlib.sha256(js.encode('utf-8')).digest()).decode()
open(p, 'w', encoding='utf-8').write(re.sub(r"script-src 'sha256-[^']*'", "script-src 'sha256-" + h + "'", s))
print('sha256-' + h)
PY
```

