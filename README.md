# Neon-Dash
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<title>Neon Dash</title>

<style>
*{
  box-sizing:border-box;
  -webkit-tap-highlight-color:transparent;
}

html,body{
  margin:0;
  width:100%;
  height:100%;
  overflow:hidden;
  background:#03030a;
  color:white;
  font-family:Arial,sans-serif;
}

button{
  font:inherit;
  color:white;
  border:0;
  cursor:pointer;
  user-select:none;
  -webkit-user-select:none;
  touch-action:manipulation;
}

#menu{
  position:fixed;
  inset:0;
  overflow:auto;
  display:flex;
  flex-direction:column;
  align-items:center;
  padding:
    max(18px,env(safe-area-inset-top))
    14px
    max(30px,env(safe-area-inset-bottom));
  background:
    radial-gradient(circle at 50% 5%,#252b78,#090a20 45%,#020207);
}

.logo{
  margin:12px 0 4px;
  font-size:clamp(30px,7vw,54px);
  font-weight:900;
  letter-spacing:clamp(2px,1vw,6px);
  text-align:center;
  text-shadow:
    0 0 10px #00eaff,
    0 0 25px #00eaff,
    0 0 45px #a855ff;
  animation:pulse 1.8s infinite alternate;
}

@keyframes pulse{
  from{transform:scale(1)}
  to{transform:scale(1.035)}
}

.subtitle{
  text-align:center;
  opacity:.7;
  font-size:clamp(13px,3vw,17px);
  margin-bottom:18px;
}

.progress{
  width:min(680px,100%);
  background:#11152d;
  border:2px solid #303963;
  border-radius:17px;
  padding:15px;
  margin-bottom:15px;
}

.progressTop{
  display:flex;
  justify-content:space-between;
  gap:10px;
  font-weight:bold;
}

.bar{
  height:13px;
  background:#050712;
  border-radius:20px;
  overflow:hidden;
  margin-top:8px;
}

#menuBar{
  height:100%;
  width:0%;
  background:linear-gradient(90deg,#00eaff,#7b5cff,#ff27d7);
  box-shadow:0 0 14px #00eaff;
  transition:.4s;
}

#doneText{
  text-align:center;
  opacity:.65;
  margin-top:7px;
}

#levels{
  width:min(680px,100%);
  display:grid;
  grid-template-columns:repeat(2,minmax(0,1fr));
  gap:10px;
}

.level{
  min-width:0;
  min-height:82px;
  text-align:left;
  padding:12px;
  border-radius:15px;
  border:2px solid #303861;
  background:linear-gradient(135deg,#171c3b,#0d1024);
  position:relative;
  overflow:hidden;
  transition:transform .1s,border-color .1s;
}

.level:hover{
  border-color:#00eaff;
}

.level:active{
  transform:scale(.96);
}

.levelStatus{
  float:right;
  font-size:20px;
}

.levelName{
  font-weight:900;
  font-size:clamp(14px,3.5vw,18px);
  padding-right:25px;
}

.levelInfo{
  font-size:12px;
  opacity:.7;
  margin-top:5px;
}

#achBtn{
  width:min(680px,100%);
  min-height:48px;
  margin-top:14px;
  padding:12px;
  border-radius:14px;
  background:#242a50;
  border:2px solid #414d7c;
  font-weight:bold;
}

#achievements,
#pause,
#finish{
  position:fixed;
  inset:0;
  z-index:20;
  display:none;
  align-items:center;
  justify-content:center;
  background:#000b;
  padding:15px;
}

.panel{
  width:min(570px,100%);
  max-height:min(90vh,700px);
  overflow:auto;
  background:#10142c;
  border:2px solid #3d4a7d;
  border-radius:20px;
  padding:20px;
  box-shadow:0 0 40px #00eaff22;
}

.panel h2{
  text-align:center;
  margin-top:0;
}

