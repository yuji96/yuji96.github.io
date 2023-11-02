---
categories:
  - memo
date: 0000-00-00 00:00:00 +0900
math: true
tags:
  - WIP
title: title
parse_block_html: true
published: false
---

## colorbar が押しつぶして plotarea のサイズが合わない

両方で colorbar を作って片方消す。

```python
plot
fig.colorbar(im, aspect=10, pad=0.05)
fig.delaxes(fig.axes[1])

plot
fig.colorbar(im, aspect=10, pad=0.05)
```

でもコレすると minipage の width が一致しないのでどうしたろうかしゃん。
subplot？あれは subcaption 使えないからダメ。

## 保存時に文字がはみ出す

```python
plt.savefig(f"figure.pdf", bbox_inches='tight', pad_inches=0.0)
```

## latex のならべかた

改行を消すと横につながる。まじかよ。