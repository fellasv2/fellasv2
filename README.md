[index.html](https://github.com/user-attachments/files/28475630/index.html)
## Hi there 👋

<!--
**fellasv2/fellasv2** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Fellas v2</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Syne:wght@700;800&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<style>
:root{
  --bg:#0a0a0a;--surface:#111418;--card:#161b20;
  --border:#1e2328;--border2:#252d35;
  --silver:#9aa5b4;--accent:#6b8fa8;
  --green:#4caf7d;--red:#e05656;
  --text:#dde3ea;--muted:#52606e;--muted2:#7a8a98;
  --sw:200px;
}
*{margin:0;padding:0;box-sizing:border-box}
body{background:var(--bg);color:var(--text);font-family:'DM Mono',monospace;min-height:100vh}

/* ── LOADING ── */
#loading{position:fixed;inset:0;background:var(--bg);display:flex;align-items:center;justify-content:center;flex-direction:column;gap:20px;z-index:9999}
.logo{font-family:'Syne',sans-serif;font-size:26px;font-weight:800;letter-spacing:4px}
.logo span{color:var(--silver)}
.bar{width:140px;height:1px;background:var(--border2)}
.bar div{height:100%;background:var(--silver);width:0;animation:lb 1.4s ease forwards}
@keyframes lb{to{width:100%}}

/* ── LOGIN ── */
#login{min-height:100vh;display:none;align-items:center;justify-content:center}
.lbox{width:340px;padding:44px 40px;background:var(--surface);border:1px solid var(--border2);border-top:2px solid var(--silver)}
.ltag{font-size:10px;letter-spacing:2px;color:var(--muted);margin:6px 0 32px;text-transform:uppercase}
.field{margin-bottom:12px}
.field label{display:block;font-size:10px;letter-spacing:1.5px;color:var(--muted);margin-bottom:6px;text-transform:uppercase}
.field input{width:100%;padding:10px 13px;background:var(--bg);border:1px solid var(--border2);color:var(--text);font-family:'DM Mono',monospace;font-size:13px;outline:none;transition:border-color .2s}
.field input:focus{border-color:var(--silver)}
.field input::placeholder{color:var(--muted)}
.lbtn{width:100%;padding:11px;margin-top:8px;background:var(--silver);color:var(--bg);border:none;font-family:'Syne',sans-serif;font-size:12px;font-weight:700;letter-spacing:2px;text-transform:uppercase;cursor:pointer;transition:opacity .2s}
.lbtn:hover{opacity:.85}
.lbtn:disabled{opacity:.4;cursor:not-allowed}
.lerr{color:var(--red);font-size:11px;margin-top:8px;display:none}

/* ── APP ── */
#app{display:none;min-height:100vh}

/* ── SIDEBAR ── */
.sidebar{position:fixed;top:0;left:0;bottom:0;width:var(--sw);background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;z-index:100}
.sb-hdr{padding:22px 16px 16px;border-bottom:1px solid var(--border)}
.sb-logo{font-family:'Syne',sans-serif;font-size:16px;font-weight:800;letter-spacing:3px}
.sb-logo span{color:var(--silver)}
.sb-user{margin-top:10px;display:flex;align-items:center;gap:8px}
.sb-av{width:26px;height:26px;border-radius:50%;background:rgba(107,143,168,.15);border:1px solid var(--accent);display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-size:11px;font-weight:700;color:var(--accent);flex-shrink:0}
.sb-nm{font-size:11px;color:var(--muted2)}
.sb-nav{padding:14px 8px;flex:1}
.nav-btn{display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:4px;cursor:pointer;font-size:12px;color:var(--muted2);border:none;background:none;width:100%;text-align:left;font-family:'DM Mono',monospace}
.nav-btn.active{background:rgba(107,143,168,.1);color:var(--accent)}
.sb-ftr{padding:12px 8px;border-top:1px solid var(--border)}
.logout-btn{display:flex;align-items:center;gap:10px;padding:9px 12px;width:100%;border:none;background:none;cursor:pointer;font-family:'DM Mono',monospace;font-size:12px;color:var(--muted);border-radius:4px;transition:all .15s}
.logout-btn:hover{color:var(--red);background:rgba(224,86,86,.08)}

/* ── MAIN ── */
.main{margin-left:var(--sw);min-height:100vh;display:flex;flex-direction:column}
.topbar{height:48px;background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 24px;position:sticky;top:0;z-index:50}
.topbar-t{font-family:'Syne',sans-serif;font-size:12px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase}
.content{padding:18px 24px;flex:1}

/* ── TOOLBAR ── */
.toolbar{display:flex;justify-content:flex-end;margin-bottom:10px}
.add-btn{padding:7px 16px;font-family:'Syne',sans-serif;font-size:11px;font-weight:700;letter-spacing:1px;text-transform:uppercase;background:var(--silver);color:var(--bg);border:none;cursor:pointer;transition:opacity .2s}
.add-btn:hover{opacity:.85}

/* ── TABLA ── */
.twrap{background:var(--card);border:1px solid var(--border);overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:12px;table-layout:fixed}
col.ch{width:64px} col.ce{width:106px} col.cn{width:auto}
col.cs{width:104px} col.cb{width:72px} col.cr{width:58px}
col.crb{width:76px} col.ci{width:52px} col.cp{width:76px}
col.crs{width:84px} col.cd{width:30px}
thead th{font-size:9px;letter-spacing:1.5px;text-transform:uppercase;color:var(--muted);padding:8px;text-align:left;border-bottom:1px solid var(--border);background:rgba(0,0,0,.25);font-weight:400;white-space:nowrap}
th.r,td.r{text-align:right} th.c,td.c{text-align:center}
tbody tr{border-bottom:1px solid rgba(30,35,40,.5)}
tbody tr:last-child{border-bottom:none}
tbody tr:hover{background:rgba(107,143,168,.025)}
tbody td{padding:4px 8px;vertical-align:middle}

.cel{background:transparent;border:none;color:var(--text);font-family:'DM Mono',monospace;font-size:12px;outline:none;width:100%;padding:3px 2px;border-bottom:1px solid transparent;transition:border-color .12s}
.cel:focus{border-bottom-color:var(--silver)}
.cel::placeholder{color:var(--muted)}
.cel.r{text-align:right}

.esel{background:transparent;border:none;font-family:'DM Mono',monospace;font-size:11px;cursor:pointer;outline:none;width:100%;padding:3px 0;-webkit-appearance:none;border-bottom:1px solid transparent;transition:border-color .12s}
.esel:focus{border-bottom-color:var(--silver)}
.ei{color:var(--muted2)} .ec{color:var(--accent)} .ef{color:var(--green)} .ex{color:var(--red)}

.itm-btn{background:none;border:1px solid var(--border2);color:var(--muted);font-family:'DM Mono',monospace;font-size:10px;padding:2px 0;cursor:pointer;border-radius:2px;width:100%;transition:all .15s}
.itm-btn.si{background:rgba(76,175,125,.15);border-color:var(--green);color:var(--green);font-weight:700}

.rp{color:var(--green);font-weight:500} .rn{color:var(--red)} .rz{color:var(--muted)}

.del-btn{background:none;border:none;color:var(--muted);cursor:pointer;font-size:12px;padding:2px 4px;opacity:.3;width:100%;transition:opacity .15s}
.del-btn:hover{opacity:1;color:var(--red)}

.add-row{width:100%;padding:9px;text-align:center;background:none;border:none;border-top:1px solid var(--border);color:var(--muted);font-family:'DM Mono',monospace;font-size:11px;cursor:pointer;transition:all .15s;letter-spacing:1px}
.add-row:hover{background:rgba(154,165,180,.06);color:var(--text)}

/* ── PASAR DATOS ── */
.pasar-wrap{display:flex;justify-content:flex-end;margin-top:12px}
.pasar-btn{padding:8px 20px;font-family:'Syne',sans-serif;font-size:11px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;background:var(--green);color:var(--bg);border:none;cursor:pointer;transition:opacity .2s}
.pasar-btn:hover{opacity:.85}

/* ── MODAL ── */
.overlay{position:fixed;inset:0;background:rgba(10,10,10,.88);display:none;align-items:center;justify-content:center;z-index:1000;backdrop-filter:blur(3px)}
.overlay.open{display:flex}
.modal{background:var(--surface);border:1px solid var(--border2);border-top:2px solid var(--green);padding:28px 32px;max-width:380px;width:90vw}
.modal-t{font-family:'Syne',sans-serif;font-size:14px;font-weight:700;margin-bottom:10px}
.modal-b{font-size:12px;color:var(--muted2);margin-bottom:20px;line-height:1.7}
.modal-a{display:flex;gap:10px;justify-content:flex-end}
.cancel-btn{padding:7px 14px;background:none;border:1px solid var(--border2);color:var(--muted2);font-family:'DM Mono',monospace;font-size:11px;cursor:pointer}
.cancel-btn:hover{border-color:var(--silver);color:var(--text)}
.confirm-btn{padding:7px 18px;background:var(--green);color:var(--bg);border:none;font-family:'Syne',sans-serif;font-size:11px;font-weight:700;letter-spacing:1px;cursor:pointer;transition:opacity .2s}
.confirm-btn:hover{opacity:.85}

/* ── TOAST ── */
.toast{position:fixed;bottom:24px;right:24px;padding:10px 18px;font-family:'Syne',sans-serif;font-size:11px;font-weight:700;z-index:9999;transform:translateY(60px);opacity:0;transition:all .25s;background:var(--silver);color:var(--bg)}
.toast.show{transform:translateY(0);opacity:1}
.toast.err{background:var(--red);color:#fff}
</style>
</head>
<body>

<div id="loading">
  <div class="logo">FELLAS <span>v2</span></div>
  <div class="bar"><div></div></div>
</div>

<div id="login">
  <div class="lbox">
    <div class="logo" style="font-size:22px">FELLAS <span>v2</span></div>
    <div class="ltag">Sistema de gestión</div>
    <div class="field">
      <label>Email</label>
      <input type="email" id="l-em" placeholder="tu@email.com" autocomplete="email">
    </div>
    <div class="field">
      <label>Contraseña</label>
      <input type="password" id="l-pw" placeholder="••••••••" autocomplete="current-password">
    </div>
    <button class="lbtn" id="lbtn">ENTRAR</button>
    <div class="lerr" id="lerr"></div>
  </div>
</div>

<div id="app">
  <nav class="sidebar">
    <div class="sb-hdr">
      <div class="sb-logo">FELLAS <span>v2</span></div>
      <div class="sb-user">
        <div class="sb-av" id="sbav">?</div>
        <span class="sb-nm" id="sbnm">—</span>
      </div>
    </div>
    <div class="sb-nav">
      <button class="nav-btn active">
        <span style="width:16px;text-align:center">◈</span> Grilla
      </button>
    </div>
    <div class="sb-ftr">
      <button class="logout-btn" onclick="logout()">⏻ Cerrar sesión</button>
    </div>
  </nav>

  <div class="main">
    <div class="topbar">
      <span class="topbar-t">Grilla del día</span>
    </div>
    <div class="content">
      <div class="toolbar">
        <button class="add-btn" onclick="agregarFila()">+ AGREGAR</button>
      </div>
      <div class="twrap">
        <table>
          <colgroup>
            <col class="ch"><col class="ce"><col class="cn"><col class="cs">
            <col class="cb"><col class="cr"><col class="crb">
            <col class="ci"><col class="cp"><col class="crs"><col class="cd">
          </colgroup>
          <thead>
            <tr>
              <th>Hora</th><th>Estado</th><th>Nombre</th><th>Sala</th>
              <th class="r">Buy In</th><th class="r">Rebuy</th><th class="r">Costo RB</th>
              <th class="c">ITM</th><th class="r">Premio</th><th class="r">Resultado</th>
              <th></th>
            </tr>
          </thead>
          <tbody id="tbody"></tbody>
        </table>
        <button class="add-row" onclick="agregarFila()">+ agregar fila</button>
      </div>
      <div class="pasar-wrap">
        <button class="pasar-btn" onclick="abrirPasar()">PASAR DATOS</button>
      </div>
    </div>
  </div>
</div>

<!-- MODAL PASAR DATOS -->
<div class="overlay" id="modal-pasar">
  <div class="modal">
    <div class="modal-t">Cerrar sesión del día</div>
    <div class="modal-b" id="modal-body">Resumen de la jornada.</div>
    <div class="modal-a">
      <button class="cancel-btn" onclick="cerrarModal()">Cancelar</button>
      <button class="confirm-btn" onclick="pasarDatos()">CONFIRMAR</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>
<datalist id="dl-salas"></datalist>

<script>
const SURL = 'https://fautwexudhpbxcydbyaf.supabase.co';
const SKEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImZhdXR3ZXh1ZGhwYnhjeWRieWFmIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODAwNjI4NjQsImV4cCI6MjA5NTYzODg2NH0._kWrbyAKOG4MnnTRcwf9DWtn8UGlMTHRcexS88JbkkA';
const sb = supabase.createClient(SURL, SKEY);

let user=null, sesion=null, filas=[], salas=[];

// ── FECHA ────────────────────────────
function hoy(){
  const d=new Date();
  if(d.getHours()<6) d.setDate(d.getDate()-1);
  return d.toISOString().split('T')[0];
}

// ── INIT ─────────────────────────────
async function init(){
  const {data:{session}} = await sb.auth.getSession();
  if(session){user=session.user; await arrancar();}
  else mostrarLogin();
}
function mostrarLogin(){
  document.getElementById('loading').style.display='none';
  document.getElementById('login').style.display='flex';
}

// ── LOGIN ─────────────────────────────
async function login(){
  const em=document.getElementById('l-em').value.trim();
  const pw=document.getElementById('l-pw').value;
  const btn=document.getElementById('lbtn');
  const err=document.getElementById('lerr');
  if(!em||!pw){showErr('Completá los dos campos');return;}
  btn.disabled=true; btn.textContent='ENTRANDO...'; err.style.display='none';
  const {data,error}=await sb.auth.signInWithPassword({email:em,password:pw});
  if(error){showErr('Email o contraseña incorrectos');btn.disabled=false;btn.textContent='ENTRAR';return;}
  user=data.user; await arrancar();
}
function showErr(m){const e=document.getElementById('lerr');e.textContent=m;e.style.display='block';}

async function logout(){
  await sb.auth.signOut();
  user=null;sesion=null;filas=[];
  document.getElementById('app').style.display='none';
  document.getElementById('login').style.display='flex';
}

// ── ARRANCAR ──────────────────────────
async function arrancar(){
  document.getElementById('loading').style.display='none';
  document.getElementById('login').style.display='none';
  document.getElementById('app').style.display='block';
  const email=user.email.split('@')[0];
  document.getElementById('sbav').textContent=email[0].toUpperCase();
  document.getElementById('sbnm').textContent=email;
  await Promise.all([cargarSalas(), obtenerSesion()]);
}

// ── SALAS ─────────────────────────────
async function cargarSalas(){
  const {data}=await sb.from('salas').select('sala_id,nombre').eq('activa',true).order('nombre');
  salas=data||[];
  document.getElementById('dl-salas').innerHTML=salas.map(s=>`<option value="${s.nombre}">`).join('');
}

// ── SESIÓN ────────────────────────────
async function obtenerSesion(){
  const fecha=hoy();
  // Buscar sesión abierta de hoy
  const {data:ex}=await sb.from('sesiones')
    .select('*').eq('jugador_id',user.id).eq('fecha',fecha).eq('estado','abierta')
    .order('sesion_id',{ascending:false}).limit(1);
  if(ex&&ex.length>0){sesion=ex[0];}
  else{
    const {data:nv,error}=await sb.from('sesiones')
      .insert({jugador_id:user.id,fecha,estado:'abierta'}).select();
    if(error){toast('Error al crear sesión: '+error.message,true);return;}
    sesion=nv[0];
  }
  await cargarGrilla();
}

// ── GRILLA ────────────────────────────
async function cargarGrilla(){
  if(!sesion) return;
  const {data}=await sb.from('grilla_entradas')
    .select('*,salas(nombre)').eq('sesion_id',sesion.sesion_id)
    .order('entrada_id',{ascending:true});
  filas=data||[];
  renderizar();
}

function renderizar(){
  document.getElementById('tbody').innerHTML=filas.map(f=>fila(f)).join('');
}

function fila(e){
  const id=e.entrada_id;
  const r=e.resultado||0;
  const rc=r>0?'rp':r<0?'rn':'rz';
  const rt=r===0?'—':(r>0?'+':'')+r.toLocaleString('es-AR');
  const ec=e.estado==='en_curso'?'ec':e.estado==='finalizado'?'ef':e.estado==='cancelado'?'ex':'ei';
  const sala=e.salas?.nombre||'';
  return `<tr data-id="${id}">
    <td><input class="cel" type="time" value="${e.hora||''}" onchange="upd(${id},'hora',this.value)"></td>
    <td>
      <select class="esel ${ec}" onchange="updE(${id},this)">
        <option value="a_iniciar" ${e.estado==='a_iniciar'?'selected':''}>A iniciar</option>
        <option value="en_curso"  ${e.estado==='en_curso' ?'selected':''}>En curso</option>
        <option value="finalizado"${e.estado==='finalizado'?'selected':''}>Finalizado</option>
        <option value="cancelado" ${e.estado==='cancelado'?'selected':''}>Cancelado</option>
      </select>
    </td>
    <td><input class="cel" type="text" value="${esc(e.nombre_torneo||'')}" placeholder="Nombre" onblur="upd(${id},'nombre_torneo',this.value)"></td>
    <td><input class="cel" type="text" value="${esc(sala)}" placeholder="Sala" list="dl-salas" onblur="updSala(${id},this.value)"></td>
    <td class="r"><input class="cel r" type="number" value="${e.buyin||''}" placeholder="0" min="0" step="any" onchange="updBuyin(${id},this.value)" onclick="this.select()"></td>
    <td class="r"><input class="cel r" type="number" value="${e.rebuys||''}" placeholder="0" min="0" onchange="updReb(${id},this.value)" onclick="this.select()"></td>
    <td class="r"><input class="cel r" id="crb${id}" type="number" value="${e.costo_rebuys||''}" placeholder="0" min="0" step="any" onchange="updCosto(${id},this.value)" onclick="this.select()"></td>
    <td class="c"><button class="itm-btn ${e.itm?'si':''}" onclick="updITM(${id},this)">${e.itm?'SÍ':'NO'}</button></td>
    <td class="r"><input class="cel r" type="number" value="${e.premio||''}" placeholder="0" min="0" step="any" onchange="updPremio(${id},this.value)" onclick="this.select()"></td>
    <td class="r ${rc}" id="res${id}">${rt}</td>
    <td class="c"><button class="del-btn" onclick="eliminar(${id})">✕</button></td>
  </tr>`;
}
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/"/g,'&quot;').replace(/</g,'&lt;');}

// ── AGREGAR FILA ──────────────────────
async function agregarFila(){
  if(!sesion){toast('Sin sesión activa',true);return;}
  const ahora=new Date().toTimeString().slice(0,5);
  const {data,error}=await sb.from('grilla_entradas')
    .insert({sesion_id:sesion.sesion_id,nombre_torneo:'',hora:ahora,buyin:0,estado:'a_iniciar',rebuys:0,costo_rebuys:0,itm:false,premio:0,resultado:0})
    .select('*,salas(nombre)');
  if(error){toast('Error: '+error.message,true);return;}
  const e=data[0]; filas.push(e);
  const tbody=document.getElementById('tbody');
  const tr=document.createElement('tr');
  tr.dataset.id=e.entrada_id;
  tr.innerHTML=fila(e).replace(/^<tr[^>]*>/,'').replace(/<\/tr>$/,'');
  tbody.appendChild(tr);
  tr.querySelector('input[type=time]')?.focus();
}

// ── UPDATES ───────────────────────────
function get(id){return filas.find(f=>f.entrada_id===id);}
function db(id,u){sb.from('grilla_entradas').update(u).eq('entrada_id',id).then(({error})=>{if(error)toast('Error al guardar',true);});}
function setRes(id,r){
  const c=document.getElementById(`res${id}`);if(!c)return;
  c.className='r '+(r>0?'rp':r<0?'rn':'rz');
  c.textContent=r===0?'—':(r>0?'+':'')+r.toLocaleString('es-AR');
}
function upd(id,col,val){const e=get(id);if(e)e[col]=val;db(id,{[col]:val});}
function updE(id,sel){
  const cls=sel.value==='en_curso'?'ec':sel.value==='finalizado'?'ef':sel.value==='cancelado'?'ex':'ei';
  sel.className='esel '+cls;
  const e=get(id);if(e)e.estado=sel.value;
  db(id,{estado:sel.value});
}
function updSala(id,nm){
  const s=salas.find(x=>x.nombre.toLowerCase()===nm.trim().toLowerCase());
  if(s){const e=get(id);if(e){e.sala_id=s.sala_id;e.salas={nombre:s.nombre};}db(id,{sala_id:s.sala_id});}
}
function updBuyin(id,v){
  const e=get(id);if(!e)return;
  const bi=parseFloat(v)||0;
  const rb=e.rebuys||0;
  const auto=rb>0&&e.costo_rebuys===rb*(e.buyin||0);
  const nc=auto?rb*bi:(e.costo_rebuys||0);
  const res=(e.premio||0)-bi-nc;
  e.buyin=bi;e.costo_rebuys=nc;e.resultado=res;
  if(auto){const i=document.getElementById(`crb${id}`);if(i)i.value=nc||'';}
  setRes(id,res);db(id,{buyin:bi,costo_rebuys:nc,resultado:res});
}
function updReb(id,v){
  const e=get(id);if(!e)return;
  const rb=parseInt(v)||0;
  const c=rb*(e.buyin||0);
  const res=(e.premio||0)-(e.buyin||0)-c;
  e.rebuys=rb;e.costo_rebuys=c;e.resultado=res;
  const i=document.getElementById(`crb${id}`);if(i)i.value=c||'';
  setRes(id,res);db(id,{rebuys:rb,costo_rebuys:c,resultado:res});
}
function updCosto(id,v){
  const e=get(id);if(!e)return;
  const c=parseFloat(v)||0;
  const res=(e.premio||0)-(e.buyin||0)-c;
  e.costo_rebuys=c;e.resultado=res;
  setRes(id,res);db(id,{costo_rebuys:c,resultado:res});
}
function updPremio(id,v){
  const e=get(id);if(!e)return;
  const p=parseFloat(v)||0;
  const res=p-(e.buyin||0)-(e.costo_rebuys||0);
  e.premio=p;e.resultado=res;
  setRes(id,res);db(id,{premio:p,resultado:res});
}
function updITM(id,btn){
  const e=get(id);if(!e)return;
  e.itm=!e.itm;
  btn.className='itm-btn'+(e.itm?' si':'');
  btn.textContent=e.itm?'SÍ':'NO';
  db(id,{itm:e.itm});
}
async function eliminar(id){
  if(!confirm('¿Eliminar este torneo?'))return;
  await sb.from('grilla_entradas').delete().eq('entrada_id',id);
  filas=filas.filter(f=>f.entrada_id!==id);
  document.querySelector(`tr[data-id="${id}"]`)?.remove();
}

// ── PASAR DATOS ───────────────────────
function abrirPasar(){
  const fin=filas.filter(f=>f.estado==='finalizado').length;
  const tot=filas.reduce((s,f)=>s+(f.resultado||0),0);
  const totStr=(tot>=0?'+':'')+tot.toLocaleString('es-AR');
  const color=tot>0?'var(--green)':tot<0?'var(--red)':'var(--muted)';
  document.getElementById('modal-body').innerHTML=
    `Torneos finalizados: <strong>${fin}</strong><br>
     Resultado del día: <strong style="color:${color}">${totStr}</strong><br><br>
     Esto cierra la sesión de hoy. ¿Confirmás?`;
  document.getElementById('modal-pasar').classList.add('open');
}
async function pasarDatos(){
  cerrarModal();
  if(!sesion)return;
  const tot=filas.reduce((s,f)=>s+(f.resultado||0),0);
  const {error}=await sb.from('sesiones')
    .update({estado:'cerrada',resultado_total:tot}).eq('sesion_id',sesion.sesion_id);
  if(error){toast('Error al cerrar sesión',true);return;}
  toast('¡Datos pasados! Sesión cerrada ✓');
  sesion=null;filas=[];
  document.getElementById('tbody').innerHTML='';
  setTimeout(()=>obtenerSesion(),800);
}
function cerrarModal(){document.querySelectorAll('.overlay').forEach(o=>o.classList.remove('open'));}

// ── TOAST ─────────────────────────────
function toast(msg,err=false){
  const el=document.getElementById('toast');
  el.textContent=msg;el.className='toast'+(err?' err':'');
  el.classList.add('show');
  setTimeout(()=>el.classList.remove('show'),3000);
}

// ── KEYBOARD ──────────────────────────
document.getElementById('l-pw').addEventListener('keydown',e=>{if(e.key==='Enter')login();});
document.getElementById('l-em').addEventListener('keydown',e=>{if(e.key==='Enter')login();});
document.getElementById('lbtn').addEventListener('click',login);
document.addEventListener('keydown',e=>{if(e.key==='Escape')cerrarModal();});

init();
</script>
</body>
</html>

- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
