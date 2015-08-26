### Install Linter for Sublime

1. gem install scss_lint
2. npm install -g coffee-script
3. Sublime package install SublimeLinter
4. install SublimeLinter-coffee
5. install Sublime​Linter-contrib-scss-lint

### 初始化和設定 coffeeLint

1. 執行 'coffeelint --makeconfig > coffeelint.json'
2. 複製 Default.coffeelint.json 內容覆蓋 platform 下的 coffeelint.json

### 初始化和設定 scss-lint

1. Default.scss-lint.yml 複製到 platform
2. Default.scss-lint.yml 更名成 .scss-lint.yml
3. 執行 'scss-lint ~/workspace/pmd_platform/assets/linker/styles/**/*.scss --config .scss-lint.yml'

### 重啟 Sublime

多了黃色、紅色小點，即表示安裝完成

### SublimeLinter 設定

#### 路徑

```
Perferenaces > Package Setting > SublimeLinter > Setting User
```

然後再 save 。會自然產生對應的設定。

建議設定：

```
"gutter_theme": "Packages/SublimeLinter/gutter-themes/Blueberry/cross/Blueberry - cross.gutter-theme"
"mark_style": "fill"
"no_column_highlights_line": true
```