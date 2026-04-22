<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>حاسبة هامة ☕</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Segoe UI', Tahoma, sans-serif; background: #111; color: #f0ebe3; min-height: 100vh; padding-bottom: 40px; }
  .header { background: linear-gradient(135deg,#1e0f05,#3d2009); padding: 18px 16px; text-align: center; border-bottom: 2px solid #5a3010; }
  .header h1 { font-size: 19px; color: #d4a96a; margin-top: 4px; }
  .header p { font-size: 11px; color: #8a6040; margin-top: 2px; }
  .tabs { display: flex; background: #181818; border-bottom: 1px solid #222; }
  .tab { flex: 1; padding: 11px 4px; background: transparent; color: #666; border: none; border-bottom: 2px solid transparent; cursor: pointer; font-family: inherit; font-size: 13px; }
  .tab.active { background: #1e0f05; color: #d4a96a; border-bottom: 2px solid #d4a96a; }
  .content { max-width: 500px; margin: 0 auto; padding: 14px; }
  .section { display: none; }
  .section.active { display: block; }
  .card { background: #1c1c1c; border-radius: 10px; padding: 14px; margin-bottom: 12px; }
  .label { color: #8a6040; font-size: 12px; margin-bottom: 6px; }
  input[type=number], input[type=text] { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #444; background: #111; color: #f0ebe3; font-size: 14px; font-family: inherit; }
  .sales-input { font-size: 24px; color: #d4a96a; font-weight: bold; text-align: center; }
  .unit { color: #8a6040; font-size: 14px; white-space: nowrap; }
  .flex { display: flex; gap: 8px; align-items: center; }
  .flex-wrap { display: flex; flex-wrap: wrap; gap: 8px; }
  .stat-card { background: #1c1c1c; border-radius: 10px; padding: 12px 14px; flex: 1; min-width: 110px; }
  .stat-label { font-size: 11px; color: #666; margin-bottom: 3px; }
  .stat-value { font-size: 16px; font-weight: bold; }
  .stat-sub { font-size: 10px; color: #555; margin-top: 2px; }
  .result-box { background: linear-gradient(135deg,#0f1a0f,#162416); border-radius: 10px; padding: 14px; margin-bottom: 12px; border: 1px solid #2a4a2a; }
  .result-title { color: #5a9a5a; font-size: 12px; margin-bottom: 10px; font-weight: bold; }
  .net-profit { background: #0a2a0a; border-radius: 10px; padding: 12px 16px; text-align: center; margin-top: 4px; }
  .net-profit.loss { background: #2a0a0a; }
  .net-profit-label { color: #666; font-size: 12px; margin-bottom: 4px; }
  .net-profit-value { font-size: 26px; font-weight: bold; color: #6dbf6d; }
  .net-profit-value.loss { color: #e05050; }
  .net-profit-margin { color: #555; font-size: 11px; margin-top: 3px; }
  .save-btn { width: 100%; padding: 13px; border-radius: 10px; background: linear-gradient(135deg,#3d2009,#5a3010); border: none; color: #d4a96a; font-size: 15px; cursor: pointer; font-family: inherit; font-weight: bold; }
  .save-btn:disabled { background: #1a1a1a; color: #444; cursor: not-allowed; }
  .saved-msg { text-align: center; color: #6dbf6d; margin-top: 8px; font-size: 13px; display: none; }
  .extra-item { background: #161616; border-radius: 8px; padding: 10px; margin-bottom: 10px; }
  .extra-from { padding: 4px 6px; border-radius: 7px; background: #1a3a1a; color: #6dbf6d; font-size: 11px; text-align: center; margin-top: 6px; }
  .remove-btn { background: #2a1010; border: none; color: #c44; border-radius: 7px; padding: 0 9px; cursor: pointer; font-size: 15px; }
  .add-btn { background: transparent; border: 1px dashed #333; color: #666; border-radius: 8px; padding: 6px 12px; cursor: pointer; font-size: 12px; font-family: inherit; }
  .today-label { text-align: center; color: #5a3010; font-size: 12px; margin-bottom: 10px; }
  .today-label span { color: #a07850; }
  .log-item { background: #1c1c1c; border-radius: 10px; padding: 14px; margin-bottom: 8px; cursor: pointer; border: 1px solid #222; }
  .log-item.open { border-color: #5a3010; }
  .log-row { display: flex; justify-content: space-between; align-items: center; }
  .log-date { color: #8a6040; font-size: 13px; }
  .log-profit { font-weight: bold; font-size: 15px; color: #6dbf6d; }
  .log-profit.loss { color: #e05050; }
  .log-sub { display: flex; justify-content: space-between; margin-top: 5px; }
  .log-detail { margin-top: 10px; border-top: 1px solid #2a2a2a; padding-top: 10px; display: none; }
  .log-detail.open { display: block; }
  .detail-row { display: flex; justify-content: space-between; padding: 4px 0; }
  .detail-key { color: #777; font-size: 13px; }
  .detail-val { font-size: 13px; }
  .summary-card { background: #1c1c1c; border-radius: 10px; padding: 14px; margin-bottom: 14px; }
  .empty { color: #555; text-align: center; margin-top: 40px; }
  .search-input { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #2a2a2a; background: #1c1c1c; color: #ddd; font-size: 14px; margin-bottom: 10px; font-family: inherit; }
  .cat-filters { display: flex; gap: 6px; flex-wrap: wrap; margin-bottom: 12px; }
  .cat-btn { padding: 5px 10px; border-radius: 20px; border: none; background: #1c1c1c; color: #777; cursor: pointer; font-size: 12px; font-family: inherit; }
  .cat-btn.active { background: #5a3010; color: #d4a96a; }
  .prod-header { display: flex; justify-content: space-between; padding: 6px 10px; color: #555; font-size: 11px; margin-bottom: 4px; }
  .prod-item { display: flex; align-items: center; background: #1c1c1c; border-radius: 8px; padding: 9px 10px; margin-bottom: 4px; }
  .prod-name { flex: 3; }
  .prod-name-text { color: #ddd; font-size: 13px; }
  .prod-cat-text { color: #555; font-size: 11px; }
  .prod-col { flex: 1; text-align: center; font-size: 13px; }
  .prod-summary { background: #1e0f05; border-radius: 10px; padding: 14px; margin-top: 12px; display: flex; justify-content: space-around; text-align: center; }
  .prod-stat-label { color: #666; font-size: 11px; }
  .prod-stat-val { color: #d4a96a; font-size: 18px; font-weight: bold; }
</style>
</head>
<body>

<div class="header">
  <div style="font-size:26px">☕</div>
  <h1>حاسبة هامة</h1>
  <p>متوسط هامش الربح: <span style="color:#d4a96a" id="avgMarginDisplay"></span></p>
</div>

<div class="tabs">
  <button class="tab active" onclick="showTab('daily')">📊 اليوم</button>
  <button class="tab" onclick="showTab('history')">📅 السجل</button>
  <button class="tab" onclick="showTab('products')">📦 المنتجات</button>
</div>

<div class="content">

  <!-- DAILY -->
  <div id="tab-daily" class="section active">
    <div class="today-label">📅 اليوم: <span id="todayDisplay"></span> — التاريخ يُحفظ تلقائياً</div>

    <div class="card">
      <div class="label">💰 إجمالي المبيعات</div>
      <div class="flex">
        <input type="number" class="sales-input" id="salesInput" placeholder="0" oninput="updateResult()">
        <span class="unit">ر.س</span>
      </div>
    </div>

    <div class="card">
      <div class="label">💸 مصاريف إضافية</div>
      <div id="extrasList"></div>
      <button class="add-btn" onclick="addExtra()">+ إضافة مصروف</button>
    </div>

    <div class="result-box" id="resultBox" style="display:none">
      <div class="result-title">📊 النتيجة</div>
      <div class="flex-wrap" style="margin-bottom:8px">
        <div class="stat-card"><div class="stat-label">💰 إجمالي المبيعات</div><div class="stat-value" style="color:#d4a96a" id="r-revenue"></div></div>
        <div class="stat-card"><div class="stat-label">📦 رأس المال</div><div class="stat-value" style="color:#e07050" id="r-capital"></div></div>
      </div>
      <div class="flex-wrap" style="margin-bottom:8px">
        <div class="stat-card"><div class="stat-label">📈 الربح الإجمالي</div><div class="stat-value" style="color:#a0cf90" id="r-gross"></div><div class="stat-sub">قبل المصاريف</div></div>
        <div class="stat-card" id="r-extras-card" style="display:none"><div class="stat-label">💸 مصاريف إضافية</div><div class="stat-value" style="color:#e0a050" id="r-extras"></div></div>
      </div>
      <div class="net-profit" id="netBox">
        <div class="net-profit-label">✅ صافي الربح</div>
        <div class="net-profit-value" id="r-net"></div>
        <div class="net-profit-margin">نسبة الربح: <span style="color:#a09fe0" id="r-margin"></span></div>
      </div>
    </div>

    <button class="save-btn" id="saveBtn" onclick="saveDay()" disabled>💾 حفظ اليوم</button>
    <div class="saved-msg" id="savedMsg">✅ تم الحفظ!</div>
  </div>

  <!-- HISTORY -->
  <div id="tab-history" class="section">
    <div id="historyContent"></div>
  </div>

  <!-- PRODUCTS -->
  <div id="tab-products" class="section">
    <input class="search-input" type="text" placeholder="🔍 ابحث عن منتج..." oninput="filterProducts(this.value)">
    <div class="cat-filters" id="catFilters"></div>
    <div class="prod-header">
      <span style="flex:3">المنتج</span>
      <span style="flex:1;text-align:center">التكلفة</span>
      <span style="flex:1;text-align:center">السعر</span>
      <span style="flex:1;text-align:center">الربح</span>
    </div>
    <div id="productsList"></div>
    <div class="prod-summary" id="prodSummary"></div>
  </div>

</div>

<script>
const products = [
  { name:"V60", cat:"مشروبات ساخنة", price:12, cost:3.75 },
  { name:"أمريكانو", cat:"مشروبات ساخنة", price:9, cost:3.35 },
  { name:"إسبريسو", cat:"مشروبات ساخنة", price:8, cost:3.70 },
  { name:"إسبريسو فاخر", cat:"مشروبات ساخنة", price:12, cost:7.75 },
  { name:"أفوكادو إسبريسو", cat:"مشروبات باردة", price:15, cost:9.15 },
  { name:"ايس V60", cat:"مشروبات باردة", price:12, cost:3.80 },
  { name:"ايس أمريكانو", cat:"مشروبات باردة", price:9, cost:3.40 },
  { name:"ايس تي توت", cat:"مشروبات باردة", price:12, cost:3.75 },
  { name:"ايس تي خوخ", cat:"مشروبات باردة", price:12, cost:3.75 },
  { name:"ايس سبانش لاتيه", cat:"مشروبات باردة", price:13, cost:5.35 },
  { name:"ايس كيمكس", cat:"مشروبات باردة", price:11, cost:3.75 },
  { name:"ايس لاتيه", cat:"مشروبات باردة", price:12, cost:4.45 },
  { name:"ايس ماتشا فراولة", cat:"ماتشا", price:18, cost:4.55 },
  { name:"ايس ماتشا فيول", cat:"ماتشا", price:10, cost:4.55 },
  { name:"ايس ماتشا لاتيه", cat:"ماتشا", price:11, cost:4.55 },
  { name:"بودينق شوكولاته", cat:"حلويات", price:9, cost:3.50 },
  { name:"بوكس قهوة 1 لتر (6 أكواب)", cat:"بوكسات", price:38, cost:27 },
  { name:"بوكس قهوة 1.5 لتر (8 أكواب)", cat:"بوكسات", price:46, cost:31 },
  { name:"تشوكلت كيك", cat:"حلويات", price:17, cost:11.50 },
  { name:"تشوكليت تشيزكيك", cat:"حلويات", price:18, cost:11.50 },
  { name:"تشيز كيك المقلوب", cat:"حلويات", price:12, cost:9.50 },
  { name:"تشيز كيك بيكان", cat:"حلويات", price:15, cost:11.50 },
  { name:"تشيز كيك توت", cat:"حلويات", price:15, cost:11.50 },
  { name:"تشيز كيك مدريد", cat:"حلويات", price:16, cost:14.00 },
  { name:"تيراميسو", cat:"حلويات", price:16, cost:14.00 },
  { name:"حلاببسي", cat:"حلويات", price:11, cost:0 },
  { name:"دولتشي كراميل", cat:"حلويات", price:16, cost:12.50 },
  { name:"سبانش لاتيه", cat:"مشروبات ساخنة", price:13, cost:6.30 },
  { name:"شاي", cat:"مشروبات ساخنة", price:3, cost:1.00 },
  { name:"فريدو", cat:"مشروبات باردة", price:10, cost:3.70 },
  { name:"فلايت وايت", cat:"مشروبات ساخنة", price:11, cost:4.10 },
  { name:"قهوة اليوم بارد صغير", cat:"مشروبات باردة", price:5, cost:2.75 },
  { name:"قهوة اليوم بارد كبير", cat:"مشروبات باردة", price:6, cost:2.75 },
  { name:"قهوة اليوم ساخن صغير", cat:"مشروبات ساخنة", price:5, cost:2.75 },
  { name:"قهوة اليوم ساخن كبير", cat:"مشروبات ساخنة", price:6, cost:3.00 },
  { name:"كابتشينو", cat:"مشروبات ساخنة", price:12, cost:4.00 },
  { name:"كب كوكيز", cat:"حلويات", price:8, cost:7.50 },
  { name:"كرانشي تشيز", cat:"حلويات", price:18, cost:11.50 },
  { name:"كركديه", cat:"مشروبات باردة", price:9, cost:0 },
  { name:"كورتادو", cat:"مشروبات ساخنة", price:11, cost:4.00 },
  { name:"كوكيز", cat:"حلويات", price:7, cost:5.00 },
  { name:"كيمكس", cat:"مشروبات ساخنة", price:11, cost:3.50 },
  { name:"لاتيه", cat:"مشروبات ساخنة", price:12, cost:4.00 },
  { name:"ماء", cat:"مشروبات باردة", price:1, cost:0 },
  { name:"ماتشا فيول", cat:"ماتشا", price:10, cost:4.55 },
  { name:"ماتشا لاتيه", cat:"ماتشا", price:11, cost:4.55 },
  { name:"ماجيك بار", cat:"حلويات", price:7, cost:0 },
  { name:"موهيتو توت أحمر", cat:"موهيتو", price:10, cost:4.00 },
  { name:"موهيتو توت أزرق", cat:"موهيتو", price:10, cost:4.00 },
  { name:"موهيتو فراولة", cat:"موهيتو", price:10, cost:4.00 },
  { name:"موهيتو ليمون نعناع", cat:"موهيتو", price:10, cost:4.00 },
  { name:"هوت شكلت+كريمه+اسبريسو+بسكوت", cat:"مشروبات ساخنة", price:17, cost:9.00 },
  { name:"هوت شوكلة+كريمه+بسكوت", cat:"مشروبات ساخنة", price:13, cost:7.00 },
  { name:"هوت شوكلت", cat:"مشروبات ساخنة", price:10, cost:4.70 },
];

const totalRev = products.reduce((s,p)=>s+p.price,0);
const totalCost = products.reduce((s,p)=>s+p.cost,0);
const avgMarginRate = (totalRev - totalCost) / totalRev;
const LOGS_KEY = "hama_logs_v3";

const fmt = n => Number(n).toLocaleString("ar-SA",{minimumFractionDigits:2,maximumFractionDigits:2});
const todayKey = () => new Date().toISOString().split("T")[0];
const todayDisplay = () => new Date().toLocaleDateString("ar-SA-u-ca-gregory",{year:"numeric",month:"2-digit",day:"2-digit"});

let extras = [{ label:"", amount:"" }];
let currentCat = "الكل";
let logs = [];

try { logs = JSON.parse(localStorage.getItem(LOGS_KEY)||"[]"); } catch {}

// Init
document.getElementById("avgMarginDisplay").textContent = (avgMarginRate*100).toFixed(1)+"%";
document.getElementById("todayDisplay").textContent = todayDisplay();
renderExtras();
renderCatFilters();
renderProducts("الكل","");

function showTab(t) {
  document.querySelectorAll(".tab").forEach((b,i)=>b.classList.toggle("active",["daily","history","products"][i]===t));
  document.querySelectorAll(".section").forEach(s=>s.classList.remove("active"));
  document.getElementById("tab-"+t).classList.add("active");
  if(t==="history") renderHistory();
}

function renderExtras() {
  const el = document.getElementById("extrasList");
  el.innerHTML = extras.map((e,i)=>`
    <div class="extra-item">
      <div class="flex" style="gap:6px;margin-bottom:6px">
        <input type="text" placeholder="البيان (إيجار، رواتب...)" value="${e.label}"
          oninput="extras[${i}].label=this.value" style="flex:2;padding:8px;border-radius:7px;border:1px solid #2a2a2a;background:#111;color:#ddd;font-size:13px;font-family:inherit">
        <input type="number" placeholder="المبلغ" value="${e.amount}"
          oninput="extras[${i}].amount=this.value;updateResult()" style="flex:1;padding:8px;border-radius:7px;border:1px solid #2a2a2a;background:#111;color:#ddd;font-size:13px;font-family:inherit">
        <span class="unit">ر.س</span>
        ${extras.length>1?`<button class="remove-btn" onclick="removeExtra(${i})">×</button>`:""}
      </div>
      <div class="extra-from">✅ تُخصم من الربح</div>
    </div>
  `).join("");
}

function addExtra() { extras.push({label:"",amount:""}); renderExtras(); }
function removeExtra(i) { extras.splice(i,1); renderExtras(); updateResult(); }

function updateResult() {
  const revenue = parseFloat(document.getElementById("salesInput").value)||0;
  const saveBtn = document.getElementById("saveBtn");
  saveBtn.disabled = !revenue;

  if(!revenue){ document.getElementById("resultBox").style.display="none"; return; }
  document.getElementById("resultBox").style.display="block";

  const capital = revenue*(1-avgMarginRate);
  const gross = revenue-capital;
  const extrasTotal = extras.reduce((s,e)=>s+(parseFloat(e.amount)||0),0);
  const net = gross-extrasTotal;
  const margin = ((net/revenue)*100).toFixed(1);

  document.getElementById("r-revenue").textContent = fmt(revenue)+" ر.س";
  document.getElementById("r-capital").textContent = fmt(capital)+" ر.س";
  document.getElementById("r-gross").textContent = fmt(gross)+" ر.س";

  const extCard = document.getElementById("r-extras-card");
  if(extrasTotal>0){
    extCard.style.display="block";
    document.getElementById("r-extras").textContent = "- "+fmt(extrasTotal)+" ر.س";
  } else { extCard.style.display="none"; }

  document.getElementById("r-net").textContent = fmt(net)+" ر.س";
  document.getElementById("r-net").className = "net-profit-value"+(net<0?" loss":"");
  document.getElementById("netBox").className = "net-profit"+(net<0?" loss":"");
  document.getElementById("r-margin").textContent = margin+"%";
}

function saveDay() {
  const revenue = parseFloat(document.getElementById("salesInput").value)||0;
  if(!revenue) return;
  const capital = revenue*(1-avgMarginRate);
  const gross = revenue-capital;
  const extrasTotal = extras.reduce((s,e)=>s+(parseFloat(e.amount)||0),0);
  const net = gross-extrasTotal;
  const entry = {
    date: todayKey(),
    dateDisplay: todayDisplay(),
    revenue, capital:+capital.toFixed(2),
    grossProfit:+gross.toFixed(2),
    extrasFromProfit:+extrasTotal.toFixed(2),
    netProfit:+net.toFixed(2),
    margin:+((net/revenue)*100).toFixed(1),
    extras: extras.filter(e=>e.label&&e.amount).map(e=>({...e}))
  };
  logs = [entry,...logs.filter(l=>l.date!==todayKey())].sort((a,b)=>b.date.localeCompare(a.date));
  localStorage.setItem(LOGS_KEY,JSON.stringify(logs));
  const msg = document.getElementById("savedMsg");
  msg.textContent = "✅ تم الحفظ بتاريخ "+todayDisplay();
  msg.style.display="block";
  setTimeout(()=>msg.style.display="none",2500);
}

function renderHistory() {
  const el = document.getElementById("historyContent");
  if(!logs.length){ el.innerHTML=`<div class="empty">لا يوجد سجلات بعد</div>`; return; }
  const totalSales = logs.reduce((s,l)=>s+l.revenue,0);
  const totalProfit = logs.reduce((s,l)=>s+l.netProfit,0);
  let html = `<div style="color:#d4a96a;font-weight:bold;margin-bottom:12px">📅 السجل اليومي (${logs.length} يوم)</div>
  <div class="summary-card">
    <div class="label">📊 إجمالي الفترة</div>
    <div class="flex-wrap">
      <div class="stat-card"><div class="stat-label">💰 مجموع المبيعات</div><div class="stat-value" style="color:#d4a96a">${fmt(totalSales)} ر.س</div></div>
      <div class="stat-card"><div class="stat-label">✅ مجموع الأرباح</div><div class="stat-value" style="color:#6dbf6d">${fmt(totalProfit)} ر.س</div></div>
    </div>
  </div>`;
  logs.forEach(l=>{
    html += `<div class="log-item" onclick="toggleLog('${l.date}')">
      <div class="log-row">
        <span class="log-date">📅 ${l.dateDisplay||l.date}</span>
        <span class="log-profit ${l.netProfit<0?'loss':''}">${l.netProfit>=0?"+":""}${fmt(l.netProfit)} ر.س</span>
      </div>
      <div class="log-sub">
        <span style="color:#666;font-size:12px">مبيعات: ${fmt(l.revenue)} ر.س</span>
        <span style="color:#a09fe0;font-size:12px">هامش: ${l.margin}%</span>
      </div>
      <div class="log-detail" id="detail-${l.date}">
        <div class="detail-row"><span class="detail-key">📦 رأس المال</span><span class="detail-val" style="color:#e07050">${fmt(l.capital)} ر.س</span></div>
        <div class="detail-row"><span class="detail-key">📈 الربح الإجمالي</span><span class="detail-val" style="color:#a0cf90">${fmt(l.grossProfit)} ر.س</span></div>
        ${l.extrasFromProfit>0?`<div class="detail-row"><span class="detail-key">💸 مصاريف</span><span class="detail-val" style="color:#e0a050">- ${fmt(l.extrasFromProfit)} ر.س</span></div>`:""}
        ${(l.extras||[]).map(e=>`<div class="detail-row" style="padding-right:10px"><span style="color:#555;font-size:12px">↳ ${e.label}</span><span style="color:#777;font-size:12px">${fmt(e.amount)} ر.س</span></div>`).join("")}
      </div>
    </div>`;
  });
  el.innerHTML = html;
}

function toggleLog(date) {
  const el = document.getElementById("detail-"+date);
  el.classList.toggle("open");
}

function renderCatFilters() {
  const cats = ["الكل",...new Set(products.map(p=>p.cat))];
  document.getElementById("catFilters").innerHTML = cats.map(c=>
    `<button class="cat-btn ${c===currentCat?'active':''}" onclick="filterCat('${c}')">${c}</button>`
  ).join("");
}

function filterCat(cat) {
  currentCat = cat;
  renderCatFilters();
  renderProducts(cat, document.querySelector(".search-input").value);
}

function filterProducts(q) { renderProducts(currentCat, q); }

function renderProducts(cat, q) {
  const filtered = products.filter(p=>(cat==="الكل"||p.cat===cat)&&(!q||p.name.includes(q)));
  document.getElementById("productsList").innerHTML = filtered.map(p=>`
    <div class="prod-item">
      <div class="prod-name"><div class="prod-name-text">${p.name}</div><div class="prod-cat-text">${p.cat}</div></div>
      <div class="prod-col" style="color:#e07050">${p.cost>0?p.cost+" ر.س":"—"}</div>
      <div class="prod-col" style="color:#d4a96a">${p.price} ر.س</div>
      <div class="prod-col" style="color:#6dbf6d">${(p.price-p.cost)>0?(p.price-p.cost).toFixed(2)+" ر.س":"—"}</div>
    </div>
  `).join("");
  const maxM = Math.max(...products.map(p=>p.price>0?(p.price-p.cost)/p.price*100:0));
  document.getElementById("prodSummary").innerHTML = `
    <div><div class="prod-stat-label">عدد المنتجات</div><div class="prod-stat-val">${products.length}</div></div>
    <div><div class="prod-stat-label">متوسط الهامش</div><div class="prod-stat-val">${(avgMarginRate*100).toFixed(1)}%</div></div>
    <div><div class="prod-stat-label">أعلى هامش</div><div class="prod-stat-val" style="color:#6dbf6d">${maxM.toFixed(0)}%</div></div>
  `;
}
</script>
</body>
</html>
