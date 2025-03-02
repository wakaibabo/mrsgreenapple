<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html lang="ja">
<head>
<meta http-equiv="Content-Style-Type" content="text/css">
<meta http-equiv="Content-Script-Type" content="text/javascript">
<title>미세스 그린애플 노래 소트</title>
<script type="text/javascript">
<!--
//*********************************************************
//
// ?価するメンバ?の名前のリスト
//
// この部分を変更して下さい。名前の削除・追加も可?です。
// 名前を引用符(")で括り、コン?(,)で区切って下さい。
// 但し、リストの最後にはコン?を入れてはいけません。
//
//*********************************************************
var namMember = new Array(

"<br>ダーリン</br>",
"<br>ビターバカンス</br>",
"<br>The White Lounge</br>",
"<br>familie</br>",
"<br>アポロドロス</br>",
"<br>コロンブス</br>",
"<br>Dear</br>",
"<br>ライラック</br>",
"<br>ナハトムジーク</br>",
"<br>あなたに</br>",
"<br>norn</br>",
"<br>橙</br>",
"<br>アンラブレス</br>",
"<br>Loneliness</br>",
"<br>Doodle</br>",
"<br>BFF</br>",
"<br>Feeling</br>",
"<br>Blizzard</br>",
"<br>ANTENNA</br>",
"<br>Magic</br>",
"<br>ケセラセラ</br>",
"<br>フロリジナル</br>",
"<br>私は最強</br>",
"<br>Soranji</br>",
"<br>Part of me</br>",
"<br>君を知らない</br>",
"<br>延々</br>",
"<br>ブルーアンビエンス (feat.asmi)</br>",
"<br>ダンスホール</br>",
"<br>ニュー・マイ・ノーマル</br>",
"<br>PRESENT(Japanese ver.)</br>",
"<br>PRESENT [English ver.]</br>",
"<br>Attitude</br>",
"<br>Viking</br>",
"<br>クダリ</br>",
"<br>Ke-Mo Sah-Bee</br>",
"<br>嘘じゃないよ</br>",
"<br>Soup</br>",
"<br>Circle</br>",
"<br>CHEERS</br>",
"<br>lovin'</br>",
"<br>インフェルノ</br>",
"<br>月とアネモネ</br>",
"<br>How-to</br>",
"<br>ロマンチシズム</br>",
"<br>灯火</br>",
"<br>Folktale</br>",
"<br>点描の唄</br>",
"<br>ア・プリオリ</br>",
"<br>青と夏</br>",
"<br>Love me, Love you</br>",
"<br>アウフヘーベン</br>",
"<br>はじまり feat. キヨサク</br>",
"<br>They are</br>",
"<br>SPLASH!!!</br>",
"<br>REVERSE</br>",
"<br>Coffee</br>",
"<br>どこかで日は昇る</br>",
"<br>PARTY</br>",
"<br>春愁</br>",
"<br>Log</br>",
"<br>WanteD! WanteD!(KERENMI Remix)</br>",
"<br>WanteD! WanteD!</br>",
"<br>WHOO WHOO WHOO</br>",
"<br>光のうた</br>",
"<br>スマイロブドリーマ</br>",
"<br>SwitCh</br>",
"<br>umbrella</br>",
"<br>絶世生物</br>",
"<br>Lion</br>",
"<br>おもちゃの兵隊</br>",
"<br>soFt-dRink</br>",
"<br>鯨の唄</br>",
"<br>うブ</br>",
"<br>Oz</br>",
"<br>Just a Friend</br>",
"<br>FACTORY</br>",
"<br>JOURNEY</br>",
"<br>ツキマシテハ</br>",
"<br>サママ・フェスティバル!</br>",
"<br>In the Morning</br>",
"<br>ノニサクウタ</br>",
"<br>庶幾の唄</br>",
"<br>HeLLo</br>",
"<br>Hug</br>",
"<br>SimPle</br>",
"<br>ミスカサズ</br>",
"<br>No.7</br>",
"<br>私</br>",
"<br>キコリ時計</br>",
"<br>藍(あお)</br>",
"<br>パブリック</br>",
"<br>愛情と矛先</br>",
"<br>えほん</br>",
"<br>恋と吟(うた)</br>",
"<br>Speaking</br>",
"<br>道徳と皿</br>",
"<br>ゼンマイ</br>",
"<br>VIP</br>",
"<br>L.P</br>",
"<br>リスキーゲーム</br>",
"<br>StaRt</br>",
"<br>WaLL FloWeR</br>",
"<br>日々と君</br>",
"<br>アンゼンパイ</br>",
"<br>CONFLICT</br>",
"<br>ナニヲナニヲ</br>",
"<br>我逢人</br>",
"<br>スターダム</br>",
"<br>アボイドノート</br>",
"<br>Theater</br>",
"<br>僕のこと</br>"

);
//*********************************************************

