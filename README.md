:: StoryInit
<<set $day = 1>>
<<set $energy = 100>>
<<set $language = 0>>
<<set $culture = 0>>
<<set $cards = []>>
<<set $maxDay = 7>>

:: StoryCaption
📅 第 <<= $day >> 天<br>
⚡ 體力：<<= $energy >><br>
🈶 華語能力：<<= $language >><br>
⭐ 文化分數：<<= $culture >><br>
📚 詞彙數：<<= $cards.length >><br>
<hr>

:: Start
<h1>🌃 台灣夜市探險記</h1>

你是一位來台灣交換的外國學生，希望透過探索夜市學習華語與認識台灣文化。

[[開始旅程->School]]

:: School
<<set $language += 10>>

<h2>🏫 華語課</h2>

今天上了華語課。

華語能力 +10

<br><br>

[[放學去夜市->NightMarket]]

:: NightMarket
<<if $energy <= 0>>
<<goto "Hotel">>
<</if>>

<h2>🌃 夜市入口</h2>

今晚要去哪裡？

<br><br>

[[🍢 小吃區->Food]]

[[🧋 飲料店->Drink]]

[[🎯 遊戲攤->Game]]

[[🏮 廟口文化區->Temple]]

[[🚌 公車站->Bus]]

[[🏨 回飯店->Hotel]]

:: Food
<<set $energy -= 15>>

<h2>🍢 小吃區</h2>

<<if !$cards.includes("蚵仔煎")>>
<<set $cards.push("蚵仔煎")>>
學到詞彙：蚵仔煎<br>
<<set $culture += 20>>
<</if>>

<<if !$cards.includes("臭豆腐")>>
<<set $cards.push("臭豆腐")>>
學到詞彙：臭豆腐<br>
<<set $culture += 20>>
<</if>>

<<if $language >= 30>>
你聽懂老闆介紹台灣小吃文化。<br>
文化分數 +30
<<set $culture += 30>>
<<else>>
你只能聽懂部分內容。
<</if>>

<br><br>

[[返回夜市->NightMarket]]

:: Drink
<<set $energy -= 10>>

<h2>🧋 飲料店</h2>

<<if !$cards.includes("珍珠奶茶")>>
<<set $cards.push("珍珠奶茶")>>
學到詞彙：珍珠奶茶<br>
<<set $culture += 20>>
<</if>>

<<if !$cards.includes("半糖")>>
<<set $cards.push("半糖")>>
學到詞彙：半糖<br>
<<set $culture += 20>>
<</if>>

<<if !$cards.includes("去冰")>>
<<set $cards.push("去冰")>>
學到詞彙：去冰<br>
<<set $culture += 20>>
<</if>>

[[返回夜市->NightMarket]]

:: Game
<<set $energy -= 20>>

<h2>🎯 遊戲攤</h2>

<<if random(1,100) > 50>>
挑戰成功！<br>
獲得夜市小禮物！<br>
<<set $culture += 50>>
文化分數 +50
<<else>>
挑戰失敗，下次再試！
<</if>>

<br><br>

[[返回夜市->NightMarket]]

:: Temple
<<set $energy -= 15>>

<h2>🏮 廟口文化區</h2>

<<if !$cards.includes("祈福")>>
<<set $cards.push("祈福")>>
學到詞彙：祈福<br>
<<set $culture += 20>>
<</if>>

<<if !$cards.includes("拜拜")>>
<<set $cards.push("拜拜")>>
學到詞彙：拜拜<br>
<<set $culture += 20>>
<</if>>

<<if $language >= 40>>
你聽懂廟方人員介紹台灣民間信仰。<br>
文化分數 +40
<<set $culture += 40>>
<</if>>

[[返回夜市->NightMarket]]

:: Bus
<<set $energy -= 10>>

<h2>🚌 公車站</h2>

<<if $language >= 50>>
你成功看懂公車路線圖。<br>
文化分數 +30
<<set $culture += 30>>
<<else>>
你看不太懂站牌資訊。
<</if>>

[[返回夜市->NightMarket]]

:: Hotel
<h2>🏨 飯店複習</h2>

今天學到：

<br><br>

<<for _i = 0; _i < $cards.length; _i++>>
• <<= $cards[_i] >><br>
<</for>>

<hr>

<<set $quiz = random(1,3)>>

<<if $quiz == 1>>

哪個是台灣著名飲料？

[[珍珠奶茶->Correct]]

[[蘋果汁->Wrong]]

<<elseif $quiz == 2>>

「拜拜」通常和哪裡有關？

[[廟宇->Correct]]

[[學校->Wrong]]

<<else>>

「去冰」是在買什麼時常用到？

[[飲料->Correct]]

[[公車票->Wrong]]

<</if>>

:: Correct
<h2>✅ 答對了！</h2>

<<set $culture += 100>>

文化分數 +100

<br><br>

[[睡覺->NextDay]]

:: Wrong
<h2>❌ 答錯了！</h2>

<<set $culture += 20>>

文化分數 +20

<br><br>

[[睡覺->NextDay]]

:: NextDay
<<set $day += 1>>
<<set $energy = 100>>

<<if $day > $maxDay>>
<<goto "Ending">>
<<else>>
<<goto "School">>
<</if>>

:: Ending
<h1>🎊 旅程結束</h1>

最終文化分數：<<= $culture >><br>
華語能力：<<= $language >><br>
學到詞彙：<<= $cards.length >> 個

<hr>

<<if $culture >= 700>>

<h2>🏆 真結局：夜市文化達人</h2>

你已經非常了解台灣夜市文化，也能用華語和當地人交流！

<<elseif $culture >= 400>>

<h2>😊 好結局：文化探索家</h2>

你對台灣文化有不錯的認識，收穫滿滿！

<<else>>

<h2>📖 普通結局：繼續努力</h2>

你還有許多台灣文化值得探索！

<</if>>

:: StoryStylesheet
body{
    background:#111;
    color:white;
    font-family:"Microsoft JhengHei",sans-serif;
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
