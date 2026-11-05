<title>คิวภารกิจกำลังพล</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@500;600;700&family=Sarabun:wght@400;500;600;700&display=swap">
<style>
/* Layout: one ruled-register column; two tabs (roster, missions); missions page adds a queue side column. */
:root{
  --bg:#ECEFE6; --surface:#F8F9F3; --ink:#1C2316; --muted:#5C6652; --line:#D2D8C6;
  --accent:#3B5A2A; --on-accent:#F3F7EA; --alert:#A8480A; --alert-bg:#FAE8D0; --ok:#2E6B3E;
  --t-sc:#2B5B8A; --t-nco:#2C7566; --t-gov:#86641A; --t-tmp:#666C78;
  --f-display:'Chakra Petch','Sarabun',system-ui,sans-serif;
  --f-body:'Sarabun',system-ui,-apple-system,'Noto Sans Thai',sans-serif;
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --bg:#12150E; --surface:#1A1E15; --ink:#E7ECD9; --muted:#9BA48D; --line:#2C3325;
    --accent:#9CC47A; --on-accent:#12150E; --alert:#F2A55A; --alert-bg:#3A2713; --ok:#8FCB9B;
    --t-sc:#8DB7E3; --t-nco:#7CCBB8; --t-gov:#E0BC6B; --t-tmp:#B4BAC6; color-scheme:dark;
  }
}
:root[data-theme="dark"]{
  --bg:#12150E; --surface:#1A1E15; --ink:#E7ECD9; --muted:#9BA48D; --line:#2C3325;
  --accent:#9CC47A; --on-accent:#12150E; --alert:#F2A55A; --alert-bg:#3A2713; --ok:#8FCB9B;
  --t-sc:#8DB7E3; --t-nco:#7CCBB8; --t-gov:#E0BC6B; --t-tmp:#B4BAC6; color-scheme:dark;
}
*{box-sizing:border-box}
body{background:var(--bg);color:var(--ink);font:16px/1.55 var(--f-body);
  padding-block:20px 56px;padding-left:max(16px,env(safe-area-inset-left,0px));padding-right:max(16px,env(safe-area-inset-right,0px))}
.app{max-width:1060px;margin:0 auto;display:flex;flex-direction:column;gap:20px}
h1,h2,h3{font-family:var(--f-display);margin:0;text-wrap:balance;line-height:1.25}
button,input,select,textarea{font:inherit;color:inherit}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}

/* header + tabs */
.top{display:flex;flex-wrap:wrap;align-items:flex-end;justify-content:space-between;gap:8px 16px}
.top h1{font-size:1.75rem;font-weight:700;letter-spacing:.01em}
.top p{margin:2px 0 0;color:var(--muted);font-size:.95rem}
.sync{font-size:.82rem;color:var(--muted);display:inline-flex;align-items:center;gap:6px}
.sync::before{content:"";width:8px;height:8px;border-radius:50%;background:var(--ok)}
.sync[data-s="saving"]::before{background:var(--alert)}
.sync[data-s="error"]::before{background:var(--alert)}
.sync[data-s="local"]::before{background:var(--muted)}
.tabs{display:flex;gap:4px;border-bottom:2px solid var(--line)}
.tab{background:none;border:0;border-bottom:3px solid transparent;margin-bottom:-2px;padding:10px 14px;cursor:pointer;
  font-family:var(--f-display);font-weight:600;font-size:1.02rem;color:var(--muted);display:flex;align-items:center;gap:8px}
.tab b{display:inline-grid;place-items:center;width:22px;height:22px;border-radius:4px;background:var(--line);color:var(--ink);font-size:.8rem}
.tab[aria-selected="true"]{color:var(--ink);border-bottom-color:var(--accent)}
.tab[aria-selected="true"] b{background:var(--accent);color:var(--on-accent)}

/* shared bits */
.card{background:var(--surface);border:1px solid var(--line);border-radius:8px;padding:16px}
.sec-head{display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:8px 12px}
.sec-head h2{font-size:1.15rem}
.muted{color:var(--muted)}
.btn{background:var(--accent);color:var(--on-accent);border:1px solid var(--accent);border-radius:6px;padding:8px 16px;font-weight:600;cursor:pointer;min-height:40px}
.btn:hover{filter:brightness(1.08)}
.btn.sec{background:transparent;color:var(--ink);border-color:var(--line)}
.btn.sec:hover{border-color:var(--muted)}
.btn.ghost{background:transparent;color:var(--accent);border-color:transparent;padding:6px 10px;min-height:36px}
.btn.danger{background:transparent;color:var(--alert);border-color:var(--alert)}
.btn.sm{padding:5px 12px;min-height:34px;font-size:.92rem}
.btn[disabled]{opacity:.45;cursor:not-allowed;filter:none}
label.f{display:flex;flex-direction:column;gap:4px;font-size:.88rem;color:var(--muted);font-weight:500;min-width:0}
input[type=text],input[type=date],input[type=number],select,textarea{
  background:var(--bg);border:1px solid var(--line);border-radius:6px;padding:8px 10px;min-height:42px;width:100%;color:var(--ink)}
textarea{min-height:96px;resize:vertical}
.grid{display:grid;gap:12px;grid-template-columns:repeat(auto-fit,minmax(min(100%,190px),1fr));align-items:end}
.tag{display:inline-block;font-size:.8rem;font-weight:600;line-height:1.2;padding:3px 9px;border-radius:4px;
  color:var(--tc);background:color-mix(in srgb,var(--tc) 14%,var(--surface));border:1px solid color-mix(in srgb,var(--tc) 35%,var(--surface));white-space:nowrap}
.t-sc{--tc:var(--t-sc)}.t-nco{--tc:var(--t-nco)}.t-gov{--tc:var(--t-gov)}.t-tmp{--tc:var(--t-tmp)}
.pill{display:inline-block;font-size:.8rem;font-weight:600;padding:2px 9px;border-radius:999px;background:var(--alert-bg);color:var(--alert);white-space:nowrap}
.pill.wait{background:var(--line);color:var(--muted)}
.pill.done{background:color-mix(in srgb,var(--ok) 16%,var(--surface));color:var(--ok)}