var lstMember = new Array();
var parent = new Array();
var equal = new Array();
var rec = new Array();
var cmp1,cmp2;
var head1,head2;
var nrec;

var numQuestion;
var totalSize;
var finishSize;
var finishFlag;

//変数の初期化+++++++++++++++++++++++++++++++++++++++++++++
function initList(){
var n = 0;
var mid;
var i;

//??トすべき配列
lstMember[n] = new Array();
for (i=0; i<namMember.length; i++) {
lstMember[n][i] = i;
}
parent[n] = -1;
totalSize = 0;
n++;

for (i=0; i<lstMember.length; i++) {
//要素数が２以上なら２分割し、
//分割された配列をlstMemberの最後に加える
if(lstMember[i].length>=2) {
mid = Math.ceil(lstMember[i].length/2);
lstMember[n] = new Array();
lstMember[n] = lstMember[i].slice(0,mid);
totalSize += lstMember[n].length;
parent[n] = i;
n++;
lstMember[n] = new Array();
lstMember[n] = lstMember[i].slice(mid,lstMember[i].length);
totalSize += lstMember[n].length;
parent[n] = i;
n++;
}
}

//保存用配列
for (i=0; i<namMember.length; i++) {
rec[i] = 0;
}
nrec = 0;

//引き分けの結果を保存するリスト
//キ?：リンク始?の値
// 値 ：リンク終?の値
for (i=0; i<=namMember.length; i++) {
equal[i] = -1;
}

cmp1 = lstMember.length-2;
cmp2 = lstMember.length-1;
head1 = 0;
head2 = 0;
numQuestion = 1;
finishSize = 0;
finishFlag = 0;
}

//リストの??ト+++++++++++++++++++++++++++++++++++++++++++
//flag：比較結果
//  -1：左を選択
//   0：引き分け
//   1：右を選択
function sortList(flag){
var i;
var str;

//recに保存
if (flag<0) {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
}
}
else if (flag>0) {
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
}
}
else {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
}
equal[rec[nrec-1]] = lstMember[cmp2][head2];
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
}
}

//片方のリストを走査し終えた後の処理
if (head1<lstMember[cmp1].length && head2==lstMember[cmp2].length) {
//リストcmp2が走査済 - リストcmp1の残りをコピ?
while (head1<lstMember[cmp1].length){
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
}
}
else if (head1==lstMember[cmp1].length && head2<lstMember[cmp2].length) {
//リストcmp1が走査済 - リストcmp2の残りをコピ?
while (head2<lstMember[cmp2].length){
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
}
}

//両方のリストの最後に到達した場合は
//親リストを更新する
if (head1==lstMember[cmp1].length && head2==lstMember[cmp2].length) {
for (i=0; i<lstMember[cmp1].length+lstMember[cmp2].length; i++) {
lstMember[parent[cmp1]][i] = rec[i];
}
lstMember.pop();
lstMember.pop();
cmp1 = cmp1-2;
cmp2 = cmp2-2;
head1 = 0;
head2 = 0;

//新しい比較を行う前にrecを初期化
if (head1==0 && head2==0) {
for (i=0; i<namMember.length; i++) {
rec[i] = 0;
}
nrec = 0;
}
}

if (cmp1<0) {
str = "Battle No."+(numQuestion-1)+"<br>"+Math.floor(finishSize*100/totalSize)+"% sorted.";
document.getElementById("battleNumber").innerHTML = str;

showResult();
finishFlag = 1;
}
else {
showImage();
}
}

