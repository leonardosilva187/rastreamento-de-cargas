[index (1).html](https://github.com/user-attachments/files/32937760/index.1.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Rastreamento de Cargas — DF e Entorno</title>
<style>
:root{
  --bg:#0E1B22; --surface:#132630; --surface2:#0B1920; --line:#1F3A46;
  --ink:#EAF2F2; --muted:#8FB0B8; --teal:#2BD4C4; --amber:#F0A93B; --red:#E2665B; --blue:#4E9CE0;
}
*{box-sizing:border-box;}
body{margin:0; background:var(--bg); color:var(--ink); font-family:-apple-system,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;}
header{position:sticky; top:0; z-index:5; display:flex; align-items:center; justify-content:space-between; gap:10px; padding:16px 22px; background:var(--surface2); border-bottom:1px solid var(--line); flex-wrap:wrap;}
header h1{font-size:18px; margin:0; font-weight:650;}
.tag{font-size:12px; padding:4px 10px; border-radius:20px; background:rgba(43,212,196,.15); color:var(--teal); font-weight:650;}
.wrap{max-width:1280px; margin:0 auto; padding:20px;}
.layout{display:grid; grid-template-columns:230px 1fr; gap:18px;}
@media (max-width:860px){.layout{grid-template-columns:1fr;}}
.panel{background:var(--surface); border:1px solid var(--line); border-radius:10px; padding:16px;}
.filters label,.form label{display:block; font-size:12px; color:var(--muted); margin:10px 0 5px;}
.filters select,.filters input,.form select,.form input{width:100%; padding:8px 9px; background:var(--surface2); border:1px solid var(--line); color:var(--ink); border-radius:7px; font-size:13.5px;}
.filters h2,.form h2{font-size:13px; margin:0; color:var(--muted); font-weight:650;}
.kpis{display:grid; grid-template-columns:repeat(auto-fit,minmax(150px,1fr)); gap:12px; margin-bottom:16px;}
.kpi{background:var(--surface); border:1px solid var(--line); border-radius:10px; padding:14px 16px;}
.kpi .n{font-size:22px; font-weight:700;}
.kpi .l{font-size:12px; color:var(--muted); margin-top:3px;}
.grid2{display:grid; grid-template-columns:1.1fr 1fr; gap:16px; margin-bottom:16px;}
@media (max-width:860px){.grid2{grid-template-columns:1fr;}}
.panel h3{margin:0 0 12px; font-size:14.5px; font-weight:650;}
.region-row{display:flex; align-items:center; gap:10px; margin:9px 0; font-size:13px;}
.region-row .name{width:150px; color:var(--muted); flex-shrink:0; font-size:12.5px; white-space:nowrap; overflow:hidden; text-overflow:ellipsis;}
.region-row .bar-track{flex:1; height:9px; background:var(--surface2); border-radius:5px; overflow:hidden; border:1px solid var(--line);}
.region-row .bar-fill{height:100%; background:linear-gradient(90deg,var(--teal),var(--blue));}
.region-row .val{width:78px; text-align:right; color:var(--muted); flex-shrink:0;}
table{width:100%; border-collapse:collapse; font-size:13px;}
th{text-align:left; color:var(--muted); font-weight:600; font-size:11.5px; padding:8px 10px; border-bottom:1px solid var(--line);}
td{padding:8px 10px; border-bottom:1px solid var(--line); vertical-align:middle;}
.tablewrap{overflow-x:auto; max-height:340px; overflow-y:auto;}
.tag.status{padding:3px 9px; border-radius:20px; font-size:11.5px; font-weight:600; white-space:nowrap;}
.tag.ok{background:rgba(43,212,196,.15); color:var(--teal);}
.tag.late{background:rgba(226,102,91,.15); color:var(--red);}
.tag.transit{background:rgba(78,156,224,.15); color:var(--blue);}
.tag.pending{background:rgba(240,169,59,.15); color:var(--amber);}
canvas{width:100%; display:block;}
.empty{color:var(--muted); font-size:13px; padding:20px 0; text-align:center;}
button{cursor:pointer; border:none; border-radius:7px; padding:9px 12px; font-size:13px; font-weight:650;}
.btn-primary{background:var(--teal); color:#04201C; width:100%; margin-top:12px;}
.btn-ghost{background:transparent; border:1px solid var(--line); color:var(--muted); width:100%;}
.del{background:transparent; color:var(--red); font-size:12px; padding:4px 8px; border:1px solid rgba(226,102,91,.3);}
.readonly-note{font-size:12px; color:var(--muted); margin-top:10px; line-height:1.5;}
.import-box{margin-top:16px;padding-top:14px;border-top:1px solid var(--line);}
.import-box h3{font-size:13px;margin:0 0 6px;}
.import-box .help{font-size:11.5px;color:var(--muted);line-height:1.45;margin-bottom:8px;}
.import-box textarea{width:100%;min-height:150px;resize:vertical;padding:9px;background:var(--surface2);border:1px solid var(--line);color:var(--ink);border-radius:7px;font:12px ui-monospace,SFMono-Regular,Consolas,monospace;}
.import-actions{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:8px;}
.import-actions button{width:100%;}
.btn-import{background:var(--blue);color:#06131B;}
.import-preview{margin-top:10px;font-size:12px;color:var(--muted);line-height:1.5;}
.import-status{margin-top:8px;padding:8px 9px;border:1px solid var(--line);border-radius:7px;background:var(--surface2);font-size:12px;display:none;}
.import-status.show{display:block;}
.import-status.ok{color:var(--teal);}
.import-status.err{color:var(--red);}
@media (max-width:520px){.import-actions{grid-template-columns:1fr;}}
</style>
</head>
<body>
<header>
  <h1>Rastreamento de Cargas <span style="color:var(--teal); font-weight:650;">· DF e Entorno</span></h1>
  <span class="tag" id="statusTag">conectando…</span>
</header>
<div class="wrap">
<div class="layout">
  <div>
    <div class="panel filters">
      <h2>Filtros</h2>
      <label>Buscar Carregamento</label>
      <input id="fCarregamento" type="text" placeholder="Ex: 9021">
      <label>Buscar NF</label>
      <input id="fNf" type="text" placeholder="Ex: 48213">
      <label>Bairro / Região Administrativa</label>
      <select id="fRegiao"><option value="">Todas</option></select>
      <label>Status</label>
      <select id="fStatus">
        <option value="">Todos</option>
        <option value="ok">Entregue no prazo</option>
        <option value="late">Entregue com atraso</option>
        <option value="transit">Em trânsito</option>
        <option value="pending">Pendente</option>
      </select>
      <label>Motorista</label>
      <select id="fMot"><option value="">Todos</option></select>
      <label>Ano</label>
      <select id="fAno"><option value="">Todos</option></select>
    </div>

    <div class="panel" id="editGate" style="margin-top:16px;">
      <h2>Modo edição</h2>
      <div id="gateLocked">
        <label>PIN de edição</label>
        <input id="pinInput" type="password" placeholder="••••">
        <button class="btn-ghost" id="btnUnlock" style="margin-top:12px;">Entrar</button>
      </div>
      <div id="formPanel" class="form" style="display:none; margin-top:8px;">
        <label>Número do Carregamento</label>
        <input id="in_carregamento" type="text" placeholder="Ex: 9021">
        <label>Número da NF</label>
        <input id="in_nf" type="number" placeholder="Ex: 48301">
        <label>Bairro / RA</label>
        <select id="in_regiao"></select>
        <label>Motorista</label>
        <input id="in_motorista" type="text" placeholder="Nome do motorista">
        <label>Valor (R$)</label>
        <input id="in_valor" type="number" placeholder="Ex: 3200">
        <label>Status</label>
        <select id="in_status">
          <option value="ok">Entregue no prazo</option>
          <option value="late">Entregue com atraso</option>
          <option value="transit">Em trânsito</option>
          <option value="pending">Pendente</option>
        </select>
        <label>Mês</label>
        <select id="in_mes"></select>
        <label>Ano</label>
        <input id="in_ano" type="number" placeholder="Ex: 2026" min="2000" max="2100">
        <button class="btn-primary" id="btnSalvar">Salvar NF</button>
      </div>
      <div class="readonly-note">Link público: qualquer pessoa vê o painel ao vivo. Só quem tiver o PIN consegue lançar/editar NFs.</div>
    </div>
  </div>

  <div>
    <div class="kpis" id="kpis"></div>
    <div class="grid2">
      <div class="panel">
        <h3>OTD (On Time Delivery)</h3>
        <canvas id="gauge" height="150"></canvas>
      </div>
      <div class="panel">
        <h3>Pendências por Bairro/RA</h3>
        <div id="regions"></div>
      </div>
    </div>
    <div class="grid2">
      <div class="panel">
        <h3>Ranking de Motoristas — Entregas no Prazo</h3>
        <canvas id="barChart" height="180"></canvas>
      </div>
      <div class="panel">
        <h3>Atraso Mensal (%)</h3>
        <canvas id="lineChart" height="180"></canvas>
      </div>
    </div>
    <div class="panel">
      <h3>Notas Fiscais</h3>
      <div class="tablewrap">
        <table>
          <thead><tr><th>Carreg.</th><th>NF</th><th>Bairro/RA</th><th>Motorista</th><th>Valor</th><th>Status</th><th>Mês</th><th>Ano</th><th></th></tr></thead>
          <tbody id="tbody"></tbody>
        </table>
      </div>
    </div>
  </div>
</div>
</div>

<script type="module">
/* ======================================================================
   CONFIGURAÇÃO DO FIREBASE
   ====================================================================== */
const firebaseConfig = {
  apiKey: "AIzaSyAYcAWcV_iDJNJiZpQsAbTP93WwF_JOQfE",
  authDomain: "rastreamento-de-cargas-d20d0.firebaseapp.com",
  projectId: "rastreamento-de-cargas-d20d0",
  storageBucket: "rastreamento-de-cargas-d20d0.firebasestorage.app",
  messagingSenderId: "114429895544",
  appId: "1:114429895544:web:62609ed30c7c190dd6de8d",
  measurementId: "G-JY8E8BJT16"
};

// PIN simples só para esconder o formulário de quem não deveria editar.
// Não é segurança forte — a proteção real de escrita fica nas Regras do Firestore.
const EDIT_PIN = "1507";

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.13.0/firebase-app.js";
import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.13.0/firebase-auth.js";
import {
  getFirestore, collection, doc, setDoc, deleteDoc, onSnapshot, writeBatch
} from "https://www.gstatic.com/firebasejs/10.13.0/firebase-firestore.js";

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const notasRef = collection(db, "notas");

const REGIOES = [
  "Plano Piloto","Gama","Taguatinga","Brazlândia","Sobradinho","Planaltina (DF)","Paranoá","Núcleo Bandeirante",
  "Ceilândia","Guará","Cruzeiro","Samambaia","Santa Maria","São Sebastião","Recanto das Emas","Lago Sul",
  "Riacho Fundo","Lago Norte","Candangolândia","Águas Claras","Riacho Fundo II","Sudoeste/Octogonal","Varjão",
  "Park Way","SCIA/Estrutural","Sobradinho II","Jardim Botânico","Itapoã","SIA","Vicente Pires","Fercal",
  "Sol Nascente/Pôr do Sol","Arniqueira","Arapoanga","Água Quente",
  "Águas Lindas de Goiás (GO)","Cidade Ocidental (GO)","Novo Gama (GO)","Valparaíso de Goiás (GO)",
  "Luziânia (GO)","Formosa (GO)","Planaltina (GO)","Santo Antônio do Descoberto (GO)","Alexânia (GO)",
  "Cristalina (GO)","Padre Bernardo (GO)"
];
const MESES = ["Jan","Fev","Mar","Abr","Mai","Jun","Jul","Ago","Set","Out","Nov","Dez"];
const STATUS_LABEL = {ok:"Entregue no prazo", late:"Entregue com atraso", transit:"Em trânsito", pending:"Pendente"};

const selNf=document.getElementById('fNf'), selRegiao=document.getElementById('fRegiao'),
      selStatus=document.getElementById('fStatus'), selMot=document.getElementById('fMot'), selAno=document.getElementById('fAno'),
      selCarregamento=document.getElementById('fCarregamento');
document.getElementById('in_ano').value = new Date().getFullYear();
REGIOES.forEach(r=>selRegiao.insertAdjacentHTML('beforeend',`<option value="${r}">${r}</option>`));
const inRegiao=document.getElementById('in_regiao'), inMes=document.getElementById('in_mes');
REGIOES.forEach(r=>inRegiao.insertAdjacentHTML('beforeend',`<option value="${r}">${r}</option>`));
MESES.forEach((m,i)=>inMes.insertAdjacentHTML('beforeend',`<option value="${i}">${m}</option>`));

let allRows = [];
let canWrite = false;

function fmtMoney(v){ return "R$ " + Number(v||0).toLocaleString('pt-BR'); }

function populateMotFilter(rows){
  const cur = selMot.value;
  const names = Array.from(new Set(rows.map(r=>r.motorista).filter(Boolean))).sort();
  selMot.innerHTML = '<option value="">Todos</option>' + names.map(n=>`<option value="${n}">${n}</option>`).join('');
  selMot.value = cur;
  const curAno = selAno.value;
  const anos = Array.from(new Set(rows.map(r=>r.ano).filter(Boolean))).sort();
  selAno.innerHTML = '<option value="">Todos</option>' + anos.map(a=>`<option value="${a}">${a}</option>`).join('');
  selAno.value = curAno;
}

function filtered(){
  const nf=selNf.value.trim(), reg=selRegiao.value, st=selStatus.value, mot=selMot.value, ano=selAno.value, carr=selCarregamento.value.trim();
  return allRows.filter(d=> (!nf||String(d.nf).includes(nf)) && (!reg||d.regiao===reg) && (!st||d.status===st) && (!mot||d.motorista===mot) && (!ano||String(d.ano)===ano) && (!carr||String(d.carregamento||'').includes(carr)) );
}

function renderKpis(rows){
  const total = rows.length;
  const ok = rows.filter(r=>r.status==='ok').length;
  const late = rows.filter(r=>r.status==='late').length;
  const pending = rows.filter(r=>r.status==='pending').length;
  const transit = rows.filter(r=>r.status==='transit').length;
  const valor = rows.reduce((a,r)=>a+(Number(r.valor)||0),0);
  const cards = [
    [total,"Total de NFs"], [ok+late,"NFs Entregues"], [pending,"NFs Pendentes"],
    [transit,"Em Trânsito"], [fmtMoney(valor),"Valor Total"],
    [total? Math.round(ok/(ok+late||1)*100)+"%":"—","OTD do Filtro"],
  ];
  document.getElementById('kpis').innerHTML = cards.map(c=>`<div class="kpi"><div class="n">${c[0]}</div><div class="l">${c[1]}</div></div>`).join('');
}

function renderRegions(rows){
  const byReg = {}; REGIOES.forEach(r=>byReg[r]={total:0,pending:0});
  rows.forEach(r=>{ if(byReg[r.regiao]){ byReg[r.regiao].total++; if(r.status==='pending') byReg[r.regiao].pending++; } });
  const el = document.getElementById('regions');
  const entries = Object.entries(byReg).filter(([,v])=>v.total>0).sort((a,b)=>b[1].pending-a[1].pending).slice(0,14);
  if(!entries.length){ el.innerHTML='<div class="empty">Nenhum dado para os filtros atuais.</div>'; return; }
  el.innerHTML = entries.map(([reg,v])=>{
    const pct = v.total? Math.round(v.pending/v.total*100):0;
    return `<div class="region-row"><span class="name">${reg}</span><div class="bar-track"><div class="bar-fill" style="width:${pct}%"></div></div><span class="val">${v.pending} pend. (${pct}%)</span></div>`;
  }).join('');
}

function renderTable(rows){
  const tbody = document.getElementById('tbody');
  if(!rows.length){ tbody.innerHTML = '<tr><td colspan="9"><div class="empty">Nenhuma NF lançada ainda para esses filtros.</div></td></tr>'; return; }
  tbody.innerHTML = rows.slice(0,80).map(r=>`<tr>
    <td>${r.carregamento||'—'}</td><td>${r.nf}</td><td>${r.regiao}</td><td>${r.motorista||'—'}</td><td>${fmtMoney(r.valor)}</td>
    <td><span class="tag status ${r.status}">${STATUS_LABEL[r.status]||r.status}</span></td>
    <td>${MESES[r.mes]||'—'}</td>
    <td>${r.ano||'—'}</td>
    <td>${canWrite ? `<button class="del" data-nf="${r.nf}">Excluir</button>` : ''}</td>
  </tr>`).join('');
  if(canWrite){
    tbody.querySelectorAll('.del').forEach(btn=>{
      btn.addEventListener('click', async ()=>{
        btn.disabled = true;
        try{ await deleteDoc(doc(db,'notas',String(btn.dataset.nf))); }
        catch(e){ btn.disabled=false; alert('Erro ao excluir: '+e.message); }
      });
    });
  }
}

function cssVar(name){ return getComputedStyle(document.body).getPropertyValue(name); }

function drawGauge(rows){
  const c = document.getElementById('gauge'); const ctx = c.getContext('2d');
  const w = c.parentElement.clientWidth; c.width = w; c.height=150;
  const ok = rows.filter(r=>r.status==='ok').length, late = rows.filter(r=>r.status==='late').length;
  const pct = (ok+late) ? ok/(ok+late) : 0;
  const cx=w/2, cy=130, radius=Math.min(w/2-20,110);
  ctx.clearRect(0,0,w,150);
  ctx.lineWidth=16; ctx.lineCap='round';
  ctx.strokeStyle = cssVar('--line');
  ctx.beginPath(); ctx.arc(cx,cy,radius,Math.PI,0); ctx.stroke();
  ctx.strokeStyle = cssVar('--teal');
  ctx.beginPath(); ctx.arc(cx,cy,radius,Math.PI,Math.PI+Math.PI*pct); ctx.stroke();
  ctx.fillStyle = cssVar('--ink');
  ctx.font='700 30px -apple-system,sans-serif'; ctx.textAlign='center';
  ctx.fillText((pct*100).toFixed(1)+'%', cx, cy-14);
  ctx.font='12px -apple-system,sans-serif'; ctx.fillStyle=cssVar('--muted');
  ctx.fillText('entregas no prazo', cx, cy+8);
}

function drawBarChart(rows){
  const c = document.getElementById('barChart'); const ctx = c.getContext('2d');
  const w = c.parentElement.clientWidth; c.width=w; c.height=180;
  const byMot = {};
  rows.forEach(r=>{ if(!byMot[r.motorista]) byMot[r.motorista]=0; if(r.status==='ok') byMot[r.motorista]++; });
  const arr = Object.entries(byMot).sort((a,b)=>b[1]-a[1]).slice(0,6);
  const max = Math.max(1,...arr.map(a=>a[1]));
  ctx.clearRect(0,0,w,180);
  if(!arr.length){ ctx.fillStyle=cssVar('--muted'); ctx.font='13px -apple-system,sans-serif'; ctx.fillText('Sem dados ainda.',0,20); return; }
  const barH=18, gap=12, top=10;
  ctx.font='12px -apple-system,sans-serif'; ctx.textBaseline='middle';
  arr.forEach((a,i)=>{
    const y = top + i*(barH+gap);
    const bw = (w-140) * (a[1]/max);
    ctx.fillStyle = cssVar('--muted'); ctx.textAlign='left'; ctx.fillText(a[0]||'—', 0, y+barH/2);
    ctx.fillStyle = cssVar('--teal'); ctx.fillRect(120,y,Math.max(2,bw),barH);
    ctx.fillStyle = cssVar('--ink'); ctx.fillText(a[1], 120+bw+8, y+barH/2);
  });
}

function drawLineChart(rows){
  const c = document.getElementById('lineChart'); const ctx = c.getContext('2d');
  const w = c.parentElement.clientWidth; c.width=w; c.height=180;
  const perMonth = MESES.slice(0,9).map((_,i)=>{
    const m = rows.filter(r=>r.mes===i);
    const late = m.filter(r=>r.status==='late').length;
    return m.length ? late/m.length*100 : 0;
  });
  ctx.clearRect(0,0,w,180);
  const padL=30, padB=22, padT=10, plotW=w-padL-10, plotH=180-padB-padT;
  const max = Math.max(10,...perMonth);
  ctx.strokeStyle = cssVar('--line');
  ctx.beginPath(); ctx.moveTo(padL,padT); ctx.lineTo(padL,padT+plotH); ctx.lineTo(padL+plotW,padT+plotH); ctx.stroke();
  ctx.beginPath();
  perMonth.forEach((v,i)=>{
    const x = padL + plotW*(i/(perMonth.length-1));
    const y = padT + plotH - (v/max)*plotH;
    if(i===0) ctx.moveTo(x,y); else ctx.lineTo(x,y);
  });
  ctx.strokeStyle = cssVar('--amber'); ctx.lineWidth=2; ctx.stroke();
  ctx.fillStyle = cssVar('--muted'); ctx.font='10.5px -apple-system,sans-serif'; ctx.textAlign='center';
  MESES.slice(0,9).forEach((m,i)=>{ const x = padL + plotW*(i/(perMonth.length-1)); ctx.fillText(m, x, 180-6); });
}

function renderAll(){
  populateMotFilter(allRows);
  const rows = filtered();
  renderKpis(rows); renderRegions(rows); renderTable(rows);
  drawGauge(rows); drawBarChart(rows); drawLineChart(rows);
}
[selNf,selRegiao,selStatus,selMot,selAno,selCarregamento].forEach(el=>el.addEventListener('input',renderAll));
window.addEventListener('resize', renderAll);

let htmlImportRows=[];
const HEADER_ALIASES={
  carregamento:['carregamento','carga','ncarregamento','numerodocarregamento','numero carga','n carga','load'],
  nf:['nf','nota','notafiscal','numnf','numeronf','numerodanota','documento','documentofiscal'],
  regiao:['bairro','bairro/ra','bairro ra','regiao','regiaoadministrativa','ra','cidade','municipio','localidade'],
  motorista:['motorista','condutor','nome motorista','transportador'],
  valor:['valor','valorr$','valordafatura','valordocarga','frete','valorfrete'],
  status:['status','situacao','statusentrega','situacaoentrega'],
  mes:['mes','mesentrega','mesdaentrega'],
  ano:['ano','anoentrega','anodaentrega']
};
function normalizeText(v){return String(v??'').normalize('NFD').replace(/[\u0300-\u036f]/g,'').toLowerCase().trim().replace(/\s+/g,' ')}
function normalizeHeader(v){return normalizeText(v).replace(/[^a-z0-9]+/g,'')}
function findColumn(headers,field){const aliases=HEADER_ALIASES[field].map(normalizeHeader);return headers.findIndex(h=>aliases.includes(normalizeHeader(h)))}
function parseMoney(v){let s=String(v??'').trim();if(!s)return 0;s=s.replace(/R\$|BRL/gi,'').replace(/\s/g,'');if(s.includes(',')&&s.includes('.'))s=s.replace(/\./g,'').replace(',','.');else if(s.includes(','))s=s.replace(',','.');const n=Number(s.replace(/[^0-9.-]/g,''));return Number.isFinite(n)?n:0}
function parseStatus(v){const s=normalizeText(v);if(['ok','entregue no prazo','no prazo','entregue','dentro do prazo'].includes(s))return'ok';if(['late','entregue com atraso','com atraso','atrasado','atraso'].includes(s))return'late';if(['transit','em transito','transito'].includes(s))return'transit';if(['pending','pendente','aguardando','nao entregue'].includes(s))return'pending';return['ok','late','transit','pending'].includes(s)?s:'pending'}
function parseMonth(v){const s=normalizeText(v);const idx=MESES.map(normalizeText).indexOf(s.slice(0,3));if(idx>=0)return idx;const n=Number(s);return Number.isInteger(n)&&n>=1&&n<=12?n-1:-1}
function parseHtmlSpreadsheet(html){
  const parsed=new DOMParser().parseFromString(html,'text/html');
  const tables=[...parsed.querySelectorAll('table')];
  if(!tables.length)throw new Error('Nenhuma tabela <table> foi encontrada no HTML informado.');
  let best=null;
  for(const table of tables){
    const trs=[...table.querySelectorAll('tr')]; if(trs.length<2)continue;
    const rows=trs.map(tr=>[...tr.querySelectorAll('th,td')].map(c=>c.textContent.replace(/\u00a0/g,' ').trim()));
    const headers=rows[0]||[];
    const recognized=['nf','carregamento','regiao','motorista','valor','status','mes','ano'].filter(f=>findColumn(headers,f)>=0).length;
    if(!best||recognized>best.recognized||(recognized===best.recognized&&rows.length>best.rows.length))best={rows,recognized};
  }
  if(!best)throw new Error('A tabela foi encontrada, mas não possui linhas suficientes para leitura.');
  const headers=best.rows[0], indexes={};
  ['carregamento','nf','regiao','motorista','valor','status','mes','ano'].forEach(f=>indexes[f]=findColumn(headers,f));
  if(indexes.nf<0)throw new Error('Não encontrei a coluna NF. Use um cabeçalho como “NF”, “Nota Fiscal” ou “Número NF”.');
  const rows=[];
  best.rows.slice(1).forEach((cells,i)=>{
    if(!cells.some(Boolean))return;
    const nf=String(indexes.nf>=0?cells[indexes.nf]:'').trim(); if(!nf)return;
    const reg=indexes.regiao>=0?String(cells[indexes.regiao]).trim():'';
    const mesRaw=indexes.mes>=0?cells[indexes.mes]:'';
    rows.push({
      nf,carregamento:indexes.carregamento>=0?String(cells[indexes.carregamento]).trim():'',
      regiao:reg||REGIOES[0],motorista:indexes.motorista>=0?String(cells[indexes.motorista]).trim():'',
      valor:parseMoney(indexes.valor>=0?cells[indexes.valor]:0),status:parseStatus(indexes.status>=0?cells[indexes.status]:''),
      mes:parseMonth(mesRaw),ano:Number(indexes.ano>=0?cells[indexes.ano]:'')||new Date().getFullYear(),_rowNumber:i+2
    });
  });
  return{rows,recognized:best.recognized};
}
function showImportStatus(msg,type='ok'){const el=document.getElementById('importStatus');el.textContent=msg;el.className='import-status show '+type}
function previewImport(){
  const html=document.getElementById('htmlImport').value.trim();
  if(!html){showImportStatus('Cole o HTML da planilha antes de fazer a leitura.','err');return false}
  try{
    const parsed=parseHtmlSpreadsheet(html);htmlImportRows=parsed.rows;
    const invalid=htmlImportRows.filter(r=>r.regiao&&!REGIOES.includes(r.regiao)).length;
    const sample=htmlImportRows.slice(0,3).map(r=>`NF ${r.nf} · ${r.motorista||'sem motorista'} · ${STATUS_LABEL[r.status]}`).join(' | ');
    document.getElementById('importPreview').innerHTML=`<strong>${htmlImportRows.length} registro(s) lido(s)</strong> · ${parsed.recognized} coluna(s) reconhecida(s).${invalid?` ${invalid} região(ões) não correspondem à lista cadastrada; o texto será mantido.`:''}<br>${sample||'Nenhuma linha válida encontrada.'}`;
    showImportStatus('Leitura concluída. Confira a prévia e clique em “Importar para o dashboard”.','ok');return true;
  }catch(e){htmlImportRows=[];document.getElementById('importPreview').textContent='Nenhuma planilha carregada.';showImportStatus(e.message,'err');return false}
}
document.getElementById('btnLerHtml').addEventListener('click',previewImport);
document.getElementById('btnImportarHtml').addEventListener('click',async()=>{
  if(!canWrite){showImportStatus('Entre no modo edição antes de importar.','err');return}
  if(!htmlImportRows.length&&!previewImport())return;
  if(!htmlImportRows.length)return;
  const unique=new Map();htmlImportRows.forEach(r=>unique.set(String(r.nf),r));
  const rows=[...unique.values()];
  if(rows.length!==htmlImportRows.length){showImportStatus(`Foram encontradas ${htmlImportRows.length-rows.length} NF(s) repetida(s). Será mantida a última ocorrência de cada NF.`,'ok')}
  const btn=document.getElementById('btnImportarHtml');btn.disabled=true;
  try{
    let imported=0;
    for(let i=0;i<rows.length;i+=400){
      const batch=writeBatch(db);
      rows.slice(i,i+400).forEach(r=>{const body={carregamento:r.carregamento,regiao:r.regiao,motorista:r.motorista,valor:r.valor,status:r.status,mes:r.mes<0?new Date().getMonth():r.mes,ano:r.ano};batch.set(doc(db,'notas',String(r.nf)),body);});
      await batch.commit();imported+=Math.min(400,rows.length-i);
    }
    showImportStatus(`${imported} NF(s) importada(s) com sucesso. Registros com a mesma NF foram atualizados.`, 'ok');
  }catch(e){showImportStatus('Erro durante a importação: '+e.message,'err')}
  finally{btn.disabled=false}
});

document.getElementById('btnUnlock').addEventListener('click', async ()=>{
  if(document.getElementById('pinInput').value !== EDIT_PIN){ alert('PIN incorreto.'); return; }
  try{ await signInAnonymously(auth); }catch(e){ alert('Erro ao autenticar: '+e.message); return; }
  canWrite = true;
  document.getElementById('gateLocked').style.display = 'none';
  document.getElementById('formPanel').style.display = 'block';
  renderAll();
});

document.getElementById('btnSalvar').addEventListener('click', async ()=>{
  const nf = document.getElementById('in_nf').value.trim();
  if(!nf) return;
  const body = {
    carregamento: document.getElementById('in_carregamento').value.trim(),
    regiao: inRegiao.value,
    motorista: document.getElementById('in_motorista').value.trim(),
    valor: Number(document.getElementById('in_valor').value)||0,
    status: document.getElementById('in_status').value,
    mes: Number(inMes.value),
    ano: Number(document.getElementById('in_ano').value) || new Date().getFullYear(),
  };
  const btn = document.getElementById('btnSalvar');
  btn.disabled = true;
  try{
    await setDoc(doc(db,'notas',nf), body);
    document.getElementById('in_carregamento').value=''; document.getElementById('in_nf').value=''; document.getElementById('in_motorista').value=''; document.getElementById('in_valor').value='';
  }catch(e){ alert('Erro ao salvar: '+e.message); }
  finally{ btn.disabled = false; }
});

const statusTag = document.getElementById('statusTag');
onSnapshot(notasRef, snap=>{
  allRows = snap.docs.map(d=>({ nf:d.id, ...d.data() }));
  statusTag.textContent = 'ao vivo';
  renderAll();
}, err=>{
  statusTag.textContent = 'erro de conexão';
  console.error(err);
});
</script>
</body>
</html>