/* stats */
.stats{display:grid;gap:10px;grid-template-columns:repeat(auto-fit,minmax(min(100%,150px),1fr))}
.stat{background:var(--surface);border:1px solid var(--line);border-radius:8px;padding:10px 14px;display:flex;flex-direction:column;gap:2px}
.stat span{font-size:.82rem;color:var(--muted)}
.stat strong{font-family:var(--f-display);font-size:1.7rem;font-variant-numeric:tabular-nums;line-height:1.15}
.stat.hot{background:var(--alert-bg);border-color:color-mix(in srgb,var(--alert) 45%,var(--surface))}
.stat.hot strong,.stat.hot span{color:var(--alert)}

/* toolbar */
.toolbar{display:flex;flex-wrap:wrap;gap:10px 12px;align-items:center;justify-content:space-between}
.chips{display:flex;flex-wrap:wrap;gap:6px}
.chip{background:transparent;border:1px solid var(--line);border-radius:999px;padding:5px 13px;cursor:pointer;font-size:.9rem;font-weight:500}
.chip[aria-pressed="true"]{background:var(--ink);color:var(--bg);border-color:var(--ink)}
.search{max-width:260px;flex:1 1 180px}
details.bulk{margin-top:12px}
details.bulk summary{cursor:pointer;color:var(--accent);font-weight:600;font-size:.92rem}
details.bulk .bulk-body{display:flex;flex-direction:column;gap:8px;margin-top:8px;align-items:flex-start}

/* person register */
.list{display:flex;flex-direction:column;border:1px solid var(--line);border-radius:8px;background:var(--surface);overflow:hidden}
.person{padding:12px 16px;border-top:1px solid var(--line);display:flex;flex-direction:column;gap:8px}
.person:first-child{border-top:0}
.person.prio{background:color-mix(in srgb,var(--alert-bg) 70%,var(--surface));box-shadow:inset 4px 0 0 var(--alert)}
.p-head{display:flex;flex-wrap:wrap;align-items:center;gap:8px 16px;justify-content:space-between}
.p-id{display:flex;flex-wrap:wrap;align-items:center;gap:6px 10px;min-width:0;flex:1 1 240px}
.p-id h3{font-size:1.05rem;font-weight:600;overflow-wrap:anywhere}
.p-score{display:flex;align-items:center;gap:10px}
.meter{display:flex;gap:3px}
.meter i{width:22px;height:9px;border-radius:2px;background:var(--line)}
.meter i.on{background:var(--alert)}
.p-n{font-size:.9rem;color:var(--muted);min-width:7.5em;font-variant-numeric:tabular-nums}
.p-n.hot{color:var(--alert);font-weight:700}
.misses{list-style:none;margin:0;padding:0;display:flex;flex-wrap:wrap;gap:6px}
.misses li{display:inline-flex;align-items:center;gap:2px;border:1px solid var(--line);background:var(--bg);border-radius:6px;padding:1px 2px 1px 10px;font-size:.88rem}
.prio .misses li{border-color:color-mix(in srgb,var(--alert) 40%,var(--line))}
.misses li.act{border-color:color-mix(in srgb,var(--t-sc) 55%,var(--line));background:color-mix(in srgb,var(--t-sc) 10%,var(--bg))}
.x{background:none;border:0;cursor:pointer;width:28px;height:28px;border-radius:4px;color:var(--muted);font-size:1.1rem;line-height:1}
.x:hover{color:var(--alert)}
.prio-note{margin:0;font-size:.88rem;color:var(--alert);font-weight:500}
.panel{border-top:1px dashed var(--line);padding-top:12px;display:flex;flex-direction:column;gap:12px}
.row{display:flex;flex-wrap:wrap;gap:10px 12px;align-items:flex-end}
.row label.f{flex:1 1 160px}
.seg{display:inline-flex;border:1px solid var(--line);border-radius:6px;overflow:hidden}
.seg button{background:var(--bg);border:0;padding:8px 18px;min-height:42px;cursor:pointer;font-weight:600}
.seg button+button{border-left:1px solid var(--line)}
.seg button[aria-pressed="true"]{background:var(--ink);color:var(--bg)}
.empty{padding:28px 16px;text-align:center;color:var(--muted);display:flex;flex-direction:column;align-items:center;gap:10px}

/* missions page */
.cols{display:grid;gap:20px;grid-template-columns:minmax(0,1fr) minmax(0,340px);align-items:start}
.col-main{display:flex;flex-direction:column;gap:16px;min-width:0}
.mform{display:flex;flex-direction:column;gap:14px}
.mform fieldset{border:0;padding:0;margin:0;min-width:0}
.mform legend{font-size:.88rem;color:var(--muted);font-weight:500;padding:0;margin-bottom:6px}
.modes{display:inline-flex;border:1px solid var(--line);border-radius:6px;overflow:hidden}
.modes label{position:relative;cursor:pointer}
.modes input{position:absolute;opacity:0;inset:0;width:100%;height:100%;cursor:pointer}
.modes span{display:block;padding:8px 16px;min-height:42px;font-weight:600;background:var(--bg)}
.modes label+label span{border-left:1px solid var(--line)}
.modes input:checked+span{background:var(--ink);color:var(--bg)}
.modes input:focus-visible+span{outline:2px solid var(--accent);outline-offset:-2px}
.chk-row{display:flex;flex-wrap:wrap;gap:8px 18px}
.chk{display:inline-flex;align-items:center;gap:8px;cursor:pointer;font-size:.95rem}
.chk input{width:18px;height:18px;accent-color:var(--accent)}
.mission{display:flex;flex-direction:column;gap:10px}
.m-head{display:flex;flex-wrap:wrap;gap:6px 12px;align-items:center;justify-content:space-between}
.m-head h3{font-size:1.08rem;overflow-wrap:anywhere}
.m-meta{display:flex;flex-wrap:wrap;gap:6px 14px;color:var(--muted);font-size:.9rem}
.picks{margin:0;padding:0;list-style:none;display:flex;flex-direction:column;border:1px solid var(--line);border-radius:6px;background:var(--bg);counter-reset:pk}
.picks li{counter-increment:pk;display:flex;flex-wrap:wrap;align-items:center;gap:4px 10px;padding:8px 12px;border-top:1px solid var(--line)}
.picks li:first-child{border-top:0}
.picks li::before{content:counter(pk);font-family:var(--f-display);font-weight:700;color:var(--muted);width:1.6em;font-variant-numeric:tabular-nums}
.picks .nm{font-weight:600;overflow-wrap:anywhere}
.picks .why{flex-basis:100%;padding-left:calc(1.6em + 10px);font-size:.85rem;color:var(--alert)}
.lack{margin:0;color:var(--alert);font-size:.92rem;font-weight:500}
.m-actions{display:flex;flex-wrap:wrap;gap:8px;align-items:center}
.note{font-size:.88rem;color:var(--muted);margin:0}
.side{position:sticky;top:12px;display:flex;flex-direction:column;gap:10px;max-height:calc(100vh - 24px);min-width:0}
.side h2{font-size:1.1rem}
.queue{margin:0;padding:0;list-style:none;overflow-y:auto;border:1px solid var(--line);border-radius:6px;background:var(--bg);max-height:60vh}
.queue li{display:flex;align-items:center;gap:8px;padding:7px 10px;border-top:1px solid var(--line);font-size:.92rem}
.queue li:first-child{border-top:0}
.queue .rk{font-family:var(--f-display);font-weight:700;color:var(--muted);width:2em;font-variant-numeric:tabular-nums;flex:none}
.queue .nm{flex:1 1 auto;min-width:0;overflow-wrap:anywhere;font-weight:500}
.queue .rd{font-size:.8rem;color:var(--muted);white-space:nowrap}
.queue li.prio{background:var(--alert-bg)}