//結果の?示+++++++++++++++++++++++++++++++++++++++++++++++
function showResult() {
var ranking = 1;
var sameRank = 1;
var str = "";
var i;

str += "<table style=\"width:200px; font-size:12px; line-height:120%; margin-left:auto; margin-right:auto; border:1px solid #000; border-collapse:collapse\" align=\"center\">";
str += "<tr><td style=\"color:#ffffff; background-color:#000; text-align:center;\">순위<\/td><td style=\"color:#ffffff; background-color:#000; text-align:center;\">이름<\/td><\/tr>";

for (i=0; i<namMember.length; i++) {
str += "<tr><td style=\"border:1px solid #000; text-align:right; padding-right:5px;\">"+ranking+"<\/td><td style=\"border:1px solid #000; padding-left:5px;\">"+namMember[lstMember[0][i]]+"<\/td><\/tr>";
if (i<namMember.length-1) {
if (equal[lstMember[0][i]]==lstMember[0][i+1]) {
sameRank++;
} else {
ranking += sameRank;
sameRank = 1;
}
}
}
str += "<\/table>";

document.getElementById("resultField").innerHTML = str;
}

//比較する２つ要素の?示+++++++++++++++++++++++++++++++++++
function showImage() {
var str0 = "Battle No."+numQuestion+"<br>"+Math.floor(finishSize*100/totalSize)+"% sorted.";
var str1 = ""+toNameFace(lstMember[cmp1][head1]);
var str2 = ""+toNameFace(lstMember[cmp2][head2]);

document.getElementById("battleNumber").innerHTML = str0;
document.getElementById("leftField").innerHTML = str1;
document.getElementById("rightField").innerHTML = str2;

numQuestion++;
}

//数値を名前（顔文字）に変換+++++++++++++++++++++++++++++++
function toNameFace(n){
var str = namMember[n];

//顔文字を追加する場合は以下のコメントアウトを外す
//namMemberのインデックスと矛盾しないように注意
/*
str += "<br>────<br>";
switch(n) {
//case -1 はサンプルなので削除すること
case -1: str+="（ ´∀｀）";break;
default: str+=""+n;
}
*/
return str;
}
//-->
</script>
<style type="text/css">
<!--
/**********************************************************

 ?のス?イルを変更する場合はここを編集してください。

**********************************************************/
#mainTable{
font-size: 12px;
font-family: '돋움',sans-serif;
text-align: center;
vertical-align: middle;
width: 410px;
margin-left: auto;
margin-right: auto;
border-collapse: separate;
border-spacing: 10px 5px;
}
#leftField{
width: 120px;
height: 150px;
border: 1px solid #000;
}
#rightField{
width: 120px;
height: 150px;
border: 1px solid #000;
}
.middleField{
width: 120px;
height: 70px;
border: 1px solid #000;
}
//-->
<!--
A{
  text-decoration : none;
}
-->
<!--
a:hover{color:#99ccff;}
-->
</style>
<meta name="generator" content="Namo WebEditor(Trial)">
<meta http-equiv="content-type" content="text/html; charset=utf-8"></head>

<body text="#000000" bgcolor="#ffffff" link="#0099ff" vlink="#0099ff" alink="#0099ff">
<table id="mainTable" align="center">
<tr>
        <td id="battleNumber" colspan="3" style="padding-bottom: 10px;">
            <p>&nbsp;</p>
        </td>
</tr>
<tr>
<td id="leftField" onClick="if(finishFlag==0)sortList(-1);" rowspan="2">
&nbsp;
</td>
<td class="middleField" onClick="if(finishFlag==0)sortList(0);">
둘 다 좋다
</td>
<td id="rightField" onClick="if(finishFlag==0)sortList(1);" rowspan="2">
</td>
</tr>
<tr>
<td class="middleField" onClick="if(finishFlag==0)sortList(0);">
모르겠다
</td>
</tr>
</table><br><br>
<div id="resultField" style="text-align:center;">
    <p><font size="2" face="돋움"><span style="">제일 좋아하는 미세스 노래를 골라주세요!</font></p>
    <p><font size="2" face="돋움">모든 문의는 트위터 @wakaibabo 로 주세요~</font></p>

</div>
<script type="text/javascript">
<!--
initList();
showImage();
//-->
</script>

</body>
</html>
