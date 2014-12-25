# TMD Naming Style

### Format (命名格式)
- Name (名稱)  
  spinal-case

### 注意
- _newAdMgmt.scss, 這名稱的命名過度龐大，目前還有許多其他模組，應該以部分模組名稱爲主，以此就以 adMgntSearchNav.scss 會是比較清楚直覺。
- class 命名，應該以動作爲主，semantic 爲優先，而不是用屬性 .float-left 這種命名就是一種不好的方式。
- 要習慣使用 sass 變數，進行固定數字，或者重複使用的變數取代。
- transition 的使用方式，請採用 compass, 這邊已經提過很多次 compass css3
- 屬性下設定的時候，要請清楚爲什麼要下這個屬性，ex, font-color 設定後，爲什麼還要在同時設定 color ?
- 如果因爲設定了 css 屬性，而影響到元件的樣式，請使用 class 命名限縮範圍，同時也進行模組樣式修正。

# 其餘參考
- [GitHub CSS Styleguide](https://github.com/styleguide/css)  
- [idiomatic CSS](https://github.com/necolas/idiomatic-css)
