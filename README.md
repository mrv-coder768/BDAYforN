<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nirmala Birthday 💜</title>

<style>
html,body{
  margin:0;
  padding:0;
  min-height:100%;
  overflow-x:hidden;
  overflow-y:auto;
  font-family:Arial, sans-serif;
  background:radial-gradient(circle at bottom,#1e1e2f,#0a0a15);
  color:white;
  text-align:center;
}

/* Content */
.content{
  max-width:700px;
  margin:auto;
  padding:20px;
  position:relative;
  z-index:2;
}

h1{
  color:#ad7eff;
  margin-bottom:10px;
}

/* Countdown */
.countdown{
  display:flex;
  justify-content:center;
  gap:15px;
  flex-wrap:wrap;
}

.time-box{
  background:#6a82fb;
  padding:15px 20px;
  border-radius:15px;
}

.time-box span{
  font-size:2em;
  font-weight:bold;
}

/* Buttons */
button{
  margin-top:15px;
  padding:10px 22px;
  border:none;
  border-radius:25px;
  background:#ff66b3;
  color:white;
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
  width:16px;
  height:16px;
  background:#ff80c1;
  clip-path:polygon(50% 0%,61% 15%,75% 15%,85% 25%,85% 40%,50% 75%,15% 40%,15% 25%,25% 15%,39% 15%);
  animation:float 5s linear infinite;
}

@keyframes float{
  to{transform:translateY(-100vh);opacity:0;}
}

/* Birthday */
#birthdayContent{display:none;}

.birthdayPhoto{
  width:220px;
  height:220px;
  object-fit:cover;
  border-radius:15px;
  margin:15px auto;
  display:block;
  box-shadow:0 0 20px rgba(255,102,179,.6);
}

/* Video */
.birthdayVideo{
  width:100%;
  max-width:480px;
  display:block;
  margin:20px auto 40px;
  border-radius:15px;
  background:black;
}

/* 🎁 Ticket Gift */
#ticketGift{
  margin-top:25px;
  cursor:pointer;
}

#ticketGift span{
  font-size:70px;
  display:inline-block;
  animation:bounce 1.6s infinite;
}

@keyframes bounce{
  0%,100%{transform:translateY(0);}
  50%{transform:translateY(-14px);}
}

#ticketArea{
  display:none;
  margin-top:25px;
}

#ticketImage{
  width:100%;
  max-width:600px;
  border-radius:18px;
  box-shadow:0 0 30px rgba(123,44,255,.6);
}

/* 💜 Ticket Message */
.ticketMessage{
  margin-top:18px;
  padding:16px 20px;
  background:rgba(255,255,255,0.08);
  border-radius:14px;
  font-size:15px;
  line-height:1.7;
  box-shadow:0 0 15px rgba(173,126,255,.4);
  min-height:120px;
}
</style>
</head>

<body>

<div class="hearts" id="hearts"></div>

<!-- COUNTDOWN -->
<div class="content" id="countdownContent">
  <h1>🎂 Countdown to Nirmala’s Birthday 💜</h1>

  <div class="countdown">
    <div class="time-box"><span id="days">00</span><div>Days</div></div>
    <div class="time-box"><span id="hours">00</span><div>Hours</div></div>
    <div class="time-box"><span id="minutes">00</span><div>Minutes</div></div>
    <div class="time-box"><span id="seconds">00</span><div>Seconds</div></div>
  </div>

  <button id="playMusicCountdown">🔊 Play Music</button>
</div>

<!-- BIRTHDAY -->
<div class="content" id="birthdayContent">
  <h1>💜 Happy Birthday Nirmala 🎂</h1>

  <p>
This is a small delayed gift and a big wish......
  </p>

  <img src="n.jpeg" class="birthdayPhoto" alt="Nirmala">

  <!-- 🎁 TICKET GIFT -->
  <div id="ticketGift">
    <span>🎁</span>
    <p>Open your special gift</p>
  </div>

  <!-- TICKET -->
  <div id="ticketArea">
    <img src="ticket.jpeg" id="ticketImage" alt="BTS Ticket">

    <div class="ticketMessage" id="ticketMessage"></div>

    <button onclick="downloadTicket()">⬇️ Download Ticket</button>
  </div>

  <button id="playMusicBirthday">🎶 Play Birthday Song</button>

  <video class="birthdayVideo" controls>
    <source src="video.mp4" type="video/mp4">
  </video>
</div>

<!-- MUSIC -->
<audio id="musicCountdown" loop>
  <source src="cd.mp3" type="audio/mp3">
</audio>

<audio id="musicBirthday" loop>
  <source src="micro.mp3" type="audio/mp3">
</audio>

<!-- 🎵 Ticket Song -->
<audio id="ticketSong" loop>
  <source src="ticket-song.mp3" type="audio/mp3">
</audio>

<script>
/* Countdown */
const target = new Date("2026-01-16T00:00:00").getTime();

const d=document.getElementById("days"),
h=document.getElementById("hours"),
m=document.getElementById("minutes"),
s=document.getElementById("seconds");

const timer=setInterval(()=>{
  const diff=target-Date.now();
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
const ts=document.getElementById("ticketSong");

document.getElementById("playMusicCountdown").onclick=()=>mc.play();
document.getElementById("playMusicBirthday").onclick=()=>mb.play();

/* Show birthday */
function showBirthday(){
  document.getElementById("countdownContent").style.display="none";
  document.getElementById("birthdayContent").style.display="block";
  mc.pause();
  mb.play().catch(()=>{});
}

/* Hearts */
function heart(){
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=Math.random()*100+"vw";
  h.style.animationDuration=3+Math.random()*4+"s";
  document.getElementById("hearts").appendChild(h);
  setTimeout(()=>h.remove(),6000);
}
setInterval(heart,400);

/* 🎁 Ticket logic */
const messageLines=[
  "💜 Dear Nirmala 💜",
  "This ticket is not just a picture.",
  "It is a promise.",
  "One day you WILL attend a real BTS concert,",
  "hear ARMY chants live,",
  "and feel this dream come true 🌟",
  "Until then — keep believing.",
  "ARMY forever 💜",
  "WAITING FOR 16-JAN-2027"
];

document.getElementById("ticketGift").onclick=()=>{
  document.getElementById("ticketGift").style.display="none";
  document.getElementById("ticketArea").style.display="block";
  mb.pause();
  ts.play().catch(()=>{});
  typeMessage();
};

function typeMessage(){
  const box=document.getElementById("ticketMessage");
  let line=0, char=0;
  box.innerHTML="";

  const typer=setInterval(()=>{
    if(line>=messageLines.length){
      clearInterval(typer);
      return;
    }
    if(char<messageLines[line].length){
      box.innerHTML+=messageLines[line].charAt(char);
      char++;
    }else{
      box.innerHTML+="<br>";
      line++;
      char=0;
    }
  },40);
}

function downloadTicket(){
  const img=document.getElementById("ticketImage");
  const canvas=document.createElement("canvas");
  const ctx=canvas.getContext("2d");
  canvas.width=img.naturalWidth;
  canvas.height=img.naturalHeight;
  ctx.drawImage(img,0,0);
  const a=document.createElement("a");
  a.download="Nirmala_BTS_Ticket.png";
  a.href=canvas.toDataURL("image/png");
  a.click();
}
</script>

</body>
</html>