.credit{border-top:1px solid var(--line);padding-top:14px;color:var(--muted);font-size:.9rem;font-weight:500}
.toast{position:fixed;left:50%;transform:translateX(-50%);bottom:calc(16px + env(safe-area-inset-bottom,0px));background:var(--ink);color:var(--bg);
  padding:10px 18px;border-radius:8px;font-weight:500;z-index:20;max-width:min(92vw,520px);text-align:center}

@media (max-width:860px){
  .cols{grid-template-columns:minmax(0,1fr)}
  .side{position:static;max-height:none}
}
@media (max-width:480px){
  .top h1{font-size:1.45rem}
  .tab{padding:10px 10px;font-size:.95rem}
  .p-n{min-width:0}
}
@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
</style>

<div class="app">
  <header class="top">
    <div>
      <h1>คิวภารกิจกำลังพล</h1>
      <p>บันทึกการไม่สแกนหน้าและการไม่เข้าร่วมกิจกรรม แล้วจัดกำลังพลเข้าภารกิจตามลำดับ</p>
    </div>
    <span class="sync" id="sync" data-s="local" role="status">กำลังโหลด…</span>
  </header>

  <nav class="tabs" role="tablist" aria-label="หน้าหลัก">
    <button class="tab" role="tab" id="tab-roster" data-action="tab" data-val="roster" aria-selected="true" aria-controls="pg-roster"><b>1</b>กำลังพล</button>
    <button class="tab" role="tab" id="tab-missions" data-action="tab" data-val="missions" aria-selected="false" aria-controls="pg-missions"><b>2</b>จัดภารกิจ</button>
  </nav>

  <main>
    <!-- หน้า 1 -->
    <section id="pg-roster" role="tabpanel" aria-labelledby="tab-roster" style="display:flex;flex-direction:column;gap:16px">
      <div class="stats" id="stats"></div>

      <form class="card" id="f-person" autocomplete="off">
        <div class="grid">
          <label class="f">ชื่อกำลังพล<input type="text" id="pn" placeholder="เช่น ร.ต. สมชาย ใจดี" required></label>
          <label class="f">ประเภทกำลังพล<select id="pt"></select></label>
          <button class="btn" type="submit">เพิ่มกำลังพล</button>
        </div>
        <details class="bulk">
          <summary>เพิ่มหลายคนพร้อมกัน</summary>
          <div class="bulk-body">
            <label class="f" style="width:100%">ชื่อ 1 คนต่อ 1 บรรทัด (ใช้ประเภทที่เลือกไว้ด้านบน)<textarea id="bulk" placeholder="จ.ส.อ. ตัวอย่าง หนึ่ง&#10;จ.ส.อ. ตัวอย่าง สอง"></textarea></label>
            <button class="btn sec" type="button" data-action="bulkadd">เพิ่มทั้งหมด</button>
          </div>
        </details>
      </form>

      <div class="toolbar">
        <div class="chips" id="filters"></div>
        <input type="text" class="search" id="search" placeholder="ค้นหาชื่อ" aria-label="ค้นหาชื่อ">
      </div>

      <div class="list" id="people"></div>
      <p class="note">การไม่สแกนหน้าและการไม่เข้าร่วมกิจกรรมนับรวมกัน ครบ 3 ครั้งกำลังพลจะเข้าคิวภารกิจก่อนลำดับปกติ เมื่อถูกจัดภารกิจแล้วระบบเริ่มนับใหม่ให้โดยอัตโนมัติ</p>
    </section>

    <!-- หน้า 2 -->
    <section id="pg-missions" role="tabpanel" aria-labelledby="tab-missions" hidden>
      <div class="cols">
        <div class="col-main">
          <form class="card mform" id="f-mission" autocomplete="off">
            <h2 style="font-size:1.15rem">เพิ่มภารกิจที่ได้รับมอบหมาย</h2>
            <div class="grid">
              <label class="f">ชื่อภารกิจ<input type="text" id="m-name" placeholder="เช่น เวรรักษาการณ์ ประจำวันเสาร์" required></label>
              <label class="f">วันที่ปฏิบัติ (ถ้ามี)<input type="date" id="m-date"></label>
            </div>
            <fieldset>
              <legend>วิธีจัดคน</legend>
              <div class="modes" role="radiogroup">
                <label><input type="radio" name="m-mode" value="type" checked><span>ระบุตามประเภท</span></label>
                <label><input type="radio" name="m-mode" value="mixed"><span>จัดคละ</span></label>
              </div>
            </fieldset>
            <div id="m-bytype" class="grid"></div>
            <div id="m-mixed" hidden style="display:flex;flex-direction:column;gap:12px">
              <label class="f" style="max-width:200px">จำนวนที่ต้องไป (คน)<input type="number" id="m-total" min="1" max="999" inputmode="numeric" value="3"></label>
              <fieldset>
                <legend>เลือกจากประเภทใดได้บ้าง</legend>
                <div class="chk-row" id="m-allowed"></div>
              </fieldset>
            </div>
            <div><button class="btn" type="submit">เพิ่มภารกิจ</button></div>
          </form>

          <div class="sec-head"><h2>ภารกิจที่รอจัด</h2><button class="btn sec sm" type="button" id="assign-all" data-action="assignall">จัดทุกภารกิจที่รอ</button></div>
          <div id="m-pending" style="display:flex;flex-direction:column;gap:12px"></div>

          <div class="sec-head"><h2>จัดแล้ว</h2></div>
          <div id="m-done" style="display:flex;flex-direction:column;gap:12px"></div>
        </div>

        <aside class="card side">
          <h2>คิวถัดไป</h2>
          <p class="note" style="margin:0">ครบ 3 ครั้งไปก่อน ที่เหลือเรียงตามรอบ ไม่ซ้ำคนจนกว่าทุกคนจะได้ไปครบรอบ</p>
          <div class="chips" id="q-filters"></div>
          <ol class="queue" id="queue"></ol>
        </aside>
      </div>
    </section>
  </main>
  <footer class="credit">จัดทำโดย ส.อ.หญิงฆีตาภัทร ทิพย์บัญฑิต</footer>
