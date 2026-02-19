<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Brother</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:sans-serif;}
body{overflow:hidden;color:white;text-align:center;background:black;}

/* Pages */
.page{
  position:absolute;
  width:100%;
  height:100vh;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  opacity:0;
  transform:scale(0.8);
  transition:0.7s;
  pointer-events:none;   /* IMPORTANT FIX */
}

.page.active{
  opacity:1;
  transform:scale(1);
  pointer-events:auto;   /* Only active page clickable */
}

img{
  width:260px;
  max-width:80%;
  border-radius:20px;
  margin:10px;
  box-shadow:0 10px 30px rgba(0,0,0,0.6);
}

button{
  padding:12px 25px;
  margin:10px;
  border:none;
  border-radius:30px;
  background:#ff2e63;
  color:white;
  font-size:16px;
  cursor:pointer;
  transition:0.3s;
}
button:hover{transform:scale(1.1);background:#ff0055;}

h1{margin-bottom:20px;font-size:26px;}

/* Typing Effect */
.typing{
  font-size:22px;
  border-right:2px solid white;
  white-space:nowrap;
  overflow:hidden;
  width:0;
  animation:typing 4s steps(40,end) forwards, blink 1s infinite;
}
@keyframes typing{to{width:100%;}}
@keyframes blink{50%{border-color:transparent;}}

/* Balloons */
.balloon{
  position:absolute;
  bottom:-100px;
  width:40px;
  height:60px;
  border-radius:50%;
  animation:float 10s linear infinite;
}
@keyframes float{
  from{transform:translateY(0);}
  to{transform:translateY(-110vh);}
}

/* Hearts */
.heart{
  position:absolute;
  animation:fall 5s linear infinite;
}
@keyframes fall{
  from{transform:translateY(-10vh);}
  to{transform:translateY(110vh);}
}

/* Fireworks */
canvas{
  position:fixed;
  top:0;
  left:0;
  z-index:-1;
}
</style>
</head>

<body>

<canvas id="fireworks"></canvas>

<!-- PAGE 1 -->
<div id="page1" class="page active">
  <h1>🎉 Happy Birthday Brother 🎂</h1>
  <div class="typing">You are  hero  ❤️</div>
  <img src="bro1.jpg.jpeg">
  <button onclick="playMusic(1)">▶ Play Song</button>
  <button onclick="nextPage(2)">Next ➜</button>
  <audio id="audio1" src="song1.mp3.mp3"></audio>
</div>

<!-- PAGE 2 -->
<div id="page2" class="page">
  <h1>💙 Memories 💙</h1>
  <img src="bro2.jpg.jpeg">
  <img src="bro3.jpg.jpeg">
  <img src="bro4.jpg.jpeg">
  <button onclick="playMusic(2)">▶ Play Song</button>
  <button onclick="nextPage(3)">Next ➜</button>
  <audio id="audio2" src="song2.mp3.mp3"></audio>
</div>

<!-- PAGE 3 -->
<div id="page3" class="page">
  <h1>🌟 Best Brother Forever 🌟</h1>
  <img src="bro5.jpg.jpeg">
  <button onclick="playMusic(3)">▶ Play Song</button>
  <audio id="audio3" src="song3.mp3.mp3"></audio>
</div>

<script>
/* MUSIC CONTROL */
function playMusic(num){
  stopAll();
  document.getElementById("audio"+num).play();
}

function stopAll(){
  for(let i=1;i<=3;i++){
    let a=document.getElementById("audio"+i);
    a.pause();
    a.currentTime=0;
  }
}

/* FIXED NEXT BUTTON */
function nextPage(page){
  stopAll();
  document.querySelectorAll(".page").forEach(p=>{
    p.classList.remove("active");
  });
  document.getElementById("page"+page).classList.add("active");
}

/* Balloons */
for(let i=0;i<10;i++){
  let b=document.createElement("div");
  b.className="balloon";
  b.style.left=Math.random()*100+"vw";
  b.style.background=`hsl(${Math.random()*360},70%,60%)`;
  b.style.animationDuration=(5+Math.random()*5)+"s";
  document.body.appendChild(b);
}

/* Heart Rain */
setInterval(()=>{
  let h=document.createElement("div");
  h.className="heart";
  h.innerHTML="💖";
  h.style.left=Math.random()*100+"vw";
  h.style.fontSize=(15+Math.random()*20)+"px";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),5000);
},300);

/* Fireworks */
const canvas=document.getElementById("fireworks");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;

function firework(){
  let x=Math.random()*canvas.width;
  let y=Math.random()*canvas.height/2;
  for(let i=0;i<50;i++){
    let angle=Math.random()*2*Math.PI;
    let speed=Math.random()*4;
    let dx=Math.cos(angle)*speed;
    let dy=Math.sin(angle)*speed;
    ctx.fillStyle=`hsl(${Math.random()*360},100%,50%)`;
    ctx.fillRect(x+dx*10,y+dy*10,3,3);
  }
}
setInterval(firework,800);
</script>

</body>
</html>