.panel button{
  width:100%;
  min-height:46px;
  margin-top:9px;
  padding:12px;
  border-radius:12px;
  background:#29335e;
  font-weight:bold;
}

.ach{
  padding:12px;
  margin:8px 0;
  border-radius:12px;
  background:#191e3b;
  opacity:.4;
}

.ach.on{
  opacity:1;
  border:1px solid #00eaff;
}

#game{
  position:fixed;
  inset:0;
  display:none;
  touch-action:none;
  overscroll-behavior:none;
}

canvas{
  position:absolute;
  inset:0;
  display:block;
  width:100%;
  height:100%;
  touch-action:none;
}

#hud{
  position:absolute;
  z-index:4;
  left:max(10px,env(safe-area-inset-left));
  right:max(10px,env(safe-area-inset-right));
  top:max(10px,env(safe-area-inset-top));
  pointer-events:none;
  text-shadow:0 2px 5px #000;
}

.hudLine{
  display:flex;
  justify-content:space-between;
  gap:8px;
  font-size:clamp(12px,2.8vw,17px);
  font-weight:bold;
}

.hudBar{
  margin-top:7px;
  height:9px;
  background:#0008;
  border-radius:20px;
  overflow:hidden;
}

#gameBar{
  height:100%;
  width:0;
  background:#00eaff;
  box-shadow:0 0 12px #00eaff;
}

.gameButtons{
  position:absolute;
  right:max(10px,env(safe-area-inset-right));
  top:max(10px,env(safe-area-inset-top));
  z-index:10;
  display:flex;
  gap:7px;
}

.gameButtons button{
  min-width:44px;
  min-height:44px;
  padding:8px 11px;
  background:#10162ddd;
  border:1px solid #53618e;
  border-radius:10px;
}

@media(max-width:650px){
  #levels{
    grid-template-columns:1fr;
  }
}

@media(min-width:1000px){
  #levels{
    grid-template-columns:repeat(3,minmax(0,1fr));
  }
}

@media(max-height:500px){
  .logo{
    margin:4px 0;
    font-size:30px;
  }

  .subtitle{
    margin-bottom:8px;
  }

  .progress{
    padding:9px;
    margin-bottom:8px;
  }

  .level{
    min-height:65px;
  }

  #achBtn{
    margin-top:8px;
  }
}
</style>
</head>

<body>

<div id="menu">

  <div class="logo">NEON DASH</div>

  <div class="subtitle">
    Ultimate Edition • Dotknij / kliknij / SPACJA
  </div>

  <div class="progress">
    <div class="progressTop">
      <span>📊 PROGRES GRY</span>
      <span id="progressText">0%</span>
    </div>

    <div class="bar">
      <div id="menuBar"></div>
    </div>

    <div id="doneText">0 / 12 poziomów</div>
  </div>

  <div id="levels"></div>

  <button id="achBtn">🏆 ACHIEVEMENTY</button>

</div>

<div id="achievements">
  <div class="panel">
    <h2>🏆 ACHIEVEMENTY</h2>
    <div id="achList"></div>
    <button id="closeAch">ZAMKNIJ</button>
  </div>
</div>

<div id="game">

  <canvas id="canvas"></canvas>

  <div id="hud">

    <div class="hudLine">
      <span id="levelName">LEVEL</span>
      <span id="coins">🪙 0/3</span>
      <span id="percent">0%</span>
    </div>

    <div class="hudBar">
      <div id="gameBar"></div>
    </div>

  </div>

  <div class="gameButtons">
    <button id="pauseBtn">⏸</button>
    <button id="soundBtn">🔊</button>
    <button id="menuBtn">☰</button>
  </div>

  <div id="pause">
    <div class="panel">
      <h2>⏸ PAUZA</h2>
      <button id="resume">▶ WRÓĆ DO GRY</button>
      <button id="pauseMenu">☰ MENU</button>
    </div>
  </div>

  <div id="finish">
    <div class="panel">
      <h2 id="finishTitle">🎉 UKOŃCZONO!</h2>
      <p id="finishInfo"></p>
      <button id="again">🔄 ZAGRAJ PONOWNIE</button>
      <button id="finishMenu">☰ MENU</button>
    </div>
  </div>

