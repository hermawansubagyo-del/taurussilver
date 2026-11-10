# taurussilver
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Belajar Seru: Perkalian, Berat &amp; Panjang</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:"Trebuchet MS",system-ui,sans-serif;background:#fff8e7;color:#2b2b3a;font-size:18px}
main{max-width:720px;margin:0 auto;padding:14px}
h1{text-align:center;font-size:1.5rem;margin:6px 0 12px}
.tabs{display:flex;gap:8px;margin-bottom:12px}
.tabs button{flex:1;padding:12px 2px;font-size:.85rem;font-weight:bold;border:3px solid #2b2b3a;border-radius:14px;background:#fff;cursor:pointer}
.tabs button.on{background:#ffcf4a}
.card{background:#fff;border:3px solid #2b2b3a;border-radius:18px;padding:14px;margin-bottom:12px}
.modes{display:flex;gap:8px;margin-bottom:10px}
.btn{font-family:inherit;font-size:1rem;font-weight:bold;padding:10px 14px;border:3px solid #2b2b3a;border-radius:12px;background:#bde7ff;cursor:pointer;min-height:46px}
.btn.on{background:#7ed99b}
.btn.go{background:#7ed99b}
.nums{display:flex;flex-wrap:wrap;gap:6px;margin:8px 0}
.nums .btn{min-width:46px;padding:8px}
.big{font-size:2rem;text-align:center;font-weight:bold;margin:8px 0}
.dots{display:flex;flex-wrap:wrap;gap:8px;justify-content:center}
.grp{border:3px dashed #e67e22;border-radius:12px;padding:6px;font-size:1.3rem;line-height:1.2;max-width:150px;text-align:center}
.opts{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:10px}
.opts .btn{font-size:1.5rem;background:#fff}
.msg{min-height:2em;text-align:center;font-weight:bold;font-size:1.1rem}
.ok{color:#1b8a3c}.no{color:#c0392b}
.score{text-align:center;font-size:1.2rem}
input[type=range]{width:100%;height:36px;accent-color:#e67e22}
input.ans{font-size:1.6rem;width:140px;padding:8px;border:3px solid #2b2b3a;border-radius:12px;text-align:center}
.blk{display:inline-block;width:70px;height:70px;border:3px solid #2b2b3a;border-radius:12px;margin:4px;font-size:.8rem;font-weight:bold;padding-top:14px;text-align:center}
.cmp{display:flex;justify-content:space-between;padding:6px 0;border-top:2px dotted #ccc}
.ruler{height:34px;border:3px solid #2b2b3a;border-radius:6px;background:#ffe9a8;position:relative;overflow:hidden}
.ruler i{position:absolute;top:0;bottom:0;background:#ffb347;border-right:3px solid #2b2b3a;transition:width .3s}
@keyframes pop{0%{transform:scale(0)}70%{transform:scale(1.3)}100%{transform:scale(1)}}
@keyframes shake{25%{transform:translateX(-10px)}75%{transform:translateX(10px)}}
@keyframes up{0%{opacity:1;transform:translateY(0) scale(1)}100%{opacity:0;transform:translateY(-160px) scale(1.6)}}
.it{display:inline-block;animation:pop .45s both}
.shake{animation:shake .4s}
.conf{position:fixed;pointer-events:none;font-size:2rem;animation:up 1.3s forwards;z-index:9}
.grp{transition:opacity .3s}
.hl{outline:5px solid #ffcf4a;background:#fff3b0}
.beam{width:240px;max-width:90%;height:12px;background:#2b2b3a;border-radius:6px;margin:34px auto 6px;transition:transform 1s cubic-bezier(.3,1.6,.5,1)}
.ruler i{display:block}
</style>
</head>
<body>
<main>
<h1>⭐ Belajar Seru ⭐</h1>
<div class="tabs" id="tabs"></div>
<div id="app"></div>
</main>
<script>
var $=function(i){return document.getElementById(i)};
var tab="kali",mode="belajar";
function R(a,b){return a+Math.floor(Math.random()*(b-a+1))}
function shuffle(a){return a.sort(function(){return Math.random()-.5})}

var tabs=[["kali","✖️ Kali"],["bagi","➗ Bagi"],["berat","⚖️ Berat"],["panjang","📏 Panjang"]];
function drawTabs(){
 $("tabs").innerHTML=tabs.map(function(t){return '<button class="'+(tab===t[0]?"on":"")+'" onclick="setTab(\''+t[0]+'\')">'+t[1]+'</button>'}).join("");
}
function setTab(t){tab=t;mode="belajar";render()}
function setMode(m){mode=m;render()}
function modes(){
 return '<div class="modes"><button class="btn '+(mode==="belajar"?"on":"")+'" onclick="setMode(\'belajar\')">📖 Belajar</button><button class="btn '+(mode==="kuis"?"on":"")+'" onclick="setMode(\'kuis\')">🎯 Kuis</button></div>';
}
function render(){clearInterval(anim);drawTabs();if(tab==="kali")mode==="belajar"?kaliLearn():kaliQuiz();else if(tab==="bagi")mode==="belajar"?bagiLearn():bagiQuiz();else mode==="belajar"?unitLearn():unitQuiz()}

/* ---------- PEMBAGIAN ---------- */
var bk=3,bq=4,anim;
function fx(ok){
 if(ok){for(var i=0;i<14;i++){var e=document.createElement("div");e.className="conf";e.textContent=["⭐","🎉","🌟","✨"][i%4];e.style.left=R(5,90)+"%";e.style.top=R(40,75)+"%";e.style.animationDelay=(i*.04)+"s";document.body.appendChild(e);setTimeout(function(x){return function(){x.remove()}}(e),1600)}}
 else{var b=document.querySelector(".big");if(b){b.classList.remove("shake");void b.offsetWidth;b.classList.add("shake")}}
}
function countAnim(){
 clearInterval(anim);
 var gs=document.querySelectorAll(".grp"),r=$("run"),i=0,s=0;
 gs.forEach(function(g){g.style.opacity=.25;g.classList.remove("hl")});r.textContent="";
 anim=setInterval(function(){
  if(i>=gs.length){clearInterval(anim);r.textContent="Jadi semuanya "+s+" 🎉";fx(true);return}
  gs[i].style.opacity=1;gs[i].classList.add("hl");s+=kn;i++;
  r.textContent="Kelompok ke-"+i+": total "+s;
 },800);
}
function shareAnim(){
 clearInterval(anim);
 var ch=document.querySelectorAll(".grp"),pile=$("pile"),r=$("run"),tot=bk*bq,n=0;
 ch.forEach(function(c){c.innerHTML="🧒<br>"});pile.innerHTML="";
 for(var i=0;i<tot;i++){var e=document.createElement("span");e.className="it";e.textContent="🍪";pile.appendChild(e)}
 anim=setInterval(function(){
  if(n>=tot){clearInterval(anim);r.innerHTML='<span class="ok">Semua anak dapat '+bq+' kue. Adil! 🎉</span>';fx(true);return}
  var c=ch[n%bk],e=document.createElement("span");e.className="it";e.textContent="🍪";c.appendChild(e);
  pile.removeChild(pile.lastChild);
  r.textContent="Kue ke-"+(n+1)+" untuk anak ke-"+(n%bk+1);n++;
 },350);
}
function bagiLearn(){
 var ks="",qs="",tot=bk*bq,g="";
 for(var i=1;i<=10;i++){ks+='<button class="btn '+(bk===i?"on":"")+'" onclick="bk='+i+';render()">'+i+'</button>';qs+='<button class="btn '+(bq===i?"on":"")+'" onclick="bq='+i+';render()">'+i+'</button>'}
 for(var j=0;j<bk;j++){var d="";for(var k=0;k<bq;k++)d+='<span class="it" style="animation-delay:'+(j*.15+k*.05)+'s">🍪</span>';g+='<div class="grp">🧒<br>'+d+'</div>'}
 $("app").innerHTML='<div class="card">'+modes()+
 '<div>Dibagi untuk berapa anak?</div><div class="nums">'+ks+'</div>'+
 '<div>Tiap anak dapat berapa kue?</div><div class="nums">'+qs+'</div>'+
 '<div class="big">'+tot+' kue dibagi rata ke '+bk+' anak</div>'+
 '<div style="text-align:center"><button class="btn go" onclick="shareAnim()">▶ Bagikan satu per satu</button></div><div class="dots" id="pile" style="min-height:44px;font-size:1.4rem"></div><div class="msg" id="run"></div>'+
 '<div class="dots">'+g+'</div>'+
 '<div class="big">'+tot+' ÷ '+bk+' = '+bq+'</div>'+
 '<p style="text-align:center">Pembagian adalah kebalikan perkalian:<br><b>'+bk+' × '+bq+' = '+tot+'</b> jadi <b>'+tot+' ÷ '+bk+' = '+bq+'</b> 🎉</p></div>';
}
var bqz=null;
function newB(){var k=R(1,10),q=R(1,10),c=q,o=[c];while(o.length<4){var w=c+R(-4,4);if(w>0&&o.indexOf(w)<0)o.push(w)}bqz={t:k*q,k:k,c:c,o:shuffle(o),done:false}}
function bagiQuiz(){
 if(!bqz)newB();
 $("app").innerHTML='<div class="card">'+modes()+
 '<div class="score">⭐ '+sc.s+' benar dari '+sc.t+' &nbsp; 🔥 beruntun: '+sc.st+'</div>'+
 '<div class="big">'+bqz.t+' ÷ '+bqz.k+' = ?</div>'+
 '<div class="opts">'+bqz.o.map(function(x){return '<button class="btn" onclick="ansB('+x+')">'+x+'</button>'}).join("")+'</div>'+
 '<div class="msg" id="msg"></div><div style="text-align:center"><button class="btn go" onclick="newB();render()">Soal berikutnya ➡️</button></div></div>';
}
function ansB(x){
 if(bqz.done)return;bqz.done=true;sc.t++;fx(x===bqz.c);
 if(x===bqz.c){sc.s++;sc.st++;$("msg").innerHTML='<span class="ok">Hebat! Benar! 🌟</span>'}
 else{sc.st=0;$("msg").innerHTML='<span class="no">Hampir! Jawabannya '+bqz.c+', karena '+bqz.k+' × '+bqz.c+' = '+bqz.t+' 💪</span>'}
 document.querySelector(".score").innerHTML='⭐ '+sc.s+' benar dari '+sc.t+' &nbsp; 🔥 beruntun: '+sc.st;
}

/* ---------- PERKALIAN ---------- */
var kn=3,kb=4,sc={s:0,t:0,st:0};
function kaliLearn(){
 var nums="",bs="";
 for(var i=1;i<=10;i++){nums+='<button class="btn '+(kn===i?"on":"")+'" onclick="kn='+i+';render()">'+i+'</button>';bs+='<button class="btn '+(kb===i?"on":"")+'" onclick="kb='+i+';render()">'+i+'</button>'}
 var g="",plus=[];
 for(var j=0;j<kb;j++){var d="";for(var k=0;k<kn;k++)d+='<span class="it" style="animation-delay:'+(j*.15+k*.05)+'s">🍎</span>';g+='<div class="grp">'+d+'</div>';plus.push(kn)}
 $("app").innerHTML='<div class="card">'+modes()+
 '<div>Pilih tabel (isi tiap kelompok):</div><div class="nums">'+nums+'</div>'+
 '<div>Berapa kelompok?</div><div class="nums">'+bs+'</div>'+
 '<div class="big">'+kb+' kelompok × '+kn+' = '+(kb*kn)+'</div>'+
 '<div class="big" style="font-size:1.2rem">'+plus.join(" + ")+' = '+(kb*kn)+'</div>'+
 '<div class="dots">'+g+'</div>'+
 '<div style="text-align:center"><button class="btn go" onclick="countAnim()">▶ Hitung bersama</button></div><div class="big" id="run" style="font-size:1.2rem"></div><p style="text-align:center">Perkalian itu penjumlahan berulang! 🎉</p></div>';
}
var kq=null;
function newK(){var a=R(1,10),b=R(1,10),c=a*b,o=[c];while(o.length<4){var w=c+R(-6,6);if(w>0&&o.indexOf(w)<0)o.push(w)}kq={a:a,b:b,c:c,o:shuffle(o),done:false}}
function kaliQuiz(){
 if(!kq)newK();
 $("app").innerHTML='<div class="card">'+modes()+
 '<div class="score">⭐ '+sc.s+' benar dari '+sc.t+' &nbsp; 🔥 beruntun: '+sc.st+'</div>'+
 '<div class="big">'+kq.a+' × '+kq.b+' = ?</div>'+
 '<div class="opts">'+kq.o.map(function(x){return '<button class="btn" onclick="ansK('+x+')">'+x+'</button>'}).join("")+'</div>'+
 '<div class="msg" id="msg"></div><div style="text-align:center"><button class="btn go" onclick="newK();render()">Soal berikutnya ➡️</button></div></div>';
}
function ansK(x){
 if(kq.done)return;kq.done=true;sc.t++;fx(x===kq.c);
 if(x===kq.c){sc.s++;sc.st++;$("msg").innerHTML='<span class="ok">Hebat! Benar! 🌟</span>'}
 else{sc.st=0;$("msg").innerHTML='<span class="no">Hampir! Jawabannya '+kq.c+'. Coba lagi ya 💪</span>'}
 document.querySelector(".score").innerHTML='⭐ '+sc.s+' benar dari '+sc.t+' &nbsp; 🔥 beruntun: '+sc.st;
}

/* ---------- SATUAN ---------- */
var U={
 berat:{big:"kg",small:"g",f:1000,icon:"🍚",name:"berat",cmp:[["🥚 Sebutir telur","± 60 g"],["🍎 Sebuah apel","± 200 g"],["🍚 Sekantong beras","1 kg"],["🎒 Tas sekolah","± 3 kg"]]},
 panjang:{big:"m",small:"cm",f:100,icon:"📏",name:"panjang",cmp:[["✏️ Sebatang pensil","± 15 cm"],["📐 Penggaris","30 cm"],["🪑 Tinggi meja","± 1 m"],["🚪 Tinggi pintu","± 2 m"]]}
};
var uv={berat:2,panjang:2};
function unitBody(){
 var u=U[tab],v=uv[tab],blocks="";
 for(var i=0;i<v;i++)blocks+='<span class="blk it" style="background:#bde7ff;animation-delay:'+(i*.1)+'s">1 '+u.big+'<br>'+u.f+' '+u.small+'</span>';
 var viz=tab==="berat"?'<div style="display:flex;justify-content:space-between;font-size:1.4rem"><span>'+u.icon.repeat(v)+' '+v+' kg</span><span>🎒 3 kg</span></div><div class="beam" id="bm"></div><p class="note" style="text-align:center">Timbangan miring ke sisi yang lebih berat!</p>':'<div class="ruler"><i id="rl" style="width:0;transition:width 1s"></i></div>';
 return '<div style="text-align:center">'+blocks+'</div><div class="big">'+v+' '+u.big+' = '+(v*u.f)+' '+u.small+'</div>'+viz+
 '<p style="text-align:center">Dari '+u.big+' ke '+u.small+': <b>kali '+u.f+'</b>.<br>Dari '+u.small+' ke '+u.big+': <b>bagi '+u.f+'</b>.</p>'+
 '<h3>Kira-kira sebesar apa?</h3>'+u.cmp.map(function(c){return '<div class="cmp"><span>'+c[0]+'</span><b>'+c[1]+'</b></div>'}).join("");
}
function unitLearn(){
 var u=U[tab];
 $("app").innerHTML='<div class="card">'+modes()+'<div class="big">1 '+u.big+' = '+u.f+' '+u.small+'</div><div>Geser untuk mengubah banyaknya '+u.big+':</div><input type="range" min="1" max="5" value="'+uv[tab]+'" oninput="uv[tab]=+this.value;unitUpd()"><div id="uc"></div></div>';
 unitUpd();
}
function unitUpd(){
 $("uc").innerHTML=unitBody();var v=uv[tab];
 setTimeout(function(){var b=$("bm"),r=$("rl");if(b)b.style.transform="rotate("+((3-v)*5)+"deg)";if(r)r.style.width=(v/5*100)+"%"},60);
}
var uq=null;
function newU(){var u=U[tab],n=R(1,9),toSmall=Math.random()<.6;uq=toSmall?{q:n+' '+u.big+' = ? '+u.small,a:n*u.f}:{q:(n*u.f)+' '+u.small+' = ? '+u.big,a:n}}
function unitQuiz(){
 newUIfNeeded();
 $("app").innerHTML='<div class="card">'+modes()+
 '<div class="score">⭐ '+sc.s+' benar dari '+sc.t+'</div>'+
 '<div class="big">'+uq.q+'</div>'+
 '<div style="text-align:center"><input class="ans" id="ans" type="number" inputmode="numeric"> <button class="btn go" onclick="ansU()">Periksa ✅</button></div>'+
 '<div class="msg" id="msg"></div>'+
 '<div style="text-align:center"><button class="btn" onclick="newU();unitQuiz()">Soal berikutnya ➡️</button></div></div>';
}
var uqTab=null;
function newUIfNeeded(){if(!uq||uqTab!==tab){newU();uqTab=tab}}
function ansU(){
 var x=parseFloat($("ans").value);if(isNaN(x))return;
 sc.t++;
 fx(x===uq.a);if(x===uq.a){sc.s++;$("msg").innerHTML='<span class="ok">Benar! Kamu pintar! 🌟</span>'}
 else{$("msg").innerHTML='<span class="no">Belum tepat. Ingat: kg→g dan m→cm dikali, kebalikannya dibagi. Jawaban: '+uq.a+'</span>'}
 document.querySelector(".score").innerHTML='⭐ '+sc.s+' benar dari '+sc.t;
}
render();
</script>
</body>
</html>