</div>
<div class="toast" id="toast" role="status" hidden></div>

<script>
/*LOGIC*/
const TYPES=[
  {k:'sc',label:'นายทหารสัญญาบัตร',short:'สัญญาบัตร'},
  {k:'nco',label:'นายทหารชั้นประทวน',short:'ประทวน'},
  {k:'gov',label:'พนักงานราชการ',short:'พนักงานราชการ'},
  {k:'tmp',label:'ลูกจ้างชั่วคราว',short:'ลูกจ้างชั่วคราว'}
];
const TMAP=Object.fromEntries(TYPES.map(t=>[t.k,t]));
const PL={am:'เช้า',pm:'เย็น'};
const pOf=m=>m.period==='pm'?1:0;
const missCmp=(a,b)=>a.date===b.date?(pOf(a)-pOf(b)||(a.id<b.id?-1:a.id>b.id?1:0)):(a.date<b.date?-1:1);
const sortMiss=l=>[...l].sort(missCmp);
const isPrio=p=>p.misses.length>=3;
const prioStamp=p=>{const m=sortMiss(p.misses)[2];return m.date+(m.period==='pm'?'b':'a');};
function order(list){
  return [...list].sort((a,b)=>{
    const pa=isPrio(a),pb=isPrio(b);
    if(pa!==pb)return pa?-1:1;
    if(pa&&pb){const sa=prioStamp(a),sb=prioStamp(b);if(sa!==sb)return sa<sb?-1:1;}
    if(a.assignCount!==b.assignCount)return a.assignCount-b.assignCount;
    if(a.lastSeq!==b.lastSeq)return a.lastSeq-b.lastSeq;
    return a.addedSeq-b.addedSeq;
  });
}
function needOf(m){return m.mode==='type'?TYPES.reduce((s,t)=>s+(+m.counts[t.k]||0),0):(+m.total||0);}
function pick(m,people){
  const short=[];let out=[];
  if(m.mode==='type'){
    for(const t of TYPES){
      const n=+m.counts[t.k]||0;if(!n)continue;
      const pool=order(people.filter(p=>p.type===t.k));
      if(pool.length<n)short.push({label:t.label,need:n,have:pool.length});
      out=out.concat(pool.slice(0,n));
    }
  }else{
    const pool=order(people.filter(p=>m.allowed.includes(p.type)));
    const n=+m.total||0;
    if(pool.length<n)short.push({label:'ประเภทที่เลือก',need:n,have:pool.length});
    out=pool.slice(0,n);
  }
  out=order(out);
  const entries=out.map(p=>({pid:p.id,name:p.name,type:p.type,prio:isPrio(p),
    snap:{misses:p.misses.map(x=>({...x})),assignCount:p.assignCount,lastSeq:p.lastSeq}}));
  return {out,entries,short};
}
function applyPick(r,seq){
  for(const p of r.out){p.misses=[];p.assignCount+=1;seq+=1;p.lastSeq=seq;}
  return seq;
}
/*END LOGIC*/