</div>

<script>
"use strict";

/* =====================================================
   POZIOMY — 12
===================================================== */

const LEVELS=[
 {
  name:"NEON RUSH",
  diff:"⭐⭐",
  speed:280,
  color:"#00eaff",
  bpm:124,
  wave:"square",
  notes:[262,330,392,523,392,330,294,330],
  gravity:1
 },
 {
  name:"CRYSTAL DRIVE",
  diff:"⭐⭐⭐",
  speed:295,
  color:"#72a7ff",
  bpm:112,
  wave:"triangle",
  notes:[196,247,294,370,494,370,294,247],
  gravity:1
 },
 {
  name:"LAVA PULSE",
  diff:"⭐⭐⭐⭐",
  speed:310,
  color:"#ff4d42",
  bpm:140,
  wave:"sawtooth",
  notes:[110,110,165,147,110,131,98,110],
  gravity:1
 },
 {
  name:"SKY CIRCUIT",
  diff:"⭐⭐⭐⭐",
  speed:305,
  color:"#9c7bff",
  bpm:132,
  wave:"sine",
  notes:[330,392,494,659,587,494,392,330],
  gravity:1
 },
 {
  name:"VIOLET RUN",
  diff:"⭐⭐⭐⭐",
  speed:320,
  color:"#d35cff",
  bpm:128,
  wave:"triangle",
  notes:[220,277,330,440,523,440,330,277],
  gravity:1
 },
 {
  name:"SHADOW FACTORY",
  diff:"⭐⭐⭐⭐⭐",
  speed:325,
  color:"#b44cff",
  bpm:118,
  wave:"square",
  notes:[147,174,220,207,147,174,233,220],
  gravity:1
 },
 {
  name:"CYBER STORM",
  diff:"⭐⭐⭐⭐⭐",
  speed:335,
  color:"#27f0c5",
  bpm:136,
  wave:"triangle",
  notes:[165,220,277,330,440,330,277,220],
  gravity:1
 },
 {
  name:"INFERNO CORE",
  diff:"⭐⭐⭐⭐⭐",
  speed:345,
  color:"#ff7338",
  bpm:145,
  wave:"sawtooth",
  notes:[98,123,147,196,147,123,110,98],
  gravity:1
 },
 {
  name:"ELECTRIC VOID",
  diff:"⭐⭐⭐⭐⭐⭐",
  speed:355,
  color:"#35b7ff",
  bpm:150,
  wave:"square",
  notes:[220,330,440,659,523,440,330,247],
  gravity:1
 },
 {
  name:"GRAVITY BREAK",
  diff:"⭐⭐⭐⭐⭐⭐",
  speed:340,
  color:"#45ff9a",
  bpm:142,
  wave:"triangle",
  notes:[196,247,330,392,494,392,330,247],
  gravity:-1
 },
 {
  name:"OVERDRIVE",
  diff:"⭐⭐⭐⭐⭐⭐",
  speed:365,
  color:"#ff3bea",
  bpm:154,
  wave:"square",
  notes:[247,330,440,523,659,523,440,330],
  gravity:1
 },
 {
  name:"FINAL CHAOS",
  diff:"⭐⭐⭐⭐⭐⭐",
  speed:375,
  color:"#ff247f",
  bpm:158,
  wave:"sawtooth",
  notes:[220,330,440,659,523,784,659,440],
  gravity:1
 }
];

/* =====================================================
   DOM
===================================================== */

const menu=document.getElementById("menu");
const game=document.getElementById("game");
const canvas=document.getElementById("canvas");
const ctx=canvas.getContext("2d");

const levelsBox=document.getElementById("levels");
const achievements=document.getElementById("achievements");
const achList=document.getElementById("achList");

