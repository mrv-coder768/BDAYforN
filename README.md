<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Happy Birthday Nirmala 🎉</title>
<style>
html,body {
  margin:0;padding:0;height:100%;overflow:hidden;
  background: radial-gradient(circle at bottom,#000b18 0%,#00030a 100%);
  font-family:'Poppins',sans-serif;color:#fff;text-align:center;
}
canvas{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;}
.content{
  position:relative;z-index:5;top:50%;transform:translateY(-50%);
  padding:0 20px;max-width:700px;margin:auto;transition: all 1s ease;opacity:1;
}
h1{
  font-size:clamp(2em,5vw,3em);color:#ffcbf2;
  text-shadow:0 0 25px #ff1b8d,0 0 50px #ff66b3;
  animation:glow 2s ease-in-out infinite alternate;margin-bottom:10px;
}
@keyframes glow{from{text-shadow:0 0 15px #ff66b3;}to{text-shadow:0 0 45px #ff1b8d;}}
h2{
  font-size:clamp(1.5em,4vw,2em);color:#ffd6ff;
  margin-top:10px;animation:jump 1s infinite alternate;
}
@keyframes jump{0%{transform:translateY(0);}50%{transform:translateY(-10px);}100%{transform:translateY(0);}}
p{font-size:clamp(1em,3vw,1.2em);color:#fff0ff;margin-top:10px;line-height:1.5;}
.gift{font-size:1.5em;color:#ffd700;font-weight:bold;margin-top:20px;text-shadow:0 0 20px #ffdd33;}
.hearts{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;overflow:hidden;z-index:2;}
.heart{
  position:absolute;bottom:0;width:20px;height:20px;background:#ff80c1;opacity:.7;
  clip-path:polygon(50% 0%,61% 15%,75% 15%,85% 25%,85% 40%,50% 75%,15% 40%,15% 25%,25% 15%,39% 15%);
  animation:floatHearts linear infinite;
}
@keyframes floatHearts{
  0%{transform:translateY(0) scale(1);opacity:1;}
  100%{transform:translateY(-100vh) scale(1.5);opacity:0;}
}
.confetti-piece{
  position:absolute;width:10px;height:10px;background:yellow;opacity:0.8;z-index:4;border-radius:50%;
}
.countdown {
  display:flex;justify-content:center;gap:20px;margin-top:30px;flex-wrap:wrap;
}
.time-box {
  background: linear-gradient(135deg, #6a82fb, #fc5c7d);
  border-radius: 20px;padding: 20px 25px;
  box-shadow: 0 0 25px rgba(106,130,251,0.8), 0 0 50px rgba(252,92,125,0.5);
  text-align: center;
}
.time-box span {
  display:block;font-size:clamp(2em, 10vw, 3em);font-weight:bold;color:#fff;
  text-shadow:0 0 20px #fff, 0 0 40px #6a82fb;animation:pulse 1s infinite alternate;
}
.time-box small {
  display:block;font-size:clamp(0.8em,3vw,1em);color:#dcdcff;margin-top:5px;text-shadow:0 0 5px #6a82fb;
}
@keyframes pulse{0%{transform:scale(1);}50%{transform:scale(1.1);}100%{transform:scale(1);}}
button#playMusicBtn{
  margin-top:20px;background:linear-gradient(90deg,#ffcc66,#ff66b3);
  color:white;border:none;padding:12px 25px;font-size:1em;border-radius:30px;
  cursor:pointer;transition:transform .2s;display:none;
}
button#playMusicBtn:hover{transform:scale(1.08);}

/* Mobile adjustments */
@media(max-width:600px){
  .content{top:55%;}
}
@media(max-width:480px){
  h1{font-size:clamp(1.5em,7vw,2.5em);}
  h2{font-size:clamp(1.2em,5vw,2em);}
  p{font-size:clamp(0.9em,3vw,1.1em);}
}
@media(max-width:400px){
  .countdown{flex-wrap:wrap;justify-content:center;}
  .time-box{flex:1 1 40%;margin-bottom:10px;}
}

/* Final screen styles (overlay) */
.final-overlay {
  position:fixed; top:0; left:0; width:100%; height:100%;
  background: rgba(255,20,147,0.9); backdrop-filter: blur(4px);
  display:none; z-index:6; padding:70px 20px; box-sizing:border-box; overflow:auto;
}
.final-overlay h1 { font-size:clamp(2.2em,6vw,3.2em); color:#fff; text-shadow:0 0 30px #ff66b3; }
.final-overlay p { color:#fff8ff; font-size:1.05rem; line-height:1.6; margin-top:15px; }
.final-overlay .closeBtn {
  margin-top:25px; padding:10px 18px; border-radius:30px; border:none;
  background:#fff;color:#ff0066;font-weight:700; cursor:pointer;
}
</style>
</head>
<body>

<canvas id="fireworks"></canvas>
<div class="hearts" id="hearts"></div>

<div class="content" id="content">
  <h1>------------------------------------------🎂 Countdown to Nirmala’s Birthday 🎂</h1>
  <div class="countdown" id="countdown">
    <div class="time-box"><span id="days">00</span><small>Days</small></div>
    <div class="time-box"><span id="hours">00</span><small>Hours</small></div>
    <div class="time-box"><span id="minutes">00</span><small>Minutes</small></div>
    <div class="time-box"><span id="seconds">00</span><small>Seconds</small></div>
  </div>
  <p id="msg">Advance Happy Birthday! 🎉💫</p>
  <button id="playMusicBtn">🔊 Play Music</button>
</div>

<!-- Countdown music -->
<audio id="bgmCountdown" loop>
  <source src="Liquid Time - Aakash Gandhi (mp3cut.net).mp3" type="audio/mp3">
</audio>

<!-- Birthday music -->
<audio id="bgmBirthday" loop>
  <source src="theuned_happy-birthday-crowd(chosic.com).mp3" type="audio/mp3">
</audio>

<!-- Final overlay -->
<div class="final-overlay" id="finalOverlay">
  <h1>💖 Happy Birthday, Dear Nirmala 💖</h1>
  <p>
    Dear Nirmala, today is your special day! 🌟 May your smile light up every corner of the world,
    may laughter and joy follow you wherever you go, and may all your dreams turn into reality 💫.
  </p>
  <p>
    On this magical day, may happiness surround you, your heart be filled with love,
    and every moment be more beautiful than the last. 💖🎂
  </p>
  <p class="gift">🎁 Your Special Gift: A token of love and appreciation 💝</p>
  <p>With endless love, hugs, and blessings — Have the happiest birthday ever!</p>
  <button class="closeBtn" id="closeOverlay">Close ✨</button>
</div>

<script>
// ---------------- Countdown ----------------
const target = new Date("2026-01-12T15:38:00").getTime();

const daysEl=document.getElementById("days"),
      hoursEl=document.getElementById("hours"),
      minutesEl=document.getElementById("minutes"),
      secondsEl=document.getElementById("seconds");

const countdownInterval = setInterval(()=>{
 const now = Date.now();
 const diff = target - now;
 if(diff <= 0){ clearInterval(countdownInterval); fadeToBirthday(); return; }
 const d = Math.floor(diff/(1000*60*60*24));
 const h = Math.floor((diff%(1000*60*60*24))/(1000*60*60));
 const m = Math.floor((diff%(1000*60*60))/(1000*60));
 const s = Math.floor((diff%(1000*60))/1000);
 daysEl.textContent = d.toString().padStart(2,'0');
 hoursEl.textContent = h.toString().padStart(2,'0');
 minutesEl.textContent = m.toString().padStart(2,'0');
 secondsEl.textContent = s.toString().padStart(2,'0');
},1000);

// ---------------- Fade and start Birthday ----------------
function fadeToBirthday(){
  const content=document.getElementById("content");
  content.style.transition="opacity 1s ease";
  content.style.opacity=0;
  setTimeout(startBirthday,1000);
}

// ---------------- Birthday ----------------
function startBirthday(){
  const countdownMusic = document.getElementById("bgmCountdown");
  countdownMusic.pause(); countdownMusic.currentTime=0;

  const birthdayMusic = document.getElementById("bgmBirthday");
  birthdayMusic.play().catch(()=>{});

  const content = document.getElementById("content");
  content.innerHTML=`
    <h1>💖 Happy Birthday, Dear Nirmala 💖</h1>
    <h2>Shine Bright Always! ✨🎉</h2>
    <p>Dear Nirmala, today is your special day! 🌟 May your smile light up every corner of the world,  
       may laughter and joy follow you wherever you go, and may all your dreams turn into reality 💫.</p>
    <p>On this magical day, may happiness surround you, your heart be filled with love,  
       and every moment be more beautiful than the last. 💖🎂</p>
    <p class="gift">🎁 Your Special Gift: Premium surprise — A token of love and appreciation 💝</p>
    <p>With endless love, hugs, and blessings — Have the happiest birthday ever!</p>
  `;
  content.style.opacity=1;

  // show final overlay with message
  const overlay = document.getElementById("finalOverlay");
  overlay.style.display = "block";

  // start heart & confetti & fireworks more actively
  startConfettiBurst();
}

// ---------------- Auto Play Countdown Music ----------------
const countdownMusic = document.getElementById("bgmCountdown");
window.addEventListener("load", ()=>{
  countdownMusic.play().catch(()=>{
    // if autoplay is blocked, show button
    document.getElementById("playMusicBtn").style.display="block";
  });
});
document.getElementById("playMusicBtn").addEventListener("click", ()=>{
  countdownMusic.play().catch(()=>{});
  document.getElementById("playMusicBtn").style.display="none";
});

// ---------------- Hearts ----------------
function createHeart(){
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=Math.random()*100+"vw";
  h.style.animationDuration=3+Math.random()*4+"s";
  document.getElementById("hearts").appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(createHeart,400);

// ---------------- Confetti ----------------
function createConfetti(){
  const colors=["#ff66b3","#ffd700","#ff80c1","#6a82fb","#fc5c7d"];
  const confetti=document.createElement("div");
  confetti.className="confetti-piece";
  confetti.style.background=colors[Math.floor(Math.random()*colors.length)];
  confetti.style.left=Math.random()*100+"vw";
  confetti.style.top="-10px";
  document.body.appendChild(confetti);
  let fall=0;
  const fallInterval=setInterval(()=>{
    fall+=5+Math.random()*5;
    confetti.style.top=fall+"px";
    confetti.style.transform=`rotate(${fall*3}deg)`;
    if(fall>window.innerHeight){confetti.remove();clearInterval(fallInterval);}
  },30);
}
setInterval(createConfetti,200);

// extra confetti burst when birthday starts
function startConfettiBurst(){
  for(let i=0;i<50;i++){ setTimeout(createConfetti, i*60); }
}

// ---------------- Fireworks ----------------
const canvas=document.getElementById("fireworks"),ctx=canvas.getContext("2d");
let w,h;
function resize(){w=canvas.width=innerWidth;h=canvas.height=innerHeight;}
window.addEventListener("resize",resize);resize();

let fireworks=[];
class Firework{
  constructor(){
    this.x=Math.random()*w;
    this.y=h;
    this.ty=Math.random()*h*0.5;
    this.color=`hsl(${Math.random()*360},100%,60%)`;
    this.speed=4+Math.random()*3;
    this.parts=[];
  }
  explode(){
    for(let i=0;i<50;i++){
      const angle = Math.random()*Math.PI*2;
      const speed = Math.random()*4+1;
      this.parts.push({x:this.x,y:this.y,vx:Math.cos(angle)*speed,vy:Math.sin(angle)*speed,a:1,color:this.color});
    }
  }
  update(){
    if(this.y>this.ty)this.y-=this.speed;
    else if(!this.parts.length)this.explode();
    this.parts.forEach(p=>{p.x+=p.vx;p.y+=p.vy;p.vy+=0.05;p.a-=0.01;});
    this.parts=this.parts.filter(p=>p.a>0);
  }
  draw(){
    if(this.parts.length===0){
      ctx.beginPath();ctx.fillStyle=this.color;ctx.arc(this.x,this.y,3,0,Math.PI*2);ctx.fill();
    }
    this.parts.forEach(p=>{
      ctx.globalAlpha = p.a;
      ctx.fillStyle = p.color;
      ctx.beginPath();ctx.arc(p.x,p.y,2,0,Math.PI*2);ctx.fill();
      ctx.globalAlpha = 1;
    });
  }
}
function animate(){
  ctx.fillStyle="rgba(0,0,0,0.2)";ctx.fillRect(0,0,w,h);
  if(Math.random()<0.03)fireworks.push(new Firework());
  fireworks.forEach((f,i)=>{
    f.update();f.draw();
    if(f.parts.length===0 && f.y<=f.ty) fireworks.splice(i,1);
  });
  requestAnimationFrame(animate);
}
animate();

// ---------------- Final overlay close ----------------
document.getElementById("closeOverlay").addEventListener("click", ()=>{
  document.getElementById("finalOverlay").style.display = "none";
});
</script>
</body>
</html>
