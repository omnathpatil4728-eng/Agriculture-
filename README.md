<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>KhetiSaathi: farm toolkit</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@600;800&family=Noto+Sans:wght@400;600&display=swap">
<style>
:root{--bg:#e8efe0;--panel:#fff;--ink:#1c2b19;--mute:#586a52;--line:#cfdcc5;--acc:#2b7a33;--acc-ink:#fff;--soft:#dcecd5;--sun:#9a6b00;--sunbg:#fdf0c9;--bad:#b03a2e;--badbg:#fbe3df;--water:#1b6aa5;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px);color-scheme:light}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#10190e;--panel:#192616;--ink:#e6f0e0;--mute:#9db393;--line:#2b3f27;--acc:#6fd078;--acc-ink:#0b1809;--soft:#213820;--sun:#f0c456;--sunbg:#3a2f0d;--bad:#ff9a8c;--badbg:#3b1d19;--water:#6db8f0;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#10190e;--panel:#192616;--ink:#e6f0e0;--mute:#9db393;--line:#2b3f27;--acc:#6fd078;--acc-ink:#0b1809;--soft:#213820;--sun:#f0c456;--sunbg:#3a2f0d;--bad:#ff9a8c;--badbg:#3b1d19;--water:#6db8f0;color-scheme:dark}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:17px/1.55 "Noto Sans",system-ui,sans-serif}
h1,h2,h3{font-family:"Baloo 2","Noto Sans",system-ui,sans-serif;margin:0;line-height:1.2}
.wrap{max-width:860px;margin:0 auto;padding:16px 14px 56px}
header{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}
.brand{font:800 26px "Baloo 2",sans-serif;color:var(--acc)}
.sub{color:var(--mute);font-size:14px}
.tabs{display:flex;gap:4px;background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:4px;margin-bottom:14px;overflow-x:auto}
.tabs button{flex:1;white-space:nowrap;border:0;background:transparent;color:var(--ink);font:600 15px "Noto Sans",sans-serif;padding:12px 12px;border-radius:10px;cursor:pointer}
.tabs button[aria-selected=true]{background:var(--acc);color:var(--acc-ink)}
.card{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:16px;margin-bottom:12px}
.btn{font:600 16px "Noto Sans",sans-serif;border:1px solid var(--acc);background:var(--acc);color:var(--acc-ink);padding:12px 18px;border-radius:10px;cursor:pointer;min-height:46px}
.btn.ghost{background:transparent;color:var(--ink);border-color:var(--line)}
.btn.sm{padding:6px 10px;font-size:14px;min-height:0}
button:focus-visible,input:focus-visible,select:focus-visible,textarea:focus-visible{outline:3px solid var(--acc);outline-offset:1px}
input,select,textarea{width:100%;font:inherit;color:var(--ink);background:var(--bg);border:1px solid var(--line);border-radius:10px;padding:11px 12px;min-height:46px}
textarea{min-height:110px}
label{display:block;font-weight:600;font-size:14px;margin-bottom:4px}
.grid{display:grid;gap:12px;grid-template-columns:1fr}
@media(min-width:620px){.grid.two{grid-template-columns:1fr 1fr}.grid.three{grid-template-columns:repeat(3,1fr)}}
.sum{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.sum div{background:var(--soft);border-radius:12px;padding:12px}
.sum b{display:block;font:800 21px "Baloo 2",sans-serif}
.sum .neg b{color:var(--bad)}
.row{display:flex;align-items:center;gap:10px;padding:9px 0;border-bottom:1px solid var(--line)}
.row:last-child{border-bottom:0}
.g{flex:1;min-width:0}
.amt{font-weight:600;white-space:nowrap}.amt.in{color:var(--acc)}.amt.out{color:var(--bad)}
.x{background:transparent;border:0;color:var(--mute);cursor:pointer;font-size:20px;padding:6px 10px}
.row input[type=checkbox]{width:26px;height:26px;min-height:0;accent-color:var(--acc);flex:none}
.row.done .g{text-decoration:line-through;color:var(--mute)}
.tag{display:inline-block;font-size:12px;font-weight:600;border-radius:99px;padding:1px 9px;background:var(--soft);color:var(--acc)}
.tag.late{background:var(--badbg);color:var(--bad)}.tag.today{background:var(--sunbg);color:var(--sun)}
.chips{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px}
.res{background:var(--soft);border-radius:12px;padding:12px;margin-top:10px}
.res b{font-family:"Baloo 2",sans-serif;font-size:20px}
.out-box{white-space:pre-wrap;background:var(--bg);border:1px solid var(--line);border-radius:12px;padding:14px;margin-top:12px;min-height:60px}
.msg{padding:10px 12px;border-radius:10px;background:var(--badbg);color:var(--bad);font-size:14px;margin-top:10px}
.add{display:flex;gap:8px;margin-top:12px;flex-wrap:wrap}
.note{font-size:13px;color:var(--mute);margin-top:22px;text-align:center}
</style>
</head>
<body>
<div class="wrap">
<header><div><div class="brand">KhetiSaathi</div><div class="sub">Farm records, tasks, calculators and crop help</div></div><button class="btn ghost sm" id="theme">Theme</button></header>
<div class="tabs" role="tablist" id="tabs"></div>
<main id="view"></main>
<p class="note">Advice here is general guidance. Confirm doses and treatments with your local agriculture officer or Krishi Vigyan Kendra. Records stay in this browser.</p>
</div>
<script>
const KEY="khetisaathi:v1";
const TABS=[["ledger","Farm ledger"],["tasks","Tasks"],["calc","Calculators"],["doctor","Crop doctor"]];
const EXP=["Seeds","Fertilizer","Pesticide","Labour","Water & power","Equipment","Transport","Other"],INC=["Crop sale","Subsidy or scheme","Other income"];
const ACRE={acre:1,hectare:2.47105,guntha:.025};
let S={tab:"ledger",crops:[],tx:[],tasks:[]};
let doc={busy:false,ctl:null};
const $=id=>document.getElementById(id);
const esc=t=>{const d=document.createElement("div");d.textContent=t;return d.innerHTML};
const uid=()=>Math.random().toString(36).slice(2,9);
const dk=d=>d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0")+"-"+String(d.getDate()).padStart(2,"0");
const inr=n=>"₹"+Math.round(n).toLocaleString("en-IN");
const fx=(n,d=2)=>isFinite(n)?(+n.toFixed(d)).toLocaleString("en-IN"):"–";
function save(){try{localStorage.setItem(KEY,JSON.stringify(S))}catch(e){}}
try{const r=localStorage.getItem(KEY);if(r)Object.assign(S,JSON.parse(r))}catch(e){}
const T=dk(new Date());
const cropName=id=>{const c=S.crops.find(x=>x.id===id);return c?c.name:"General"};
const acres=c=>(+c.area||0)*ACRE[c.unit];

function vLedger(){
 const inc=S.tx.filter(t=>t.type==="inc").reduce((s,t)=>s+t.amt,0),exp=S.tx.filter(t=>t.type==="exp").reduce((s,t)=>s+t.amt,0),pr=inc-exp;
 const tx=[...S.tx].sort((a,b)=>b.date.localeCompare(a.date)).slice(0,15);
 return `<div class="card"><div class="sum"><div><span class="sub">Income</span><b>${inr(inc)}</b></div><div><span class="sub">Expenses</span><b>${inr(exp)}</b></div><div class="${pr<0?"neg":""}"><span class="sub">Profit</span><b>${inr(pr)}</b></div></div></div>
 <div class="card"><h3>Profit by crop</h3>${S.crops.length?S.crops.map(c=>{const i=S.tx.filter(t=>t.crop===c.id&&t.type==="inc").reduce((s,t)=>s+t.amt,0),e=S.tx.filter(t=>t.crop===c.id&&t.type==="exp").reduce((s,t)=>s+t.amt,0),p=i-e,a=acres(c);
  return `<div class="row"><div class="g"><b>${esc(c.name)}</b><br><span class="sub">${fx(+c.area)} ${c.unit}${c.sown?" · sown "+esc(c.sown):""}<br>In ${inr(i)} · Out ${inr(e)}${a>0?" · "+inr(p/a)+" per acre":""}</span></div><span class="amt ${p<0?"out":"in"}">${inr(p)}</span><button class="x" data-a="delcrop" data-id="${c.id}" aria-label="Remove ${esc(c.name)}">×</button></div>`}).join(""):`<p class="sub">Add your first crop or plot below to see profit for each one.</p>`}
 <details style="margin-top:12px"><summary style="cursor:pointer;font-weight:600">Add a crop or plot</summary><div class="grid three" style="margin-top:10px"><div><label for="cn">Crop name</label><input id="cn" placeholder="e.g. Onion, plot 1"></div><div><label for="ca">Area</label><input id="ca" type="number" min="0" step="0.1"></div><div><label for="cu">Unit</label><select id="cu"><option>acre</option><option>guntha</option><option>hectare</option></select></div><div><label for="cs">Sowing date</label><input id="cs" type="date"></div></div><div class="add"><button class="btn" data-a="addcrop">Add crop</button></div></details></div>
 <div class="card"><h3>Add income or expense</h3><div class="grid two" style="margin-top:10px"><div><label for="tt">Type</label><select id="tt"><option value="exp">Expense</option><option value="inc">Income</option></select></div><div><label for="tc">Category</label><select id="tc">${EXP.map(x=>`<option>${x}</option>`).join("")}</select></div>
 <div><label for="tr">Crop</label><select id="tr"><option value="">General (whole farm)</option>${S.crops.map(c=>`<option value="${c.id}">${esc(c.name)}</option>`).join("")}</select></div><div><label for="tm">Amount (₹)</label><input id="tm" type="number" min="0" inputmode="decimal"></div>
 <div><label for="td">Date</label><input id="td" type="date" value="${T}"></div><div><label for="tn">Note</label><input id="tn" placeholder="Optional"></div></div><div class="add"><button class="btn" data-a="addtx">Save entry</button></div><div id="terr" class="msg" style="display:none" role="status"></div></div>
 <div class="card"><h3>Recent entries</h3>${tx.length?tx.map(t=>`<div class="row"><div class="g"><b>${esc(t.cat)}</b> <span class="tag">${esc(cropName(t.crop))}</span><br><span class="sub">${esc(t.date)}${t.note?" · "+esc(t.note):""}</span></div><span class="amt ${t.type==="inc"?"in":"out"}">${t.type==="inc"?"+":"−"}${inr(t.amt)}</span><button class="x" data-a="deltx" data-id="${t.id}" aria-label="Delete entry">×</button></div>`).join(""):`<p class="sub">No entries yet.</p>`}</div>`}

function vTasks(){
 const ts=[...S.tasks].sort((a,b)=>(a.done-b.done)||a.date.localeCompare(b.date));
 return `<div class="card"><h3>Add a farm task</h3><div class="chips" style="margin-top:10px">${["Irrigate","Spray","Apply fertilizer","Weeding","Harvest","Sell at mandi"].map(x=>`<button class="btn ghost sm" data-a="chip" data-v="${x}">${x}</button>`).join("")}</div>
 <div class="grid two"><div><label for="kt">Task</label><input id="kt" placeholder="e.g. Irrigate onion plot"></div><div><label for="kd">Due date</label><input id="kd" type="date" value="${T}"></div><div><label for="kc">Crop</label><select id="kc"><option value="">General</option>${S.crops.map(c=>`<option value="${c.id}">${esc(c.name)}</option>`).join("")}</select></div></div><div class="add"><button class="btn" data-a="addtask">Add task</button></div></div>
 <div class="card"><h3>Your tasks</h3>${ts.length?ts.map(t=>{const tag=t.done?"":t.date<T?`<span class="tag late">Overdue</span>`:t.date===T?`<span class="tag today">Today</span>`:"";return `<div class="row ${t.done?"done":""}"><input type="checkbox" id="k${t.id}" data-a="done" data-id="${t.id}" ${t.done?"checked":""}><label class="g" for="k${t.id}" style="margin:0;font-weight:400">${esc(t.title)} ${tag}<br><span class="sub">${esc(t.date)} · ${esc(cropName(t.crop))}</span></label><button class="x" data-a="deltask" data-id="${t.id}" aria-label="Delete task">×</button></div>`}).join(""):`<p class="sub">No tasks yet. Add watering, spraying or harvest reminders.</p>`}</div>`}

function vCalc(){
 return `<div class="card"><h3>Land area</h3><div class="grid two" style="margin-top:10px"><div><label for="la">Area</label><input id="la" type="number" min="0" step="0.1" inputmode="decimal" data-c="1"></div><div><label for="lu">Unit</label><select id="lu" data-c="1"><option>acre</option><option>guntha</option><option>hectare</option></select></div></div><div class="res" id="r1">Enter your area to convert.</div></div>
 <div class="card"><h3>Seed or fertilizer needed</h3><p class="sub">Use the rate from your soil test report or agriculture officer.</p><div class="grid two"><div><label for="fr">Rate per acre (kg)</label><input id="fr" type="number" min="0" step="0.1" inputmode="decimal" data-c="1"></div><div><label for="fb">Bag size (kg)</label><input id="fb" type="number" min="0" value="50" data-c="1"></div><div><label for="fp">Price per bag (₹)</label><input id="fp" type="number" min="0" inputmode="decimal" data-c="1"></div></div><div class="res" id="r2">Enter area and rate.</div></div>
 <div class="card"><h3>Irrigation water and pump time</h3><div class="grid two"><div><label for="id">Water depth per irrigation (mm)</label><input id="id" type="number" min="0" value="50" data-c="1"></div><div><label for="if">Pump flow (litres per hour)</label><input id="if" type="number" min="0" inputmode="decimal" data-c="1"></div></div><div class="res" id="r3">Enter area and depth.</div></div>`}
function calc(){
 const g=id=>parseFloat($(id).value)||0,a=g("la")*ACRE[$("lu").value];
 $("r1").innerHTML=a?`<b>${fx(a)}</b> acre · <b>${fx(a/ACRE.hectare)}</b> hectare · <b>${fx(a*40,1)}</b> guntha`:"Enter your area to convert.";
 const kg=a*g("fr"),bags=g("fb")?kg/g("fb"):0;
 $("r2").innerHTML=a&&g("fr")?`Total <b>${fx(kg,1)} kg</b>${g("fb")?` · about <b>${Math.ceil(bags)}</b> bags`:""}${g("fp")&&g("fb")?` · cost about <b>${inr(Math.ceil(bags)*g("fp"))}</b>`:""}`:"Enter area and rate.";
 const L=a*4046.86*g("id"),h=g("if")?L/g("if"):0;
 $("r3").innerHTML=a&&g("id")?`<b>${Math.round(L).toLocaleString("en-IN")}</b> litres per irrigation${h?` · pump runs about <b>${fx(h,1)} hours</b>`:""}`:"Enter area and depth.";
}

function vDoctor(){
 return `<div class="card"><h3>Describe the problem</h3><p class="sub">Say what you see on the crop. Claude suggests likely causes and safe first steps.</p>
 <div class="grid two" style="margin-top:10px"><div><label for="dc">Crop</label><input id="dc" placeholder="e.g. Tomato"></div><div><label for="dl">Reply language</label><select id="dl"><option>English</option><option>Hindi</option><option>Marathi</option></select></div></div>
 <label for="ds" style="margin-top:12px">What do you see? How long, and how much of the field?</label><textarea id="ds" placeholder="e.g. Yellow spots on lower leaves for 5 days, spreading after rain"></textarea>
 <div class="add"><button class="btn" id="ask" data-a="ask">Get advice</button></div><div id="derr"></div><div class="out-box" id="dout" aria-live="polite">Advice will appear here.</div></div>`}
async function ask(){
 const crop=$("dc").value.trim(),sym=$("ds").value.trim(),lang=$("dl").value,out=$("dout"),btn=$("ask"),er=$("derr");er.innerHTML="";
 if(sym.length<10){er.innerHTML=`<div class="msg">Describe what you see in a sentence or two.</div>`;return}
 btn.disabled=true;btn.textContent="Thinking…";out.textContent="Thinking…";
 try{
  const sample=await claude.use("sample");if(!sample)throw{code:"unavailable"};
  const p=`You are a practical crop health advisor for smallholder farmers in India. Reply in ${lang}, in simple short sentences.
Crop: ${crop||"not stated"}
Problem: ${sym}
Give: 1) the 2-3 most likely causes, 2) low-cost checks the farmer can do today, 3) safe first steps (cultural, organic or field-hygiene measures first), 4) when to contact the local agriculture officer or Krishi Vigyan Kendra and what to carry (sample leaf, photo).
Do not give exact pesticide doses or brand names. Say what you are unsure of. Keep it under 250 words.`;
  await sample(p,{modelTier:"default",cache:false,onText:({text})=>{out.textContent=text}});
 }catch(e){
  out.textContent="Advice will appear here.";
  er.innerHTML=`<div class="msg">${{unavailable:"Crop doctor isn’t available in this view.",not_granted:"Permission to use Claude was declined. Allow it to get advice.",rate_limited:"Too many requests. Wait a minute and try again."}[e&&e.code]||"Couldn’t get advice. Check your connection and try again."}</div>`;
 }finally{btn.disabled=false;btn.textContent="Get advice"}
}

function render(){
 $("tabs").innerHTML=TABS.map(t=>`<button role="tab" data-a="tab" data-id="${t[0]}" aria-selected="${S.tab===t[0]}">${t[1]}</button>`).join("");
 $("view").innerHTML={ledger:vLedger,tasks:vTasks,calc:vCalc,doctor:vDoctor}[S.tab]();
 if(S.tab==="calc")calc();
}
function bad(id,m){const e=$(id);e.style.display="block";e.textContent=m}
document.addEventListener("click",e=>{
 const b=e.target.closest("[data-a]");if(!b)return;const a=b.dataset.a,id=b.dataset.id;
 if(a==="tab")S.tab=id;
 else if(a==="addcrop"){const n=$("cn").value.trim();if(!n){$("cn").focus();return}S.crops.push({id:uid(),name:n,area:+$("ca").value||0,unit:$("cu").value,sown:$("cs").value})}
 else if(a==="delcrop"){if(!confirm("Remove this crop? Its entries stay under General."))return;S.crops=S.crops.filter(x=>x.id!==id);S.tx.forEach(t=>{if(t.crop===id)t.crop=""});S.tasks.forEach(t=>{if(t.crop===id)t.crop=""})}
 else if(a==="addtx"){const m=parseFloat($("tm").value);if(!(m>0)){bad("terr","Enter an amount greater than zero.");return}S.tx.push({id:uid(),type:$("tt").value,cat:$("tc").value,crop:$("tr").value,amt:m,date:$("td").value||T,note:$("tn").value.trim()})}
 else if(a==="deltx"){if(!confirm("Delete this entry?"))return;S.tx=S.tx.filter(x=>x.id!==id)}
 else if(a==="chip"){$("kt").value=b.dataset.v;$("kt").focus();return}
 else if(a==="addtask"){const t=$("kt").value.trim();if(!t){$("kt").focus();return}S.tasks.push({id:uid(),title:t,date:$("kd").value||T,crop:$("kc").value,done:false})}
 else if(a==="done")S.tasks.find(x=>x.id===id).done=b.checked;
 else if(a==="deltask")S.tasks=S.tasks.filter(x=>x.id!==id);
 else if(a==="ask"){ask();return}
 else return;
 save();render()});
document.addEventListener("input",e=>{if(e.target.dataset.c)calc()});
document.addEventListener("change",e=>{if(e.target.id==="tt")$("tc").innerHTML=(e.target.value==="inc"?INC:EXP).map(x=>`<option>${x}</option>`).join("");else if(e.target.dataset.c)calc()});
$("theme").onclick=()=>{const r=document.documentElement,d=r.dataset.theme?r.dataset.theme==="dark":matchMedia("(prefers-color-scheme:dark)").matches;r.dataset.theme=d?"light":"dark"};
render();
</script>
</body>
</html>
