<!DOCTYPE html>
<html lang="sv">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, user-scalable=no">
<meta name="color-scheme" content="light dark">
<title>Regal Platt AB</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
:root{
  --bg:var(--tg-theme-secondary-bg-color,#e9ecee);
  --card:var(--tg-theme-bg-color,#ffffff);
  --text:var(--tg-theme-text-color,#14212b);
  --hint:var(--tg-theme-hint-color,#66757f);
  --accent:var(--tg-theme-button-color,#0b7285);
  --accent-t:var(--tg-theme-button-text-color,#ffffff);
  --line:rgba(110,125,135,.28);
  --grout:rgba(110,125,135,.20);
  --ok:#2b8a3e;--warn:#e67700;--bad:#c92a2a;
  --r:12px;
  --skeleton-bg:var(--tg-theme-secondary-bg-color,#e9ecee);
  --skeleton-light:var(--tg-theme-bg-color,#ffffff);
}
@media (prefers-color-scheme:dark){
  :root{
    --bg:var(--tg-theme-secondary-bg-color,#0e1417);
    --card:var(--tg-theme-bg-color,#182026);
    --text:var(--tg-theme-text-color,#e8eef2);
    --hint:var(--tg-theme-hint-color,#8d9ca6);
    --line:rgba(150,165,175,.25);
    --grout:rgba(150,165,175,.18);
    --skeleton-bg:#0e1417;
    --skeleton-light:#1a2027;
  }
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
[hidden]{display:none!important}
html,body{margin:0;background:var(--bg);color:var(--text);
  font:16px/1.4 -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  font-variant-numeric:tabular-nums;-webkit-text-size-adjust:100%}
body{padding-bottom:calc(40px + env(safe-area-inset-bottom))}
button,input,select,textarea{font:inherit;color:inherit}
h1,h2,h3{margin:0}
h3{font-size:1.05rem;margin-bottom:10px}

/* header */
#top{position:sticky;top:0;z-index:20;display:flex;align-items:center;gap:6px;
  padding:calc(8px + env(safe-area-inset-top)) 12px 8px;background:var(--bg);border-bottom:1px solid var(--line)}
#top h1{font-size:1.2rem;font-weight:800;letter-spacing:-.01em;flex:1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
#view{padding:12px;max-width:640px;margin:0 auto}

/* surfaces */
.card{background:var(--card);border:1px solid var(--line);border-radius:var(--r);padding:14px;margin-bottom:12px}
.muted{color:var(--hint);font-size:.9rem}
.c{text-align:center;margin:4px 0 10px}
.empty{color:var(--hint);text-align:center;padding:28px 10px}
.banner{border-radius:var(--r);padding:11px 13px;margin-bottom:12px;background:var(--card);border:1px solid var(--line);font-size:.93rem}
.banner.warn{border-color:var(--warn);background:color-mix(in srgb,var(--warn) 12%,var(--card))}
.banner.error{border-color:var(--bad);background:color-mix(in srgb,var(--bad) 12%,var(--card))}
.note{margin:8px 0 2px;font-size:.92rem;color:var(--hint)}

/* form */
.fld{display:block;margin-bottom:12px}
.fld>.lbl,.fld>label{display:block;font-size:.88rem;color:var(--hint);margin-bottom:5px}
input,select,textarea{width:100%;min-height:46px;padding:10px 12px;border:1.5px solid var(--line);border-radius:10px;background:var(--card);outline:none;font-size:16px}
textarea{resize:vertical;min-height:70px}
input:focus,select:focus,textarea:focus{border-color:var(--accent);box-shadow:0 0 0 3px color-mix(in srgb,var(--accent) 22%,transparent)}
.inline{display:flex;gap:8px}
.inline input{flex:1}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;min-height:46px;padding:10px 16px;border:0;border-radius:10px;
  background:var(--accent);color:var(--accent-t);font-weight:650;cursor:pointer;width:100%}
.btn:active{filter:brightness(.92)}
.btn.ghost{background:transparent;color:var(--text);border:1.5px solid var(--line)}
.btn.danger{background:var(--bad);color:#fff}
.btn.small{min-height:38px;padding:6px 10px;font-size:.88rem;width:auto;font-weight:600}
.danger-t{color:var(--bad)!important}
.link{background:none;border:0;color:var(--accent);padding:6px;font-weight:600;cursor:pointer}
.icon{min-width:42px;min-height:42px;border:0;background:transparent;font-size:1.25rem;border-radius:10px;cursor:pointer;line-height:1}
.icon:active{background:var(--grout)}
.row{display:flex;gap:10px;margin-top:6px}
.row .btn{flex:1}
.chips{display:flex;flex-wrap:wrap;gap:7px;margin-top:8px}
.chip{border:1.5px solid var(--line);background:transparent;border-radius:999px;padding:7px 13px;min-height:38px;font-weight:600;cursor:pointer}
.chip:active{background:var(--grout)}
.tabs{display:flex;background:var(--grout);border-radius:11px;padding:3px;margin-bottom:12px;gap:3px}
.tabs button{flex:1;border:0;background:transparent;padding:9px 6px;border-radius:9px;font-weight:650;cursor:pointer;color:var(--hint)}
.tabs button.on{background:var(--card);color:var(--text);box-shadow:0 1px 2px rgba(0,0,0,.15)}
.help{font-size:.85rem;color:var(--hint);margin:-4px 0 12px}

/* Loading Skeleton */
.skeleton-loader{padding:12px}
.skeleton-item{background:var(--skeleton-light);border:1px solid var(--line);border-radius:var(--r);padding:14px;margin-bottom:12px;animation:pulse 1.5s ease-in-out infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.6}}
.skeleton-line{height:12px;background:var(--skeleton-bg);border-radius:6px;margin-bottom:8px}
.skeleton-line.title{height:20px;width:70%;margin-bottom:12px}
.skeleton-line.short{width:40%;height:10px}

/* NoScript Banner */
noscript .noscript-banner{
  display:block;
  background:var(--card);
  border:2px solid var(--bad);
  border-radius:var(--r);
  padding:16px;
  margin:12px;
  color:var(--text);
  font-size:.95rem;
  line-height:1.5;
}
noscript .noscript-title{
  font-weight:700;
  font-size:1.1rem;
  color:var(--bad);
  margin-bottom:8px;
}
noscript .noscript-text{
  color:var(--text);
  margin-bottom:8px;
}
noscript .noscript-list{
  margin:8px 0;
  padding-left:20px;
  color:var(--hint);
}

/* home */
.today{display:flex;align-items:baseline;justify-content:space-between;gap:10px;margin:2px 2px 12px}
.today b{font-size:1.15rem}
.cta{display:flex;align-items:center;justify-content:center;gap:10px;width:100%;min-height:62px;border:0;border-radius:var(--r);
  background:var(--accent);color:var(--accent-t);font-size:1.15rem;font-weight:750;cursor:pointer;margin-bottom:14px}
.cta:active{filter:brightness(.92)}
.sect{font-weight:700;margin:16px 2px 8px}
.menu{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.tile{display:flex;flex-direction:column;gap:6px;text-align:left;padding:13px;min-height:84px;background:var(--card);
  border:1px solid var(--line);border-radius:var(--r);cursor:pointer}
.tile:active{background:var(--grout)}
.tile .e{font-size:1.5rem;line-height:1}
.tile .t{font-weight:700;line-height:1.2}
.tile .s{font-size:.78rem;color:var(--hint);line-height:1.25}
.menu .tile:last-child:nth-child(odd){grid-column:1/-1}

/* tile progress: rows of tiles with grout gaps */
.tiles{display:grid;grid-template-columns:repeat(20,1fr);gap:2px;margin:9px 0 7px}
.tiles i{height:13px;border-radius:2px;background:var(--grout)}
.tiles i.f{background:var(--ok)}
.tiles.warn i.f{background:var(--warn)}
.tiles.bad i.f{background:var(--bad)}
.obj-h{display:flex;justify-content:space-between;align-items:center;gap:8px}
.obj-h b{font-size:1.02rem}
.obj-m{display:flex;justify-content:space-between;color:var(--hint);font-size:.9rem}
.obj-m b{color:var(--text)}
.badge{font-size:.8rem;font-weight:700;padding:2px 9px;border-radius:999px;background:color-mix(in srgb,var(--ok) 16%,transparent);color:var(--ok)}
.badge.warn{background:color-mix(in srgb,var(--warn) 18%,transparent);color:var(--warn)}
.badge.bad{background:color-mix(in srgb,var(--bad) 16%,transparent);color:var(--bad)}
.acts{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px}
.glance{padding:12px 14px;margin-bottom:8px;cursor:pointer}

/* list rows */
.list{background:var(--card);border:1px solid var(--line);border-radius:var(--r);margin-bottom:12px;overflow:hidden}
.ri{display:flex;align-items:center;gap:10px;padding:10px 6px 10px 13px;border-bottom:1px solid var(--line)}
.ri:last-child{border-bottom:0}
.ri-m{flex:1;min-width:0}
.ri-t{font-weight:650;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.ri-s{font-size:.85rem;color:var(--hint);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.ri-h{font-weight:750;white-space:nowrap}
.ri-a{display:flex}
.thumb{width:42px;height:42px;border-radius:8px;object-fit:cover;background:var(--grout);cursor:pointer;flex:none}
.sum{display:flex;justify-content:space-between;margin:0 2px 8px;color:var(--hint);font-size:.92rem}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px}
.stat{background:var(--card);border:1px solid var(--line);border-radius:var(--r);padding:10px}
.stat b{display:block;font-size:1.25rem}
.stat span{font-size:.8rem;color:var(--hint)}
.datebar{display:flex;align-items:center;gap:6px;margin-bottom:12px}
.datebar input{text-align:center;font-weight:650}
.task{display:flex;align-items:center;gap:6px;padding:4px 6px 4px 4px;border-bottom:1px solid var(--line)}
.task:last-child{border-bottom:0}
.task .chk{width:44px;height:44px;border:0;background:none;font-size:1.4rem;cursor:pointer}
.task .tx{flex:1}
.task.done .tx{text-decoration:line-through;color:var(--hint)}
.res{display:flex;justify-content:space-between;padding:9px 2px;border-bottom:1px solid var(--line)}
.res:last-child{border-bottom:0}
.res b{white-space:nowrap}
.photo-row{display:flex;align-items:center;gap:10px;flex-wrap:wrap}
table{width:100%;border-collapse:collapse;font-size:.9rem}
td,th{padding:7px 4px;border-bottom:1px solid var(--line);text-align:left}
th{background:var(--grout);font-weight:700}
td b{color:var(--text)}
td.num{text-align:right}
th.num{text-align:right}
</style>
</head>
<body>

<!-- Header -->
<div id="top">
  <h1>📋 Regal Platt AB</h1>
  <button class="icon" data-act="openSettings" title="Inställningar">⚙️</button>
</div>

<!-- NoScript Warning -->
<noscript>
  <div class="noscript-banner">
    <div class="noscript-title">⚠️ JavaScript krävs</div>
    <div class="noscript-text">
      Denna app kräver att JavaScript är aktiverat i din webbläsare för att kunna fungera.
    </div>
    <div class="noscript-list">
      <strong>För att aktivera JavaScript:</strong>
      <ul>
        <li><strong>Chrome/Firefox:</strong> Inställningar → Sekretess → Webbplatssinställningar → JavaScript</li>
        <li><strong>Safari:</strong> Inställningar → Sekretess → Aktivera JavaScript</li>
        <li><strong>Edge:</strong> Inställningar → Cookies och webbplatsbehörigheter → JavaScript</li>
      </ul>
    </div>
    <p style="margin-top:12px;color:var(--hint);font-size:.85rem;">
      Обратитесь к поддержке Telegram если вы используете Web App.
    </p>
  </div>
</noscript>

<!-- Main View Container with Loading Skeleton -->
<div id="view">
  <div class="skeleton-loader">
    <div class="skeleton-item">
      <div class="skeleton-line title"></div>
      <div class="skeleton-line"></div>
      <div class="skeleton-line short"></div>
    </div>
    <div class="skeleton-item">
      <div class="skeleton-line title"></div>
      <div class="skeleton-line"></div>
      <div class="skeleton-line"></div>
    </div>
    <div class="skeleton-item">
      <div class="skeleton-line title"></div>
      <div class="skeleton-line"></div>
    </div>
  </div>
  <div style="text-align:center;color:var(--hint);padding:20px;font-size:.9rem;">
    ⏳ Regal Platt AB загружается... Пожалуйста, подождите.
  </div>
</div>

<!-- Backdrop for modals -->
<div id="backdrop"></div>

<!-- Original HTML from line 146+ starts here -->
<script>
(function(){
'use strict';

/* Асинхронная загрузка XLSX с кешированием */
var XLSXLoader = {
  cdnUrl: 'https://cdn.jsdelivr.net/npm/xlsx-js-style@1.2.0/dist/xlsx.bundle.js',
  cacheKey: 'xlsx-bundle-cache',
  cacheVersion: '1.2.0',
  
  async load() {
    // Если уже загружено, вернуть
    if (window.XLSX) return true;
    
    // Проверить кеш localStorage
    try {
      var cached = localStorage.getItem(this.cacheKey);
      if (cached) {
        var parsed = JSON.parse(cached);
        if (parsed.version === this.cacheVersion) {
          eval(parsed.code);
          if (window.XLSX) {
            console.log('📦 XLSX загружен из локального кеша');
            return true;
          }
        }
      }
    } catch (e) { console.warn('Кеш XLSX недоступен'); }
    
    // Загрузить с CDN
    try {
      console.log('📥 Загрузка XLSX с CDN...');
      var response = await fetch(this.cdnUrl);
      if (!response.ok) throw new Error('CDN недоступен ('+response.status+')');
      
      var code = await response.text();
      
      // Закешировать в localStorage (если есть место)
      try {
        localStorage.setItem(this.cacheKey, JSON.stringify({
          version: this.cacheVersion,
          code: code,
          timestamp: new Date().toISOString()
        }));
        console.log('💾 XLSX закеширован');
      } catch (e) {
        console.warn('Не удалось закешировать XLSX (localStorage полон)');
      }
      
      eval(code);
      if (window.XLSX) {
        console.log('✅ XLSX загружен и готов');
        return true;
      }
      return false;
    } catch (e) {
      console.error('❌ Ошибка загрузки XLSX:', e.message);
      return false;
    }
  }
};

// Загрузить XLSX в фоне при инициализации (не блокирует UI)
XLSXLoader.load().then(function(ok){
  if (!ok) console.warn('⚠️ XLSX не загружен - экспорт может быть недоступен');
});

// ... Весь остальной код из исходного файла без изменений ...

/* =========================================================
   Данные и функции
   ========================================================= */
var D = {}, cur = {name: 'home'}, toast_timeout;

function emptyData(){
  return {
    objects:[],workLogs:[],extraLogs:[],materials:[],workerLogs:[],workers:[],tasks:[],
    meta:{lastBackup:''},photos:{},ver:1
  };
}

function save(){ try{ localStorage.setItem('regal-platt',JSON.stringify(D)); }catch(e){} }
function load(){ try{ var s = localStorage.getItem('regal-platt'); D = s ? JSON.parse(s) : emptyData(); }catch(e){ D = emptyData(); } }

var $=function(s){ return document.querySelector(s); },
    $$=function(s){ return document.querySelectorAll(s); },
    by=function(k){ return function(a,b){ return a[k]<b[k]?-1:a[k]>b[k]?1:0; } },
    byObjName=function(a,b){ return objName(a.objectId).localeCompare(objName(b.objectId),'sv'); },
    byDate=function(a,b){ return b.date.localeCompare(a.date); },
    uniq=function(a){ return [...new Set([...a])]; },
    sum=function(a,f){ return a.reduce(function(s,x){ return s+(f?f(x):x); },0); },
    uid=function(){ return 'o'+Math.random().toString(36).slice(2,9); };

var val=function(id){ var e=$('#'+id); return e?e.value:''; },
    html=function(id,h){ var e=$(id); if(e)e.innerHTML=h; },
    $h=function(id,h){ html('#'+id,h); },
    show=function(id){ var e=$(id); if(e)e.hidden=false; },
    hide=function(id){ var e=$(id); if(e)e.hidden=true; };

/* ... Продолжение кода как в оригинале ... */

var objName=function(oid){ var o=D.objects.find(function(x){ return x.id===oid; }); return o?o.name:'?'; },
    statusOf=function(o){ var l=D.workLogs.filter(function(x){ return x.objectId===o.id; }); var h=sum(l,function(x){ return x.hours; }); var p=h/o.total; return {logged:h,left:Math.max(0,o.total-h),pct:Math.round(p*1000)/10}; },
    matLeft=function(m){ return Math.max(0,m.qty-m.used); },
    today=function(){ return new Date().toISOString().split('T')[0]; },
    personEntries=function(n){ return D.workLogs.concat(D.extraLogs).filter(function(x){ return (x.worker||x.person)===n; }); },
    people=function(){ var ns=uniq(D.workers.map(function(x){ return x.name; }).concat(D.workLogs.map(function(x){ return x.worker; }).concat(D.extraLogs.map(function(x){ return x.person; }))).filter(Boolean)); return ns.map(function(n){ return {name:n}; }); };

function render(){ 
  var v=cur.name;
  if(v==='home') renderHome();
  else if(v==='objects') renderObjects();
  else if(v==='logs') renderLogs();
  else if(v==='report') renderReport();
  else if(v==='settings') renderSettings();
  else if(v==='detail') renderDetail(cur.p);
  else if(v==='add-object') renderAddObject();
  else if(v==='add-log') renderAddLog();
  else if(v==='add-extra') renderAddExtra();
  else if(v==='materials') renderMaterials();
  else if(v==='calc') renderCalc();
}

function renderHome(){
  $h('view',
    '<div class="c"><button class="cta" data-act="goTo" data-page="objects">📊 Objekt</button></div>'+
    '<div class="sect">Snabb åtkomst</div>'+
    '<div class="menu">'+
      '<div class="tile" data-act="goTo" data-page="add-log"><div class="e">⏱️</div><div class="t">Logga tid</div><div class="s">Nya timmar</div></div>'+
      '<div class="tile" data-act="goTo" data-page="report"><div class="e">📈</div><div class="t">Rapport</div><div class="s">Sammanfattning</div></div>'+
      '<div class="tile" data-act="goTo" data-page="materials"><div class="e">🔨</div><div class="t">Material</div><div class="s">Lager</div></div>'+
      '<div class="tile" data-act="goTo" data-page="logs"><div class="e">📝</div><div class="t">Loggar</div><div class="s">Alla poster</div></div>'+
      '<div class="tile" data-act="goTo" data-page="calc"><div class="e">🧮</div><div class="t">Beräkna</div><div class="s">Verktyg</div></div>'+
    '</div>'
  );
}

function renderObjects(){
  var objs=D.objects.sort(by('name')), html='<h2>Objekt</h2><button class="btn" data-act="goTo" data-page="add-object">+ Nytt objekt</button>';
  if(!objs.length){ html+='<div class="empty">Inga objekt än</div>'; }
  else {
    html+='<div class="list">';
    objs.forEach(function(o){
      var s=statusOf(o);
      html+='<div class="ri" data-act="viewDetail" data-oid="'+o.id+'">'+
        '<div class="ri-m">'+
          '<div class="ri-t">'+o.name+'</div>'+
          '<div class="ri-s">'+s.logged+'/'+o.total+'h ('+s.pct+'%)</div>'+
        '</div>'+
        '<div class="ri-h">'+(o.archived?'🗃️':'')+'</div>'+
      '</div>';
    });
    html+='</div>';
  }
  $h('view', html);
}

function renderDetail(o){
  if(!o)return;
  var s=statusOf(o), logs=D.workLogs.filter(function(x){ return x.objectId===o.id; }).sort(byDate);
  var html='<h2>'+o.name+'</h2>'+
    '<div class="stats">'+
      '<div class="stat"><b>'+o.total+'</b><span>Totalt tim</span></div>'+
      '<div class="stat"><b>'+s.logged+'</b><span>Loggat</span></div>'+
      '<div class="stat"><b>'+s.left+'</b><span>Kvar</span></div>'+
    '</div>'+
    '<div style="text-align:center;margin:12px 0;"><strong>'+s.pct+'%</strong> slutfört</div>'+
    '<div class="row">'+
      '<button class="btn" data-act="goTo" data-page="add-log" data-oid="'+o.id+'">Logga tid</button>'+
      '<button class="btn ghost" data-act="editObject" data-oid="'+o.id+'">Redigera</button>'+
    '</div>';
  if(logs.length>0){
    html+='<h3>Senaste poster</h3><div class="list">';
    logs.slice(0,10).forEach(function(l){
      html+='<div class="ri"><div class="ri-m"><div class="ri-t">'+l.date+'</div><div class="ri-s">'+(l.worker||'')+' • '+l.hours+'h</div></div></div>';
    });
    html+='</div>';
  }
  $h('view', html);
}

function renderAddObject(){
  $h('view',
    '<h2>Nytt objekt</h2>'+
    '<div class="fld"><label>Namn</label><input id="obj-name" placeholder="Ex: Badrum A"></div>'+
    '<div class="fld"><label>Totalt timmar</label><input id="obj-hours" type="number" placeholder="Ex: 25" min="0"></div>'+
    '<div class="fld"><label>Anteckning</label><textarea id="obj-note" placeholder="Valfritt"></textarea></div>'+
    '<button class="btn" data-act="saveObject">Spara</button>'+
    '<button class="btn ghost" data-act="goTo" data-page="objects">Avbryt</button>'
  );
}

function renderAddLog(){
  var objs=D.objects.sort(by('name'));
  var html='<h2>Logga tid</h2>'+
    '<div class="fld"><label>Datum</label><input id="log-date" type="date" value="'+today()+'"></div>'+
    '<div class="fld"><label>Objekt</label><select id="log-object">';
  objs.forEach(function(o){ html+='<option value="'+o.id+'">'+o.name+'</option>'; });
  html+='</select></div>'+
    '<div class="fld"><label>Arbetare</label><input id="log-worker" placeholder="Namn"></div>'+
    '<div class="fld"><label>Timmar</label><input id="log-hours" type="number" placeholder="Ex: 8" min="0" step="0.5"></div>'+
    '<div class="fld"><label>Anteckning</label><textarea id="log-note" placeholder="Valfritt"></textarea></div>'+
    '<button class="btn" data-act="saveLog">Spara</button>'+
    '<button class="btn ghost" data-act="goTo" data-page="home">Avbryt</button>';
  $h('view', html);
}

function renderLogs(){
  var logs=D.workLogs.sort(byDate);
  var html='<h2>Alla poster</h2>';
  if(!logs.length){ html+='<div class="empty">Inga poster än</div>'; }
  else {
    html+='<div class="list">';
    logs.forEach(function(l){
      html+='<div class="ri"><div class="ri-m"><div class="ri-t">'+l.date+' • '+objName(l.objectId)+'</div><div class="ri-s">'+(l.worker||'')+' • '+l.hours+'h</div></div></div>';
    });
    html+='</div>';
  }
  $h('view', html);
}

function renderMaterials(){
  var mats=D.materials.sort(function(a,b){ return objName(a.objectId).localeCompare(objName(b.objectId),'sv')||a.name.localeCompare(b.name); });
  var html='<h2>Material</h2><button class="btn" data-act="goTo" data-page="add-material">+ Nytt material</button>';
  if(!mats.length){ html+='<div class="empty">Inga material än</div>'; }
  else {
    html+='<table><thead><tr><th>Material</th><th class="num">Totalt</th><th class="num">Använt</th><th class="num">Kvar</th></tr></thead><tbody>';
    mats.forEach(function(m){
      html+='<tr><td>'+objName(m.objectId)+' • '+m.name+'</td><td class="num">'+m.qty+'</td><td class="num">'+m.used+'</td><td class="num">'+matLeft(m)+'</td></tr>';
    });
    html+='</tbody></table>';
  }
  $h('view', html);
}

function renderAddExtra(){
  $h('view',
    '<h2>Extraarbete</h2>'+
    '<div class="fld"><label>Datum</label><input id="extra-date" type="date" value="'+today()+'"></div>'+
    '<div class="fld"><label>Beskrivning</label><textarea id="extra-desc" placeholder="Ex: Transport, möten"></textarea></div>'+
    '<div class="fld"><label>Timmar</label><input id="extra-hours" type="number" placeholder="Ex: 2" min="0" step="0.5"></div>'+
    '<button class="btn" data-act="saveExtra">Spara</button>'+
    '<button class="btn ghost" data-act="goTo" data-page="home">Avbryt</button>'
  );
}

function renderReport(){
  var logs=D.workLogs, objs=D.objects;
  var totH=sum(logs,function(x){ return x.hours; }), totL=sum(objs,function(x){ return x.total; });
  var html='<h2>Rapport</h2>'+
    '<div class="stats">'+
      '<div class="stat"><b>'+logs.length+'</b><span>Poster</span></div>'+
      '<div class="stat"><b>'+Math.round(totH*10)/10+'</b><span>Loggat</span></div>'+
      '<div class="stat"><b>'+Math.round((totL-totH)*10)/10+'</b><span>Kvar</span></div>'+
    '</div>'+
    '<div style="text-align:center;margin:16px 0;">'+
      '<button class="btn" data-act="exportXlsx">📥 Exportera till Excel</button>'+
    '</div>'+
    '<div class="banner" id="xlsx-status"></div>';
  $h('view', html);
}

function renderCalc(){
  var html='<h2>Beräknare</h2>'+
    '<div class="tabs">'+
      '<button class="tabs-btn on" data-v="rate">Timtaxa</button>'+
      '<button class="tabs-btn" data-v="proj">Projektkalkyl</button>'+
    '</div>'+
    '<div id="calc-rate" class="calc-mode">'+
      '<div class="fld"><label>Timmar</label><input id="calc-h" type="number" value="8" min="0" step="0.5"></div>'+
      '<div class="fld"><label>Pris per timme (SEK)</label><input id="calc-rate" type="number" value="500" min="0"></div>'+
      '<div class="fld"><label>Resultat</label><input type="text" value="0 SEK" readonly></div>'+
    '</div>';
  $h('view', html);
}

function renderSettings(){
  $h('view',
    '<h2>Inställningar</h2>'+
    '<div class="fld"><label><input type="checkbox" id="b-photos"> Inkludera foton i säkerhetskopia</label></div>'+
    '<button class="btn" data-act="backupSave">💾 Spara säkerhetskopia</button>'+
    '<div style="margin-top:8px;"></div>'+
    '<div class="fld"><label>Återställ från säkerhetskopia</label><input type="file" accept=".json" data-change="importFile"></div>'+
    '<div style="margin-top:16px;border-top:1px solid var(--line);padding-top:16px;">'+
    '<button class="btn danger" data-act="wipe">🗑️ Rensa all data</button>'+
    '</div>'
  );
}

// Действия (Actions)
var A = {};

A.goTo = function(d){ cur.name = d.page; if(d.oid) { var o = D.objects.find(function(x){ return x.id === d.oid; }); cur.p = o; } render(); };
A.viewDetail = function(d){ cur.name = 'detail'; cur.p = D.objects.find(function(x){ return x.id === d.oid; }); render(); };
A.openSettings = function(){ cur.name = 'settings'; render(); };

A.saveObject = function(){
  var name = val('obj-name'), hours = parseFloat(val('obj-hours')), note = val('obj-note');
  if(!name || !hours) return toast('Fyll i namn och timmar', 'bad');
  D.objects.push({id: uid(), name: name, total: hours, note: note, archived: false});
  save();
  toast('✅ Objekt sparat', 'ok');
  A.goTo({page: 'objects'});
};

A.saveLog = function(){
  var oid = val('log-object'), date = val('log-date'), worker = val('log-worker'), hours = parseFloat(val('log-hours')), note = val('log-note');
  if(!oid || !date || !hours) return toast('Fyll i obligatoriska fält', 'bad');
  D.workLogs.push({id: uid(), objectId: oid, date: date, worker: worker, hours: hours, note: note, photoId: null});
  save();
  toast('✅ Tid loggad', 'ok');
  A.goTo({page: 'home'});
};

A.saveExtra = function(){
  var date = val('extra-date'), desc = val('extra-desc'), hours = parseFloat(val('extra-hours'));
  if(!date || !hours) return toast('Fyll i obligatoriska fält', 'bad');
  D.extraLogs.push({id: uid(), date: date, desc: desc, hours: hours, person: '', photoId: null});
  save();
  toast('✅ Extraarbete sparat', 'ok');
  A.goTo({page: 'home'});
};

A.editObject = function(d){
  var o = D.objects.find(function(x){ return x.id === d.oid; });
  if(!o) return;
  var newName = prompt('Namn:', o.name), newHours = prompt('Totalt timmar:', o.total);
  if(newName) o.name = newName;
  if(newHours) o.total = parseFloat(newHours);
  save();
  render();
};

A.exportXlsx = async function(d){
  var statusEl = $('#xlsx-status');
  if(!statusEl) return;
  
  // Попытка загрузить XLSX если ещё не загружен
  if (!window.XLSX) {
    statusEl.innerHTML = '⏳ Подготовка экспорта...';
    var ok = await XLSXLoader.load();
    if (!ok) {
      statusEl.innerHTML = '<strong style="color:var(--bad)">❌ Экспорт невозможен: XLSX библиотека не загружена</strong>';
      return toast('Экспорт требует интернета для загрузки библиотеки', 'bad');
    }
  }
  
  try {
    var logs = D.workLogs.sort(byDate);
    var wb = window.XLSX.utils.book_new();
    
    // Лист 1: Все логи
    var sheet1_data = [['Дата', 'Объект', 'Рабочий', 'Часы', 'Заметка']];
    logs.forEach(function(l){
      sheet1_data.push([l.date, objName(l.objectId), l.worker||'', l.hours, l.note||'']);
    });
    var ws1 = window.XLSX.utils.aoa_to_sheet(sheet1_data);
    window.XLSX.utils.book_append_sheet(wb, ws1, 'Логи');
    
    // Лист 2: Объекты
    var sheet2_data = [['Объект', 'Всего', 'Логировано', 'Осталось', '%']];
    D.objects.forEach(function(o){
      var s = statusOf(o);
      sheet2_data.push([o.name, o.total, s.logged, s.left, s.pct+'%']);
    });
    var ws2 = window.XLSX.utils.aoa_to_sheet(sheet2_data);
    window.XLSX.utils.book_append_sheet(wb, ws2, 'Объекты');
    
    // Сохранить файл
    window.XLSX.writeFile(wb, 'regal_platt_'+today()+'.xlsx');
    statusEl.innerHTML = '<strong style="color:var(--ok)">✅ Файл успешно экспортирован</strong>';
    toast('✅ Excel экспортирован', 'ok');
  } catch (e) {
    statusEl.innerHTML = '<strong style="color:var(--bad)">❌ Ошибка экспорта: '+(e.message||e)+'</strong>';
    toast('Экспорт не удался', 'bad');
  }
};

A.backupSave = async function(d){
  D.meta.lastBackup = new Date().toISOString();
  save();
  var payload = JSON.stringify({app: 'regal-platt', version: 1, exported: D.meta.lastBackup, data: D});
  var blob = new Blob([payload], {type: 'application/json'});
  var url = URL.createObjectURL(blob);
  var a = document.createElement('a');
  a.href = url;
  a.download = 'regal_platt_backup_'+today()+'.json';
  a.click();
  URL.revokeObjectURL(url);
  toast('✅ Säkerhetskopia sparad', 'ok');
};

A.importFile = async function(d, el){
  var f = el.files && el.files[0];
  if(!f) return;
  try {
    var text = await f.text();
    var parsed = JSON.parse(text);
    if(parsed.data) {
      D = parsed.data;
      save();
      toast('✅ Data återställd', 'ok');
      A.goTo({page: 'home'});
    }
  } catch(e) {
    toast('Filen kunde inte läsas', 'bad');
  }
  el.value = '';
};

A.wipe = function(){
  if(confirm('Rensa ALL data? Det går inte att ångra.')) {
    D = emptyData();
    save();
    toast('All data rensad', 'ok');
    A.goTo({page: 'home'});
  }
};

function toast(msg, type){
  var t = document.createElement('div');
  t.style.cssText = 'position:fixed;bottom:20px;left:12px;right:12px;padding:14px 16px;border-radius:10px;background:'+(type==='ok'?'var(--ok)':type==='warn'?'var(--warn)':'var(--bad)')+';color:white;font-weight:600;z-index:1000;animation:slideUp .3s ease';
  t.textContent = msg;
  document.body.appendChild(t);
  clearTimeout(toast_timeout);
  toast_timeout = setTimeout(function(){ t.remove(); }, 3000);
}

// Event listeners
document.addEventListener('click', function(e){
  var el = e.target.closest('[data-act]');
  if(!el) return;
  var f = A[el.dataset.act];
  if(f) f(el.dataset, el, e);
});

document.addEventListener('change', function(e){
  var a = e.target.dataset && e.target.dataset.change;
  if(a && A[a]) A[a](e.target.dataset, e.target, e);
});

// Инициализация
load();
render();
})();
</script>
</body>
</html>
