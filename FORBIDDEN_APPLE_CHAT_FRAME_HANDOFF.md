# Forbidden Apple Tavern 聊天框续接文档

更新时间：2026-05-15

## 当前规则

- 不打开真实 SillyTavern，用户正在使用酒馆。
- 不访问或刷新真实酒馆端口。
- 不修改用户已有酒馆主题文件。
- 后续如果导入，也要新建主题或单独 CSS，不覆盖原主题。
- 只用当前工作区的虚拟网页预览。

当前虚拟预览地址：

```text
http://127.0.0.1:8765/forbidden-apple-chat-frame-stretchable-web.html
```

对应文件：

```text
C:\Users\凡人歌\Documents\Codex\2026-05-11\sillytavern-forbidden-apple-tavern-landing-page\forbidden-apple-chat-frame-stretchable-web.html
```

## 用户想要的方向

- 现在做的是聊天框，不是头像框，不是网页 landing page。
- `char` 和 `user` 要不一样。
- `char` 用绿色 / 奶油纸 / 复古手账感。
- `user` 用红色 / 粉红纸 / 红丝带感。
- 顶部和底部可以复杂，苹果、蕾丝、藤线、蜡封、丝带都可以放在固定区域。
- 中间必须干净，可纵向拉伸，不能有苹果、叶子、蜡封、锁扣、明显装饰或会被拉坏的边缘。
- 整体要像贴纸聊天框，但消息很长时不能变形。

## 已经试过但不适合的方案

### 1. 整张 PNG 直接拉伸

失败原因：

- 苹果、蜡封、锁扣、叶子会被横向或纵向拉坏。
- 短消息勉强，长消息很怪。

### 2. `border-image` 九宫格

失败原因：

- 复杂贴纸边框不适合普通九宫格。
- 装饰会挤压正文，红色 user 框尤其明显。

### 3. 从旧完整聊天框硬切 top / middle / bottom

失败原因：

- 中段带进了锁扣、叶子、阴影、小红籽等杂物。
- 去掉中段图片后，CSS 色块像一张矩形纸贴上去。
- 上下装饰和中段纸面接不上。

### 4. 六宫格 contact sheet 裁切

当前文件夹：

```text
C:\Users\凡人歌\Documents\Codex\2026-05-11\sillytavern-forbidden-apple-tavern-landing-page\chat-frame-assets\generated-three-slice-v2
```

文件：

```text
forbidden-apple-char-top.png
forbidden-apple-char-middle.png
forbidden-apple-char-bottom.png
forbidden-apple-user-top.png
forbidden-apple-user-middle.png
forbidden-apple-user-bottom.png
```

当前问题：

- top / middle / bottom 不是同一套精确切片，所以接缝仍明显。
- 左右边线有错位。
- user 短消息更容易看出三段分离。
- char 长消息时顶部和中段连接仍不自然。

结论：方向是对的，但资产必须重新做成真正的三段式专用切片，而不是 contact sheet 裁切。

## 下一步正确方案

重新生成两套三段式聊天框资产，共 6 张透明 PNG：

```text
char-top.png
char-middle.png
char-bottom.png
user-top.png
user-middle.png
user-bottom.png
```

建议尺寸：

```text
1200 x 280 top
1200 x 420 middle
1200 x 280 bottom
```

关键要求：

- 每张单独生成，不要再生成 contact sheet。
- 同一套的三张必须同宽。
- 左右边线必须在相同 x 坐标。
- top 的下边缘必须是干净可连接的水平纸面。
- middle 只能是干净纸面、左右细边线、轻微纹理。
- bottom 的上边缘必须是干净可连接的水平纸面。
- 装饰只放在 top / bottom，不放在 middle。
- 不要文字，不要头像，不要 UI 截图。

推荐 HTML 结构：

```html
<div class="fa-chat-frame char">
  <div class="fa-frame-top"></div>
  <div class="fa-frame-middle">
    <div class="fa-frame-content">消息内容</div>
  </div>
  <div class="fa-frame-bottom"></div>
</div>
```

推荐 CSS 思路：

```css
.fa-chat-frame {
  display: grid;
  grid-template-rows: var(--top-h) minmax(var(--mid-min), auto) var(--bottom-h);
}

.fa-frame-top {
  background: var(--top-img) center top / 100% auto no-repeat;
}

.fa-frame-middle {
  background: var(--mid-img) center / 100% 100% no-repeat;
}

.fa-frame-bottom {
  background: var(--bottom-img) center bottom / 100% auto no-repeat;
}
```

## 生成提示词要点

每次只生成一张透明 PNG，并明确它是三段式聊天框中的某一段：

```text
Generate exactly one transparent PNG asset, not a contact sheet.
This is one slice of a 3-part stretchable chat message frame.
All slices in the set must share the same width, same left/right border positions, and same paper color.
The bottom edge of the top slice and the top edge of the middle slice must align seamlessly.
The middle slice must be plain clean paper only, vertically stretchable, with no decorations.
No text, no character avatar, no UI screenshot.
```

## Catbox 记录

旧完整聊天框已经上传，但不适合作为最终拉伸聊天框：

```text
char 旧整图：https://files.catbox.moe/7gi8jf.png
user 旧整图：https://files.catbox.moe/e6idxz.png
参考拼图：https://files.catbox.moe/li2caz.png
```

新的六张三段式资产还没有上传，等资产确认可用后再上传。

## 当前优先级

1. 先重做真正可拼接的六张三段式聊天框 PNG。
2. 更新虚拟网页预览。
3. 用截图验证短消息、普通消息、超长消息。
4. 用户确认后再上传 Catbox。
5. 最后再考虑新建 SillyTavern 主题，不改原主题。

## 2026-05-16 续做记录

已生成新的三段式素材草案，来源是新图像生成 contact sheet：

```text
C:\Users\凡人歌\.codex\generated_images\019e1585-4592-7d81-ab62-e4cf3da29fc0\ig_0f8f19ecb6996dde016a0743c44440819a8f0586c20f877bcb.png
```

当前推荐版本是 v5：

```text
C:\Users\凡人歌\Documents\Codex\2026-05-11\sillytavern-forbidden-apple-tavern-landing-page\chat-frame-assets\generated-three-slice-v5
```

v5 文件：

```text
forbidden-apple-char-top.png
forbidden-apple-char-middle.png
forbidden-apple-char-bottom.png
forbidden-apple-user-top.png
forbidden-apple-user-middle.png
forbidden-apple-user-bottom.png
```

当前虚拟网页已经切到 v5。

v3 问题：top 固定段太高，正文被压得太低。  
v6 问题：裁掉接缝线后露出了中段色块，像矩形纸块，不如 v5 自然。  
v5 当前状态：上中下已经能接成整体，接缝有细线但比色块更自然；char 长消息可纵向拉伸，user 也有独立红色版本。

当前截图：

```text
C:\Users\凡人歌\Documents\Codex\2026-05-11\sillytavern-forbidden-apple-tavern-landing-page\screenshots\forbidden-apple-chat-frame-v5-shorter-top.png
```

后续建议：让用户先看 v5。如果认可，再上传 v5 六张 PNG 到 Catbox；如果还嫌接缝明显，需要重新生成更严格的独立 6 张资产，而不是继续硬裁。
