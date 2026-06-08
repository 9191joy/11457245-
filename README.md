# 留學夜市日記（Twine SugarCube 期末專題）

## 遊戲名稱

留學夜市日記

## 遊戲類型

生活模擬、文化學習、互動故事

## 遊戲背景

玩家扮演一位來台灣旅遊的外國學生，希望透過探索台灣夜市認識台灣文化與華語詞彙。

白天在學校學習基礎華語，晚上前往夜市探索不同攤位與場景。透過與攤販、居民互動，學習新的詞彙與文化知識，並將學習內容加入記憶卡系統。

每天回到飯店後，玩家必須複習當天學到的內容並完成測驗，獲得文化學習分數。當文化分數累積達1000分時，即可完成文化探索之旅並達成結局。

---

## 遊戲目標

累積文化學習分數達1000分。

---

## 遊戲流程

白天上課
↓
提升華語能力
↓
晚上探索夜市
↓
觸發事件
↓
學習詞彙與文化知識
↓
加入記憶卡
↓
回飯店複習
↓
完成測驗
↓
獲得文化分數
↓
進入下一天

---

## 場景設計

1. 夜市入口
2. 小吃攤
3. 飲料店
4. 遊戲攤位
5. 服飾攤
6. 廟口
7. 市場
8. 公車站
9. 飯店

---

## 數值系統

### 體力 Energy

初始值：100

移動場景 -10

與攤販互動 -5

參加遊戲 -15

體力歸零必須回飯店休息

---

### 華語能力 Language

初始值：0

每天上課增加10點

影響後續對話內容

---

### 文化分數 Score

學習新詞彙 +20

學習文化知識 +30

測驗答對 +100

測驗答錯 +20

達到1000分獲勝

---

## 記憶卡系統

飲料店：

珍珠奶茶

半糖

去冰

小吃攤：

蚵仔煎

臭豆腐

排隊

廟口：

祈福

香火

拜拜

服飾攤：

殺價

試穿

便宜

---

## 結局

文化分數小於1000：

普通結局

「你還有許多台灣文化等待探索。」

文化分數大於等於1000：

真結局

「恭喜成為夜市文化達人！」

---

# SugarCube 程式碼

## StoryInit

```javascript
<<set $day = 1>>
<<set $energy = 100>>
<<set $score = 0>>
<<set $language = 0>>
<<set $cards = []>>
```

## Start

```html
<h1>🌃 留學夜市日記</h1>

你是一位來台灣旅遊的外國學生。

[[開始旅程->School]]
```

## School

```html
<<set $language += 10>>

<h2>🏫 學校</h2>

今天學習了新的華語內容。

華語能力 +10

[[前往夜市->NightMarket]]
```

## NightMarket

```html
<h2>🌃 夜市入口</h2>

[[🍢 小吃攤->Food]]

[[🧋 飲料店->Drink]]

[[🎯 遊戲攤位->Game]]

[[👕 服飾攤->Clothes]]

[[🏮 廟口->Temple]]

[[🏨 回飯店->Hotel]]
```

## Food

```html
<<if !$cards.includes("蚵仔煎")>>
<<set $cards.push("蚵仔煎")>>
<<set $score += 20>>
<</if>>

<<set $energy -= 10>>

學到新詞彙：蚵仔煎

[[返回夜市->NightMarket]]
```

## Drink

```html
<<if !$cards.includes("珍珠奶茶")>>
<<set $cards.push("珍珠奶茶")>>
<<set $score += 20>>
<</if>>

<<set $energy -= 10>>

學到新詞彙：珍珠奶茶

[[返回夜市->NightMarket]]
```

## Game

```html
<<set $energy -= 15>>

<<if random(1,100) > 50>>
挑戰成功！
<<set $score += 50>>
<<else>>
挑戰失敗！
<</if>>

[[返回夜市->NightMarket]]
```

## Clothes

```html
<<if !$cards.includes("殺價")>>
<<set $cards.push("殺價")>>
<<set $score += 20>>
<</if>>

<<set $energy -= 10>>

學到新詞彙：殺價

[[返回夜市->NightMarket]]
```

## Temple

```html
<<if !$cards.includes("祈福")>>
<<set $cards.push("祈福")>>
<<set $score += 30>>
<</if>>

<<set $energy -= 10>>

學到文化知識：祈福

[[返回夜市->NightMarket]]
```

## Hotel

```html
<h2>🏨 飯店複習</h2>

今日學習內容：

<<for _i = 0; _i < $cards.length; _i++>>
* <<= $cards[_i] >>
<</for>>

問題：

珍珠奶茶屬於哪種類別？

[[飲料->PassQuiz]]

[[水果->FailQuiz]]
```

## PassQuiz

```html
<<set $score += 100>>

測驗成功！

[[睡覺->NextDay]]
```

## FailQuiz

```html
<<set $score += 20>>

測驗失敗。

[[睡覺->NextDay]]
```

## NextDay

```html
<<set $day += 1>>
<<set $energy = 100>>

<<if $score >= 1000>>
<<goto "Ending">>
<<else>>
<<goto "School">>
<</if>>
```

## Ending

```html
<h1>🏆 夜市文化達人</h1>

恭喜完成台灣夜市文化探索之旅！

最終文化分數：

<<= $score >>
```

---

## Story Stylesheet

```css
body{
background:#0b0b0b;
color:white;
font-family:"Microsoft JhengHei";
}

h1{
color:#FFD700;
text-align:center;
}

h2{
color:#00FFFF;
}

a{
color:#FF66CC;
font-weight:bold;
}

a:hover{
color:#FFD700;
}

.passage{
max-width:900px;
margin:auto;
}
```