const pause=document.getElementById("pause");
const finish=document.getElementById("finish");

const levelName=document.getElementById("levelName");
const coinsText=document.getElementById("coins");
const percent=document.getElementById("percent");
const menuBar=document.getElementById("menuBar");
const gameBar=document.getElementById("gameBar");
const progressText=document.getElementById("progressText");
const doneText=document.getElementById("doneText");

/* =====================================================
   STORAGE
===================================================== */

function get(key,def){
  try{
    const v=localStorage.getItem(key);
    return v===null?def:v;
  }catch(e){
    return def;
  }
}

function set(key,val){
  try{
    localStorage.setItem(key,String(val));
  }catch(e){}
}

function completed(i){
  return get("nd_level_"+i,"0")==="1";
}

function completedCount(){
  let n=0;

  for(let i=0;i<LEVELS.length;i++){
    if(completed(i)) n++;
  }

  return n;
}

/* =====================================================
   ACHIEVEMENTY
===================================================== */

const ACH=[
 ["first","🎮 Pierwszy krok","Ukończ poziom 1."],
 ["three","⚡ Rozgrzewka","Ukończ 3 poziomy."],
 ["six","🔥 Weteran","Ukończ 6 poziomów."],
 ["all","👑 Mistrz Neon Dash","Ukończ wszystkie poziomy."],
 ["final","💀 Chaos pokonany","Ukończ FINAL CHAOS."],
 ["coins10","🪙 Łowca monet","Zbierz 10 monet."],
 ["coins25","💰 Kolekcjoner","Zbierz 25 monet."],
 ["perfect","💎 Perfekcja","Ukończ poziom bez śmierci."],
 ["survivor","🛡️ Twardziel","Ukończ poziom po 3+ śmierciach."],
 ["allcoins","🌟 Pełna kolekcja","Zbierz wszystkie 3 monety."]
];

function achUnlocked(id){
  return get("nd_ach_"+id,"0")==="1";
}

function unlock(id){
  if(achUnlocked(id)) return;

  set("nd_ach_"+id,"1");
  renderAchievements();
}

function checkAchievements(){

  const n=completedCount();

  if(n>=1) unlock("first");
  if(n>=3) unlock("three");
  if(n>=6) unlock("six");
  if(n>=12) unlock("all");

  if(completed(11)) unlock("final");

  const total=Number(get("nd_totalCoins","0"));

  if(total>=10) unlock("coins10");
  if(total>=25) unlock("coins25");

  if(deaths===0) unlock("perfect");
  if(deaths>=3) unlock("survivor");

  if(runCoins===3) unlock("allcoins");
}

function renderAchievements(){

  achList.innerHTML="";

  ACH.forEach(a=>{

    const d=document.createElement("div");

    d.className=
      "ach"+
      (achUnlocked(a[0])?" on":"");

    d.innerHTML=
      "<b>"+a[1]+"</b><br>"+
      "<small>"+a[2]+"</small>";

    achList.appendChild(d);
  });
}

/* =====================================================
   MENU
===================================================== */

function renderMenu(){

  levelsBox.innerHTML="";

  /*
    WAŻNE:
    Poziomy są tworzone dopiero tutaj,
    po załadowaniu całego JavaScriptu.
  */

  LEVELS.forEach((l,i)=>{

    const b=document.createElement("button");

    b.type="button";
    b.className="level";

    b.innerHTML=
      '<span class="levelStatus">'+
      (completed(i)?"✅":"▶️")+
      '</span>'+
      '<div class="levelName">'+
      (i+1)+". "+l.name+
      '</div>'+
      '<div class="levelInfo">'+
      l.diff+
      " • "+
      l.speed+
      " px/s"+
      '</div>';

    b.addEventListener("click",function(e){

      e.preventDefault();
      e.stopPropagation();

      startLevel(i,true);
    });

    levelsBox.appendChild(b);
  });

  const done=completedCount();

  const p=Math.round(
    done/LEVELS.length*100
  );

  progressText.textContent=p+"%";
  menuBar.style.width=p+"%";

  doneText.textContent=
    done+" / "+
    LEVELS.length+
    " poziomów";
}

