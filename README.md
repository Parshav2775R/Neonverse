
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NEONVERSE | TechNeon Studio</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;background:#080b16;color:#fff;
 font-family:Arial,sans-serif;
}
header{
 padding:22px 18px;
 background:linear-gradient(120deg,#101b38,#241044);
 border-bottom:1px solid #27345c;
}
.logo{color:#43d9ff;font-size:25px;font-weight:bold}
.sub{color:#aebbd3;font-size:12px;margin-top:5px}
main{max-width:850px;margin:auto;padding:20px}
.hero{
 padding:25px 18px;border-radius:16px;
 background:linear-gradient(135deg,#14264b,#291446);
 margin-bottom:20px;
}
h1{font-size:29px;margin:0 0 10px}
p{color:#bdc8df;line-height:1.6}
.card{
 background:#11182a;border:1px solid #283654;
 border-radius:14px;padding:18px;margin:15px 0;
}
h2{font-size:19px;color:#54dfff}
button{
 background:#1769d2;color:white;border:0;
 padding:12px 17px;border-radius:9px;
 font-weight:bold;cursor:pointer;margin:5px 3px;
}
button:hover{background:#2789ff}
.option{
 display:block;width:100%;text-align:left;
 background:#202c45;margin:9px 0;
}
.stat{color:#54dfff;font-weight:bold}
footer{text-align:center;padding:25px;color:#8493b1;font-size:12px}
#storyText{min-height:65px}
</style>
</head>
<body>

<header>
 <div class="logo">✦ NEONVERSE</div>
 <div class="sub">AN INTERACTIVE UNIVERSE BY TECHNEON STUDIO</div>
</header>

<main>
 <section class="hero">
  <h1>ENTER THE UNKNOWN.</h1>
  <p>A new world. Hidden mysteries. Your choices decide what happens next.</p>
  <button onclick="startStory()">Start Your Journey</button>
 </section>

 <section class="card">
  <h2>PLAYER PROFILE</h2>
  <p>Explorer Level: <span class="stat" id="level">1</span></p>
  <p>Total XP: <span class="stat" id="xp">0</span></p>
  <p>Completed Missions: <span class="stat" id="missions">0</span></p>
 </section>

 <section class="card">
  <h2>DAILY MYSTERY</h2>
  <p>What can reveal a hidden message inside a computer file?</p>
  <button class="option" onclick="answer(0)">A. Background colour</button>
  <button class="option" onclick="answer(1)">B. Metadata</button>
  <button class="option" onclick="answer(2)">C. Screen brightness</button>
  <p id="result"></p>
 </section>

 <section class="card" id="story">
  <h2>STORY MODE</h2>
  <p id="storyText">A strange signal has appeared on your screen. Are you ready to investigate?</p>
  <div id="choices">
   <button onclick="startStory()">Begin Story</button>
  </div>
 </section>

 <section class="card">
  <h2>YOUR MISSION</h2>
  <p>Explore the universe, solve mysteries and discover hidden stories.</p>
  <p class="stat">More missions coming soon...</p>
 </section>
</main>

<footer>
 © 2026 TechNeon Studio | NEONVERSE
</footer>

<script>
let xp=Number(localStorage.getItem("nv_xp"))||0;
let missions=Number(localStorage.getItem("nv_missions"))||0;
let answered=localStorage.getItem("nv_answered")==="true";

function update(){
 document.getElementById("xp").textContent=xp;
 document.getElementById("missions").textContent=missions;
 document.getElementById("level").textContent=Math.floor(xp/100)+1;
 localStorage.setItem("nv_xp",xp);
 localStorage.setItem("nv_missions",missions);
}
function answer(n){
 const r=document.getElementById("result");
 if(answered){r.textContent="You have already completed today's question.";return;}
 if(n===1){
  xp+=20;missions++;
  r.textContent="Correct! You earned 20 XP.";
 }else{
  r.textContent="Not quite! The correct answer is Metadata.";
 }
 answered=true;
 localStorage.setItem("nv_answered","true");
 update();
}
function startStory(){
 document.getElementById("storyText").textContent=
 "Chapter 1: The Unknown Signal. Your device receives a mysterious message. What will you do?";
 document.getElementById("choices").innerHTML=
 '<button onclick="choice(1)">Investigate the signal</button>'+
 '<button onclick="choice(2)">Ignore the message</button>';
}
function choice(n){
 const t=document.getElementById("storyText");
 if(n===1){
  t.textContent="You follow the signal and discover a mysterious symbol. The real adventure has just begun!";
 }else{
  t.textContent="You ignore the message, but a new signal appears. This mystery is not over yet!";
 }
 document.getElementById("choices").innerHTML=
 '<button onclick="finishStory()">Complete Mission</button>';
}
function finishStory(){
 xp+=10;missions++;
 update();
 document.getElementById("storyText").textContent=
 "Mission complete! You earned 10 XP. More adventures await.";
 document.getElementById("choices").innerHTML=
 '<button onclick="startStory()">Play Again</button>';
}
update();
</script>
</body>
</html>
