> 版本:: v1.0 Jerry 2022/10/14  
> 來源:: [簡睿隨筆](https://jdev.tw/blog/)  
> PDF下載: [Obsidian-Introduction-2022.pdf](https://drive.google.com/drive/folders/1uXGuLqBIOBwTr2_gCJO62De6QWV-O3Qj?usp=sharing)

## 1\. 安裝與設定

### 1.1. 安裝

1.  安裝後建立文件資料夾
2.  建議資料夾使用Dropbox或Google Drive等雲端硬碟，屆時可同步到其他電腦與設備

-   官網：[Obsidian](https://obsidian.md/) 「A second brain, for you, forever.」
-   簡體中文說明網頁 [由此开始 – Obsidian 中文帮助 – Obsidian Publish](https://publish.obsidian.md/help-zh/%E7%94%B1%E6%AD%A4%E5%BC%80%E5%A7%8B)
-   說明文件GitHub，zh資料夾內是簡體中文的檔案，可以拿來當做第一個練習的儲存庫:
    -   Git SSH: [git@github.com](mailto:git@github.com):obsidianmd/obsidian-docs.git
    -   Git HTTPS: [https://github.com/obsidianmd/obsidian-docs.git](https://github.com/obsidianmd/obsidian-docs.git)

___

### 1.2. 初始設定

| 設定選項 | 大項 | 設定項目 | 建議 | 說明 |
| --- | --- | --- | --- | --- |
| 編輯器 | 顯示 | 縮減行寬 | 勾選 | 勾選後編輯區左右邊界空白變大 |
|  |  | 精確的換行符號 | 不勾選 | 勾選啟用嚴格的Markdown換行 |
|  |  | 顯示正文前頁 | 不勾選 | 預覽時顯示YAML區 |
| 檔案與鏈接 |  | 始終更新內部鏈接 | 勾選 | 變更檔名後自動更新所有引用 |
|  |  | 新建筆記儲存位置 | 下方指定的資料夾 | 建立inbox資料夾 |
|  |  | 偵測所有的副檔名 | 勾選 | .html、.jpg等能也能看到 |
|  |  | 新附件的預設位置 | 下方指定的資料夾 | 建立attachments，附件集中存放 |
| 外觀 | 基本佈景主題 | 佈景主題 | 點擊管理後挑選 | 選用Sanctum以測試 |
|  | Advanced | Show inline title | 不勾選 | 編輯區最上出現檔名 |
|  | CSS片段 |  |  |  |
| 快捷鍵 |  | 切換標題 | Ctrl+Alt+H | 測試如何設定 |
| 關於 | App | 檢查更新 |  | 版本更新 |
|  |  | 語言 |  | 切換Obsidian的語言 |
| 核心外掛程式 | 外掛程式清單 | Markdown格式轉換器 | 勾選 |  |
| 第三方外掛程式 |  | Turn on |  | 點擊以啟用 |
|  |  | 瀏覽 |  | 點擊以顯示外掛清鼉 |

___

### 1.3. 建議安裝外掛

| 分類 | 外掛 | 初始設定 | 建議 |
| --- | --- | --- | --- |
| 外觀 | Style Settings | 安裝並啟用，展開Sanctum |  |
|  |  | Active line highlighting | Subtitle highlight |
|  |  | Headings | 設定各級標題外觀
分別儲存H1~H6字體顏色

可用七彩色增強識別性

 |
| 使用介面加強 | Pane Relief |  | 分頁前進、後退顯示開檔數 |
| 編輯 | cMenu | cMenu columns | 增加數字以在一行容納更多按鈕 |
|  |  | 新增「切換標題」 | 點擊右下角切換顯示 |
|  | Markdown Table Editor | 點擊左側邊欄或設定快捷鍵 | 設定→快捷鍵，搜尋table，點擊按鍵 |

___

### 1.4. CSS片段

【設定】→【外觀】→【CSS片段】，點擊![📂](https://s.w.org/images/core/emoji/14.0.0/svg/1f4c2.svg)，在「`儲存庫根目錄\.obsidian\snippets`」裡新增common.css (任意檔名，副檔名.css)。

1.  新增檔案內容如下：

```
/* 頁籤上方加上顯著邊框 */
.is-focused .mod-active .workspace-tab-header.is-active {
  border-top: 3px solid orange;
}

/* caret line */
.theme-dark .cm-active, .theme-dark .suggestion-item.is-selected {
  background-color: #414040 !important;
}

.theme-light .cm-active, .theme-light .suggestion-item.is-selected {
  background-color: lightyellow !important;
}
```

2.  CSS片段裡啟用common.css
3.  頁籤上方會出現橘色邊框，游標所在列背景色顯著呈現

___

## 2\. 系統資料夾

\==文件資料夾/.obsidian==是系統目錄，內有子目錄：

1.  /plugins: 外掛資料夾，每個外掛佔用各自的目錄
2.  /themes: 佈景主題，每個主題佔用各自的目錄
3.  /snippets: CSS片段，用來自訂HTML的CSS類別

-   `.obsidian/*.json`: 系統的設定檔

## 3\. 常用快捷鍵

> macOS: Ctrl=Cmd，Alt=Option

| 按鍵 | 功能 | 安裝外掛 |
| --- | --- | --- |
| Ctrl+P | 開啟命令面板 |  |
| Ctrl+O | 快速切換(開檔) |  |
| Ctrl+T | 開啟新分頁 |  |
| Ctrl+Shift+T | 重新開啟剛關閉分頁 |  |
| Ctrl+W | 關閉當前分頁 |  |
| Ctrl+N | 建立新筆記 |  |
| Ctrl+Y | 刪除行 | Code Editor Shortcuts |
| Ctrl+D | 複製行 | Code Editor Shortcuts |
| Ctrl+J | 連接兩行 | Code Editor Shortcuts |
| Alt+↑ | 跳到上個標題 | Code Editor Shortcuts |
| Alt+↓ | 跳到下個標題 | Code Editor Shortcuts |
| Shift+Enter | 往下插入空行 |  |
| Ctrl+Enter | 複選框切換 (自行設定) |  |
| Ctrl+Shift+F | 全域搜尋 |  |
| Ctrl+K | 選取文字後按鍵，形成超鏈接 |  |
| Ctrl+← | 1\. 英文：向左一個Word
2\. 中文：向左一句

 |  |
| Ctrl+→ | 1\. 英文：向右一個Word

2\. 中文：向右一句

 |  |

___

| 按鍵 | 滑鼠操作 | 命令 | 功用 |
| --- | --- | --- | --- |
| Ctrl+Enter | Ctrl/Cmd+Click | Open link under cursor in new tab | 將游標位置的超鏈接開啟在新分頁 |
| Ctrl+Alt+Enter | Ctrl/Cmd+Alt+Click | Open link under cursor to the right | 將游標位置的超鏈開啟在新窗格 |
| Ctrl+Alt+Shift+Enter | Ctrl/Cmd+Alt+Shift+Click | Open link under cursor in new window | 將游標位置的超鏈開啟在新視窗 |

## 4\. 簡化Markdown操作

1.  安裝Markdown Shortcuts外掛，輸入 `>` 會彈出Markdown選單
2.  安裝Obsidian Editing Toolbar，在編輯區最上方顯示編輯工具列 (未上架)
3.  安裝Markdown Table Editor，可開啟表格編輯面板 (或使用Advanced Tables外掛)

___

## 5\. 善用YAML區

1.  YAML區在筆記最開頭
2.  以三個減號開頭與結尾
3.  內有`欄位名: 欄位值`的欄位來定義筆記的屬性（Meta data，詮釋資料或後設資料，就是描述資料的資料）
4.  YAML是另一個標記語言，完整語法可參考 [一文看懂 YAML 是什么？YAML 语法和用途简介](https://www.redhat.com/zh/topics/automation/what-is-yaml)
5.  最常用的欄位：
    1.  created (建檔日期): 名稱自訂
    2.  updated (修改日期): 名稱自訂
    3.  aliases: 筆記的代名，視同檔名
    4.  tags: 筆記的標籤，一或多個
    5.  cssClass: 頁面特定的CSS類別

### 5.1. YAML用處：使用Dataview外掛

筆記內可以用`欄位名::欄位值`建立Dataview的欄位。

> \[!TIP\] 參考  
> [Dataview使用說明](https://blacksmithgu.github.io/obsidian-dataview/)

> Q1. 找出最近一周內新增或修改的筆記

````
```dataview
table dateformat(file.ctime, "yyyy-MM-dd HH:mm") as 建檔時間,
  dateformat(file.mtime, "yyyy-MM-dd HH:mm") as 修改時間
from ""
where file.mtime>=date(2022-10-03) 
  and !contains(file.name, "template-") 
  and !contains(file.name, "!query-")
  and !contains(file.name, "202")
sort file.mtime desc
```
````

> Q2. 找出 #java 本年內新增或修改的筆記

````
```dataview
table dateformat(file.ctime, "yyyy-MM-dd HH:mm") as 建檔時間,
  dateformat(file.mtime, "yyyy-MM-dd HH:mm") as 修改時間
from #java
where file.mtime>=date(2022-01-01) 
  and !contains(file.name, "template-") 
  and !contains(file.name, "!query-")
  and !contains(file.name, "202")
sort file.mtime desc
```
````

___

## 6\. 標籤

-   在YAML區的tags欄位或筆記裡的任何位置皆可插入標籤
-   以井號開頭，不能夾有空白（井號後有空白就變成標題了）
-   可以用底線(`_`)或減號(`-`)當做分隔字元
-   不能全為數字：`#3c`可以用，但`#2022`無法使用
-   能用正斜線(`/`)形成巢狀式標籤：`#3c/notebook`、`#3c/mobilephone`

> \[!TIP\] 技巧![💡](https://s.w.org/images/core/emoji/14.0.0/svg/1f4a1.svg)  
> 為筆記加入可能用來==查詢==或==分類==的所有標籤

## 7\. 標題

標題裡的內容可以被獨立引用，因此添加內容時應做好等級區分與適當分類。修訂筆記時可開啟大綱面板以瀏覽筆記的章節大綱。

## 8\. 截圖

建議把圖檔存到雲端，Obsidian裡直接用網址，以免檔案遺失之類的問題。

> \[!INFO\] 參考  
> [upgit－使用GitHub圖床：快速上傳圖檔到GitHub並插入圖片網址到Obsidian](http://jdev.tw/blog/6982/)

___

## 9\. 我的筆記方法

依使用場景分成靈感筆記、閱讀筆記、彙總筆記、永久筆記、專案筆記、索引筆記與其他類型的筆記等。

### 9.1. 靈感筆記

靈光一閃、稍蹤即逝的絕妙想法必須立即記錄下來，建立在inbox裡，每天定時整理下列事項：

#### 9.1.1. 是新的且獨立的內容

1.  加上容易搜尋的標籤
2.  添加延伸想法並修訂原有內容
3.  打開歸屬分類的索引筆記，添加其檔名鏈接
4.  搬移至其他分類的資料夾

#### 9.1.2. 能歸屬到現有筆記的片段

-   添加標題後插入現有筆記裡
-   如果主題明確且時間允許，可略過inbox的操作而直接插入

### 9.2. 閱讀(文獻)筆記

將有明確來源的內容製作成的筆記，如文章、書籍、網頁、影片、Podcasts等。

-   以內容的本身為重點編寫的筆記，而不是僅僅歸檔而已
-   用自己的話重新改寫它，以確保完全理解它的概念
-   如果必須引用原文，使用 `>` 引用標記

### 9.3. 彙總筆記 (MOC)

某個會持續更新的知識建立彙總筆記，例如：

-   網頁技術筆記，蒐集網頁相關技術，隨著知識的累積會逐步建立新的彙總筆記，獨立出來的筆記會留下鏈接
    -   HTML筆記
    -   CSS筆記
    -   JavaScript筆記
    -   UI/UX筆記
    -   等等…
-   Obsidian筆記，記錄Obsidian使用相關知識，在學習過程中逐步形成新的筆記
    -   Obsidian Plugins筆記，常用外掛又再獨立出專門筆記
        -   Dataview筆記
        -   QuickAdd筆記
        -   Templater筆記
        -   等等…
    -   Obsidian CSS筆記
    -   筆記方法思考
    -   等等…

### 9.4. 永久筆記

一個自身邏輯完整的內容就是一個永久筆記。永久的意思是會==持續修訂==、永久保存，而不是一成不變。

> \[!TIP\] 技巧![💡](https://s.w.org/images/core/emoji/14.0.0/svg/1f4a1.svg)  
> 永久筆記可視同一個程式函數，能被不同程式調用

#### 9.4.1. 原子性（Atomicity）的思考

卡片盒筆記法強調原子性：一個筆記是一個自身邏輯完整的最小內容。我個人認為不必為了這個概念而強制原子性，有時原子性反而將知識分割成很難整合的狀態。筆記內容的粒度粗細會隨著學習的進展而逐步精鍊，一開始只要記錄下來就好。

> \[!TIP\] 技巧![💡](https://s.w.org/images/core/emoji/14.0.0/svg/1f4a1.svg)
> 
> 1.  先有內容，再形成結構
> 2.  盡量以寫文章的方式來記錄，方便引用

其實原子性的目的是為了提高重用性（Reusibility），對應到軟體設計就是要==模組化==，達到低耦合（Coupling）、高內聚（Cohesion）的目標：

-   低耦合：兩個筆記間的關連性或相依性要低
-   高內聚：筆記本身不需依賴其他筆記，就能具有完整Context（上下文）的閱讀性

> \[!TIP\] 技巧![💡](https://s.w.org/images/core/emoji/14.0.0/svg/1f4a1.svg)  
> 越獨立的內容越容易被引用，重用性越高。

例如在Obsidian的彙總筆記裡，可以把常用快捷鍵獨立成筆記，要使用的其他筆記用`![[Obsidian常用快捷鍵]]`的方式引用。  
也可以用標題直接寫在彙總筆記裡：

```
## Obsidian常用快捷鍵
...
```

要使用的其他筆記用`![[Obsidian筆記#Obsidian常用快捷鍵]]`的方式引用。

___

> \[!REF\] 我的想法…
> 
> -   一個想法就獨立一張卡片(一個筆記檔案)在學習上有實質困難，因為學習的**特定事物**原本就有連續性與一貫性，強制分割反而造成閱讀上的障礙
> -   應該善用標題段落、區塊來形成連續的內容，也能方便被引用

### 9.5. 專案筆記

最終的**輸出用**筆記，通常完成後就不會再變動，例如Blog的文章、分享的技術文件PDF等。  
^test-123

### 9.6. 索引筆記 (MOC的另一種形式)

另一種形式的彙總筆記，將相同主題的筆記以清單形式逐筆列出。它的目的是==註冊==該主題的所有筆記，從而減少孤兒筆記。  
例如Obsidian-Index：

```
# Obsidian Index
## 1. 彙總筆記
- [[Obsidian Notes]]
- [[Obsidian Plugins Notes]]
    - [[Obsidian Dataview Notes]]
    - [[Obsidian QuickAdd Notes]]
    - [[Obsidian Templater Notes]]
- [[Obsidian Thinking Notes]]

## 2. Obsidian影片
 Obsidian教學系列播放清單: https://www.youtube.com/playlist?list=PLWg9zacwOnwfcpVm5pAKgOHms7PntsgJS

- [[Obs＃01 超強筆記軟體Obsidian (黑曜石)介紹與Zettelkasten筆記系統簡述]]
- ...

## 3. Articles/簡報
- [[Obsidian筆記工具簡介-2021]]
- [[Obsidian Introduction-2022]]
...
```

-   如果你的筆記YAML記錄得很精確，索引筆記的內容應該能以Dataview來產生
-   Obsidian的彙總筆記和索引筆記是否疊床架屋？為何不把索引清單寫在彙總筆記裡？原因如下：
    -   彙總筆記注重的是==內容==，而索引筆記要的是有順序、分類明確的清單==資料==
    -   特定領域主題產生出的專案筆記可能為數眾多，獨立存放在索引筆記裡不致造成彙總筆記過大或龐雜，修改速度較不受影響

___

### 9.7. 其他類型的筆記

1.  各類紀錄：會議紀錄、關鍵字筆記(Glossary)等
2.  每日筆記 (含任務待辦清單)、Review筆記、Kanban筆記、Excalidraw或Draw.io筆記等
3.  Obsidian專用筆記：模板、主頁、跳轉用筆記等
4.  蒐集到的參考文章

## 10\. Chrome擴充

1.  [TabCopy](https://chrome.google.com/webstore/detail/tabcopy/micdllihgoppmejpecmkilggmaagfdmb): 複製分頁的標題與網址
2.  [MarkDownload](https://chrome.google.com/webstore/detail/markdownload-markdown-web/pcmpcfapbekmbjjkdalcgopdkipoggdi)：將網頁轉換成Markdown格式
3.  [HTML Table to Markdown](https://chrome.google.com/webstore/detail/html-table-to-markdown/ghcdpakfleapaahmemphphdojhdabojj): 將HTML table轉換成Markdown語法
4.  [Markdown Here](https://chrome.google.com/webstore/detail/markdown-here/elifhakcjgalahccnjkneoccemfahfoa): Gmail的Markdown內容轉換成網頁內容

___

## 教學影片

\[Obs＃100\]到\[Obs＃104\]連著五支Obsidian教學影片是我在2022年10月14日錄製的新手入門教學，對象是對Obsidian有興趣的軟體開發人員，大部份沒有使用過Obsidian，有八成可以說是Obsidian的新手小白。

希望這些影片對於想要學習Obsidian又深怕學習曲線陡峭的朋友們，能夠有些幫助。如果你覺得我的分享對你有些微助益的話，請不吝訂閱、分享、按贊，並多看些廣告或按超級感謝。自媒體創作者很需要觀眾的支持與鼓勵，謝謝。

![✅](https://s.w.org/images/core/emoji/14.0.0/svg/2705.svg) 教學文章: [https://jdev.tw/blog/7745/](https://jdev.tw/blog/7745/)

![✅](https://s.w.org/images/core/emoji/14.0.0/svg/2705.svg) 教學文件的PDF可由[Google Dirve](https://drive.google.com/drive/folders/1uXGuLqBIOBwTr2_gCJO62De6QWV-O3Qj?usp=sharing)下載

1.  \[Obs＃100\] 新手入門1/5-安裝與外觀設定、外掛安裝  
    ![🔗](https://s.w.org/images/core/emoji/14.0.0/svg/1f517.svg) [https://youtu.be/oCdgY0omd8I](https://youtu.be/oCdgY0omd8I)
2.  \[Obs＃101\] 新手入門2/5-初始設定與建議外掛：YAML、Tabs/Panes、Style settings  
    ![🔗](https://s.w.org/images/core/emoji/14.0.0/svg/1f517.svg) [https://youtu.be/AJ9iUcfuOX8](https://youtu.be/AJ9iUcfuOX8)
3.  \[Obs＃102\] 新手入門3/5-大綱、Markdown外掛、快捷鍵、CSS片段  
    ![🔗](https://s.w.org/images/core/emoji/14.0.0/svg/1f517.svg) [https://youtu.be/j8RwDQHipz0](https://youtu.be/j8RwDQHipz0)
4.  \[Obs＃103\] 新手入門4/5-建立筆記、YAML詳解、Dataview、標籤使用要點  
    ![🔗](https://s.w.org/images/core/emoji/14.0.0/svg/1f517.svg) [https://youtu.be/x2q79T0FyqM](https://youtu.be/x2q79T0FyqM)
5.  \[Obs＃104\] 新手入門5/5-我的筆記方法 (完)  
    ![🔗](https://s.w.org/images/core/emoji/14.0.0/svg/1f517.svg) [https://youtu.be/hWpi74UrUw0](https://youtu.be/hWpi74UrUw0)

＃＃

#### 您可能也會有興趣的類似文章

-   [\[Obs＃86\] 分享與編輯器相關的21個Obsidian外掛](https://jdev.tw/blog/7102/21-obsidian-plugins-for-editor "[Obs＃86] 分享與編輯器相關的21個Obsidian外掛") (0則留言, 2022/05/08)
-   [\[Obs＃95\] Obsidian v0.16對於使用介面的強化![🚀](https://s.w.org/images/core/emoji/14.0.0/svg/1f680.svg)](https://jdev.tw/blog/7658/obsidian-v0-16-tabs-enhancements "[Obs＃95] Obsidian v0.16對於使用介面的強化🚀") (0則留言, 2022/09/04)
-   [\[Obs＃45\] 軟體工程師必備的6個Obsidian外掛](https://jdev.tw/blog/6778/obsidian-plugins-for-developers "[Obs＃45] 軟體工程師必備的6個Obsidian外掛") (0則留言, 2021/08/13)
-   [\[Obs＃92\] Obsidian彙編文章的簡單方法：2個外掛＋1個CSS片段](https://jdev.tw/blog/7190/obsidian-compile-notes-and-dynamic-embed "[Obs＃92] Obsidian彙編文章的簡單方法：2個外掛＋1個CSS片段") (0則留言, 2022/07/16)
-   [\[Obs＃78\] 輔助Markdown初學者的利器：Markdown Shortcuts與cMenu](https://jdev.tw/blog/7048/markdown-shortcuts-and-cmenu "[Obs＃78] 輔助Markdown初學者的利器：Markdown Shortcuts與cMenu") (0則留言, 2022/03/27)
-   [\[Obs＃96\] Obsidian分頁調整： CSS樣式與外掛，讓分頁操作更簡便](https://jdev.tw/blog/7676/obsidian-tabs-css-snippets-and-autohotkey-script "[Obs＃96] Obsidian分頁調整： CSS樣式與外掛，讓分頁操作更簡便") (0則留言, 2022/09/10)
-   [\[Obs＃85\] 分享使用中與外觀有關的10個外掛](https://jdev.tw/blog/7095/obsidian-ui-related-10-plugins "[Obs＃85] 分享使用中與外觀有關的10個外掛") (0則留言, 2022/05/01)
-   [Obsidian (黑曜石)筆記軟體的基本操作指引](https://jdev.tw/blog/6319/obsidian-users-guide "Obsidian (黑曜石)筆記軟體的基本操作指引") (0則留言, 2020/06/23)
-   [\[Obs#12\] Obsidian v0.8.4~v0.8.9的新增功能](https://jdev.tw/blog/6409/obs12-obsidian-v0-8-9-features "[Obs#12] Obsidian v0.8.4~v0.8.9的新增功能") (0則留言, 2020/09/06)
-   [\[Obs＃88\] 綜合練習：快速設定的6種方法─使用8個Obsidian外掛](https://jdev.tw/blog/7114/obs%ef%bc%8388-%e7%b6%9c%e5%90%88%e7%b7%b4%e7%bf%92%ef%bc%9a%e5%bf%ab%e9%80%9f%e8%a8%ad%e5%ae%9a%e7%9a%846%e7%a8%ae%e6%96%b9%e6%b3%95%e2%94%80%e4%bd%bf%e7%94%a88%e5%80%8bobsidian%e5%a4%96%e6%8e%9b "[Obs＃88]  綜合練習：快速設定的6種方法─使用8個Obsidian外掛") (0則留言, 2022/05/21)
-   [\[Obs＃22\] 讓有效學習更簡單！Markdown匯出到Anki | 使用Flashcards外掛](https://jdev.tw/blog/6505/obsidian-plugin-flashcards-integrates-anki "[Obs＃22] 讓有效學習更簡單！Markdown匯出到Anki | 使用Flashcards外掛") (0則留言, 2020/12/12)
-   [超強筆記軟體Obsidian (黑曜石)介紹與Zettelkasten筆記系統簡述](https://jdev.tw/blog/6315/obsidian-and-zettelkasten-introduction "超強筆記軟體Obsidian (黑曜石)介紹與Zettelkasten筆記系統簡述") (0則留言, 2020/06/21)
-   [\[Obs＃33\] Media-Extended：嵌入多媒體檔案的簡單方法](https://jdev.tw/blog/6626/obsidian-plugin-media-extended "[Obs＃33] Media-Extended：嵌入多媒體檔案的簡單方法") (0則留言, 2021/04/17)
-   [\[Obs＃69\] 由豆瓣建立Minimal樣式主題的閱讀書單卡片](https://jdev.tw/blog/6988/minimal-theme-cards-with-douban-books "[Obs＃69] 由豆瓣建立Minimal樣式主題的閱讀書單卡片") (0則留言, 2022/02/11)
-   [Obsidian Tab Shortcuts彙總](https://jdev.tw/blog/7645/obsidian-tab-shortcuts%e5%bd%99%e7%b8%bd "Obsidian Tab Shortcuts彙總") (0則留言, 2022/08/31)