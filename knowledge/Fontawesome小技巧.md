## Fontawesome 小技巧

`<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">`

引入fontawesome以後，你可以把<i>標籤用在各個地方！

### 基本 Icons

```
  <i class="fa fa-camera-retro"></i> fa-camera-retro
```

### 較大的 Icon

這裏提供以下五種 size 供大家選擇，當然也可以用 CSS 自訂

`fa-lg`, `fa-2x`, `fa-3x`, `fa-4x`, `fa-5x`

```
  <i class="fa fa-camera-retro fa-lg"></i> fa-lg
  <i class="fa fa-camera-retro fa-2x"></i> fa-2x
  <i class="fa fa-camera-retro fa-3x"></i> fa-3x
  <i class="fa fa-camera-retro fa-4x"></i> fa-4x
  <i class="fa fa-camera-retro fa-5x"></i> fa-5x
```

### 固定寬度的 Icons

使用 `fa-fw` 的方法來固定圖標的寬度，才不會讓每個圖標的寬度不一

```
  <div class="list-group">
    <a class="list-group-item" href="#"><i class="fa fa-home fa-fw"></i>&nbsp; Home</a>
    <a class="list-group-item" href="#"><i class="fa fa-book fa-fw"></i>&nbsp; Library</a>
    <a class="list-group-item" href="#"><i class="fa fa-pencil fa-fw"></i>&nbsp; Applications</a>
    <a class="list-group-item" href="#"><i class="fa fa-cog fa-fw"></i>&nbsp; Settings</a>
  </div>
```

### 列表 Icons

使用 `fa-ul` 跟 `fa-li` 取代原本 ul, li 的黑色小原點

```
  <ul class="fa-ul">
    <li><i class="fa-li fa fa-check-square"></i>List icons</li>
    <li><i class="fa-li fa fa-check-square"></i>can be used</li>
    <li><i class="fa-li fa fa-spinner fa-spin"></i>as bullets</li>
    <li><i class="fa-li fa fa-square"></i>in lists</li>
  </ul>
```

### 有邊框的 Icons

使用 `fa-border` 的方法在 Icons 外加上邊框

```
  <i class="fa fa-quote-left fa-3x fa-border"></i>
```

### 轉動的 Icons

>  IE9(含)以下的 GG

主要分兩種轉動的方式 `fa-spin`, `fa-pulse`

目前比較適合轉動的 Icons 有 `fa-spinner`, `fa-circle-o-notch`, `fa-refresh`, `fa-cog` 的這四種

```
<!-- # fa-spin -->
  <i class="fa fa-spinner fa-spin"></i>
  <i class="fa fa-circle-o-notch fa-spin"></i>
  <i class="fa fa-refresh fa-spin"></i>
  <i class="fa fa-cog fa-spin"></i>
<!-- # fa-pulse -->
  <i class="fa fa-spinner fa-pulse"></i>
  <i class="fa fa-circle-o-notch fa-pulse"></i>
  <i class="fa fa-refresh fa-pulse"></i>
  <i class="fa fa-cog fa-pulse"></i>
```

### 旋轉與翻轉的 Icon (靜態)

旋轉: `fa-rotate-90`, `fa-rotate-180`, `fa-rotate-270`

翻轉: `a-flip-horizontal`, `icon-flip-vertical`

```
  <i class="fa fa-shield"></i> normal<br>
  <i class="fa fa-shield fa-rotate-90"></i> fa-rotate-90<br>
  <i class="fa fa-shield fa-rotate-180"></i> fa-rotate-180<br>
  <i class="fa fa-shield fa-rotate-270"></i> fa-rotate-270<br>
  <i class="fa fa-shield fa-flip-horizontal"></i> fa-flip-horizontal<br>
  <i class="fa fa-shield fa-flip-vertical"></i> icon-flip-vertical
```

### 疊加的 Icon

外層使用 `fa-stack`

`fa-stack-1x` 代表孩子， `fa-stack-2x` 代表父親

可能 icon 同時會有兩個都是黑色或白色的，因此也可以用 `fa-inverse` 將顏色反轉過來

```
  <span class="fa-stack fa-lg">
    <i class="fa fa-square-o fa-stack-2x"></i>
    <i class="fa fa-twitter fa-stack-1x"></i>
  </span>
  fa-twitter on fa-square-o<br>
  <span class="fa-stack fa-lg">
    <i class="fa fa-circle fa-stack-2x"></i>
    <i class="fa fa-flag fa-stack-1x fa-inverse"></i>
  </span>
  fa-flag on fa-circle<br>
  <span class="fa-stack fa-lg">
    <i class="fa fa-square fa-stack-2x"></i>
    <i class="fa fa-terminal fa-stack-1x fa-inverse"></i>
  </span>
  fa-terminal on fa-square<br>
  <span class="fa-stack fa-lg">
    <i class="fa fa-camera fa-stack-1x"></i>
    <i class="fa fa-ban fa-stack-2x text-danger"></i>
  </span>
  fa-ban on fa-camera
```

### 總結

整理出來的這些東西，是告訴大家有工具就儘量用吧！也方便統一樣式 :)