(function(){
const LS='kiw-phaarakit-v1';
const $=s=>document.querySelector(s);
const esc=s=>String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const uid=()=>Math.random().toString(36).slice(2,9)+Date.now().toString(36).slice(-3);
const pad=n=>String(n).padStart(2,'0');
const toISO=d=>d.getFullYear()+'-'+pad(d.getMonth()+1)+'-'+pad(d.getDate());
const today=()=>toISO(new Date());
const ago=n=>{const d=new Date();d.setDate(d.getDate()-n);return toISO(d);};
const fmtDate=s=>{if(!s)return '';const [y,m,d]=s.split('-').map(Number);
  return new Date(y,m-1,d).toLocaleDateString('th-TH',{weekday:'short',day:'numeric',month:'short',year:'2-digit'});};

let S={v:1,seq:0,mseq:0,people:[],missions:[]};
const ui={tab:'roster',filter:'all',q:'',open:null,period:{},date:{},adate:{},aname:{},confirm:null,qType:'all',mode:'type'};

function normalize(d){
  const o=JSON.parse(JSON.stringify(d||{}));
  return {v:1,seq:+o.seq||0,mseq:+o.mseq||0,
    people:(o.people||[]).map(p=>({id:p.id,name:p.name||'',type:TMAP[p.type]?p.type:'sc',misses:Array.isArray(p.misses)?p.misses:[],
      assignCount:+p.assignCount||0,lastSeq:+p.lastSeq||0,addedSeq:+p.addedSeq||0,sample:!!p.sample})),
    missions:(o.missions||[]).map(m=>({id:m.id,name:m.name||'',date:m.date||'',mode:m.mode==='mixed'?'mixed':'type',
      counts:m.counts||{},total:+m.total||0,allowed:Array.isArray(m.allowed)?m.allowed:TYPES.map(t=>t.k),
      status:m.status==='assigned'?'assigned':'pending',assigned:m.assigned||[],assignedSeq:+m.assignedSeq||0,assignedOn:m.assignedOn||'',sample:!!m.sample}))
  };
}
try{const raw=localStorage.getItem(LS);if(raw)S=normalize(JSON.parse(raw));}catch(e){}

/* ---------- persistence ---------- */
let ref=null,saveT=null,saving=false,dirty=false;
function setSync(s,txt){const el=$('#sync');el.dataset.s=s;el.textContent=txt;}
function persist(){
  try{localStorage.setItem(LS,JSON.stringify(S));}catch(e){}
  if(ref){dirty=true;setSync('saving','กำลังบันทึก…');clearTimeout(saveT);saveT=setTimeout(flush,350);}
}
async function flush(){
  if(saving){saveT=setTimeout(flush,300);return;}
  if(!dirty)return;
  dirty=false;saving=true;
  try{await ref.set(JSON.parse(JSON.stringify(S)));if(!dirty)setSync('ok','บันทึกแล้ว');}
  catch(e){setSync('error','บันทึกไม่สำเร็จ ลองใหม่อีกครั้ง');}
  saving=false;
  if(dirty)flush();
}
async function initDb(){
  let db=null;
  try{db=window.claude&&window.claude.use?await window.claude.use('db'):null;}catch(e){db=null;}
  if(!db){setSync('local','เก็บในเบราว์เซอร์นี้เท่านั้น');return;}
  ref=db.doc('roster/state');
  setSync('ok','บันทึกแล้ว');
  ref.onSnapshot(snap=>{
    if(snap.metadata&&snap.metadata.hasPendingWrites)return;
    if(!snap.exists){if(S.people.length||S.missions.length){dirty=true;flush();}return;}
    if(dirty||saving)return;
    const next=normalize(snap.data());
    if(JSON.stringify(next)===JSON.stringify(S))return;
    S=next;
    try{localStorage.setItem(LS,JSON.stringify(S));}catch(e){}
    renderAll();setSync('ok','บันทึกแล้ว');
  },()=>setSync('error','เชื่อมต่อที่เก็บข้อมูลไม่ได้'));
}

/* ---------- helpers ---------- */
let toastT=null;
function toast(msg){const t=$('#toast');t.textContent=msg;t.hidden=false;clearTimeout(toastT);toastT=setTimeout(()=>{t.hidden=true;},3600);}
const person=id=>S.people.find(p=>p.id===id);
const tagHTML=k=>`<span class="tag t-${k}">${esc(TMAP[k].label)}</span>`;
const missText=m=>m.kind==='act'?fmtDate(m.date)+' · ไม่เข้าร่วม '+(m.act||'กิจกรรม'):fmtDate(m.date)+' · ไม่สแกน'+(PL[m.period]||'');
function reqText(m){
  if(m.mode==='type')return TYPES.filter(t=>+m.counts[t.k]>0).map(t=>t.short+' '+m.counts[t.k]).join(' · ')||'—';
  const al=m.allowed.length===TYPES.length?'ทุกประเภท':m.allowed.map(k=>TMAP[k].short).join(' · ');
  return 'คละ '+m.total+' คน ('+al+')';
}

/* ---------- render: page 1 ---------- */
function renderStats(){
  const c=k=>S.people.filter(p=>p.type===k).length;
  const hot=S.people.filter(isPrio).length;
  $('#stats').innerHTML=
    `<div class="stat"><span>กำลังพลทั้งหมด</span><strong>${S.people.length}</strong></div>`+
    TYPES.map(t=>`<div class="stat"><span>${esc(t.label)}</span><strong>${c(t.k)}</strong></div>`).join('')+
    `<div class="stat ${hot?'hot':''}"><span>ครบ 3 ครั้ง</span><strong>${hot}</strong></div>`;
}
function renderFilters(){
  const hot=S.people.filter(isPrio).length;
  const items=[['all','ทั้งหมด'],['prio','ครบ 3 ครั้ง ('+hot+')']].concat(TYPES.map(t=>[t.k,t.short]));
  $('#filters').innerHTML=items.map(([k,l])=>`<button type="button" class="chip" data-action="filter" data-val="${k}" aria-pressed="${ui.filter===k}">${esc(l)}</button>`).join('');
}
function personHTML(p){
  const n=p.misses.length,prio=n>=3,open=ui.open===p.id;
  const segs=[0,1,2].map(i=>`<i class="${i<n?'on':''}"></i>`).join('');
  const chips=sortMiss(p.misses).map(m=>`<li class="${m.kind==='act'?'act':''}"><span>${esc(missText(m))}</span><button type="button" class="x" data-action="delmiss" data-id="${p.id}" data-mid="${m.id}" aria-label="ลบ ${esc(missText(m))}">×</button></li>`).join('');
  const label=prio?('ครบ 3 ครั้ง'+(n>3?' (รวม '+n+')':'')):('ไม่สแกน/ไม่เข้าร่วม '+n+'/3');
  let panel='';
  if(open){
    const per=ui.period[p.id]||'am',dt=ui.date[p.id]||today();
    const opts=TYPES.map(t=>`<option value="${t.k}" ${t.k===p.type?'selected':''}>${esc(t.label)}</option>`).join('');
    const del=ui.confirm===('p:'+p.id)
      ?`<button type="button" class="btn danger sm" data-action="delperson" data-id="${p.id}">ยืนยันลบ ${esc(p.name)}</button><button type="button" class="btn sec sm" data-action="cancel">ยกเลิก</button>`
      :`<button type="button" class="btn danger sm" data-action="delperson" data-id="${p.id}">ลบกำลังพล</button>`;
    panel=`<div class="panel">
      <div class="row">
        <label class="f" style="flex:0 1 190px">วันที่ไม่สแกน<input type="date" id="d-${p.id}" value="${dt}"></label>
        <div class="seg" role="group" aria-label="ช่วงเวลา">
          <button type="button" data-action="period" data-id="${p.id}" data-val="am" aria-pressed="${per==='am'}">เช้า</button>
          <button type="button" data-action="period" data-id="${p.id}" data-val="pm" aria-pressed="${per==='pm'}">เย็น</button>
        </div>
        <button type="button" class="btn" data-action="addmiss" data-id="${p.id}">บันทึกไม่สแกน</button>
      </div>
      <div class="row">
        <label class="f" style="flex:0 1 190px">วันที่ไม่เข้าร่วมกิจกรรม<input type="date" id="ad-${p.id}" value="${ui.adate[p.id]||today()}"></label>
        <label class="f">ชื่อกิจกรรมที่ไม่เข้าร่วม<input type="text" id="an-${p.id}" value="${esc(ui.aname[p.id]||'')}" placeholder="เช่น เคารพธงชาติ กีฬาสี อบรม"></label>
        <button type="button" class="btn" data-action="addact" data-id="${p.id}">บันทึกไม่เข้าร่วม</button>
      </div>
      <div class="row">
        <label class="f">ชื่อ<input type="text" id="n-${p.id}" value="${esc(p.name)}"></label>
        <label class="f" style="flex:0 1 220px">ประเภท<select id="t-${p.id}">${opts}</select></label>
        <button type="button" class="btn sec sm" data-action="saveedit" data-id="${p.id}">บันทึกการแก้ไข</button>
        ${del}
      </div>
    </div>`;
  }
  return `<article class="person${prio?' prio':''}">
    <div class="p-head">
      <div class="p-id"><h3>${esc(p.name)}</h3>${tagHTML(p.type)}</div>
      <div class="p-score"><div class="meter" role="img" aria-label="ไม่สแกนหรือไม่เข้าร่วมกิจกรรม ${n} จาก 3 ครั้ง">${segs}</div><span class="p-n${prio?' hot':''}">${label}</span></div>
      <button type="button" class="btn ghost sm" data-action="toggle" data-id="${p.id}" aria-expanded="${open}">${open?'ปิด':'บันทึก / แก้ไข'}</button>
    </div>
    ${n?`<ul class="misses">${chips}</ul>`:''}
    ${prio?'<p class="prio-note">เข้าคิวรับภารกิจก่อนลำดับปกติ เมื่อถูกจัดภารกิจแล้วจะเริ่มนับใหม่</p>':''}
    ${panel}
  </article>`;
}
function renderPeople(){
  const q=ui.q.trim().toLowerCase();
  let ps=S.people.filter(p=>(ui.filter==='all'||(ui.filter==='prio'?isPrio(p):p.type===ui.filter))&&(!q||p.name.toLowerCase().includes(q)));
  ps.sort((a,b)=>(isPrio(b)-isPrio(a))||(b.misses.length-a.misses.length)||(a.addedSeq-b.addedSeq));
  const box=$('#people');
  if(!S.people.length){
    box.innerHTML=`<div class="empty"><span>ยังไม่มีกำลังพลในทะเบียน เพิ่มรายชื่อด้านบน หรือลองดูตัวอย่างการทำงานก่อน</span><button type="button" class="btn sec" data-action="sample">ใส่ข้อมูลตัวอย่าง</button></div>`;
    return;
  }
  if(!ps.length){box.innerHTML=`<div class="empty"><span>ไม่พบกำลังพลตามตัวกรองนี้</span></div>`;return;}
  let html=ps.map(personHTML).join('');
  if(S.people.some(p=>p.sample)||S.missions.some(m=>m.sample))
    html+=`<div class="empty" style="padding:12px"><span class="note">มีข้อมูลตัวอย่างอยู่ในทะเบียน</span><button type="button" class="btn sec sm" data-action="clearsample">ล้างข้อมูลตัวอย่าง</button></div>`;
  box.innerHTML=html;
}

/* ---------- render: page 2 ---------- */
function simulate(){
  const ps=JSON.parse(JSON.stringify(S.people));let seq=S.seq;const res={};
  for(const m of S.missions.filter(x=>x.status==='pending')){
    const r=pick(m,ps);res[m.id]=r;
    if(!r.short.length)seq=applyPick(r,seq);
  }
  return res;
}
function picksHTML(entries,showWhy){
  return `<ol class="picks">`+entries.map(e=>`<li><span class="nm">${esc(e.name)}</span>${tagHTML(e.type)}${e.prio?'<span class="pill">ครบ 3 ครั้ง</span>':''}`+
    (showWhy&&e.prio?`<span class="why">ไม่สแกน/ไม่เข้าร่วม: ${esc(sortMiss(e.snap.misses).map(missText).join(' · '))}</span>`:'')+`</li>`).join('')+`</ol>`;
}
function renderMissions(){
  const sim=simulate();
  const pend=S.missions.filter(m=>m.status==='pending');
  const done=S.missions.filter(m=>m.status==='assigned').sort((a,b)=>b.assignedSeq-a.assignedSeq);
  const lastSeq=done.length?done[0].assignedSeq:0;
  $('#assign-all').hidden=pend.length<2;
  $('#m-pending').innerHTML=pend.length?pend.map((m,i)=>{
    const r=sim[m.id];
    const delBtn=ui.confirm==='m:'+m.id
      ?`<button type="button" class="btn danger sm" data-action="delmission" data-id="${m.id}">ยืนยันลบ</button><button type="button" class="btn sec sm" data-action="cancel">ยกเลิก</button>`
      :`<button type="button" class="btn sec sm" data-action="delmission" data-id="${m.id}">ลบภารกิจ</button>`;
    const body=r.short.length
      ?`<p class="lack">ยังจัดไม่ได้ ${r.short.map(s=>esc(s.label)+' มี '+s.have+' ต้องการ '+s.need).join(' · ')}</p>`
      :`<div><p class="note" style="margin-bottom:6px">${i===0?'จะจัดให้ตามคิวปัจจุบัน':'จะจัดให้หลังจากภารกิจก่อนหน้าถูกจัดแล้ว'}</p>${picksHTML(r.entries,true)}</div>`;
    const act=i===0
      ?`<button type="button" class="btn" data-action="assign" data-id="${m.id}" ${r.short.length?'disabled':''}>จัดกำลังพล</button>`
      :`<span class="note">รอภารกิจก่อนหน้า</span>`;
    return `<article class="card mission"><div class="m-head"><h3>${esc(m.name)}</h3><span class="pill wait">รอจัด</span></div>
      <div class="m-meta"><span>ต้องการ ${needOf(m)} คน</span><span>${esc(reqText(m))}</span>${m.date?`<span>${esc(fmtDate(m.date))}</span>`:''}</div>
      ${body}<div class="m-actions">${act}${delBtn}</div></article>`;
  }).join(''):`<div class="card empty"><span>ไม่มีภารกิจที่รอจัด เพิ่มภารกิจใหม่ด้านบน</span></div>`;
  $('#m-done').innerHTML=done.length?done.map(m=>{
    const delBtn=ui.confirm==='m:'+m.id
      ?`<button type="button" class="btn danger sm" data-action="delmission" data-id="${m.id}">ยืนยันลบ</button><button type="button" class="btn sec sm" data-action="cancel">ยกเลิก</button>`
      :`<button type="button" class="btn sec sm" data-action="delmission" data-id="${m.id}">ลบบันทึก</button>`;
    const undo=m.assignedSeq===lastSeq?`<button type="button" class="btn sec sm" data-action="undo" data-id="${m.id}">ยกเลิกการจัด</button>`:'';
    const reset=m.assigned.filter(e=>e.snap.misses.length).length;
    return `<article class="card mission"><div class="m-head"><h3>${esc(m.name)}</h3><span class="pill done">จัดแล้ว ${esc(fmtDate(m.assignedOn))}</span></div>
      <div class="m-meta"><span>${m.assigned.length} คน</span><span>${esc(reqText(m))}</span>${m.date?`<span>${esc(fmtDate(m.date))}</span>`:''}</div>
      ${picksHTML(m.assigned,true)}
      ${reset?`<p class="note">เริ่มนับการไม่สแกนใหม่ให้ ${reset} คนที่มีประวัติไม่สแกนแล้ว</p>`:''}
      <div class="m-actions">${undo}${delBtn}</div></article>`;
  }).join(''):`<div class="card empty"><span>ยังไม่มีภารกิจที่จัดแล้ว</span></div>`;
}
function renderQueue(){
  const items=[['all','ทั้งหมด']].concat(TYPES.map(t=>[t.k,t.short]));
  $('#q-filters').innerHTML=items.map(([k,l])=>`<button type="button" class="chip" data-action="qtype" data-val="${k}" aria-pressed="${ui.qType===k}">${esc(l)}</button>`).join('');
  const all=order(S.people);
  const list=ui.qType==='all'?all:all.filter(p=>p.type===ui.qType);
  $('#queue').innerHTML=list.length?list.map((p,i)=>`<li class="${isPrio(p)?'prio':''}"><span class="rk">${i+1}</span><span class="nm">${esc(p.name)}</span>${isPrio(p)?'<span class="pill">ครบ 3 ครั้ง</span>':`<span class="rd">ไปแล้ว ${p.assignCount} รอบ</span>`}</li>`).join('')
    :`<li><span class="muted">ยังไม่มีกำลังพล</span></li>`;
}
function renderTabs(){
  for(const k of ['roster','missions']){
    $('#tab-'+k).setAttribute('aria-selected',String(ui.tab===k));
    $('#pg-'+k).hidden=ui.tab!==k;
  }
}
function renderAll(){renderTabs();renderStats();renderFilters();renderPeople();renderMissions();renderQueue();}

/* ---------- actions ---------- */
function addPerson(name,type){
  const nm=name.trim();if(!nm)return false;
  const min=S.people.length?Math.min(...S.people.map(p=>p.assignCount)):0;
  S.seq+=1;
  S.people.push({id:uid(),name:nm,type,misses:[],assignCount:min,lastSeq:0,addedSeq:S.seq,sample:false});
  return true;
}
function commit(m){
  const r=pick(m,S.people);
  if(r.short.length)return false;
  S.seq=applyPick(r,S.seq);
  m.status='assigned';m.assigned=r.entries;m.assignedSeq=++S.mseq;m.assignedOn=today();
  return true;
}
const handlers={
  tab(el){ui.tab=el.dataset.val;renderTabs();if(ui.tab==='missions')renderMissions();},
  filter(el){ui.filter=el.dataset.val;renderFilters();renderPeople();},
  qtype(el){ui.qType=el.dataset.val;renderQueue();},
  toggle(el){ui.open=ui.open===el.dataset.id?null:el.dataset.id;ui.confirm=null;renderPeople();},
  period(el){ui.period[el.dataset.id]=el.dataset.val;renderPeople();},
  cancel(){ui.confirm=null;renderPeople();renderMissions();},
  addmiss(el){
    const p=person(el.dataset.id);if(!p)return;
    const date=($('#d-'+p.id)||{}).value;
    if(!date){toast('เลือกวันที่ก่อนบันทึก');return;}
    const period=ui.period[p.id]||'am';ui.date[p.id]=date;
    if(p.misses.some(m=>m.kind!=='act'&&m.date===date&&m.period===period)){toast('บันทึกวันและช่วงนี้ไว้แล้ว');return;}
    p.misses.push({id:uid(),date,period});
    persist();renderAll();
    toast(p.misses.length>=3?p.name+' ไม่สแกนครบ 3 ครั้ง เข้าคิวภารกิจแล้ว':'บันทึกแล้ว ไม่สแกน '+p.misses.length+'/3');
  },
  addact(el){
    const p=person(el.dataset.id);if(!p)return;
    const date=($('#ad-'+p.id)||{}).value;
    const act=(($('#an-'+p.id)||{}).value||'').trim();
    if(!date){toast('เลือกวันที่ก่อนบันทึก');return;}
    if(!act){toast('ใส่ชื่อกิจกรรมที่ไม่เข้าร่วม');return;}
    ui.adate[p.id]=date;
    if(p.misses.some(m=>m.kind==='act'&&m.date===date&&m.act===act)){toast('บันทึกกิจกรรมนี้ในวันเดียวกันไว้แล้ว');return;}
    p.misses.push({id:uid(),kind:'act',date,period:'',act});
    ui.aname[p.id]='';
    persist();renderAll();
    toast(p.misses.length>=3?p.name+' ครบ 3 ครั้ง เข้าคิวภารกิจแล้ว':'บันทึกแล้ว นับรวม '+p.misses.length+'/3');
  },
  delmiss(el){const p=person(el.dataset.id);if(!p)return;p.misses=p.misses.filter(m=>m.id!==el.dataset.mid);persist();renderAll();},
  saveedit(el){
    const p=person(el.dataset.id);if(!p)return;
    const nm=($('#n-'+p.id).value||'').trim();if(!nm){toast('ชื่อต้องไม่ว่าง');return;}
    p.name=nm;p.type=$('#t-'+p.id).value;persist();renderAll();toast('แก้ไขแล้ว');
  },
  delperson(el){
    const id=el.dataset.id;
    if(ui.confirm!=='p:'+id){ui.confirm='p:'+id;renderPeople();return;}
    S.people=S.people.filter(p=>p.id!==id);ui.open=null;ui.confirm=null;persist();renderAll();toast('ลบแล้ว');
  },
  bulkadd(){
    const type=$('#pt').value;
    const lines=$('#bulk').value.split('\n').map(s=>s.trim()).filter(Boolean);
    if(!lines.length){toast('ใส่ชื่ออย่างน้อย 1 บรรทัด');return;}
    lines.forEach(n=>addPerson(n,type));$('#bulk').value='';persist();renderAll();toast('เพิ่ม '+lines.length+' คนแล้ว');
  },
  assign(el){
    const m=S.missions.find(x=>x.id===el.dataset.id);if(!m)return;
    if(!commit(m)){toast('กำลังพลไม่พอสำหรับภารกิจนี้');return;}
    persist();renderAll();toast('จัดกำลังพลแล้ว เริ่มนับการไม่สแกนใหม่ให้ผู้ที่ถูกจัด');
  },
  assignall(){
    let n=0;
    for(const m of S.missions.filter(x=>x.status==='pending')){
      if(!commit(m)){toast('จัดแล้ว '+n+' ภารกิจ หยุดที่ "'+m.name+'" เพราะกำลังพลไม่พอ');persist();renderAll();return;}
      n++;
    }
    persist();renderAll();if(n)toast('จัดแล้ว '+n+' ภารกิจ');
  },
  undo(el){
    const m=S.missions.find(x=>x.id===el.dataset.id);if(!m)return;
    for(const e of m.assigned){
      const p=person(e.pid);if(!p)continue;
      p.misses=e.snap.misses.concat(p.misses);p.assignCount=e.snap.assignCount;p.lastSeq=e.snap.lastSeq;
    }
    m.status='pending';m.assigned=[];m.assignedSeq=0;m.assignedOn='';
    persist();renderAll();toast('ยกเลิกการจัดแล้ว คืนจำนวนไม่สแกนให้ทุกคน');
  },
  delmission(el){
    const id=el.dataset.id;
    if(ui.confirm!=='m:'+id){ui.confirm='m:'+id;renderMissions();return;}
    S.missions=S.missions.filter(m=>m.id!==id);ui.confirm=null;persist();renderAll();toast('ลบภารกิจแล้ว');
  },
  sample(){
    const mk=(name,type,misses)=>{S.seq+=1;return {id:uid(),name,type,misses:misses.map(([d,p])=>({id:uid(),date:ago(d),period:p})),assignCount:0,lastSeq:0,addedSeq:S.seq,sample:true};};
    S.people.push(
      mk('ตัวอย่าง ก (สัญญาบัตร)','sc',[[6,'am'],[4,'pm'],[1,'am']]),
      mk('ตัวอย่าง ข (สัญญาบัตร)','sc',[[3,'pm']]),
      mk('ตัวอย่าง ค (ประทวน)','nco',[[7,'pm'],[5,'am'],[2,'pm']]),
      mk('ตัวอย่าง ง (ประทวน)','nco',[[2,'am'],[1,'pm']]),
      mk('ตัวอย่าง จ (ประทวน)','nco',[]),
      mk('ตัวอย่าง ฉ (พนักงานราชการ)','gov',[[4,'am']]),
      mk('ตัวอย่าง ช (พนักงานราชการ)','gov',[]),
      mk('ตัวอย่าง ซ (ลูกจ้างชั่วคราว)','tmp',[[5,'pm'],[3,'am']]),
      mk('ตัวอย่าง ฌ (ลูกจ้างชั่วคราว)','tmp',[])
    );
    S.missions.push(
      {id:uid(),name:'ตัวอย่าง: เวรรักษาการณ์',date:'',mode:'type',counts:{sc:1,nco:2,gov:0,tmp:0},total:0,allowed:TYPES.map(t=>t.k),status:'pending',assigned:[],assignedSeq:0,assignedOn:'',sample:true},
      {id:uid(),name:'ตัวอย่าง: ช่วยงานกิจกรรมหน่วย',date:'',mode:'mixed',counts:{},total:3,allowed:TYPES.map(t=>t.k),status:'pending',assigned:[],assignedSeq:0,assignedOn:'',sample:true}
    );
    persist();renderAll();toast('ใส่ข้อมูลตัวอย่างแล้ว');
  },
  clearsample(){
    S.people=S.people.filter(p=>!p.sample);S.missions=S.missions.filter(m=>!m.sample);
    persist();renderAll();toast('ล้างข้อมูลตัวอย่างแล้ว');
  }
};
document.addEventListener('click',e=>{
  const el=e.target.closest('[data-action]');if(!el||el.disabled)return;
  const h=handlers[el.dataset.action];if(h)h(el);
});
document.addEventListener('input',e=>{
  const t=e.target;
  if(t.id&&t.id.startsWith('d-'))ui.date[t.id.slice(2)]=t.value;
  else if(t.id&&t.id.startsWith('ad-'))ui.adate[t.id.slice(3)]=t.value;
  else if(t.id&&t.id.startsWith('an-'))ui.aname[t.id.slice(3)]=t.value;
});
$('#search').addEventListener('input',e=>{ui.q=e.target.value;renderPeople();});

/* ---------- static forms ---------- */
$('#pt').innerHTML=TYPES.map(t=>`<option value="${t.k}">${esc(t.label)}</option>`).join('');
$('#m-bytype').innerHTML=TYPES.map(t=>`<label class="f">${esc(t.label)} (คน)<input type="number" id="mn-${t.k}" min="0" max="999" inputmode="numeric" value="0"></label>`).join('');
$('#m-allowed').innerHTML=TYPES.map(t=>`<label class="chk"><input type="checkbox" name="m-al" value="${t.k}" checked>${esc(t.label)}</label>`).join('');
function syncMode(){
  const mixed=ui.mode==='mixed';
  $('#m-bytype').hidden=mixed;
  $('#m-mixed').hidden=!mixed;
  $('#m-mixed').style.display=mixed?'flex':'none';
}
document.querySelectorAll('input[name="m-mode"]').forEach(r=>r.addEventListener('change',()=>{ui.mode=document.querySelector('input[name="m-mode"]:checked').value;syncMode();}));
syncMode();

$('#f-person').addEventListener('submit',e=>{
  e.preventDefault();
  if(addPerson($('#pn').value,$('#pt').value)){
    $('#pn').value='';persist();renderAll();$('#pn').focus();toast('เพิ่มกำลังพลแล้ว');
  }
});
$('#f-mission').addEventListener('submit',e=>{
  e.preventDefault();
  const name=$('#m-name').value.trim();if(!name){toast('ใส่ชื่อภารกิจ');return;}
  const m={id:uid(),name,date:$('#m-date').value,mode:ui.mode,counts:{},total:0,allowed:TYPES.map(t=>t.k),status:'pending',assigned:[],assignedSeq:0,assignedOn:'',sample:false};
  if(ui.mode==='type'){
    TYPES.forEach(t=>{m.counts[t.k]=Math.max(0,Math.floor(+$('#mn-'+t.k).value||0));});
    if(!needOf(m)){toast('ระบุจำนวนคนอย่างน้อย 1 คน');return;}
  }else{
    m.total=Math.max(0,Math.floor(+$('#m-total').value||0));
    m.allowed=[...document.querySelectorAll('input[name="m-al"]:checked')].map(x=>x.value);
    if(!m.total){toast('ระบุจำนวนคนอย่างน้อย 1 คน');return;}
    if(!m.allowed.length){toast('เลือกประเภทอย่างน้อย 1 ประเภท');return;}
  }
  S.missions.push(m);
  $('#m-name').value='';$('#m-date').value='';
  persist();renderAll();toast('เพิ่มภารกิจแล้ว');
});

renderAll();
initDb();
})();
</script>
