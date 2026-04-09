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

.colA{ width:5cm; }
.colB{ width:4cm; }

.active{
background:#2196F3;
color:white;
}

.pagination{
margin-top:10px;
}

button{
margin:3px;
}

</style>
</head>

<body>

<div class="main">

<div class="left">
<h3>Dán dữ liệu Excel</h3>
<textarea id="input"></textarea>
<br><br>
<button onclick="loadData()">Hiển thị</button>
</div>

<div class="right">
<table id="table"></table>
<div class="pagination" id="pages"></div>
</div>

</div>

<script>

let data=[];
let page=1;
let rowsPerPage=30;
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

}

function render(){

let start=(page-1)*rowsPerPage;
let end=start+rowsPerPage;

let html="";

for(let i=start;i<end && i<data.length;i++){

html+="<tr>";

html+=`<td class="colA" onclick="copy(this,'${data[i][0]}')">${data[i][0]}</td>`;
html+=`<td class="colB" onclick="copy(this,'${data[i][1]}')">${data[i][1]}</td>`;

html+="</tr>";

}

document.getElementById("table").innerHTML=html;

renderPages();

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
