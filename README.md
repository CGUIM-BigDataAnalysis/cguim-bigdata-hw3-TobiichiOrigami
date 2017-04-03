長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
#install.packages("rvest")
library(rvest) ##第一次使用要先安裝 install.packages("rvest")
```

    ## Warning: package 'rvest' was built under R version 3.3.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 3.3.3

``` r
siteURL<-"https://www.ptt.cc"
targetURL<-paste0(siteURL, "/bbs/LoL/index.html")
##read_html
##html_nodes
##html_text
rownumber<-0
AllDatas<-NULL
while(rownumber<100){
    btns<-read_html(targetURL) %>% html_nodes(".action-bar a") %>% html_attr("href")
    previouspage<-btns[4]
    Titles<-read_html(targetURL) %>% html_nodes(".title") %>% html_text()
    PushNums<-read_html(targetURL) %>% html_nodes(".nrec") %>% html_text()
    Authors<-read_html(targetURL) %>% html_nodes(".author") %>% html_text()
    targetURL<-paste0(siteURL, previouspage)
    tempDatas<-data.frame(Title=c(Titles), PushNum=c(PushNums), Author=c(Authors))
    if(is.null(AllDatas)){
        rownumber<-nrow(tempDatas)
        AllDatas<-tempDatas
    }
    else{
        AllDatas<-rbind(AllDatas, tempDatas)
        rownumber<-nrow(AllDatas)
    }
}
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(AllDatas)
```

| Title                                            | PushNum | Author       |
|:-------------------------------------------------|:--------|:-------------|
| (本文已被刪除) \[alive211079\]                   | 9       | -            |
| \[實況\] 晴時多雲偶陣雨 火龍果妹                 | 13      | XDos         |
| \[實況\] Troll死你們 草人爬分台                  |         | yulymoon     |
| \[問題\] LCK 飛斯 逆命 雷尼克頓                  | 11      | ezo786       |
| Re: \[閒聊\] 新故事的汎根本是個碧曲吧！？        | 9       | LightEcho    |
| \[問題\] 請問丁特該不該回歸？                    | 3       | s6622156     |
| Re: \[ANSI\] 索娜 Sona                           | 10      | f222051618   |
| Re: \[閒聊\] 新故事的汎根本是個碧曲吧！？        | 6       | Stabberlol   |
| \[公告\] LoL║英雄 ┌──┐４月閒聊區┌→               | 98      | rainnawind   |
| \[公告\] LoL 英雄聯盟板板規（Patch 17.01.01）    |         | rainnawind   |
| \[電競\] 近期賽事                                | 41      | superRKO     |
| \[實況\] SKT T1 kkOma(關                         | 5       | narutodante  |
| \[問題\] 最快打完前十場的方法                    | 2       | Campione3310 |
| \[情報\] 約德爾人的主題日！兒童節可愛優惠        | 23      | LegendDragon |
| \[問題\] 電競館門票問題                          | 10      | ex8338       |
| \[問題\] 招換師技能互換為何勝率會大增            | 10      | songgood     |
| \[閒聊\] 台服現在最強寇格魔是誰?                 | 77      | seysem       |
| Re: \[閒聊\] Apex回答太狂 還是大魚功力不足？     |         | shintrain    |
| \[問題\] 清明節會有人幫阿姆姆掃墓嗎?             | 34      | iamfenixsc   |
| \[實況\] RPG Evi 韓服 日本隊上路                 | 16      | zxc7         |
| \[閒聊\] 新故事的汎根本是個碧曲吧！？            | 37      | f222051618   |
| Re: \[閒聊\] Apex回答太狂 還是大魚功力不足？     | 5       | joe255118    |
| (已被samhou6刪除) <iloveykk> D1                  | 4       | -            |
| \[ANSI\] 索娜 Sona                               | 52      | shyin7089    |
| \[實況\] 性感荷官 彈性積分五排                   | 3       | MRsoso       |
| (已被samhou6刪除) <starfishkira> D1              | 19      | -            |
| \[實況\] 獸控實況主Dog4ni – 高端魔術秀           | 1       | wuisgod54    |
| \[實況\] I3utterfly0v0/蝴蝶兒&lt;3               |         | airiguodala  |
| \[閒聊\] 為什麼Riot都不出多控英雄                | 24      | azjba89xz    |
| \[實況\]麥麥貝比/今天適合練腳 練到105cm長腿      | 6       | chulashiy    |
| \[閒聊\] 球z跟丁特誰的JG比較強?                  | 21      | womantalk    |
| \[閒聊\] LOL有關於魔道的角色嗎?                  | 7       | iloveykk     |
| (本文已被刪除) \[sky082\]                        |         | -            |
| \[閒聊\] 徵求LMS 4/8門票兩張                     | 5       | iverson242i  |
| \[問題\] 除了opgg有其他網站嗎                    | 3       | disa26118    |
| (本文已被刪除) \[Aatrox5566\]                    | 1       | -            |
| Re: \[閒聊\] Apex回答太狂 還是大魚功力不足？     | 98      | eltar        |
| \[外絮\] JCRE FB                                 | 爆      | dinter9921   |
| \[閒聊\] LMS 2017 Spring 數據整理(~4/2)          | 39      | fkc          |
| \[影片\] 歐洲最強逆命精華                        | 14      | waiting0212  |
| \[閒聊\] 在傳說啟程發現一件事情                  | 3       | cocoinin     |
| \[實況\] TPS King / GodJJ 回來了                 | 34      | eqer         |
| Re: \[閒聊\] 大家按Q技能會用小拇指嗎?            | 1       | handsomeLin  |
| \[心得\] 國動真的對積分現況有所改革了            | 38      | machiner     |
| \[心得\] 真的很OP－野區暴徒 暴走重砲 吉茵珂絲    |         | x236x55x3    |
| \[閒聊\] 我在召喚峽谷裡得到了救贖                |         | bubuno35     |
| (本文已被刪除) \[ooqr1995tw\]                    |         | -            |
| \[問題\] 會戰找不到自己游標怎麼辦                | 8       | d995511      |
| \[揪團\] 跟女友吵架的單雙（滿                    | 6       | jkonk9527    |
| (本文已被刪除) \[HITTEN\]                        | 1       | -            |
| \[閒聊\] J特真的比動主播好                       | X1      | asd0952      |
| Re: \[問題\] 國動的崛起是否意味著lol走偏了       |         | tigotigo5566 |
| \[問題\] 潘森是線霸嗎?                           | 14      | FrogStar     |
| \[閒聊\] 探討犽宿的風牆效用                      | X2      | Baledu       |
| (本文已被刪除) \[LIN6627\]                       |         | -            |
| \[問題\] 不投降跟風氣差 跟張家兄弟有什麼關係?    |         | godband5566  |
| \[閒聊\] 打野該積極gank嗎                        | X2      | FollowMe6    |
| Re: \[閒聊\] Apex回答太狂 還是大魚功力不足？     |         | birdanderson |
| \[閒聊\] 國棟的鼻地戰術是傳承了中國武術？        | 76      | stu88001     |
| (本文已被刪除) \[qwertytrew\]                    |         | -            |
| \[閒聊\] 賈克斯打sup為啥不行                     |         | tigotigo5566 |
| Re: \[閒聊\] Apex回答太狂 還是大魚功力不足？     | 5       | InnGee       |
| \[問題\] 殞落王者之劍是不是很適合特朗德?         | 33      | FrogStar     |
| \[閒聊\] WS如果要贏到底還缺了甚麼東西?           | 20      | orange0319   |
| \[實況\] 胡瓜太郎 Otofu 台服鑽二Sup遊玩中        | 18      | goodjob622   |
| \[實況\] M17 APEX                                | 爆      | shan0825     |
| \[問題\] ARAM也有高低端場分別嗎?                 | 22      | osbsd1       |
| \[實況\] FW NL / 煞氣o狂by衝崩銨                 | 29      | ns96729      |
| \[閒聊\] 解說記得的正宗中文教學                  | 6       | diefish5566  |
| \[問題\] 丁特有考慮練蒙多醫生JG嗎？              | 2       | ru04ul4      |
| \[閒聊\] HKE韓服成績真的深不可測                 | 8       | stben        |
| \[閒聊\] 會看EU&其他區比賽的人 是用什麼心情在看? | 15      | jakert123    |
| \[外絮\] Peanut安慰沒進入季後賽的Gorilla         | 60      | aaronshell   |
| \[閒聊\] 如果實況界沒統神現在會是甚麼風氣?       | 8       | KENDO777     |
| \[影片\]【國動】被戳到爆氣開啟動粉見面會         | 24      | sky082       |
| Re: \[閒聊\] 如果實況界沒統神現在會是甚麼風氣?   |         | ardan3355    |
| (本文已被刪除) \[asd0952\]                       |         | -            |
| \[揪團\] 金牌彈性-1                              |         | jun12344     |
| \[閒聊\] Apex回答太狂 還是大魚功力不足？         | 51      | Tiandai      |
| \[閒聊\] Weekly LCK Mic check                    | 23      | s80554       |
| (本文已被刪除) \[pttpig\]                        |         | -            |
| Re: \[閒聊\] Apex回答太狂 還是大魚功力不足？     | 51      | bingtsien    |
| (本文已被刪除) \[melon1001\]                     |         | -            |
| \[閒聊\] 有沒有專精克雷德的玩家來交流個          | 43      | silly7995    |
| \[揪團\] 找上白金的夥伴                          | 1       | trollriven   |
| \[揪團\] 銅銀小號雙排                            | 2       | FJUmars      |
| Re: \[問題\] 死不投降是不是台服素質如此差的原因? | X1      | McHamburger  |
| \[實況\] 刺刺的 韓服 金三                        |         | ym19950822   |
| (本文已被刪除) \[hongou\]                        |         | -            |
| \[實況\] 藍色風暴 龍獸 金牌RANK<sub>~</sub>      |         | pcnetworld   |
| Re: \[問題\] 國動的崛起是否意味著lol走偏了       | 7       | tenshoufly   |
| \[閒聊\] 是不是應該拔除某些玩家的投票權          |         | joshua0606   |
| \[閒聊\] 同人圖分享-你以為有貓我就會推嗎？       | 6       | f222051618   |
| \[閒聊\] 【統神】深夜真性情—那些年的誤會委屈     | 11      | g8320484816  |
| \[閒聊\] 小熊 Yuniko FB                          | 20      | Comebuy      |
| \[ANSI\] 瓦羅然沒有派對                          | 18      | AlzioNever   |
| \[閒聊\] 大家按Q技能會用小拇指嗎?                | 48      | phillp0804   |
| Re: \[問題\] 國動的崛起是否意味著lol走偏了       | 4       | sincossincos |
| Re: \[閒聊\] 這季MVP該給誰                       | 3       | Re12345      |
| \[閒聊\] 一發死的角色是不是逐漸消失中?           | 12      | greattower   |
| Re: \[問題\] 死不投降是不是台服素質如此差的原因? | 2       | kingion      |
| (本文已被刪除) \[dant123\]                       |         | -            |
| \[發錢\] 國考放榜來猜猜灰鵝喜歡的LCK選手(Done)   | 82      | where1993    |
| \[閒聊\] HKE vs. M17 G2 分析台+國人訪問逐字      | 38      | eltar        |
| Re: \[閒聊\] 大家按Q技能會用小拇指嗎?            | 17      | s930406      |
| Re: \[閒聊\] LMS春季第一隊的上路會是誰？         | 2       | willia5566   |
| Re: \[問題\] 國動的崛起是否意味著lol走偏了       | 11      | arrenwu      |
| Re: \[閒聊\] LMS春季第一隊的上路會是誰？         | 3       | kingion      |
| \[閒聊\] 美板官方粉絲團 FB                       | 17      | Comebuy      |
| \[閒聊\] ROC是不是很悲情？                       | 31      | andy82116    |
| \[電競\] 2017 NA LCS夏季升降賽Day3 NV vs. GCU    | 3       | cherrycheese |

解釋爬蟲結果
------------

``` r
#這是R Code Chunk
nrow(AllDatas)
```

    ## [1] 111

這是我爬到的堆文數量,因為我是讓程式判斷抓到超過100筆就停，因此每次結果不盡想同，隨時有人發文都將改變抓到的資料

``` r
#這是R Code Chunk
table(AllDatas$Author)
```

    ## 
    ##            -       ezo786   f222051618    LightEcho   rainnawind 
    ##           14            1            3            1            2 
    ##     s6622156   Stabberlol     superRKO         XDos     yulymoon 
    ##            1            1            1            1            1 
    ##  airiguodala    azjba89xz Campione3310    chulashiy       ex8338 
    ##            1            1            1            1            1 
    ##   iamfenixsc    joe255118 LegendDragon       MRsoso  narutodante 
    ##            1            1            1            1            1 
    ##       seysem    shintrain    shyin7089     songgood    womantalk 
    ##            1            1            1            1            1 
    ##    wuisgod54         zxc7      asd0952     bubuno35     cocoinin 
    ##            1            1            1            1            1 
    ##      d995511   dinter9921    disa26118        eltar         eqer 
    ##            1            1            1            2            1 
    ##          fkc  handsomeLin     iloveykk  iverson242i    jkonk9527 
    ##            1            1            1            1            1 
    ##     machiner  waiting0212    x236x55x3       Baledu birdanderson 
    ##            1            1            1            1            1 
    ##  diefish5566    FollowMe6     FrogStar  godband5566   goodjob622 
    ##            1            1            2            1            1 
    ##       InnGee      ns96729   orange0319       osbsd1      ru04ul4 
    ##            1            1            1            1            1 
    ##     shan0825        stben     stu88001 tigotigo5566   aaronshell 
    ##            1            1            1            2            1 
    ##    ardan3355    bingtsien      FJUmars    jakert123     jun12344 
    ##            1            1            1            1            1 
    ##     KENDO777  McHamburger   pcnetworld       s80554    silly7995 
    ##            1            1            1            1            1 
    ##       sky082   tenshoufly      Tiandai   trollriven   ym19950822 
    ##            1            1            1            1            1 
    ##   AlzioNever    andy82116      arrenwu cherrycheese      Comebuy 
    ##            1            1            1            1            2 
    ##  g8320484816   greattower   joshua0606      kingion   phillp0804 
    ##            1            1            1            2            1 
    ##      Re12345      s930406 sincossincos    where1993   willia5566 
    ##            1            1            1            1            1

照ID出現次數列出，可以看到發文最多的Author，這次次數最多者是刪文者，其作者並不一定相同，無法判定誰是真正發文王，但其實大家在前100筆資料內發文數差不多，大多非1即2

人工結論與解釋： 這支程式是抓取最新的至少100筆資料，一邊寫程式一邊有人發文，所以抓到的資料一直變動，有點難解釋誰是發文最多或者抓到的資料有幾筆，因為會隨著最新發文而可能有些許的改變。 另外我本人完全不懂LOL，雖知是個好玩的遊戲，但一直沒有過身的涉略，所以找尋有趣的現象也滿困難的，如果是抓Tennis看板的話，我一定可以滔滔不絕的說出各種最新網球動態的。 真的要說有趣的事情那就是一票人喜歡問問題卻掛閒聊的標籤，然後針對閒聊標籤回文數也比較多，真正掛問題標籤得到的回應數反而比較少www
