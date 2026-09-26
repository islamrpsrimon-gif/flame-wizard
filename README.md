<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>Flame Wizard - Final</title>
<style>
body{margin:0;background:#10101d;color:#fff;font-family:sans-serif}
.top{display:flex;justify-content:space-between;padding:12px}
.card{background:linear-gradient(145deg,#2a2a3e,#1a1a2e);border:1px solid #ffcc66;border-radius:12px;padding:10px;text-align:center}
.btn{background:#ffcc66;color:#000;border:none;padding:8px 15px;border-radius:20px;font-weight:bold;cursor:pointer}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;padding:10px}
.wiz{background:#232336;border-radius:10px;padding:8px;text-align:center;border:1px solid #444}
.tabs{display:flex;gap:5px;padding:10px}
.tabs button{flex:1;background:#333;color:#fff;border:none;padding:10px;border-radius:8px}
.active{background:#ffcc66!important;color:#000!important}
.sec{display:none;padding:10px}.show{display:block}
</style>
</head>
<body>
<div class="top">
<div class="card">🔥 Balance: <b id="bal">226</b></div>
<div class="card">💰 Daily: +<b id="dinc">0</b>/day</div>
</div>

<div class="tabs">
<button id="t1" class="active" onclick="tab('m')">Magician</button>
<button id="t2" onclick="tab('d')">Deposit</button>
<button id="t3" onclick="tab('w')">Withdraw</button>
<button id="t4" onclick="tab('p')">Partners</button>
</div>

<div id="m" class="sec show">
<div class="card" style="margin:10px">
<h3>🧙 Wizard Lv 37</h3>
<p style="font-size:24px">🔥 <span id="c">0.7500</span></p>
<button class="btn" onclick="collect()">COLLECT</button>
<p>Magic: <span id="mg">1708</span> 🔮</p>
</div>
<div class="grid" id="g"></div>
<div class="card" style="margin:10px">
<h3>Wizard Shop - Daily 20%</h3>
<div id="shop" style="display:flex;gap:8px;overflow:auto"></div>
</div>
</div>

<div id="d" class="sec"><div class="card">Deposit<br><input id="da" placeholder="Amount" style="width:90%;padding:10px;margin:10px;border-radius:8px"><br><button class="btn" onclick="alert('Deposit Address: TON... Copy করুন')">Get Address</button></div></div>
<div id="w" class="sec"><div class="card">Withdraw<br><input id="wa" placeholder="Min 50 Flame" style="width:90%;padding:10px;margin:10px;border-radius:8px"><input placeholder="Wallet Address" style="width:90%;padding:10px;border-radius:8px"><br><br><button class="btn" onclick="alert('Withdraw Request Sent!')">Withdraw</button></div></div>
<div id="p" class="sec"><div class="card">Invite Friends & Earn 10%<br><br><input value="https://t.me/flamewizard_bd_bot?start=123" style="width:90%;padding:10px" readonly><br><br><p>Level 1: 10% | Level 2: 5% | Level 3: 2%</p></div></div>

<script>
let bal=226, cm=0.75, mg=1708, wiz=[
{c:10,i:2,n:4},{c:25,i:5,n:3},{c:50,i:10,n:3},{c:100,i:20,n:13},{c:250,i:50,n:8},{c:500,i:100,n:3}
];
function render(){
document.getElementById('bal').innerText=bal.toFixed(2);
document.getElementById('c').innerText=cm.toFixed(4);
document.getElementById('mg').innerText=mg;
let g=document.getElementById('g'),s=document.getElementById('shop'),di=0;g.innerHTML='';s.innerHTML='';
wiz.forEach((w,idx)=>{di+=w.n*w.i;g.innerHTML+=`<div class="wiz">🧙<br>${w.n} pcs<br>🔥 +${w.i}<br><button class="btn" style="font-size:11px" onclick="buy(${idx})">Buy 🔥${w.c}</button></div>`;s.innerHTML+=`<div class="wiz">Lv ${idx+1}<br>+${w.i}/day<br><button class="btn" onclick="buy(${idx})">🔥 ${w.c}</button></div>`});
document.getElementById('dinc').innerText=di;
}
function buy(i){if(bal>=wiz[i].c){bal-=wiz[i].c;wiz[i].n++;render()}else alert('Balance কম!')}
function collect(){bal+=cm;cm=0;render()}
function tab(t){document.querySelectorAll('.sec').forEach(e=>e.classList.remove('show'));document.getElementById(t).classList.add('show');document.querySelectorAll('.tabs button').forEach(b=>b.classList.remove('active'));document.getElementById('t'+(t=='m'?1:t=='d'?2:t=='w'?3:4)).classList.add('active')}
setInterval(()=>{let di=0;wiz.forEach(w=>di+=w.n*w.i);cm+=di/86400;document.getElementById('c').innerText=cm.toFixed(4)},1000);
render();
</script>
</body>
</html>
