<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Chia dữ liệu Excel thành 2 cột</title>

<style>
body{
font-family: Arial;
margin:20px;
}

textarea{
width:100%;
height:120px;
font-size:14px;
}

button{
margin-top:10px;
padding:8px 15px;
}

.container{
display:flex;
gap:20px;
margin-top:20px;
}

.column{
flex:1;
border:1px solid #333;
padding:10px;
min-height:200px;
background:#f5f5f5;
}
</style>
</head>

<body>

<h3>Dán dữ liệu từ Excel</h3>

<textarea id="inputData" placeholder="Copy từ Excel rồi dán vào đây"></textarea>
<br>
<button onclick="processData()">Hiển thị</button>

<div class="container">
<div class="column" id="col1"></div>
<div class="column" id="col2"></div>
</div>

<script>

function processData(){

let text = document.getElementById("inputData").value.trim();

let rows = text.split(/\r?\n/);

let col1="";
let col2="";

for(let i=0;i<rows.length;i++){

let cells = rows[i].split(/\t/);

if(cells[0]) col1 += cells[0] + "<br>";
if(cells[1]) col2 += cells[1] + "<br>";

}

document.getElementById("col1").innerHTML = col1;
document.getElementById("col2").innerHTML = col2;

}

</script>

</body>
</html>
