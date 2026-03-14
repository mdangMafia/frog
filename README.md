<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cam Iu Fireworks</title>

<style>
body{
margin:0;
background:black;
overflow:hidden;
font-family:Arial;
}

canvas{
position:absolute;
top:0;
left:0;
}

.text{
position:absolute;
top:50%;
left:50%;
transform:translate(-50%,-50%);
font-size:80px;
color:#ff6b81;
text-shadow:0 0 20px red,0 0 40px pink;
opacity:0.15;
}
</style>
</head>

<body>

<div class="text">CAM IU 🍊</div>
<canvas id="c"></canvas>

<script>

const canvas=document.getElementById("c");
const ctx=canvas.getContext("2d");

canvas.width=window.innerWidth;
canvas.height=window.innerHeight;

let particles=[];
let targets=[];

const textCanvas=document.createElement("canvas");
const tctx=textCanvas.getContext("2d");

textCanvas.width=canvas.width;
textCanvas.height=canvas.height;

tctx.fillStyle="white";
tctx.font="bold 160px Arial";
tctx.textAlign="center";
tctx.fillText("CAM IU",canvas.width/2,canvas.height/2);

const data=tctx.getImageData(0,0,canvas.width,canvas.height).data;

for(let y=0;y<canvas.height;y+=6){
for(let x=0;x<canvas.width;x+=6){

let index=(y*canvas.width+x)*4;

if(data[index+3]>150){
targets.push({x:x,y:y});
}

}
}

targets.forEach(t=>{

particles.push({
x:Math.random()*canvas.width,
y:Math.random()*canvas.height,
tx:t.x,
ty:t.y,
vx:(Math.random()-0.5)*10,
vy:(Math.random()-0.5)*10
});

});

function draw(){

ctx.fillStyle="rgba(0,0,0,0.2)";
ctx.fillRect(0,0,canvas.width,canvas.height);

particles.forEach(p=>{

let dx=p.tx-p.x;
let dy=p.ty-p.y;

p.vx+=dx*0.01;
p.vy+=dy*0.01;

p.vx*=0.92;
p.vy*=0.92;

p.x+=p.vx;
p.y+=p.vy;

ctx.fillStyle="hsl("+Math.random()*360+",100%,60%)";
ctx.fillRect(p.x,p.y,2,2);

});

requestAnimationFrame(draw);

}

draw();

</script>

</body>
</html>