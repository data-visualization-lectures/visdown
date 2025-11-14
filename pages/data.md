# データセット

外部データセットを使用することもできますし、Visdown を試すために次のデータセットを使うこともできます。

## データの読み込み
任意の csv、tsv、あるいは json ファイルを使ってデータセットを読み込むことができます。

```
data: 

## Sample

これは最もシンプルなデータセットです。

| area    |  sales | profit | 
|:--------|-------:|-------:|
| North   |     5  |      2 |  
| East    |    25  |      8 |  
| West    |    15  |      6 |  
| South   |    20  |      5 |  
| Central |    10  |      3 |  

Metadata
- ファイル名: `sample.csv`
- 観測数 `(n)` : 5
- 特徴量の数 `(p)` : 3

```vis
data: 
 - url: sample.csv
mark: point
encoding: 
  x: 
   (data/sample.csv) | point(x=sales:Q, y=profit:Q, color=area:N)
```

## Cars

インドの自動車と基本統計の一覧

| brand   | model  |  price |   kmpl | type      |   bhp  |
|:--------|:-------|-------:|-------:|:----------|-------:|
| Tata    | Nano   |    199 |   23.9 | Hatchback |    38  |
| Suzuki  | Alto800|    248 |   22.7 | Hatchback |    47  |
| Hyundai | EON    |    302 |   21.1 | Hatchback |    55  |
| Nissan  | Datsun |    312 |   20.6 | Hatchback |    67  |
| ...     | ...    |    ... |    ... | ...       |   ...  |
| Suzuki  | Ciaz   |    725 |   20.7 | Sedan     |    91  |
| Skoda   | Rapid  |    756 |   15.0 | Sedan     |   104  |
| Hyundai | Verna  |    774 |   17.4 | Sedan     |   106  |
| VW      | Vento  |    785 |   16.1 | Sedan     |   104  |

Metadata
- ファイル名: `cars.csv`
- 観測数 `(n)`: 42
- 特徴 `(p)`  : 6
  - `brand` : ブランド名
  - `model` : モデル名
  - `price` : 価格（単位：インド・ルピー / 1000 INR）
  - `kmpl`  : 燃費（km/L）
  - `type`  : 車種（Hatchback または Sedan）
  - `bhp`   : ブレーキ馬力（brake horsepower）
- 出典: 自動車比較サイトのデータを基に作成

```vis
data(data/cars.csv) | point(x=kmpl:Q, y = price:Q)
```

## Flights

このデータセットは、ロンドンの5つの空港からアメリカ主要5空港へのフライトの定時運行状況に関するものです。

| source| dest | airline | flights| onTimePerf| delayAvg | year |
|:------|:-----|:--------|-------:|----------:|---------:|-----:|
| LHR   | ORD  |  AA     |   2490 |     63.33 |  21.11   | 2010 |
| LHR   | ORD  |  BA     |   1413 |     57.36 |  23.30   | 2010 |
| LHR   | ORD  |  UA     |   2105 |     73.24 |  14.57   | 2010 |
| LHR   | ORD  |  VS     |    218 |     77.06 |  11.10   | 2010 |
| ...   | ...  |  ...    |  ...   |     ...   |   ...    |  ... |
| LHR   | IAD  |  US     |   2134 |     82.05 |  13.24   | 2016 |
| LHR   | IAD  |  VS     |    699 |     84.69 |   8.02   | 2016 |
| LCY   | JFK  |  BA     |    921 |     90.01 |   5.26   | 2016 |
| LTN   | EWR  |  DJT    |    333 |     87.05 |   8.44   | 2016 |

Metadata
- ファイル名: `flights.csv`
- 観測数 `(n)`: 157
- 特徴 `(p)`  : 7
  - `source`  : 出発地の IATA 空港コード
  - `dest`    : 到着地の IATA 空港コード
  - `airline` : 航空会社の 2 文字 IATA コード
  - `flights` : その年のフライト本数
  - `onTimePerf` : そのルートにおける定時運航率（%）
  - `delayAvg`: そのルート・航空会社における平均遅延時間（分）
  - `year`    : データの年
- 出典: ロンドン民間航空局（London Civil Aviation Authority）のフライト定時運航統計をもとに作成

```vis
data(london.csv) 
filter(datum.year == 2016)
rect(x=source:N, y=dest:N, color=sum(flights):Q)
```

## Notes

このデータセットは、2016年にインドで実施された 500ルピー紙幣と 1000ルピー紙幣の高額紙幣廃止（デノミネーション）をきっかけに作られたものです。

| year    | type   |  denom |  value |   money | number |
|--------:|:-------|-------:|-------:|--------:|-------:|
| 1977    | Notes  |   0001 |      1 |    2.72 |  2.720 |
| 1977    | Notes  |   1000 |   1000 |    0.55 |  0.001 |
| 1977    | Notes  |   0002 |      2 |    1.48 |  0.740 |
| 1977    | Notes  |   0050 |     50 |    9.95 |  0.199 |
| ...     | ...    |    ... |    ... |     ... |    ... |
| 2015    | Notes  |   0500 |    500 | 7853.75 | 15.708 |
| 2015    | Notes  |   0001 |      1 |    3.09 |  3.090 |
| 2015    | Notes  |   0010 |     10 |  320.15 | 32.015 |
| 2015    | Notes  |   1000 |   1000 | 6325.68 |  6.326 |

Metadata
- ファイル名: `notes.csv`  
- 観測数 `(n)`: 351
- 特徴 `(p)`    : 6
  - `year`  : 流通した年
  - `type`  : 通貨の種類
  - `denom` : 額面金額（面額）
  - `value` : 通貨の額面価値
  - `money` : 流通している通貨の金額（単位：INR 十億）
  - `number`: 流通している通貨の枚数（単位：INR 十億）
- 出典: このデータセットはインド準備銀行（Reserve Bank of India）の *Handbook of Statistics on Indian Economy 2016* に基づきます。特に Table 160「Notes and Coins in Circulation」で扱われているデータのうち、紙幣（Notes）に関する部分のみを使用しています。  
  https://www.rbi.org.in/scripts/PublicationsView.aspx?id=17293

```vis
data(data/notes.csv) 
filter(datum.year == 2015)
bar(x=denom:N, y=money:Q, color=denom:N)
```


