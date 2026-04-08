<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Bảng mã</title>

<style>

body{
font-family: Arial;
display:flex;
flex-direction:column;
align-items:center;
margin-top:40px;
}

textarea{
width:420px;
height:120px;
margin-bottom:15px;
}

table{
border-collapse:collapse;
margin-top:20px;
}

td{
border:1px solid black;
padding:4px;
text-align:center;
cursor:pointer;
}

.colA{
width:5cm;
}

.colB{
width:4cm;
}

.copied{
background:#4CAF50;
color:white;
}

</style>

</head>

<body>

<h3>Dán dữ liệu từ Excel</h3>

<textarea id="input"></textarea>
<br>
<button onclick="render()">Hiển thị</button>

<table id="table"></table>

<script>

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

el.classList.add("copied");

}

</script>

</body>
</html>