document.getElementById("achBtn")
.addEventListener("click",()=>{
  achievements.style.display="flex";
  renderAchievements();
});

document.getElementById("closeAch")
.addEventListener("click",()=>{
  achievements.style.display="none";
});

/* =====================================================
   RESPONSIVE CANVAS
===================================================== */

let W=window.innerWidth;
let H=window.innerHeight;
let ground=H*.78;

/*
  Player deklarujemy WCZEŚNIEJ niż resize().
  To usuwa błąd, przez który menu mogło się nie pojawić.
*/

const player={
  x:150,
  y:0,
  size:34,
  vy:0,
  rot:0,
  grounded:false
};

function resize(){

  W=Math.max(240,window.innerWidth);
  H=Math.max(240,window.innerHeight);

  const d=Math.min(
    Math.max(window.devicePixelRatio||1,1),
    2
  );

  canvas.width=Math.round(W*d);
  canvas.height=Math.round(H*d);

  canvas.style.width=W+"px";
  canvas.style.height=H+"px";

  ctx.setTransform(d,0,0,d,0,0);

  ground=Math.max(
    160,
    Math.min(
      H-55,
      H*.78
    )
  );

  if(
    typeof player!=="undefined" &&
    !running
  ){
    player.y=ground-player.size;
  }

  createStars();
}

window.addEventListener(
  "resize",
  resize,
  {passive:true}
);

window.addEventListener(
  "orientationchange",
  ()=>{
    setTimeout(resize,100);
  },
  {passive:true}
);

/* =====================================================
   GAME STATE
===================================================== */

let current=0;
let running=false;
let paused=false;
let finished=false;
let dying=false;

let world=0;
let last=0;
let raf=0;

let deaths=0;
let runCoins=0;

let collected=new Set();

let obstacles=[];
let coinObjects=[];
let pads=[];
let portals=[];
let particles=[];
let stars=[];
let trail=[];

let shake=0;
let flash=0;

let gravityDirection=1;

let audio=null;
let musicTimer=null;
let musicIndex=0;

let sound=
  get("nd_sound","1")==="1";

/* =====================================================
   START
===================================================== */

function resetPlayer(){

  player.x=Math.max(
    80,
    Math.min(180,W*.22)
  );

  player.y=
    gravityDirection===1?
    ground-player.size:
    0;

  player.vy=0;
  player.rot=0;
  player.grounded=true;
}

function startLevel(index,newRun=true){

  if(
    index<0||
    index>=LEVELS.length
  ) return;

  current=index;

  if(newRun){

    deaths=0;
    runCoins=0;
    collected=new Set();
  }

  running=false;
  paused=false;
  finished=false;
  dying=false;

  if(raf){
    cancelAnimationFrame(raf);
    raf=0;
  }

  stopMusic();

  game.style.display="block";
  menu.style.display="none";

  pause.style.display="none";
  finish.style.display="none";

  world=0;
  last=performance.now();

  particles=[];
  trail=[];
  shake=0;
  flash=0;

  gravityDirection=
    LEVELS[current].gravity;

  resetPlayer();

  generateLevel();
  createStars();

  levelName.textContent=
    (current+1)+
    " • "+
    LEVELS[current].name;

  coinsText.textContent=
    "🪙 "+
    runCoins+
    "/3";

  running=true;

  if(sound){
    startMusic();
  }

  draw();

  raf=requestAnimationFrame(loop);
}

/* =====================================================
   GENEROWANIE POZIOMU
===================================================== */

