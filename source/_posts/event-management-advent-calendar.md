---
title: WebAudio界隈とWebAudio.tokyo
date: 2016-12-15 20:00:00
tags:
---

この記事は[IT勉強会/コミュニティ運営 Advent Calendar 2016](http://qiita.com/advent-calendar/2016/event-management)の15日目です。

WebAudio.tokyoは今年の9月に第1回を迎えたばかりの勉強会です。
今回はどういった思いでWebAudio.tokyoというコミュニティを作り、今後どのようにWebAudio界隈と関わっていきたいかを書こうと思います。
始めたばかりの勉強会が他のコミュニティとどのように関わり、どういった助けを得ているかといった、これから勉強会やってみようという人向けの話になります。

## どのように始めたか
---
WebAudio.tokyoはWeb Audio APIのための勉強会です。
Web Audio APIとはブラウザ上で音声の信号処理を可能にするAPIで、`audio`タグとは違って音を鳴らすだけでなく、その場で音を生成したり音にエフェクトをかけたりといったことが可能です。
そのためWeb Audio APIの他にもWeb MIDI API, WebRTCなども組み合わせてシンセを作ろう、エフェクターを作ろうといった活動は活発で、[Web Music Developers JP](https://groups.google.com/forum/#!forum/web-music-developers-jp)という大きなコミュニティもすでに存在します。

そんな中で、Web Audio APIに特化して、Web Audio APIの新たな使い道を探っていきたいという気持ちで始めたのが、このWebAudio.tokyoです。

## WebAudio.tokyoとWeb Music Developers JP
---
WebAudio.tokyoのできる前、今年の7月に[Web Music ハッカソン #5](https://developers-jp.googleblog.com/2016/06/web-music-5.html)に参加しました。
これは先の[Web Music Developers JP](https://groups.google.com/forum/#!forum/web-music-developers-jp)が主催されたイベントで、Webと音楽をテーマにしたハッカソンです。
私自身、今年の春に初めてWeb Audio APIを触り、これがWeb Audio APIに関係するコミュニティへの初めての参加でした。
当日は実際にmidiキーボードなどの機材も用意され、Web Audio APIだけでなくその他のブラウザ技術も取り入れられた作品はどれも大変刺激的でした。
このハッカソンに参加したことで、音声の信号処理や波形のビジュアライズ、音楽をする上での時間の管理などWeb Audio APIの奥深さに触れ、Web Audio APIに特化したコミュニティを作ろうと思った大きなきっかけとなりました。

そして、WebAudio.tokyoの第1回から2ヶ月後、[Web Music Developers JP](https://groups.google.com/forum/#!forum/web-music-developers-jp)の代表である河合良哉さんが主催された[Web Audio API 初心者向けハンズオン](https://connpass.com/event/41470/)にメンターとして参加させていただきました。
ここでも[Web Music Developers JP](https://groups.google.com/forum/#!forum/web-music-developers-jp)の方々にお世話になった他、WebAudio.tokyoの#1, #2共にLTをして頂いたり、[Web Audio API 初心者向けハンズオン](https://connpass.com/event/41470/)からも次回#3にて初心者向けLTとして出て頂いたりと、技術面、運営面共に大きくお世話になっています。

## WebAudio.tokyoとJS勉強会
---
Web Audio APIもJavaScriptの技術の一つです。
そのため、JSのコミュニティでもWeb Audio APIの話題が上がることがあります。
私も[Meguro.es](https://meguro.es/2016/12/08/advent-calendar-2016/)の運営に携わっており、毎回Web Audio APIの話をしていますが、何回か繰り返して気づいたのがJS勉強会でWeb Audio APIの話をしても内容によってはよくわからない…といった空気になってしまうということです。
[Web Audio API 初心者向けハンズオン](https://connpass.com/event/41470/)でも感じたことですが、JSは書けても音声信号処理となると音楽、数学、ちょこっと物理あたりの知識も必要になり始め、専門性はかなり高くなります。
そこで、私が外のJS勉強会でWeb Audio APIの話をする際には、できるだけ音楽のことも説明するように心がけています。
たとえJSっぽい話が少なくなってしまっても、音楽の用語の説明に時間を割くこともあります。
幸い、見映え（聴映え？）のいいDEMOができるのがWeb Audio APIの強みでもあるので、説明した音楽がブラウザ上でできればそれだけでWeb Audio APIすごい！ とわかってもらえます。
そして、こうした勉強会でWeb Audio APIに興味を持ってもらえたら、WebAudio.tokyoに来て濃い話に花を咲かせてもらうといった魂胆です。
実際、参加したJS勉強会から参加してもらったり、JS界隈でコミュニティを運営している方にWebAudio.tokyoの運営を助けてもらったりもしています。

## ニッチなジャンルだからこその良さ
---
WebAudio.tokyoでは、このように実際に私が足を運んだイベントから来てもらう人が多いです。
その他にも、Web Audio APIに関するブログを書いている人にtwitterで連絡を取ることも多いです。
JS技術の中でも専門性が高く分野もニッチなので、毎回多くの人が集まるわけではありませんが、懇親会は濃い話で盛り上がります。
まだまだ大きく広げられていないので、見知った顔も多く内輪ネタのような話で盛り上がっている節もありますが、やはり既にできているコミュニティから顔を出してくださる方々の話は面白いです。
この界隈のコミュニティの数が多くないということもあり、まだ出来たばかりのコミュニティでもWeb Audio APIに強い方と交流できるのはニッチなジャンルの良さなのではないかと思います。

## WebAudio.tokyoとこれから
---
JS勉強会で専門性を薄めて話をしても、やはりWebAudio.tokyoがニッチな分野の濃い話をする場所であるという部分は変えたくないです。
WebAudio.tokyoがWeb Audio APIの新たな使い道を探る場であるためには、少人数でも深い話ができる場でありたいと思っています。
しかし、音楽に興味はあるけれど専門性が高くて手が出せないという層が一定数いるのもまた事実です。
[Web Audio API 初心者向けハンズオン](https://connpass.com/event/41470/)のようなイベントには引き続き協力していきたいし、そういった場を用意できるようにもなりたいと思っています。
そんな中で、WebAudio.tokyo #3では初心者向けLT枠を用意することにしました。
[Web Audio API 初心者向けハンズオン](https://connpass.com/event/41470/)の開催から2ヶ月と少し、ここでWeb Audio APIを触り始めた方々が何か出来たものを発表してくださればとても嬉しいです
（もちろん、このイベント以外で触り始めた方のご参加もお待ちしております）。

WebAudio.tokyoの始まりの話ということもあり自分の話が多くなってしまって恐縮ですが、これから勉強会をやってみたい人、始めたばかりの勉強会を運営している人の参考になれば幸いです。
