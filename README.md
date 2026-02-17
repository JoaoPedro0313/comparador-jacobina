# comparador-jacobina
<title>Comparador de Carteiras — JACOBINA</title> <script src=" https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script> <style> @import url(' https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Syne:wght@700;800&family=DM+Sans:wght@300;400;500&display=swap ');
:root { --bg: #0d0f14; --surface: #161922; --border: #252a36; --accent: #f5a623; --accent2: #3ecf8e; --danger: #ff5c5c; --muted: #4a5168; --text: #e8eaf0; --text-dim: #7c839a; --added: rgba(62, 207, 142, 0.08); --removed: rgba(255, 92, 92, 0.08); --changed: rgba(245, 166, 35, 0.08); --added-border: #3ecf8e; --removed-border: #ff5c5c; --changed-border: #f5a623; }
{ box-sizing: border-box; margin: 0; padding: 0; }
corpo { fundo: var(--bg); cor: var(--texto); família da fonte: 'DM Sans', sans-serif; tamanho da fonte: 14px; altura mínima: 100vh; }
cabeçalho { preenchimento: 28px 40px 20px; borda inferior: 1px sólida var(--borda); exibição: flexível; alinhamento de itens: centro; espaço: 16px; }
.logo-mark { width: 38px; height: 38px; background: var(--accent); display: grid; place-items: center; font-family: 'Syne', sans-serif; font-weight: 800; font-size: 18px; color: #000; flex-shrink: 0; }
cabeçalho h1 { família de fontes: 'Syne', sans-serif; peso da fonte: 800; tamanho da fonte: 18px; espaçamento entre letras: -0,5px; }
cabeçalho span { cor: var(--text-dim); tamanho da fonte: 12px; família da fonte: 'DM Mono', monoespaçada; margem esquerda: 4px; }
.main { padding: 32px 40px; max-width: 1400px; }
/* Zona de upload */ .upload-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 24px; }
.upload-card { background: var(--surface); border: 1.5px dashed var(--border); border-radius: 10px; padding: 28px; text-align: center; cursor: pointer; transition: border-color 0.2s, background 0.2s; position: relative; }
.upload-card:hover, .upload-card.drag-over { border-color: var(--accent); background: rgba(245, 166, 35, 0.04); }
.upload-card.loaded { border-style: solid; border-color: var(--accent2); background: rgba(62, 207, 142, 0.04); }
.upload-card input { position: absolute; inset: 0; opacity: 0; cursor: pointer; width: 100%; height: 100%; }
.upload-label { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--text-dim); margin-bottom: 8px; display: flex; align-items: center; justify-content: center; gap: 6px; }
.upload-icon { tamanho da fonte: 28px; margem inferior: 8px; }
.upload-name { font-family: 'DM Mono', monospace; font-size: 12px; color: var(--accent2); margin-top: 4px; }
.upload-hint { color: var(--text-dim); font-size: 12px; }
/* Controles */ .controls { display: flex; align-items: center; gap: 12px; margin-bottom: 28px; flex-wrap: wrap; }
select { background: var(--surface); border: 1px solid var(--border); color: var(--text); padding: 8px 12px; border-radius: 6px; font-family: 'DM Sans', sans-serif; font-size: 13px; cursor: pointer; }
selecionar:foco { contorno: 1px sólido var(--accent); }
label.ctrl-label { tamanho da fonte: 12px; cor: var(--text-dim); família da fonte: 'DM Mono', monospace; }
.btn-compare { background: var(--accent); color: #000; border: none; padding: 10px 22px; border-radius: 6px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 13px; cursor: pointer; letter-spacing: 0.5px; transition: opacity 0.2s; margin-left: auto; }
.btn-compare:hover { opacity: 0.85; } .btn-compare:disabled { opacity: 0.4; cursor: not-allowed; }
/* Cartões de resumo */ .summary-row { display: flex; gap: 12px; margin-bottom: 28px; flex-wrap: wrap; }
.stat-card { background: var(--surface); border: 1px solid var(--border); border-radius: 8px; padding: 14px 20px; min-width: 130px; }
.stat-card .stat-val { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 28px; line-height: 1; margin-bottom: 4px; }
.stat-card .stat-label { font-size: 11px; color: var(--text-dim); text-transform: uppercase; letter-spacing: 1px; font-family: 'DM Mono', monospace; }
.color-added { color: var(--accent2); } .color-removed { color: var(--danger); } .color-changed { color: var(--accent); } .color-same { color: var(--muted); }
/* Abas de filtro */ .filter-tabs { display: flex; gap: 4px; margin-bottom: 16px; border-bottom: 1px solid var(--border); padding-bottom: 0; }
.tab-btn { background: none; border: none; color: var(--text-dim); padding: 8px 16px; cursor: pointer; font-family: 'DM Sans', sans-serif; font-size: 13px; border-bottom: 2px solid transparent; margin-bottom: -1px; transition: color 0.15s, border-color 0.15s; }
.tab-btn:hover { color: var(--text); } .tab-btn.active { color: var(--text); border-bottom-color: var(--accent); }
/* Filtros */ .tab-badge { display: inline-block; font-size: 10px; background: var(--surface); border: 1px solid var(--border); border-radius: 10px; padding: 1px 6px; margin-left: 5px; font-family: 'DM Mono', monospace; vertical-align: middle; }
/* Pesquisar */ .search-bar { margin-bottom: 16px; }
.search-bar input { background: var(--surface); border: 1px solid var(--border); color: var(--text); padding: 9px 14px; border-radius: 6px; font-family: 'DM Mono', monospace; font-size: 13px; width: 320px; }
.search-bar input::placeholder { color: var(--text-dim); } .search-bar input:focus { outline: 1px solid var(--accent); }
/* Tabela */ .table-wrap { overflow-x: auto; border: 1px solid var(--border); border-radius: 10px; }
tabela { largura: 100%; recolhimento da borda: recolhimento; tamanho da fonte: 12,5px; }
thead th { background: var(--surface); padding: 10px 14px; text-align: left; font-family: 'DM Mono', monospace; font-size: 11px; color: var(--text-dim); text-transform: uppercase; letter-spacing: 0.5px; border-bottom: 1px solid var(--border); white-space: nowrap; cursor: pointer; user-select: none; }
thead th:hover { color: var(--text); }
tbody tr { border-bottom: 1px solid rgba(255,255,255,0.04); transition: background 0.1s; }
tbody tr:hover { background: rgba(255,255,255,0.03); }
tbody tr.row-added { background: var(--added); border-left: 3px solid var(--added-border); } tbody tr.row-removed { background: var(--removed); border-left: 3px solid var(--removed-border); } tbody tr.row-changed { background: var(--changed); border-left: 3px solid var(--changed-border); }
td { padding: 9px 14px; max-width: 200px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; vertical-align: middle; }
td.changed-cell { background: rgba(245, 166, 35, 0.12); border-radius: 3px; }
.badge { display: inline-flex; align-items: center; gap: 4px; font-size: 10px; font-family: 'DM Mono', monospace; padding: 2px 7px; border-radius: 4px; font-weight: 500; white-space: nowrap; }
.badge-added { background: rgba(62, 207, 142, 0.15); color: var(--accent2); } .badge-removed { background: rgba(255, 92, 92, 0.15); color: var(--danger); } .badge-changed { background: rgba(245, 166, 35, 0.15); color: var(--accent); }
.old-val { color: var(--danger); text-decoration: line-through; font-size: 11px; } .new-val { color: var(--accent2); }
/* Vazio / carregando */ .empty-state { text-align: center; padding: 60px 20px; color: var(--text-dim); }
.empty-state .big { font-size: 40px; margin-bottom: 12px; } .empty-state p { font-size: 13px; }
/* Seleção de colunas */ .col-select-wrap { display: flex; align-items: center; gap: 8px; flex-wrap: wrap; }
.col-chip { background: var(--surface); border: 1px solid var(--border); border-radius: 5px; padding: 4px 9px; font-size: 11px; font-family: 'DM Mono', monospace; cursor: pointer; user-select: none; transition: all 0.15s; color: var(--text-dim); }
.col-chip.active { border-color: var(--accent); color: var(--accent); background: rgba(245, 166, 35, 0.08); }
.section-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--text-dim); margin-bottom: 8px; }
.divider { altura: 1px; fundo: var(--border); margem: 24px 0; }
.loading { display: flex; align-items: center; gap: 8px; padding: 20px 0; color: var(--text-dim); font-family: 'DM Mono', monospace; font-size: 13px; }
@keyframes spin { to { transform: rotate(360deg); } } .spinner { width: 16px; height: 16px; border: 2px solid var(--border); border-top-color: var(--accent); border-radius: 50%; animation: spin 0.7s linear infinite; }
.col-changed-detail { tamanho da fonte: 11px; altura da linha: 1,6; }
/* Responsivo */ @media (max-width: 700px) { .upload-grid { grid-template-columns: 1fr; } header, .main { padding-left: 16px; padding-right: 16px; } } </style>
J

