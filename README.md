<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Sheep Farm Simulator</title>

<style>
body{
    font-family:Arial,sans-serif;
    background:#e8f5e9;
    padding:15px;
    max-width:700px;
    margin:auto;
}

h1{
    text-align:center;
}

.card{
    background:white;
    padding:12px;
    margin:10px 0;
    border-radius:10px;
    box-shadow:0 0 5px rgba(0,0,0,.15);
}

button{
    padding:10px;
    margin:5px;
    font-size:16px;
}

#log{
    height:220px;
    overflow:auto;
    background:#fafafa;
}
</style>
</head>

<body>

<h1>🐑 Sheep Farm Simulator</h1>

<div class="card">
<h3>Stats</h3>

<p>💰 Money: <span id="money"></span> som</p>
<p>🐑 Lambs: <span id="lambs"></span></p>
<p>🐏 Rams: <span id="rams"></span></p>
<p>🌾 Intakes: <span id="food"></span></p>
<p>👨‍🌾 Workers: <span id="workers"></span></p>
<p>📅 Month: <span id="month"></span></p>
</div>

<div class="card">
<h3>Market</h3>

<button onclick="buyLamb()">Buy Lamb (2M)</button>
<button onclick="buyFood()">Buy Intake (500K)</button>
<button onclick="sellRam()">Sell Ram (5M)</button>
</div>

<div class="card">
<h3>Workers</h3>

<button onclick="hireWorker()">Hire Worker</button>
</div>

<div class="card">
<h3>Time</h3>

<button onclick="nextMonth()">Next Month</button>
</div>

<div class="card">
<h3>Farm Report</h3>
<div id="log"></div>
</div>

<script>

let money = 10000000;

let lambs = [];
let rams = 0;
let food = 0;
let workers = 0;
let month = 1;

function updateUI(){

document.getElementById("money").innerText =
money.toLocaleString();

document.getElementById("lambs").innerText =
lambs.length;

document.getElementById("rams").innerText =
rams;

document.getElementById("food").innerText =
food;

document.getElementById("workers").innerText =
workers;

document.getElementById("month").innerText =
month;

}

function log(text){

document.getElementById("log").innerHTML =
text + "<br>" +
document.getElementById("log").innerHTML;

}

function buyLamb(){

if(money < 2000000){
log("❌ Not enough money.");
return;
}

money -= 2000000;

lambs.push({
age:0
});

log("🐑 Bought 1 lamb.");

updateUI();
}

function buyFood(){

if(money < 500000){
log("❌ Not enough money.");
return;
}

money -= 500000;
food++;

log("🌾 Bought 1 intake.");

updateUI();
}

function sellRam(){

if(rams <= 0){
log("❌ No ram to sell.");
return;
}

rams--;
money += 5000000;

log("🐏 Sold 1 ram.");

updateUI();
}

function hireWorker(){

if(money < 5000000){
log("❌ Need 5M cash.");
return;
}

workers++;

log("👨‍🌾 Worker hired.");

updateUI();
}

function nextMonth(){

month++;

let fed = 0;
let newRams = 0;

for(let i=lambs.length-1;i>=0;i--){

if(food <= 0)
break;

food--;
fed++;

lambs[i].age++;

if(lambs[i].age >= 4){

lambs.splice(i,1);

rams++;
newRams++;
}
}

let salary = workers * 5000000;

money -= salary;

log(
"📅 Month " + month +
"<br>🌾 Intakes used: " + fed +
"<br>🐏 New Rams: " + newRams +
"<br>💵 Salaries: -" +
salary.toLocaleString()
);

updateUI();
}

updateUI();

log("🐑 Welcome to Sheep Farm Simulator!");

</script>

</body>
</html>
