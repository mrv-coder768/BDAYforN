<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nirmala’s Birthday 💜🎂</title>

<style>
html,body{
  margin:0;
  padding:0;
  min-height:100%;
  overflow-x:hidden;
  overflow-y:auto;
  font-family:'Poppins',sans-serif;
  background:radial-gradient(circle at bottom,#1e1e2f,#0a0a15);
  color:white;
  text-align:center;
}

canvas{
  position:fixed;
  inset:0;
  z-index:0;
}

.content{
  position:relative;
  z-index:2;
  max-width:850px;
  margin:auto;
  padding:20px;
}

h1{
  font-size:clamp(2em,5vw,3em);
  color:#ad7eff;
  text-shadow:0 0 20px #ff66b3,0 0 40px #ad7eff;
}

/* Countdown */
.countdown{
  display:flex;
  justify-content:center;
  gap:20px;
  margin-top:30px;
  flex-wrap:wrap;
}

.time-box{
  background:linear-gradient(135deg,#6a82fb,#fc5c7d);
  padding:20px 25px;
  border-radius:20px;
}

.time-box span{
  font-size:2.5em;
  font-weight:bold;
  display:block;
}

button{
  margin-top:20px;
  padding:12px 25px;
  border:none;
  border-radius:30px;
  background:linear-gradient(90deg,#ffcc66,#ff66b3);
  color:white;
  font-size:1em;
  cursor:pointer;
}

/* Hearts */
.hearts{
  position:fixed;
  inset:0;
  pointer-events:none;
  z-index:1;
}

.heart{
  position:absolute;
  bottom:0;
  width:18px;
  height:18px;
  background:#ff80c1;
  opacity:.7;
  clip-path:polygon(50% 0%,61% 15%,75% 15%,85% 25%,85% 40%,50% 75%,15% 40%,15% 25%,25% 15%,39% 15%);
  animation:float 5s linear infinite;
}

@keyframes float{
  to{transform:translateY(-100vh) scale(1.4);opacity:0;}
}

/* Birthday */
#birthdayContent{
  display:none;
}

.birthdayPhoto{
  width:100%;
  max-width:420px;
  max-height:420px;
  object-fit:contain;
  margin:20px auto;
  border-radius:18px;
  box-shadow:0 0 25px rgba(173,126,255,0.6);
}

/* Video */
.birthdayVideo{
  width:100%;
  max-width:600px;
  margin:25px auto 40px;
  display:block;
  border-radius:18px;
  box-shadow:0 0 30px rgba(255,102,179,0.7);
}
</style>
</head>

<body>

<canvas id="fireworks"></canvas>
<div class="hearts" id="hearts"></div>

<!-- Countdown Page -->
<div class="content" id="countdownContent">
  <h1>🎂 Countdown to Nirmala’s Birthday 💜</h1>

  <div class="countdown">
    <div class="time-box"><span id="days">00</span><small>Days</small></div>
    <div class="time-box"><span id="hours">00</span><small>Hours</small></div>
    <div class="time-box"><span id="minutes">00</span><small>Minutes</small></div>
    <div class="time-box"><span id="seconds">00</span><small>Seconds</small></div>
  </div>

  <button id="playMusicCountdown">🔊 Play Music</button>
</div>

<!-- Birthday Page -->
<div class="content" id="birthdayContent">
  <h1>💜 Happy Birthday Nirmala 🎂✨</h1>
  <p>May your day be filled with love and happiness 💜</p>

  <img src="n.jpeg" alt="Nirmala" class="birthdayPhoto">

  <button id="playMusicBirthday">🔊 Play Birthday Song</button>

  <!-- Video -->
  <video class="birthdayVideo" controls autoplay muted playsinline>
    <source src="video.mp4" type="video/mp4">
  </video>
</div>

<!-- Music -->
<audio id="musicCountdown" loop>
  <source src="cd.mp3" type="audio/mp3">
</audio>

<audio id="musicBirthday" loop>
  <source src="micro.mp3" type="audio/mp3">
</audio>

<script>
/* Countdown */
const target=new Date("2026-01-14T10:00:00").getTime();
const d=document.getElementById("days"),
      h=document.getElementById("hours"),
      m=document.getElementById("minutes"),
      s=document.getElementById("seconds");

const timer=setInterval(()=>{
  const now=Date.now();
  const diff=target-now;
  if(diff<=0){
    clearInterval(timer);
    showBirthday();
    return;
  }
  d.textContent=Math.floor(diff/86400000);
  h.textContent=Math.floor(diff%86400000/3600000);
  m.textContent=Math.floor(diff%3600000/60000);
  s.textContent=Math.floor(diff%60000/1000);
},1000);

/* Music */
const mc=document.getElementById("musicCountdown");
const mb=document.getElementById("musicBirthday");

window.onload=()=>mc.play().catch(()=>{});

document.getElementById("playMusicCountdown").onclick=()=>mc.play();

document.getElementById("playMusicBirthday").onclick=()=>{
  mb.play();
  const v=document.querySelector(".birthdayVideo");
  v.muted=false;
  v.play();
};

/* Hearts */
function heart(){
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=Math.random()*100+"vw";
  h.style.animationDuration=3+Math.random()*4+"s";
  document.getElementById("hearts").appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(heart,400);

/* Birthday Show */
function showBirthday(){
  document.getElementById("countdownContent").style.display="none";
  document.getElementById("birthdayContent").style.display="block";
  mc.pause(); mc.currentTime=0;
  mb.play().catch(()=>{});
}

/* Fireworks */
const canvas=document.getElementById("fireworks");
const ctx=canvas.getContext("2d");

function resize(){
  canvas.width=innerWidth;
  canvas.height=innerHeight;
}
window.addEventListener("resize",resize);
resize();

let fireworks=[];
class Firework{
  constructor(){
    this.x=Math.random()*canvas.width;
    this.y=canvas.height;
    this.ty=Math.random()*canvas.height/2;
    this.v=4+Math.random()*3;
    this.p=[];
  }
  explode(){
    for(let i=0;i<40;i++){
      const a=Math.random()*Math.PI*2;
      this.p.push({x:this.x,y:this.y,vx:Math.cos(a)*4,vy:Math.sin(a)*4,a:1});
    }
  }
  update(){
    if(this.y>this.ty) this.y-=this.v;
    else if(!this.p.length) this.explode();
    this.p.forEach(o=>{
      o.x+=o.vx;
      o.y+=o.vy;
      o.vy+=0.05;
      o.a-=0.01;
    });
    this.p=this.p.filter(o=>o.a>0);
  }
  draw(){
    if(!this.p.length){
      ctx.fillStyle="#ad7eff";
      ctx.beginPath();
      ctx.arc(this.x,this.y,3,0,6.28);
      ctx.fill();
    }
    this.p.forEach(o=>{
      ctx.globalAlpha=o.a;
      ctx.fillStyle="#ff66b3";
      ctx.beginPath();
      ctx.arc(o.x,o.y,2,0,6.28);
      ctx.fill();
    });
    ctx.globalAlpha=1;
  }
}

function animate(){
  ctx.fillStyle="rgba(0,0,0,0.2)";
  ctx.fillRect(0,0,canvas.width,canvas.height);
  if(Math.random()<0.03) fireworks.push(new Firework());
  fireworks.forEach((f,i)=>{
    f.update();
    f.draw();
    if(!f.p.length && f.y<=f.ty) fireworks.splice(i,1);
  });
  requestAnimationFrame(animate);
}
animate();
</script>

</body>
</html>
