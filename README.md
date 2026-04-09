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
width:420px;
}

textarea{
width:100%;
height:200px;
}

.controls{
margin-top:10px;
}

table{
border-collapse:collapse;
table-layout:fixed;   /* giữ kích thước cột cố định */
}

td{
border:1px solid black;
padding:5px;
text-align:center;
cursor:pointer;
height:28px;          /* chiều cao cố định */
vertical-align:middle;
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

button{
margin:2px;
}

</style>
</head>

<body>

<div class="main">

<div class="left">

<h3>Dán dữ liệu Excel</h3>

<textarea id="input"></textarea>

<div class="controls">

<button onclick="loadData()">Hiển thị</button>

<span id="pages"></span>

</div>

</div>

<div class="right">

<table id="table"></table>

</div>

</div>

<script>

let data=[];
let page=1;
const rowsPerPage=30;
let lastCell=null;

function loadData(){

let text=document.getElementById("input").value.trim();
let rows=text.split(/\r?\n/);

data=[];

for(let r of rows){
let cell=r.split(/\t/);
data.push([cell[0]||"",cell[1]||""]);
}

page=1;
render();
renderPages();

}

function render(){

let start=(page-1)*rowsPerPage;

let html="";

for(let i=0;i<rowsPerPage;i++){

let index=start+i;

let a="";
let b="";

if(index<data.length){
a=data[index][0];
b=data[index][1];
}

html+="<tr>";
html+=`<td class="colA" onclick="copy(this,'${a}')">${a}</td>`;
html+=`<td class="colB" onclick="copy(this,'${b}')">${b}</td>`;
html+="</tr>";

}

document.getElementById("table").innerHTML=html;

}

function renderPages(){

let total=Math.ceil(data.length/rowsPerPage);

let html="";

for(let i=1;i<=total;i++){
html+=`<button onclick="goPage(${i})">${i}</button>`;
}

document.getElementById("pages").innerHTML=html;

}

function goPage(p){
page=p;
render();
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
