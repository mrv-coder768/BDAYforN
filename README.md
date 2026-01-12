<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nirmala’s BTS Birthday 💜🎂</title>
<style>
html, body{
  margin:0; padding:0; height:100%; overflow:hidden;
  font-family:'Poppins',sans-serif;
  background: radial-gradient(circle at bottom,#1e1e2f,#0a0a15);
  color:white; text-align:center; transition: opacity 1s ease;
}
body.fade-out{opacity:0; transform:scale(1.05);}
canvas{position:fixed; inset:0; z-index:0;}
.content{position:relative; z-index:2; top:50%; transform:translateY(-50%);
max-width:700px; margin:auto; padding:20px;}
h1{font-size:clamp(2em,5vw,3em); color:#ad7eff; text-shadow:0 0 25px #ff66b3,0 0 50px #ad7eff; animation:glow 2s infinite alternate;}
@keyframes glow{0%{text-shadow:0 0 15px #ad7eff;}100%{text-shadow:0 0 45px #ff66b3;}}
.countdown{display:flex; justify-content:center; gap:20px; margin-top:30px; flex-wrap:wrap;}
.time-box{background: linear-gradient(135deg,#6a82fb,#fc5c7d); padding:20px 25px; border-radius:20px;
box-shadow:0 0 25px rgba(106,130,251,.8);}
.time-box span{display:block; font-size:clamp(2em,10vw,3em); font-weight:bold; animation:pulse 1s infinite alternate;}
@keyframes pulse{0%{transform:scale(1);}50%{transform:scale(1.1);}100%{transform:scale(1);}}
.time-box small{color:#eee;}
p, .tagline{margin-top:15px; color:#ffccff; font-size:1.1em;}
.hearts{position:fixed; inset:0; pointer-events:none; z-index:1;}
.heart{position:absolute; bottom:0; width:20px; height:20px; background:#ff80c1; opacity:.7;
clip-path: polygon(50% 0%,61% 15%,75% 15%,85% 25%,85% 40%,50% 75%,15% 40%,15% 25%,25% 15%,39% 15%);
animation:float 5s linear infinite;}
@keyframes float{to{transform:translateY(-100vh) scale(1.5);opacity:0;}}
button{margin-top:20px;padding:12px 25px;border:none;border-radius:30px;background:linear-gradient(90deg,#ffcc66,#ff66b3);
color:white;cursor:pointer;}

/* Birthday content */
#birthdayContent{display:none;}
h2{color:#ffd6ff; margin-top:10px;}
p.gift{color:#ffdd66; font-weight:bold; margin-top:15px; font-size:1.2em;}
#btsLogos{position:fixed; inset:0; pointer-events:none; z-index:3;}
.btsLogo{position:absolute; width:30px; height:30px; background:url('bts_logo.png') no-repeat center/contain;
opacity:0.8; animation:floatLogo 5s linear forwards;}
@keyframes floatLogo{0%{transform:translateY(100vh) rotate(0deg);opacity:1;}100%{transform:translateY(-50px) rotate(360deg);opacity:0;}}

/* Confetti */
.confetti-piece{
  position:absolute; width:10px; height:10px; border-radius:50%;
  opacity:0.8; z-index:4;
}

/* Photo */
.birthdayPhoto {
  width:180px; height:180px; border-radius:50%;
  object-fit:cover; border:4px solid #ff66b3; box-shadow:0 0 25px #ff66b3,0 0 50px #ad7eff;
  animation:photoGlow 2s ease-in-out infinite alternate;
  margin:15px 0;
}
@keyframes photoGlow{
  0%{box-shadow:0 0 25px #ff66b3,0 0 50px #ad7eff;}
  100%{box-shadow:0 0 50px #ff66b3,0 0 80px #ad7eff;}
}
</style>
</head>
<body>

<canvas id="fireworks"></canvas>
<div class="hearts" id="hearts"></div>
<div id="btsLogos"></div>

<div class="content" id="countdownContent">
  <h1>🎂 Countdown to Nirmala’s Birthday 🎂💜</h1>
  <div class="countdown">
    <div class="time-box"><span id="days">00</span><small>Days</small></div>
    <div class="time-box"><span id="hours">00</span><small>Hours</small></div>
    <div class="time-box"><span id="minutes">00</span><small>Minutes</small></div>
    <div class="time-box"><span id="seconds">00</span><small>Seconds</small></div>
  </div>
  <p class="tagline">Keep shining like BTS, smiling like Jimin, and spreading love like ARMY 💜🎶</p>
  <button id="playMusicCountdown">🔊 Play Countdown Music</button>
</div>

<div class="content" id="birthdayContent">
  <h1>💜 Happy Birthday, Nirmala! 🎂✨</h1>
  <img src="n.jpeg" alt="Nirmala" class="birthdayPhoto">
  <h2>Shine Bright Like BTS 💫🎶</h2>
  <p>Dear Nirmala, today is your special day! 🌟<br>
     May your smile light up the world, your dreams come true,<br>
     and your days be as joyful as your favorite BTS songs.</p>
  <p class="gift">🎁 Your Special Gift: A token of love 💜</p>
  <p>Keep shining, dancing, and smiling like only you can. Happy Birthday 💖🎶</p>
  <button id="playMusicBirthday">🔊 Play Birthday Music</button>
</div>

<!-- Music files -->
<audio id="musicCountdown" loop>
  <source src="Liquid Time-Aakash Gandhi (mp3cut.net).mp3" type="audio/mp3">
</audio>
<audio id="musicBirthday" loop>
  <source src="micro.mp3" type="audio/mp3">
</audio>

<script>
// ---------------- Countdown ----------------
const target = new Date("2026-01-16T00:00:00").getTime();
const dEl=document.getElementById("days"), hEl=document.getElementById("hours"),
      mEl=document.getElementById("minutes"), sEl=document.getElementById("seconds");

const countdownInterval = setInterval(()=>{
  const now=Date.now();
  const diff=target-now;
  if(diff<=0){
    clearInterval(countdownInterval);
    document.body.classList.add("fade-out");
    setTimeout(startBirthday,1000);
    return;
  }
  dEl.textContent=Math.floor(diff/(1000*60*60*24)).toString().padStart(2,'0');
  hEl.textContent=Math.floor((diff%(1000*60*60*24))/(1000*60*60)).toString().padStart(2,'0');
  mEl.textContent=Math.floor((diff%(1000*60*60))/(1000*60)).toString().padStart(2,'0');
  sEl.textContent=Math.floor((diff%(1000*60))/1000).toString().padStart(2,'0');
},1000);

// ---------------- Music Buttons ----------------
const musicCountdown = document.getElementById("musicCountdown");
const musicBirthday = document.getElementById("musicBirthday");

window.onload = () => {
  musicCountdown.play().catch(()=>{document.getElementById("playMusicCountdown").style.display="inline-block";});
};

document.getElementById("playMusicCountdown").onclick = () => {
  musicCountdown.play(); 
  document.getElementById("playMusicCountdown").style.display = "none";
};

document.getElementById("playMusicBirthday").onclick = () => {
  musicBirthday.play(); 
  document.getElementById("playMusicBirthday").style.display = "none";
};

// ---------------- Hearts ----------------
function createHeart(){
  const h=document.createElement("div"); h.className="heart";
  h.style.left=Math.random()*100+"vw"; h.style.animationDuration=3+Math.random()*4+"s";
  document.getElementById("hearts").appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(createHeart,400);

// ---------------- Birthday ----------------
function startBirthday(){
  document.getElementById("countdownContent").style.display="none";
  document.getElementById("birthdayContent").style.display="block";
  musicCountdown.pause(); musicCountdown.currentTime=0;
  musicBirthday.play().catch(()=>{document.getElementById("playMusicBirthday").style.display="inline-block";});
}

// ---------------- BTS Logos ----------------
function spawnLogo(){
  const logo=document.createElement("div");
  logo.className="btsLogo"; logo.style.left=Math.random()*100+'vw';
  logo.style.animationDuration=(4+Math.random()*3)+'s';
  document.getElementById('btsLogos').appendChild(logo);
  setTimeout(()=>logo.remove(),7000);
}
setInterval(spawnLogo,500);

// ---------------- Confetti ----------------
function createConfetti(){
  const colors=["#ad7eff","#ff66b3","#ffccff","#8a2be2","#d580ff"];
  const c=document.createElement("div"); c.className="confetti-piece";
  c.style.background=colors[Math.floor(Math.random()*colors.length)];
  c.style.left=Math.random()*100+"vw";
  c.style.top="-10px";
  document.body.appendChild(c);
  let fall=0;
  const fallInterval=setInterval(()=>{
    fall+=5+Math.random()*5;
    c.style.top=fall+"px";
    c.style.transform=`rotate(${fall*3}deg)`;
    if(fall>window.innerHeight){ c.remove(); clearInterval(fallInterval);}
  },30);
}
setInterval(createConfetti,200);

// ---------------- Fireworks ----------------
const canvas=document.getElementById("fireworks"), ctx=canvas.getContext("2d");
let w,h;
function resize(){ w=canvas.width=innerWidth; h=canvas.height=innerHeight; }
window.addEventListener("resize",resize); resize();
let fireworksArr=[];
class Firework{
  constructor(){ this.x=Math.random()*w; this.y=h; this.ty=Math.random()*h*0.5; this.color=`hsl(${Math.random()*360},100%,70%)`; this.speed=4+Math.random()*3; this.parts=[]; }
  explode(){ for(let i=0;i<50;i++){ const angle=Math.random()*Math.PI*2; const speed=Math.random()*4+1; const colors=['#ad7eff','#ff66b3','#ffccff','#8a2be2','#d580ff']; const color=colors[Math.floor(Math.random()*colors.length)]; this.parts.push({x:this.x,y:this.y,vx:Math.cos(angle)*speed,vy:Math.sin(angle)*speed,a:1,color}); } }
  update(){ if(this.y>this.ty) this.y-=this.speed; else if(!this.parts.length) this.explode(); this.parts.forEach(p=>{p.x+=p.vx;p.y+=p.vy;p.vy+=0.05;p.a-=0.01;}); this.parts=this.parts.filter(p=>p.a>0); }
  draw(){ if(this.parts.length===0){ ctx.beginPath(); ctx.fillStyle=this.color; ctx.arc(this.x,this.y,3,0,Math.PI*2); ctx.fill(); } this.parts.forEach(p=>{ ctx.globalAlpha=p.a; ctx.fillStyle=p.color; ctx.beginPath(); ctx.arc(p.x,p.y,2,0,Math.PI*2); ctx.fill(); ctx.globalAlpha=1;}); }
}
function animate(){ ctx.fillStyle="rgba(0,0,0,0.2)"; ctx.fillRect(0,0,w,h); if(Math.random()<0.03) fireworksArr.push(new Firework()); fireworksArr.forEach((f,i)=>{ f.update(); f.draw(); if(f.parts.length===0 && f.y<=f.ty) fireworksArr.splice(i,1); }); requestAnimationFrame(animate);}
animate();
</script>

</body>
</html>
