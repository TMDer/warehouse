## 安裝 Sublimelinter (Install Linter for Sublime)

1. 開啟 Sublime Package
2. 搜尋 Sublimelinter 並安裝

## 安裝 CoffeeLinter (Install Coffeescript's linter)

1. 開啟 Sublime Package
2. 搜尋 Sublimelinter-coffeelint 並安裝
3. 開啟 terminal
4. 執行 npm install -g coffeelint
5. 複製 Default.coffeelint.json 內容 → [Link](https://github.com/TMDer/warehouse/blob/master/codeStyles/SublimeLinter%20Config/Default.coffeelint.json)
6. 專案根目錄新增 coffeelint.json 並貼上剛才複製的內容
7. 重開 Sublime

> 來源：https://github.com/SublimeLinter/SublimeLinter-coffeelint

## 安裝 SCSS Linter (Install SCSS linter)

1. 開啟 Sublime Package
2. 搜尋 sublimelinter-contrib-scss-lint 並安裝
3. 開啟 terminal
4. 執行 gem install scss_lint
5. 複製 Default.scss-lint.yml 內容 → [Link](https://github.com/TMDer/warehouse/blob/master/codeStyles/SublimeLinter%20Config/Default.scss-lint.yml)
6. 專案根目錄新增 .scss-lint.yml 並貼上剛才複製的內容
7. 執行 `scss-lint ~/workspace/pmd_platform/assets/linker/styles/**/*.scss --config .scss-lint.yml`
8. 重開 Sublime

> 來源：https://github.com/attenzione/SublimeLinter-scss-lint

## 安裝 JSON Linter (Install JSON's linter)

### *待補*

> 來源：https://github.com/SublimeLinter/SublimeLinter-json

## 安裝 Jade Linter (Install Jade's linter)

### *待補*

> 來源：https://github.com/benedfit/SublimeLinter-contrib-jade-lint

## Sublimelinter Setting

路徑：

`Perferenaces > Package Setting > SublimeLinter > Setting User`

| 欄位 | 建議設定 |
|---|---|
| gutter_theme | Packages/SublimeLinter/gutter-themes/Blueberry/cross/Blueberry - cross.gutter-theme |
| mark_style | fill |
| no_column_highlights_line | true |

## 問題排除

| 問題 | 解決方式 |
|---|---|
| coffeelint 無法正常執行 | 1. 開啟 terminal 執行 which coffeelint <br> 2. 複製搜尋出的路徑 <br> 3. 開啟 Sublimelinter 的 User 設定 [註1] <br> 4. 將 coffeelint 路徑放到 paths > osx [註2] <br> 5. 如果你用 nvm 和 zsh, 請確保設定是在 .zshenv 不是 .zshrc. [註3]

 |

* 註1：位置參照 [Sublimelinter 設定](#sublimelinter-setting)
* 註2：coffeelint 路徑記得前後加單引號（雙引號也可）
* 註3：參考連結 [SublimeLinter-coffeelint](#https://github.com/SublimeLinter/SublimeLinter-coffeelint)

## 參考

1. SublimeLinter：http://www.sublimelinter.com/en/latest/about.html
2. coffeelint： http://www.coffeelint.org/
3. scss-lint： https://github.com/brigade/scss-lint