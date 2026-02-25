<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mi Baby Shower</title>

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">

<style>
*{margin:0;padding:0;box-sizing:border-box}
body{
font-family:'Poppins',sans-serif;
background:#f9f6f2;
color:#444;
overflow-x:hidden;
}

.section{
min-height:100vh;
display:flex;
align-items:center;
justify-content:center;
flex-direction:column;
padding:30px 15px;
}

.hero{
background:url("https://drive.google.com/uc?export=view&id=1-deP-ALK7zQzw_O3_fYSzuymVDiKvkWX") center/contain no-repeat;
width:100%;
height:100vh;
position:relative;
}

.hero h1{
position:absolute;
bottom:15%;
width:100%;
text-align:center;
font-family:'Playfair Display';
font-size:2.4rem;
}

.hero h2{
position:absolute;
bottom:9%;
width:100%;
text-align:center;
font-size:1.1rem;
}

.envelope{
position:fixed;
inset:0;
background:linear-gradient(135deg,#fbd3e9,#cce7ff);
display:flex;
align-items:center;
justify-content:center;
z-index:9999;
}

.card{
padding:25px 40px;
background:white;
border-radius:18px;
box-shadow:0 15px 40px rgba(0,0,0,.15);
font-size:1.2rem;
cursor:pointer;
animation:pulse 1.8s infinite;
}

@keyframes pulse{
0%,100%{transform:scale(1)}
50%{transform:scale(1.05)}
}

.countdown{
font-size:2rem;
font-weight:600;
}

.map iframe{
width:100%;
max-width:500px;
height:300px;
border-radius:15px;
border:none;
}

.itinerary img{
width:100%;
max-width:500px;
border-radius:20px;
}

form{
background:white;
padding:25px;
border-radius:20px;
box-shadow:0 15px 35px rgba(0,0,0,.1);
max-width:420px;
width:100%;
}

input,textarea{
width:100%;
padding:12px;
margin:8px 0;
border-radius:12px;
border:1px solid #ddd;
font-size:1rem;
}

button{
padding:12px;
border:none;
border-radius:14px;
font-size:1rem;
cursor:pointer;
margin-top:10px;
}

.btn{
background:#7fb5ff;
color:white;
}

.btn.red{
background:#ff8080;
}

audio{display:none}
</style>
</head>

<body>

<div class="envelope" id="cover" onclick="abrir()">
<div class="card">Toca para abrir ✨</div>
</div>

<audio id="musica" loop>
<source src="https://drive.google.com/uc?export=download&id=1YEu2P5o-SJsTrNmbzyt80bOTqHEDxHR9">
</audio>

<section class="section hero">
<h1>Mi Baby Shower</h1>
<h2>25 / 04 / 2026</h2>
</section>

<section class="section">
<h2>Faltan</h2>
<div class="countdown" id="timer"></div>
</section>

<section class="section map">
<h2>Ubicación</h2><br>
<iframe src="https://maps.google.com/maps?q=23%20de%20Abril%2058%20San%20Pedro%20Xalpa&t=&z=17&ie=UTF8&iwloc=&output=embed"></iframe>
</section>

<section class="section itinerary">
<h2>Itinerario</h2><br>
<img src="https://drive.google.com/uc?export=view&id=1H7N0MMEmSrqnU4S27ZNAmiErLBBXBc1n">
</section>

<section class="section">
<h2>Confirmación</h2><br>

<form onsubmit="enviar(event)">

<input id="nombre" placeholder="Nombre" required>

<input id="personas" type="number" min="1" placeholder="Personas que asistirán" required>

<textarea id="alergias" placeholder="Alergias / Comentarios"></textarea>

<button class="btn">Confirmar asistencia</button>

<button type="button" class="btn red" onclick="noAsistire()">No podré asistir</button>

</form>
</section>

<script>
const fecha = new Date("2026-04-25T14:30:00");

setInterval(()=>{
const ahora = new Date();
let diff = fecha - ahora;
if(diff<0) return;
let d=Math.floor(diff/86400000);
let h=Math.floor(diff%86400000/3600000);
let m=Math.floor(diff%3600000/60000);
let s=Math.floor(diff%60000/1000);
timer.innerHTML=`${d} días ${h}h ${m}m ${s}s`;
},1000);

function abrir(){
cover.style.display="none";
musica.play();
}

function enviar(e){
e.preventDefault();

let n=nombre.value;
let p=personas.value;
let a=alergias.value;

let msg=`Confirmación Baby Shower\nNombre: ${n}\nPersonas: ${p}\nAlergias: ${a}`;

window.open(`https://api.whatsapp.com/send?phone=5215659859496&text=${encodeURIComponent(msg)}`);

fetch("https://script.google.com/macros/s/AKfycbyNcbx_33z4fMTvcyyHi2ny1CoZB-2C81e8GkY-JIOumyPyp4r3FO4gPno-0dBxPqjR/exec",{
method:"POST",
body:JSON.stringify({nombre:n,personas:p,alergias:a,asistencia:"SI"})
});

alert("¡Gracias por confirmar!");
}

function noAsistire(){
let msg="No podré asistir al Baby Shower 😢";

window.open(`https://api.whatsapp.com/send?phone=5215659859496&text=${encodeURIComponent(msg)}`);

fetch("https://script.google.com/macros/s/AKfycbyNcbx_33z4fMTvcyyHi2ny1CoZB-2C81e8GkY-JIOumyPyp4r3FO4gPno-0dBxPqjR/exec",{
method:"POST",
body:JSON.stringify({nombre:"",personas:0,alergias:"",asistencia:"NO"})
});

alert("Gracias por avisar ❤️");
}
</script>

</body>
</html>
