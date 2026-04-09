<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Công cụ copy mã</title>

<style>

body{
font-family:Arial;
margin:20px;
}

.main{
display:flex;
gap:40px;
align-items:flex-start;
}

.left{
width:400px;
}

textarea{
width:100%;
height:200px;
}

table{
border-collapse:collapse;
}

td{
border:1px solid black;
padding:5px;
text-align:center;
cursor:pointer;
}

.colA{
width:5cm;
}

.colB{
width:4cm;
}

.active{
background:#2196F3;
color:white;
}

</style>

</head>

<body>

<div class="main">

<div class="left">

<h3>Dán dữ liệu Excel</h3>

<textarea id="input"></textarea>
<br><br>

<button onclick="render()">Hiển thị</button>

</div>

<div class="right">

<table id="table"></table>

</div>

</div>

<script>

let lastCell=null;

function render(){

let text=document.getElementById("input").value.trim();
let rows=text.split(/\r?\n/);

let html="";

for(let i=0;i<rows.length;i++){

let cell=rows[i].split(/\t/);

html+="<tr>";

html+=`<td class="colA" onclick="copy(this,'${cell[0]||""}')">${cell[0]||""}</td>`;
html+=`<td class="colB" onclick="copy(this,'${cell[1]||""}')">${cell[1]||""}</td>`;

html+="</tr>";

}

document.getElementById("table").innerHTML=html;

}

function copy(el,text){

if(!text) return;

navigator.clipboard.writeText(text);

if(lastCell){
lastCell.classList.remove("active");
}

el.classList.add("active");

lastCell=el;

}

</script>

</body>
</html>
