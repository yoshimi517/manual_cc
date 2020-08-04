# Markdown 書式のヘルプ


## 1. 見出しの書き方と運用ルール

# h1 ドキュメントタイトル
## h2 チャプター
### h3 セクション
#### h4 パート
##### h5 トピック → 非推奨、下記、リストなどをつかってください。

## 2. リスト

### 2-1. 番号付きリスト

1. リスト
    1. リスト
    1. リスト
1. リスト

### 2-2. 番号なしリスト

- リスト
    - リスト
    - リスト
        - リスト
    - リスト
- リスト

### 2-3. 組み合わせ

1. リスト  
    - リスト  
    - リスト  
1. リスト  


## 3. ヒントタグ

{% hint style='info' %}
チェックポイント: 情報です。
{% endhint %}

{% hint style='tip' %}
お役立ち情報: こんなことができます！
{% endhint %}

{% hint style='danger' %}
警告: 呼損するぜ
{% endhint %}

{% hint style='working' %}
working: 作業中、あとで編集するぜ
{% endhint %}

## 4. 画像の挿入
![サンプル画像](..\images/image_sample.png)  
キャプションと画像番号は自動採番

## 5. 表
表のキャプションと番号を採番する方法がない。。

### 5-1. Markdown 書式

| デフォルト | 左寄せ | 右寄せ | センター
|-|:---|---:|:------:|
| ○ | ○ | ○ | ○ |
| × | × | × | × |

セルのアライメントは、コロンの付け方で調整する。  

### 5-2. csv 形式（直接入力）

{% includeCsv useHeader="true" %}
c1,c2,c3
1,1,1
2,2,2
{% endincludeCsv %}

### 5-3. csv 形式（ファイルインポート）
{% includeCsv src="./user.csv", encoding="shift_jis", useHeader="true" %}
{% endincludeCsv %}

## 6. 数式

$$ e^{j\theta} = \cos(\theta) + j\sin(\theta) $$  

$$f(x) = sin(x) +12$$

$$f(x) = \frac{a_0}{2} + \sum_{n = 1}^{\infty} a_n \cos nx + b_n \sin nx$$

## 7. UML

### 7-1. アクティビティ図

```plantuml
@startuml

skinparam {
  shadowing false
  defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
  BackgroundColor #afeeee
  ArrowColor black
}

skinparam activity  {
  BorderColor #000000
  DiamondBorderColor #008000
  BackgroundColor #ffffff
}
title アクティビティ図.1 [OA 自動ログイン判定]\n

start
:OperatorAgent 起動;
if (内線番号情報が不要) then
  -[#blue]-> 　Yes ： 不要;
else
  -[#red]-> No ： 不要ではない;
  if (内線番号必須) then
    -[#blue]-> Yes;
    if (内線番号入力済) then
      -[#blue]-> Yes;
    else
      -[#red]-> \nNo ： 未入力;
      :ログインダイアログ表示;
      end
    endif
  else
    -[#red]-> RR がローカルで動いていない場合に必要;
    if (サーバ認識構成) then
    -[#blue]-> \nYes;
      if (内線番号入力済) then
        -[#blue]-> Yes ： 入力済;
      else
        -[#red]-> \nNo ： 未入力;
        :ログインダイアログ表示;
        end
      endif
    else
      -[#red]-> \nNo ： クライアント\n認識構成;
    endif
  endif
endif
if (\nユーザIDとパスワードの両方が\n自動入力されている\n) then
  -[#blue]-> \nYes;
  if (自動ログインの設定は有効か？) then
    -[#blue]-> \nYes;
  else
    -[#red]-> \nNo;
    :ログインダイアログ表示;
    end
  endif
else
  -[#red]-> No : いずれかもしくは両方が未入力;
  if (\nコマンドライン実行(※) で、引数により\nユーザIDとパスワードが設定されている\n) then
    -[#blue]-> Yes;
    if (自動ログインの設定は有効か？) then
      -[#blue]-> Yes;
    else
      -[#red]-> \n No ： 無効;
      :ログインダイアログ表示;
      end
    endif
  else
    -[#red]-> \n No ： 無効;
    :ログインダイアログ表示;
    end
  endif
endif
#dbff00:自動ログイン実行;
floating note right: ※ コマンドライン引数については \n 1-2-6. コマンドラインからの OperatorAgent 操作 \nを参照して下さい。
@enduml
```

### 7-2. シーケンス図

```plantuml
@startuml
autonumber "00"

skinparam {
	shadowing false
	defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
	BackgroundColor #afeeee
	ParticipantBorderColor black
	LifeLineBorderColor black
	SequenceLifeLineBorderColor black
	ArrowColor black
	ActorBorderColor black
}

title シーケンス図.1 [座席モジュール Comet による非同期通信]\n

participant "座席モジュール\n内線番号 : 1000" as 1000
participant "StreamingRecognizer" as sr
participant "ControlCenter" as cc

1000 -[#red]>> cc ++ : モニタ開始要求
cc <-] : 通話開始\n（内線番号 1000）
1000 <<-[#red]- cc : 状態変更通知 <b>[通話開始]
1000 -> 1000 : 画面描画 <b>[通話開始]
1000 -[#blue]>> sr ++ : モニタリングテキスト要求

loop 音声が終わるまで
	sr -> sr : テキスト化
	1000 <<-[#blue]- sr : 認識結果通知
	1000 -> 1000 : 画面描画 <b>[認識結果]
end
cc <-] : 通話終了\n（内線番号 1000）
1000 <<-[#red]- cc : 状態変更通知 <b>[通話終了]
1000 -> 1000 : 画面描画 <b>[通話終了]
deactivate sr

@enduml
```

## 8. グラフ

{% graph %}
    {
        "title":"cos(2*PI*x/2)*(1+0.5cos(2*PI*x/100))",     
        "grid":true,
        "xAxis": {
            "label":"Sample",
            "domain": [0,300]
        },
        "yAxis": {
            "label":"Amplitude",
            "domain": [-1.5,1.5]
        },
        "data": [
            { "fn": "cos(2*PI*x/2)*(1+0.5cos(2*PI*x/100))"},         
            { "fn": "(1+0.5cos(2*PI*x/100))"}
        ]
    }
{% endgraph %}

## 9. コードブロック

```
import math  
print(math.pi)  
```  

```
abcdefg  
ああああああ  
```

## 10. 作業者

1. さかまき@maru9makky
1. しろた@t-shirota
1. ごうど
1. 担当者
1. 担当者
1. 担当者
1. 担当者
