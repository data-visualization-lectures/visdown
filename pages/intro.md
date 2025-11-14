# Visdown

**マークダウンだけで可視化を作る**

コードを書くように、シンプルな宣言的マークアップを使って可視化を書きます。三つのバッククォートで囲み、言語として `vis` を指定するだけです。

*シンプルな静的可視化を作る*


```vis
data:
  url: data/cars.csv
mark: point
encoding: 
  x: 
    field: kmpl
    type: quantitative
  y: 
    field: price
    type: quantitative
```

Visdown は、対話型グラフィックの文法（Vega-Lite）に基づいており、可視化を宣言的な方法で記述することを可能にします。これにより、インタラクションを含むビジュアライゼーション全体を宣言的に指定できます。

*インタラクティブな可視化を作る*

マウスで円を選択します

```vis
data:
  url: "data/cars.csv"
mark: circle
selection:
  brush:
    type: interval
encoding:
  x:
    type: quantitative
    field: kmpl
    scale:
     domain: [12,25]
  y:
    type: quantitative
    field: price
    scale:
     domain: [100,900]
  color:
    condition:
      selection: brush
      field: type
      type: nominal
    value: grey
  size:
    type: quantitative
    field: bhp
width: 450
height: 300
```

---
Handcrafted by [Amit Kapoor](http://amitkaps.com)