function generateLevel(){

  obstacles=[];
  coinObjects=[];
  pads=[];
  portals=[];

  const length=
    11500+
    current*600;

  let x=650;
  let p=0;

  const patterns=[
    "spike",
    "double",
    "saw",
    "gap",
    "pad",
    "spike",
    "saw",
    "speed",
    "double",
    "gap",
    "spikeSaw",
    "gravity",
    "triple",
    "saw"
  ];

  while(x<length){

    const type=
      patterns[p%patterns.length];

    if(type==="spike"){

      spike(x);
      x+=430;

    }else if(type==="double"){

      spike(x);
      spike(x+65);
      x+=520;

    }else if(type==="triple"){

      spike(x);
      spike(x+65);
      spike(x+130);
      x+=610;

    }else if(type==="saw"){

      saw(x);
      x+=520;

    }else if(type==="spikeSaw"){

      spike(x);
      saw(x+230);
      x+=650;

    }else if(type==="gap"){

      gap(x,150);
      x+=630;

    }else if(type==="pad"){

      pad(x);
      spike(x+190);
      x+=600;

    }else if(type==="speed"){

      speedPortal(x,1.18);
      spike(x+250);
      saw(x+480);
      x+=760;

    }else if(type==="gravity"){

      gravityPortal(x);
      spike(x+280);
      spike(x+345);
      x+=720;
    }

    p++;
  }

  /*
    Dokładnie 3 monety.
  */

  const positions=[
    length*.25,
    length*.52,
    length*.79
  ];

  positions.forEach((cx,i)=>{

    let finalX=cx;

    for(let a=0;a<40;a++){

      let bad=false;

      for(const o of obstacles){

        if(o.type==="gap"){

          if(
            finalX>o.x-100 &&
            finalX<
              o.x+
              o.w+
              100
          ){
            bad=true;
            break;
          }

        }else{

          if(
            Math.abs(
              finalX-o.x
            )<120
          ){
            bad=true;
            break;
          }
        }
      }

      if(!bad) break;

      finalX+=120;
    }

    coinObjects.push({
      id:i,
      x:finalX,
      collected:
        collected.has(i)
    });
  });
}

/* =====================================================
   OBIEKTY
===================================================== */

function spike(x){
  obstacles.push({
    type:"spike",
    x:x
  });
}

function saw(x){
  obstacles.push({
    type:"saw",
    x:x,
    r:28
  });
}

function gap(x,w){
  obstacles.push({
    type:"gap",
    x:x,
    w:w
  });
}

function pad(x){
  pads.push({
    x:x,
    used:false
  });
}

function speedPortal(x,mult){
  portals.push({
    type:"speed",
    x:x,
    mult:mult,
    used:false
  });
}

function gravityPortal(x){
  portals.push({
    type:"gravity",
    x:x,
    used:false
  });
}

/* =====================================================
   STEROWANIE
===================================================== */

function jump(){

  if(
    !running||
    paused||
    dying||
    finished
  ) return;

  if(player.grounded){

    player.vy=
      -730*
      gravityDirection;

    player.grounded=false;

    particlesJump();

    shake=3;
  }
}

game.addEventListener(
  "pointerdown",
  e=>{

    if(
      e.target.closest(".gameButtons")||
      e.target.closest("#pause")||
      e.target.closest("#finish")
    ) return;

    jump();
  },
  {passive:true}
);

window.addEventListener(
  "keydown",
  e=>{

    if(
      e.code==="Space"||
      e.code==="ArrowUp"||
      e.code==="KeyW"
    ){

      e.preventDefault();
      jump();
    }

    if(
      e.code==="Escape"||
      e.code==="KeyP"
    ){

      if(running){
        togglePause();
      }
    }
  }
);

/* =====================================================
   UPDATE
===================================================== */

function update(dt){

  let speed=
    LEVELS[current].speed;

  for(const p of portals){

    if(
      p.type==="speed"&&
      world+player.x>
        p.x&&
      world+player.x<
        p.x+180
    ){

      speed*=p.mult;
    }
  }

  world+=speed*dt;

  const g=
    2100*
   