Comparador de Carteiras // JACOBINA

Arquivos para comparar
📂
📅 Arquivo Anterior (Base)
Arraste ou clique para selecionar
📋
📅 Arquivo Novo (Comparação)
Arraste ou clique para selecionar
Aba: →<label class="ctrl-label" style="margin-left:12px">Chave:</label>
<select id="key-col"></select>

<button class="btn-compare" id="btn-compare" onclick="compare()" disabled>Comparar</button>

Colunas monitoradas (clique para ativar/desativar)
Analisando alterações...
Resumo das alterações
<div class="filter-tabs" id="filter-tabs"></div>
<div class="search-bar">
  <input type="text" id="search-input" placeholder="Buscar por NOTA, PEP, status..." oninput="renderTable()">
</div>
<div class="table-wrap">
  <table>
    <thead id="thead"></thead>
    <tbody id="tbody"></tbody>
  </table>
</div>
<div id="empty-msg" class="empty-state" style="display:none">
  <div class="big">🔍</div>
  <p>Nenhum resultado para este filtro.</p>
</div>

<script> const state = { wbA: null, wbB: null, nameA: '', nameB: '', results: [], filter: 'all', watchCols: [], allCols: [], keyCol: 'NOTA', }; // --- Arrastar e soltar --- function onDrag(e, id) { e.preventDefault(); document.getElementById('card-'+id).classList.add('drag-over'); } function offDrag(id) { document.getElementById('card-'+id).classList.remove('drag-over'); } function onDrop(e, id) { e.preventDefault(); offDrag(id); const file = e.dataTransfer.files[0]; if (file) processFile(file, id); } function loadFile(e, id) { const file = e.target.files[0]; if (file) processFile(file, id); } function processFile(file, id) { const reader = new FileReader(); reader.onload = (e) => { const wb = XLSX.read(e.target.result, { type: 'array' }); if (id === 'a') { state.wbA = wb; state.nameA = file.name; } else { state.wbB = wb; state.nameB = file.name; } document.getElementById('name-'+id).textContent = file.name; document.getElementById('hint-'+id).textContent = 'Carregado ✓'; document.getElementById('card-'+id).classList.remove('drag-over'); document.getElementById('card-'+id).classList.add('loaded'); updateSheetOptions(); }; reader.readAsArrayBuffer(file); } function updateSheetOptions() { const selA = document.getElementById('sheet-a'); const selB = document.getElementById('sheet-b'); if (state.wbA) { const prev = selA.value; selA.innerHTML = state.wbA.SheetNames.map(s => `${s}`).join(''); } if (state.wbB) { const prev = selB.value; selB.innerHTML = state.wbB.SheetNames.map(s => `${s}`).join(''); } document.getElementById('btn-compare').disabled = !(state.wbA && state.wbB); if (state.wbA && state.wbB) preloadCols(); } function getSheetData(wb, sheetName) { const ws = wb.Sheets[sheetName]; const raw = XLSX.utils.sheet_to_json(ws, { header: 1, defval: '' }); // Encontrar a linha de cabeçalho (procurar por 'NOTA') let headerIdx = 0; for (let i = 0; i < Math.min(10, raw.length); i++) { if (raw[i].some(c => String(c).toUpperCase().includes('NOTA'))) { headerIdx = i; break; } } const headers = raw[headerIdx].map(h => String(h).trim()); const rows = raw.slice(headerIdx + 1).filter(r => r.some(c => c !== '')); return { headers, rows }; } function preloadCols() { const sheetNameA = document.getElementById('sheet-a').value; if (!sheetNameA || !state.wbA) return; const { headers } = getSheetData(state.wbA, sheetNameA); state.allCols = headers.filter(h => h); // Coluna de chave const keyEl = document.getElementById('key-col'); const prevKey = keyEl.value || 'NOTA'; keyEl.innerHTML = state.allCols.map(h => `${h}`).join(''); // Chips de coluna const WATCH_DEFAULTS = ['STATUS DA OBRA', 'OBS STATUS', 'ENCARREGADO', 'SUPERVISOR', 'MUNICIPIO', 'TÍTULO']; if (state.watchCols.length === 0) { state.watchCols = state.allCols.filter(c => WATCH_DEFAULTS.includes(c)); } renderColChips(); document.getElementById('col-section').style.display = 'block'; } function renderColChips() { const el = document.getElementById('col-chips'); el.innerHTML = state.allCols.map(c => { const active = state.watchCols.includes(c); return `
${c}
`; }).join(''); } function toggleCol(col) { const idx = state.watchCols.indexOf(col); if (idx >= 0) state.watchCols.splice(idx, 1); else state.watchCols.push(col); renderColChips(); } function compare() { document.getElementById('loading').style.display = 'flex'; document.getElementById('summary').style.display = 'none'; setTimeout(() => { try { const sheetNameA = document.getElementById('sheet-a').value; const sheetNameB = document.getElementById('sheet-b').value; const keyCol = document.getElementById('key-col').value; state.keyCol = keyCol; const { headers: hA, rows: rA } = getSheetData(state.wbA, sheetNameA); const { headers: hB, rows: rB } = getSheetData(state.wbB, sheetNameB); const keyIdxA = hA.findIndex(h => h === keyCol); const keyIdxB = hB.findIndex(h => h === keyCol); if (keyIdxA < 0 || keyIdxB < 0) { alert('Coluna chave "' + keyCol + '" não encontrado em uma das abas.'); document.getElementById('loading').style.display = 'none'; return; } // Construir mapas const mapA = new Map(); rA.forEach(row => { const key = String(row[keyIdxA]).trim(); if (key) mapA.set(key, row); }); const mapB = new Map(); rB.forEach(row => { const key = String(row[keyIdxB]).trim(); if (key) mapB.set(key, row); }); const cols = state.watchCols.length > 0 ? state.watchCols : hB.filter(h => h); const results = []; // Adicionado mapB.forEach((rowB, key) => { if (!mapA.has(key)) { const obj = { type: 'added', key }; hB.forEach((h, i) => { if (cols.includes(h)) obj[h] = { val: String(rowB[i] ?? '').trim() }; }); results.push(obj); } }); // Removido mapA.forEach((rowA, key) => { if (!mapB.has(key)) { const obj = { type: 'removed', key }; hA.forEach((h, i) => { if (cols.includes(h)) obj[h] = { val: String(rowA[i] ?? '').trim() }; }); results.push(obj); } }); // Alterado mapB.forEach((rowB, key) => { if (!mapA.has(key)) return; const rowA = mapA.get(key); const diffs = {}; let hasDiff = false; cols.forEach(col => { const idxA = hA.indexOf(col); const idxB = hB.indexOf(col); const va = idxA >= 0 ? String(rowA[idxA] ?? '').trim() : ''; const vb = idxB >= 0 ? String(rowB[idxB] ?? '').trim() : ''; if (va !== vb) { diffs[col] = { old: va, new: vb }; hasDiff = true; } else { diffs[col] = { val: vb }; } }); if (hasDiff) { results.push({ type: 'changed', key, ...diffs }); } }); state.results = results; state.filter = 'all'; document.getElementById('loading').style.display = 'none'; renderSummary(); renderTable(); document.getElementById('summary').style.display = 'block'; } catch(err) { document.getElementById('loading').style.display = 'none'; alert('Erro ao comparar: ' + err.message); console.error(err); } }, 50); } function renderSummary() { const added = state.results.filter(r => r.type === 'added').length; const removed = state.results.filter(r => r.type === 'removed').length; const changed = state.results.filter(r => r.type === 'changed').length; const total = state.results.length; document.getElementById('summary-row').innerHTML = `
${total}
Alterações totais
${adicionado}
Novas Obras
${removido}
Obras Removidas
${alterado}
Obras Modificadas
`; document.getElementById('filter-tabs').innerHTML = ` Todas ${total} Novas ${added} Removidas ${removed} Modificadas ${changed} `; } function setFilter(f) { state.filter = f; renderSummary(); renderTable(); } function renderTable() { const search = document.getElementById('search-input').value.toLowerCase(); let rows = state.results; if (state.filter !== 'all') rows = rows.filter(r => r.type === state.filter); if (search) rows = rows.filter(r => { return JSON.stringify(r).toLowerCase().includes(search); }); const cols = state.watchCols.length > 0 ? state.watchCols : []; // Cabeçalho document.getElementById('thead').innerHTML = ` Tipo ${state.keyCol} ${cols.map(c => `${c.length > 18 ? c.slice(0,17)+'…' : c}`).join('')} `; if (rows.length === 0) { document.getElementById('tbody').innerHTML = ''; document.getElementById('empty-msg').style.display = 'block'; return; } document.getElementById('empty-msg').style.display = 'none'; document.getElementById('tbody').innerHTML = rows.map(r => { const cls = `row-${r.type}`; const badge = r.type === 'added' ? ` ＋ nova ` : r.type === 'removed' ? ` − removido ` : ` ✎ alterado `; const cells = cols.map(col => { const d = r[col]; if (!d) return '—'; if (d.old !== undefined) { return `
${esc(d.old) || '(vazio)'}
▶ ${esc(d.new) || '(vázio)'}
`; } return `${esc(d.val)}`; }).join(''); return ` ${badge} ${esc(r.key)} ${cells} `; }).join(''); } function esc(s) { if (!s) return ''; return String(s).replace(/&/g,'&').replace(//g,'>'); } </script>
