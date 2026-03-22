<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="Cortisolo">
<title>Cortisolo Basso</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root{--cream:#f5f0e8;--sage:#7a9e7e;--sl:#a8c5ac;--sd:#4a7150;--clay:#c4845a;--ink:#2a2a22;--il:#5a5a50;--bg:#f0ece0;--wh:#faf8f2}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--ink);overflow-x:hidden}
.hero{background:var(--ink);padding:52px 20px 36px;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:-60px;right:-60px;width:280px;height:280px;border-radius:50%;background:radial-gradient(circle,rgba(122,158,126,.25) 0%,transparent 70%)}
.hero-label{font-size:.7rem;letter-spacing:4px;text-transform:uppercase;color:var(--sl);margin-bottom:10px}
.hero h1{font-family:'Playfair Display',serif;font-size:1.75rem;color:var(--cream);line-height:1.25}
.hero h1 em{font-style:italic;color:var(--sl)}
.hero-sub{margin-top:10px;color:#8a8a7a;font-size:.85rem;font-weight:300}
.prog-bar{background:var(--wh);border-bottom:1px solid #e0dace;padding:12px 20px;display:flex;align-items:center;gap:14px;flex-wrap:wrap}
.prog-label{font-size:.75rem;color:var(--il);letter-spacing:1px;text-transform:uppercase}
.prog-track{flex:1;min-width:100px;height:6px;background:#e0dace;border-radius:3px;overflow:hidden}
.prog-fill{height:100%;background:linear-gradient(90deg,var(--sage),var(--sd));border-radius:3px;transition:width .5s ease}
.prog-count{font-size:.82rem;font-weight:500;color:var(--sd)}
.reset-btn{margin-left:auto;font-size:.75rem;color:var(--il);background:none;border:1px solid #d0cabe;padding:5px 12px;border-radius:20px;cursor:pointer;font-family:'DM Sans',sans-serif}
.controls{padding:14px 20px;display:flex;gap:8px;flex-wrap:wrap;align-items:center;background:var(--bg);border-bottom:1px solid #e0dace;position:sticky;top:0;z-index:10;box-shadow:0 2px 10px rgba(42,42,34,.06)}
.search-box{padding:8px 12px;border-radius:8px;border:1.5px solid #d8d2c4;background:var(--wh);color:var(--ink);font-size:.85rem;font-family:'DM Sans',sans-serif;width:100%;outline:none}
.search-box:focus{border-color:var(--sage)}
.pills{display:flex;gap:6px;flex-wrap:wrap;width:100%}
.pill{padding:6px 14px;border-radius:20px;border:1.5px solid #d0cabe;background:transparent;color:var(--il);font-size:.78rem;cursor:pointer;transition:all .2s;font-family:'DM Sans',sans-serif;font-weight:500;white-space:nowrap}
.pill.active{background:var(--sd);color:var(--cream);border-color:var(--sd)}
.grid{padding:18px 16px 60px;display:grid;grid-template-columns:1fr;gap:14px}
@media(min-width:600px){.grid{grid-template-columns:repeat(2,1fr)}}
.card{background:var(--wh);border-radius:14px;border:1.5px solid #e8e2d4;padding:18px;display:flex;flex-direction:column;gap:10px;position:relative;overflow:hidden;transition:transform .2s,box-shadow .2s}
.card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;border-radius:14px 14px 0 0}
.card[data-cat="Mattino"]::before{background:linear-gradient(90deg,#f4a35a,#e8c060)}
.card[data-cat="Alimentazione"]::before{background:linear-gradient(90deg,#6abf8a,#3d9e60)}
.card[data-cat="Movimento"]::before{background:linear-gradient(90deg,#5aace0,#3480c0)}
.card[data-cat="Mente"]::before{background:linear-gradient(90deg,#a87ad0,#7850b0)}
.card[data-cat="Sera"]::before{background:linear-gradient(90deg,#4070c0,#203080)}
.card[data-cat="Connessione"]::before{background:linear-gradient(90deg,#e05a80,#b03060)}
.card.done{background:#f0f5f1;border-color:var(--sl);opacity:.85}
.card.done::before{background:var(--sage)!important}
.card-header{display:flex;align-items:flex-start;gap:10px}
.card-icon{font-size:1.5rem;line-height:1;flex-shrink:0;margin-top:2px}
.card-title{font-family:'Playfair Display',serif;font-size:1rem;font-weight:700;color:var(--ink);line-height:1.3}
.card.done .card-title{text-decoration:line-through;color:var(--il)}
.cat-tag{font-size:.68rem;letter-spacing:1.5px;text-transform:uppercase;font-weight:500;color:var(--il)}
.card-desc{font-size:.83rem;color:var(--il);line-height:1.6;font-weight:300}
.card-meta{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
.meta-chip{display:flex;align-items:center;gap:4px;font-size:.72rem;padding:3px 9px;border-radius:20px;background:#f0ece0;color:var(--il);border:1px solid #e0dace}
.diff-dots{display:flex;gap:3px;align-items:center}
.dot{width:7px;height:7px;border-radius:50%;background:#e0dace}
.dot.filled{background:var(--sd)}
.diff-label{font-size:.72rem;color:var(--il);margin-left:3px}
.ev-badge{font-size:.68rem;padding:2px 8px;border-radius:10px;font-weight:500}
.ev-alta{background:#e0f0e4;color:#2a7040}
.ev-media{background:#fef0e0;color:#8a5020}
.learn-toggle{background:none;border:none;font-size:.75rem;color:var(--sd);cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:500;padding:0;display:flex;align-items:center;gap:4px}
.learn-panel{background:#f8f4ec;border:1px solid #e8e0cc;border-radius:8px;padding:12px 14px;font-size:.8rem;color:var(--il);line-height:1.65;display:none}
.learn-panel.open{display:block}
.tip-highlight{background:#f0f5f1;border-left:3px solid var(--sage);padding:6px 10px;border-radius:0 6px 6px 0;margin-top:8px;font-style:italic;color:var(--sd);font-size:.78rem}
.done-btn{margin-top:2px;display:flex;align-items:center;justify-content:center;gap:8px;background:none;border:1.5px solid #d8d2c4;border-radius:10px;padding:9px 16px;cursor:pointer;font-family:'DM Sans',sans-serif;font-size:.82rem;color:var(--il);transition:all .2s;width:100%}
.card.done .done-btn{background:var(--sd);border-color:var(--sd);color:#fff}
.footer-count{text-align:center;padding:0 0 30px;font-size:.78rem;color:#aaa8a0}
</style>
</head>
<body>
<div class="hero">
<p class="hero-label">Routine · Benessere · Cortisolo</p>
<h1>Gesti quotidiani per tenere il cortisolo <em>basso</em></h1>
<p class="hero-sub">Impara, pratica e spunta ogni abitudine giornaliera.</p>
</div>
<div class="prog-bar">
<span class="prog-label">Oggi</span>
<div class="prog-track"><div class="prog-fill" id="progFill" style="width:0%"></div></div>
<span class="prog-count" id="progCount">0 / 24</span>
<button class="reset-btn" onclick="resetAll()">↺ Reset</button>
</div>
<div class="controls">
<input class="search-box" id="searchInput" type="text" placeholder="🔍 Cerca abitudine..." oninput="applyFilters()">
<div class="pills">
<button class="pill active" onclick="filterCat('all',this)">Tutti</button>
<button class="pill" onclick="filterCat('Mattino',this)">🌅 Mattino</button>
<button class="pill" onclick="filterCat('Alimentazione',this)">🥗 Cibo</button>
<button class="pill" onclick="filterCat('Movimento',this)">🏃 Corpo</button>
<button class="pill" onclick="filterCat('Mente',this)">🧘 Mente</button>
<button class="pill" onclick="filterCat('Sera',this)">🌙 Sera</button>
<button class="pill" onclick="filterCat('Connessione',this)">🤝 Relazioni</button>
</div>
</div>
<div class="grid" id="grid"></div>
<p class="footer-count" id="footerCount"></p>
<script>
const H=[
{id:1,cat:'Mattino',icon:'🌅',title:'Luce naturale appena svegli',time:'5–10 min',diff:1,ev:'alta',desc:'Esporsi alla luce solare entro 30 min sincronizza il ritmo circadiano e regola il picco mattutino di cortisolo.',learn:'Il cortisolo raggiunge il suo picco fisiologico (CAR) entro 30-45 min dal risveglio. La luce naturale rafforza questo picco nel momento giusto e facilita il calo nel corso della giornata.',tip:'Anche 5 min sul balcone fanno la differenza rispetto a restare al buio.'},
{id:2,cat:'Mattino',icon:'💧',title:'Bicchiere d\'acqua al risveglio',time:'1 min',diff:1,ev:'media',desc:'Reidratarsi stabilizza la glicemia mattutina e riduce lo stress fisiologico delle cellule.',learn:'Durante la notte si perdono 400-500 ml di liquidi. La lieve disidratazione mattutina può alzare il cortisolo perché il corpo la percepisce come stressor.',tip:'Tieni un bicchiere già pronto sul comodino la sera prima.'},
{id:3,cat:'Mattino',icon:'☕',title:'Ritarda la caffeina di 60–90 min',time:'— attesa',diff:2,ev:'alta',desc:'Aspettare prima del caffè permette all\'adenosina di dissiparsi, evitando un picco di cortisolo indotto dalla caffeina.',learn:'La caffeina inibisce i recettori dell\'adenosina e stimola ulteriormente il cortisolo già elevato al mattino. Aspettando 60–90 min il corpo gestisce da solo l\'energia e la caffeina risulta più efficace.',tip:'Usa questo tempo per acqua, luce e 5 minuti di quiete.'},
{id:4,cat:'Mattino',icon:'📵',title:'No al telefono per i primi 20 min',time:'20 min',diff:2,ev:'media',desc:'Evitare news, social e notifiche appena svegli previene un\'attivazione precoce della risposta allo stress.',learn:'Controllare il telefono subito espone il cervello a stimoli ansiogeni prima che la corteccia prefrontale sia attiva. I primi 20 minuti di veglia sono una finestra preziosa di calma cognitiva.',tip:'Metti il telefono in un\'altra stanza o in modalità aereo la notte.'},
{id:5,cat:'Mattino',icon:'🌬️',title:'Respirazione lenta (4-7-8)',time:'5 min',diff:1,ev:'alta',desc:'Respirare lentamente attiva il nervo vago e il sistema parasimpatico, abbassando rapidamente il cortisolo.',learn:'Tecniche come il 4-7-8 o la coerenza cardiaca (6 respiri/min per 5 min) stimolano il nervo vago e aumentano l\'HRV. Studi mostrano riduzioni significative del cortisolo salivare dopo soli 5 minuti.',tip:'Prova l\'app Respirazione integrata nel tuo iPhone.'},
{id:6,cat:'Alimentazione',icon:'🥣',title:'Colazione proteica',time:'—',diff:2,ev:'alta',desc:'Proteine e grassi a colazione stabilizzano la glicemia, evitando i picchi insulinemici che alzano il cortisolo.',learn:'I picchi di glucosio post-prandiali innescano insulina e, in risposta all\'ipoglicemia reattiva, cortisolo. Le proteine rallentano l\'assorbimento glucidico. Obiettivo: 20-30g di proteine a colazione.',tip:'Uova, yogurt greco, frutta secca o skyr sono ottime basi.'},
{id:7,cat:'Alimentazione',icon:'🐟',title:'Omega-3 ogni giorno',time:'—',diff:1,ev:'alta',desc:'Gli omega-3 (EPA/DHA) riducono l\'infiammazione sistemica e attenuano la risposta cortisolicа allo stress.',learn:'Studi randomizzati mostrano che 2-3g/die di EPA+DHA riducono significativamente il cortisolo plasmatico. Gli omega-3 modulano i recettori per i glucocorticoidi e abbassano le citochine infiammatorie.',tip:'Salmone, sgombro, sardine 2-3x/settimana o 2g/die di olio di pesce.'},
{id:8,cat:'Alimentazione',icon:'🫘',title:'Magnesio ogni giorno',time:'—',diff:1,ev:'alta',desc:'Il magnesio è essenziale per la regolazione dell\'asse HPA: la carenza è direttamente associata a cortisolo elevato.',learn:'Il magnesio agisce come freno sull\'asse HPA. In carenza (oltre il 70% della popolazione occidentale), l\'asse diventa iper-reattivo. Bisglicinato o glicinato hanno la migliore biodisponibilità.',tip:'Semi di zucca, verdure a foglia verde, cacao amaro e mandorle.'},
{id:9,cat:'Alimentazione',icon:'🫐',title:'Antiossidanti colorati',time:'—',diff:1,ev:'media',desc:'Polifenoli e antiossidanti riducono lo stress ossidativo che stimola il cortisolo come risposta protettiva.',learn:'Lo stress ossidativo è percepito come minaccia cellulare e attiva il cortisolo. I polifenoli in mirtilli, melograno, tè verde e olio EVO contrastano questo processo.',tip:'Mira a 5 colori diversi di frutta e verdura ogni giorno.'},
{id:10,cat:'Alimentazione',icon:'🚫',title:'Limita zuccheri raffinati e alcol',time:'—',diff:3,ev:'alta',desc:'Zuccheri e alcol creano picchi glicemici e alterano l\'asse HPA, mantenendo il cortisolo elevato.',learn:'Ogni picco glicemico è seguito da insulina e ipoglicemia reattiva, gestita alzando il cortisolo. L\'alcol altera il ritmo circadiano del cortisolo e peggiora il sonno anche a basse dosi.',tip:'Sostituisci i dolci con frutta fresca e noci.'},
{id:11,cat:'Movimento',icon:'🚶',title:'Camminata 20–30 min',time:'20–30 min',diff:1,ev:'alta',desc:'L\'esercizio moderato abbassa il cortisolo basale, migliora la sensibilità ai glucocorticoidi e riduce l\'ansia.',learn:'L\'aerobica moderata (60-70% FC max) è uno dei meccanismi più studiati per ridurre il cortisolo cronico. Stimola endorfine, BDNF e serotonina. Al contrario, l\'esercizio troppo intenso può innalzarlo.',tip:'Una camminata in natura riduce il cortisolo del 16% in più rispetto all\'asfalto.'},
{id:12,cat:'Movimento',icon:'🧘',title:'Yoga o stretching leggero',time:'15–20 min',diff:1,ev:'alta',desc:'Lo yoga combina respirazione, movimento e mindfulness: triplice azione anti-cortisolo con evidenza solida.',learn:'Meta-analisi su 3.000+ partecipanti mostrano che yoga regolare riduce il cortisolo salivare del 25% in media. Anche 15 min di stretching lento con respirazione consapevole producono effetti misurabili.',tip:'Non serve essere flessibili: yoga per principianti ha gli stessi effetti.'},
{id:13,cat:'Movimento',icon:'🏋️',title:'Allenamento di forza moderato',time:'30–45 min',diff:2,ev:'alta',desc:'La muscolazione regolare aumenta la sensibilità ai glucocorticoidi e migliora la composizione corporea.',learn:'La massa muscolare migliora la sensibilità all\'insulina e riduce l\'infiammazione. Sessioni <45 min ottimizzano il rapporto testosterone/cortisolo. L\'overtraining invece lo eleva cronicamente.',tip:'2-3 sessioni/settimana di 30-40 min sono meglio di sessioni lunghe quotidiane.'},
{id:14,cat:'Movimento',icon:'🌳',title:'15 min nella natura',time:'15+ min',diff:1,ev:'alta',desc:'Il "bagno nella foresta" abbassa cortisolo, pressione e frequenza cardiaca in soli 15 minuti.',learn:'Ricerche sui forest baths mostrano riduzioni del cortisolo del 13-16% dopo 15-20 min tra gli alberi. I meccanismi includono fitoncidi, riduzione del sistema simpatico e stimolazione del parasimpatico.',tip:'Un parco urbano con alberi è sufficiente.'},
{id:15,cat:'Mente',icon:'🧘',title:'Meditazione mindfulness 10 min',time:'10 min',diff:2,ev:'alta',desc:'La meditazione riduce l\'iperattività dell\'amigdala e abbassa il cortisolo basale in modo strutturale.',learn:'8 settimane di mindfulness riducono il volume dell\'amigdala e aumentano la materia grigia nella corteccia prefrontale. Il cortisolo salivare scende del 20% nei praticanti regolari.',tip:'App come Insight Timer o Calm offrono sessioni guidate in italiano.'},
{id:16,cat:'Mente',icon:'📓',title:'Journaling 5–10 min',time:'5–10 min',diff:1,ev:'media',desc:'Scrivere pensieri e preoccupazioni scarica il sistema limbico e abbassa l\'ansia anticipatoria.',learn:'La scrittura espressiva riduce i marcatori di stress biologico incluso il cortisolo (Pennebaker, UT Austin). Un brain dump serale riduce il rimuginio notturno e il cortisolo del mattino.',tip:'Basta flusso di coscienza. Carta e penna funzionano meglio del digitale.'},
{id:17,cat:'Mente',icon:'🎵',title:'Musica rilassante 10–20 min',time:'10–20 min',diff:1,ev:'media',desc:'La musica lenta (60-80 bpm) sincronizza le onde cerebrali e abbassa il cortisolo rapidamente.',learn:'Meta-analisi mostrano riduzioni del cortisolo salivare del 12-15% ascoltando musica rilassante. L\'effetto è maggiore con musica scelta dal soggetto, preferibilmente strumentale.',tip:'Binaural beats o musica classica lenta funzionano bene anche in background.'},
{id:18,cat:'Mente',icon:'😂',title:'Risate autentiche ogni giorno',time:'—',diff:1,ev:'media',desc:'Il vero riso abbassa cortisolo e adrenalina e aumenta endorfine e ossitocina.',learn:'L\'anticipazione di una risata riduce il cortisolo del 39% e l\'adrenalina del 70% (Lee Berk, Loma Linda). Il riso autentico attiva il diaframma e inibisce il sistema nervoso simpatico.',tip:'Anche l\'anticipazione di qualcosa di divertente abbassa già il cortisolo.'},
{id:19,cat:'Mente',icon:'🎯',title:'Una cosa alla volta',time:'—',diff:3,ev:'media',desc:'Il multitasking mantiene il cervello in allerta cronica, elevando il cortisolo durante tutta la giornata.',learn:'Il task-switching rapido ha costi cognitivi e cortisolicò ad ogni cambio. Lavorare su più cose aumenta il cortisolo del 15-20% rispetto al monotasking.',tip:'Pomodoro: 25 min focus + 5 min pausa. Ripeti 4 volte, poi 20 min di pausa lunga.'},
{id:20,cat:'Sera',icon:'🌙',title:'Routine serale costante',time:'—',diff:2,ev:'alta',desc:'Un rituale serale regolare segnala al sistema nervoso che il pericolo è passato, abbassando il cortisolo.',learn:'Il cortisolo raggiunge il minimo intorno a mezzanotte. Una routine prevedibile (stessa ora, stesse azioni) condiziona il cervello a disattivare il simpatico e facilita il calo naturale.',tip:'Punta alla stessa ora di sonno ogni giorno, weekend inclusi.'},
{id:21,cat:'Sera',icon:'📵',title:'No schermi 60–90 min prima di dormire',time:'—',diff:3,ev:'alta',desc:'La luce blu inibisce la melatonina e mantiene il cortisolo elevato nelle ore serali.',learn:'La luce blu degli schermi sopprime la melatonina. Senza melatonina il cortisolo resta elevato. Occhiali anti-luce blu attenuano ma non eliminano il problema.',tip:'Sostituisci gli schermi serali con lettura, podcast o conversazione.'},
{id:22,cat:'Sera',icon:'🛁',title:'Bagno caldo prima di dormire',time:'10–15 min',diff:1,ev:'alta',desc:'Il raffreddamento post-bagno mima il calo termico naturale del sonno e abbassa il cortisolo.',learn:'La temperatura corporea scende di 0.5-1°C durante l\'addormentamento. Un bagno caldo 60-90 min prima accelera questo processo, riducendo arousal e cortisolo.',tip:'Temperatura ideale dell\'acqua: 40-42°C.'},
{id:23,cat:'Connessione',icon:'🤗',title:'Abbracci e contatto fisico',time:'—',diff:1,ev:'alta',desc:'Il contatto affettuoso rilascia ossitocina, che inibisce direttamente il cortisolo a livello ipotalamico.',learn:'Un abbraccio di 20+ secondi stimola l\'ossitocina che inibisce il CRH ipotalamico, riducendo a cascata ACTH e cortisolo. Anche le coccole con animali domestici hanno lo stesso effetto.',tip:'6-8 abbracci al giorno è la dose raccomandata dagli studiosi del benessere.'},
{id:24,cat:'Connessione',icon:'💬',title:'Conversazioni significative',time:'—',diff:2,ev:'media',desc:'Le relazioni di qualità sono uno dei più potenti buffer contro il cortisolo cronico.',learn:'La solitudine cronica è associata a cortisolo basale più elevato del 23%. Le interazioni positive attivano il sistema oppioide endogeno. Anche 10 min con una persona cara abbassano misurabilmente il cortisolo.',tip:'La qualità conta più della quantità: una conversazione profonda vale più di 10 scambi veloci.'}
];
let cur='all';
let ds=new Set(JSON.parse(localStorage.getItem('cd')||'[]'));
function save(){try{localStorage.setItem('cd',JSON.stringify([...ds]));}catch(e){}}
function toggleDone(id){ds.has(id)?ds.delete(id):ds.add(id);save();updateProg();const c=document.querySelector(`.card[data-id="${id}"]`);if(c){c.classList.toggle('done',ds.has(id));c.querySelector('.done-btn').innerHTML=ds.has(id)?'✓ Fatto oggi!':'○ Segna come fatto';}}
function toggleLearn(id){const p=document.getElementById('lp'+id),b=document.getElementById('lt'+id),o=p.classList.toggle('open');b.textContent=o?'▲ Chiudi':'▼ Scopri perché funziona';}
function updateProg(){const n=[...ds].filter(id=>H.find(h=>h.id===id)).length;document.getElementById('progFill').style.width=(n/H.length*100)+'%';document.getElementById('progCount').textContent=n+' / '+H.length;}
function resetAll(){ds.clear();save();updateProg();document.querySelectorAll('.card.done').forEach(c=>c.classList.remove('done'));document.querySelectorAll('.done-btn').forEach(b=>b.innerHTML='○ Segna come fatto');}
function getF(){const q=document.getElementById('searchInput').value.toLowerCase();return H.filter(h=>(cur==='all'||h.cat===cur)&&(!q||h.title.toLowerCase().includes(q)||h.desc.toLowerCase().includes(q)));}
function applyFilters(){renderGrid();}
function filterCat(cat,btn){cur=cat;document.querySelectorAll('.pill').forEach(b=>b.classList.remove('active'));btn.classList.add('active');renderGrid();}
const evL={alta:'Alta evidenza',media:'Evidenza media'};
const dL=['','Facile','Medio','Sfidante'];
function renderGrid(){
const list=getF(),g=document.getElementById('grid');
if(!list.length){g.innerHTML='<div style="text-align:center;padding:40px;color:#aaa;font-style:italic">Nessuna abitudine trovata.</div>';return;}
g.innerHTML=list.map(h=>{
const d=ds.has(h.id),dots=[1,2,3].map(i=>`<div class="dot ${i<=h.diff?'filled':''}"></div>`).join('');
return`<div class="card ${d?'done':''}" data-cat="${h.cat}" data-id="${h.id}">
<div class="card-header"><div class="card-icon">${h.icon}</div><div><div class="card-title">${h.title}</div><span class="cat-tag">${h.cat}</span></div></div>
<p class="card-desc">${h.desc}</p>
<div class="card-meta">${h.time!=='—'?`<span class="meta-chip">⏱ ${h.time}</span>`:''}<span class="meta-chip"><span class="diff-dots">${dots}</span><span class="diff-label">${dL[h.diff]}</span></span><span class="ev-badge ev-${h.ev}">${evL[h.ev]}</span></div>
<button class="learn-toggle" id="lt${h.id}" onclick="toggleLearn(${h.id})">▼ Scopri perché funziona</button>
<div class="learn-panel" id="lp${h.id}">${h.learn}<div class="tip-highlight">💡 ${h.tip}</div></div>
<button class="done-btn" onclick="toggleDone(${h.id})">${d?'✓ Fatto oggi!':'○ Segna come fatto'}</button>
</div>`;}).join('');
document.getElementById('footerCount').textContent=list.length+' abitudini visualizzate';
updateProg();}
renderGrid();
</script>
</body>
</html>
