<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Hiển thị mã</title>

<style>

body{
font-family: Arial;
display:flex;
flex-direction:column;
align-items:center;
margin-top:40px;
}

textarea{
width:400px;
height:120px;
margin-bottom:15px;
}

.container{
display:flex;
flex-direction:column;
gap:8px;
align-items:center;
}

.row{
display:flex;
gap:10px;
}

.cell{
border:1px solid black;
text-align:center;
cursor:pointer;
padding:4px;
}

.row1 .cell{
width:5cm;
}

.row2 .cell{
width:4cm;
}

</style>

</head>

<body>

<h3>Dán dữ liệu Excel</h3>

<textarea id="input"></textarea>
<br>
<button onclick="render()">Hiển thị</button>

<div class="container">
<div class="row row1" id="row1"></div>
<div class="row row2" id="row2"></div>
</div>

<script>

function render(){

let text=document.getElementById("input").value.trim();
let rows=text.split(/\r?\n/);

let r1="";
let r2="";

for(let i=0;i<rows.length;i++){

let cell=rows[i].split(/\t/);

if(cell[0]){
r1+=`<div class="cell" onclick="copyText('${cell[0]}')">${cell[0]}</div>`;
}

if(cell[1]){
r2+=`<div class="cell" onclick="copyText('${cell[1]}')">${cell[1]}</div>`;
}

}

document.getElementById("row1").innerHTML=r1;
document.getElementById("row2").innerHTML=r2;

}

function copyText(text){

navigator.clipboard.writeText(text);
alert("Đã copy: "+text);

}

</script>

</body>
</html>
