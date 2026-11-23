<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DAQA</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',Tahoma,sans-serif}
body{background:#000;color:#fff;overflow:hidden;height:100vh}
.bg{position:fixed;inset:0;background:url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=1920') center/cover;z-index:0;transition:.5s}
.bg.dim{filter:brightness(.6)}
header{position:fixed;top:0;left:0;right:0;display:flex;justify-content:space-between;align-items:center;padding:14px 20px;z-index:10}
.logo{font-weight:900;font-size:22px;letter-spacing:3px}
.logo span{color:#00e676}
.clock{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);text-align:center;z-index:5;transition:.3s}
.clock .date{font-size:18px;font-weight:600;text-shadow:0 2px 10px #000}
.clock .time{font-size:110px;font-weight:900;line-height:1;text-shadow:0 5px 25px rgba(0,0,0,.6)}
.widgets{position:fixed;top:200px;left:15px;right:15px;display:flex;justify-content:space-between;z-index:5;direction:ltr}
.batt{font-size:13px;font-weight:700;text-shadow:0 2px 8px #000}
.batt .bar{width:90px;height:5px;background:rgba(255,255,255,.3);border-radius:10px;margin-top:5px;overflow:hidden}
.batt .fill{width:94%;height:100%;background:#fff}
.temp{font-size:13px;font-weight:700;text-align:center;text-shadow:0 2px 8px #000}
.temp b{font-size:22px}
.hint{position:fixed;bottom:90px;left:0;right:0;text-align:center;z-index:6;font-size:12px;background:rgba(0,0,0,.45);width:fit-content;margin:auto;padding:6px 14px;border-radius:20px}
.btns{position:fixed;bottom:20px;left:15px;right:15px;display:flex;gap:10px;z-index:6}
.btns button{flex:1;padding:13px;border-radius:25px;border:none;font-weight:900;cursor:pointer}
.btns button:first-child{background:#ff3b30;color:#fff}
.btns button:last-child{background:#fff;color:#000}
</style>
</head>
<body>
<div class="bg" id="bg"></div>
<header><div class="logo"><span>دقة</span> DAQA</div><div>🔍 &nbsp; ↗</div></header>
<div class="widgets"><div class="batt">🔋 94%<br>Battery Level<div class="bar"><div class="fill"></div></div></div><div class="temp">🕐<br><b>29°</b><br>26&nbsp;&nbsp;30</div></div>
<div class="clock" id="clock"><div class="date" id="date"></div><div class="time" id="time"></div></div>
<div class="hint" id="hint">كليك يخفي / دبل كليك الساعة قدام وورا</div>
<div class="btns"><button onclick="changeBg()">خلفية عشوائية 🔄</button><button onclick="downloadBg()">تنزيل ⬇</button></div>
<script>
const imgs=["https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=1920","https://images.unsplash.com/photo-1469474968028-56623f02e42e?w=1920","https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=1920","https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?w=1920","https://images.unsplash.com/photo-1503376780353-7e6692767b70?w=1920","https://images.unsplash.com/photo-1503376780353-7e6692767b70?w=1920"];
let cur=0;
function changeBg(e){if(e) e.stopPropagation();cur=(cur+1)%imgs.length;document.getElementById('bg').style.backgroundImage=`url('${imgs[cur]}')`}
function downloadBg(e){if(e) e.stopPropagation();let a=document.createElement('a');a.href=imgs[cur];a.target='_blank';a.click()}
let clickTimer=null;
document.body.addEventListener('click',()=>{
  if(clickTimer){clearTimeout(clickTimer);clickTimer=null;let c=document.getElementById('clock');c.style.zIndex=c.style.zIndex=='0'?'5':'0';return}
  clickTimer=setTimeout(()=>{clickTimer=null;let c=document.getElementById('clock');c.style.opacity=c.style.opacity=='0'?'1':'0'},250);
});
function clock(){let n=new Date();document.getElementById('time').textContent=String(n.getHours()).padStart(2,'0')+':'+String(n.getMinutes()).padStart(2,'0');document.getElementById('date').textContent=n.toLocaleDateString('en-US',{weekday:'long',day:'numeric',month:'long'})}
setInterval(clock,1000);clock();
</script>
</body>
</html>
