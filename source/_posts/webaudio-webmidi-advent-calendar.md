---
title: WebAudioの基本機能でエフェクターを作ってみる
date: 2016-12-10 23:03:51
tags:
---

この記事は[WebAudio Web MIDI API Advent Calendar 2016](http://qiita.com/advent-calendar/2016/webaudio)の10日目です。

今回は[Web Audio API | Codelab](https://webmusicdevelopers.appspot.com/codelabs/webaudio/index.html)の内容を少しだけいじってエフェクターを作ってみたいと思います。
この半年ほどでWeb Audio APIの勉強会やハッカソン・ハンズオンなどに参加してきましたが、「音が鳴って楽しい！」「なんかいろいろできそう！」といったポジティブな意見を聞く反面、初心者には少し敷居が高い部分もあると感じています。
これは

- 音楽の知識諸々が必要（楽器のことから音の波形とか信号制御といったことまで）
- ノードグラフがピンとこないと何を実装すればいいか見えてこない

の2つが大きな原因であると思っています。
そこで、先のCodelabで作れるものから少しだけいじって、ノードグラフに何を足せば、音にどのような変化が出るのかといったことを実感してみます。

## 今回作るもの
---
エフェクターと一言で言っても本当にいろいろ種類があるので、今回は

- Peak Filter
- Flanger

の2種類のみを作っていきます。
この2つを選んだ理由としては、

- Peak Filterは`BiquadFilter`だけで簡単に実装できるのに、DJっぽいエフェクトができて楽しい
- FlangerはCodelabで実装するディレイを改造すれば作れる

からです。
また、今回の内容は先日の[Meguro.es](https://meguro.es/)なる勉強会で発表したものの使い回しです。
その時はPeak Filterとは、Flangerとはなんぞや、という部分に焦点を当てたので、本記事ではその実装部分を見ていきます。
そのため、この2つのエフェクターが何であるかについては、[当日の資料](https://speakerdeck.com/hirotan/party-night-with-webaudio-api)を参考にしていただきたいです。

## Peak Filter
---
Peak FilterはWeb Audio APIの`BiquadFilter`を使うだけで実装できます。
`BiquadFilter`は特定の周波数より大きい（小さい）部分をカットする、特定の周波数より大きい（小さい）部分を増幅させる、などの全8種類の機能がありますが、その中のピーキングフィルターを使います。
これは特定の周波数の部分を増幅させるフィルターです。
音源に対してフィルターのノードを1つつけるだけなので非常に単純です。
```
<body>
<input type="range" min="100" max="10000" id="freq" size="10" value="5000" oninput="ChangeFrequency()"/>
</body>
<script>
var audioctx = new AudioContext();
var filter = audioctx.createBiquadFilter();
var src = audioctx.createBufferSource();
var buffer = null;

LoadSample(audioctx, "path/to/your/audio/file");
src.buffer = buffer;
src.connect(filter);
filter.connect(audioctx.destination);
src.start(0);

function ChangeFrequency() {
  filter.gain.value = 50.0;
  filter.frequency.value = parseFloat(document.getElementById("freq").value);
}
document.onmouseup = function (event) {
  filter.gain.value = 0;
}
</script>
```
LoadSampleは音楽ファイルを読み込むための関数ですが、この実装はCodelabを参照してください。
スライダーの部分は昨日紹介されていたWebAudio-Controlsを使うとそれっぽくなります。

## Flanger
---
Flangerの実装はCodelabで作った[ディレイを適用する](https://webmusicdevelopers.appspot.com/codelabs/webaudio/index.html?ja-jp#6)と[オシレータを揺らしてみる](https://webmusicdevelopers.appspot.com/codelabs/webaudio/index.html?ja-jp#4)の合わせ技となります。
再生部分やパラメーターの設定部分はそのまま使いまわせます。
以下のコードも重複している部分が多々ありますが、ノードグラフの部分は載せたかったのでご容赦ください。
```
<body>
<table>
  <tr><td>Bypass :</td><td><input id="bypass" type="checkbox"/></td></tr>
  <tr><td>LFO Freq : </td><td><input type="text" size="10" id="lfofreq" value="5"/></td></tr>
  <tr><td>Depth : </td><td><input type="text" size="10" id="depth" value="0.5"/></td></tr>
  <tr><td>Time : </td><td><input type="text" size="8" id="time" value="0.005"/></td></tr>
  <tr><td>Feedback : </td><td><input type="text" size="8" id="feedback" value="0.4"/></td></tr>
  <tr><td>Mix : </td><td><input type="text" size="8" id="mix" value="0.4"/></td></tr>
</table>
</body>
<script>
var audioctx = new AudioContext();

var buffer = null;
var src = audioctx.createBufferSource();
var input = audioctx.createGain();
var delay = audioctx.createDelay();
var wetgain = audioctx.createGain();
var drygain = audioctx.createGain();
var feedback = audioctx.createGain();
var lfo = audioctx.createOscillator();
var depth = audioctx.createGain();

input.connect(delay);
input.connect(drygain);
delay.connect(wetgain);
delay.connect(feedback);
feedback.connect(delay);
wetgain.connect(filter);
drygain.connect(filter);
lfo.connect(depth);
depth.connect(delay.delayTime);

src.buffer = buffer;
src.connect(input);
src.start(0);
lfo.start(0);

document.onkeydown = function (event) {
  if (event.keyCode==70) {
    lfo.frequency.value = parseFloat(document.getElementById("lfofreq").value);
    depthRate = parseFloat(document.getElementById("depth").value);
    wetgain.gain.value = mix;
    drygain.gain.value = 1 - mix;
    depth.gain.value = delay.delayTime.value * depthRate;
  }
}
document.onkeyup = function (event) {
  if (event.keyCode==70) {
    wetgain.gain.value = 0;
    drygain.gain.value = 1;
    depth.gain.value = 0;
  }
}
</script>
```
flangerなのでfのキーを押したらエフェクトがかかるようになっています。
[オシレータを揺らしてみる](https://webmusicdevelopers.appspot.com/codelabs/webaudio/index.html?ja-jp#4)ではオシレーターの`frequency`に`depth`を繋いでいたのですが、flangerではディレイノードの`delayTime`に繋いでいるのがポイントです。
ちなみに綺麗にパラメーターをセットするとジェット機のような音が音源に重なって聞こえるそうですが、どうやれば綺麗にかかるのかは勉強不足でわかりませんでした…

## さいごに
---
Web Audioちょっと触ったことがある人なら理解に苦しむところはないと思います。
音楽の知識がないと何やってるのかわかりにくいかもしれませんが、僕もコードを書きながら音がこんな風に変わるんだろうなぁと明確にわかっているわけではありません。
今回も実装よりもパラメーターの設定の方が時間使ったんじゃないかと思うくらいです。
簡単なものから書いてみて、実際にどんな効果がかかるのかを聞いてみて、Web Audioに興味を持ってもらえたらと思います。
