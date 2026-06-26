<!-- World Cup 2026 — INTERACTIVE v8: real results through MD2 (Groups A–C complete); standings+knockout via official Annex C. -->
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>World Cup 2026 — Predicted</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Archivo:wght@500;600;700;800;900&family=Inter:wght@400;500;600&display=swap');

  :root{
    --bg:#0A0D1A;
    --panel:#141A30;
    --panel-2:#1B2240;
    --line:#28304F;
    --ink:#EEF1FB;
    --muted:#8B93B6;
    --faint:#646C90;
    --gold:#F4C660;
    --gold-soft:rgba(244,198,96,.14);
    --coral:#FF5C6E;
    --teal:#37D2C6;
    --violet:#8C7CF7;
    --radius:16px;
    --shadow:0 18px 50px -22px rgba(0,0,0,.8);
  }

  *{box-sizing:border-box}
  html{-webkit-text-size-adjust:100%}
  body{
    margin:0; background:
      radial-gradient(1200px 600px at 80% -10%, rgba(140,124,247,.10), transparent 60%),
      radial-gradient(900px 500px at -10% 10%, rgba(55,210,198,.08), transparent 55%),
      var(--bg);
    color:var(--ink);
    font-family:'Inter',system-ui,sans-serif;
    line-height:1.5;
    -webkit-font-smoothing:antialiased;
  }
  .wrap{max-width:1040px; margin:0 auto; padding:22px 18px 80px}

  /* ---- masthead ---- */
  .mast{display:flex; align-items:flex-end; justify-content:space-between; gap:16px; flex-wrap:wrap; margin-bottom:6px}
  .kicker{font-family:'Archivo'; font-weight:800; letter-spacing:.32em; font-size:11px; color:var(--teal); text-transform:uppercase}
  h1{font-family:'Archivo'; font-weight:900; font-size:clamp(30px,7vw,56px); line-height:.92; letter-spacing:-.02em; margin:6px 0 0}
  h1 .yr{color:var(--gold)}
  .sub{color:var(--muted); font-size:13.5px; margin-top:8px; max-width:54ch}
  .hosts{font-family:'Archivo'; font-weight:700; font-size:12px; letter-spacing:.12em; color:var(--muted); text-align:right; white-space:nowrap}
  .hosts b{color:var(--ink)}

  /* ---- caveat ---- */
  .caveat{
    margin:18px 0 22px; padding:12px 14px; border-radius:12px;
    background:linear-gradient(180deg, rgba(255,92,110,.10), rgba(255,92,110,.04));
    border:1px solid rgba(255,92,110,.28); color:#FFD2D7; font-size:12.5px;
  }
  .caveat b{color:#fff}

  /* ---- tabs ---- */
  .tabs{position:sticky; top:0; z-index:20; display:flex; gap:6px; padding:10px 0;
    background:linear-gradient(180deg, var(--bg) 70%, transparent); margin-bottom:18px}
  .tab{
    font-family:'Archivo'; font-weight:700; font-size:13px; letter-spacing:.02em;
    color:var(--muted); background:var(--panel); border:1px solid var(--line);
    padding:9px 14px; border-radius:999px; cursor:pointer; transition:.18s;
  }
  .tab:hover{color:var(--ink); border-color:#39426b}
  .tab[aria-selected="true"]{color:#0A0D1A; background:var(--gold); border-color:var(--gold)}
  .tab:focus-visible{outline:2px solid var(--teal); outline-offset:2px}

  .panel-view{display:none; animation:fade .35s ease}
  .panel-view.on{display:block}
  @keyframes fade{from{opacity:0; transform:translateY(6px)}to{opacity:1; transform:none}}

  /* ---- champion hero ---- */
  .champ{
    position:relative; overflow:hidden; border-radius:var(--radius); border:1px solid rgba(244,198,96,.35);
    background:
      radial-gradient(600px 240px at 50% -40%, var(--gold-soft), transparent 70%),
      linear-gradient(180deg, var(--panel-2), var(--panel));
    padding:26px 22px 24px; text-align:center; box-shadow:var(--shadow);
  }
  .champ .tag{font-family:'Archivo'; font-weight:800; letter-spacing:.3em; font-size:11px; color:var(--gold); text-transform:uppercase}
  .champ .flag{font-size:64px; line-height:1; margin:10px 0 2px; filter:drop-shadow(0 6px 18px rgba(0,0,0,.5))}
  .champ .name{font-family:'Archivo'; font-weight:900; font-size:clamp(34px,9vw,64px); letter-spacing:-.02em; line-height:1}
  .champ .final{display:inline-flex; align-items:center; gap:14px; margin-top:14px; padding:10px 18px;
    background:rgba(10,13,26,.5); border:1px solid var(--line); border-radius:999px; font-size:14px}
  .champ .final .sc{font-family:'Archivo'; font-weight:900; font-size:22px; letter-spacing:.04em; font-variant-numeric:tabular-nums}
  .champ .meta{color:var(--muted); font-size:12px; margin-top:12px; letter-spacing:.04em}

  /* ---- favourites strip ---- */
  .h2{font-family:'Archivo'; font-weight:800; font-size:13px; letter-spacing:.2em; text-transform:uppercase; color:var(--muted); margin:30px 4px 12px}
  .fav-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(150px,1fr)); gap:10px}
  .fav{display:flex; align-items:center; gap:10px; padding:11px 13px; background:var(--panel); border:1px solid var(--line); border-radius:12px}
  .fav .f{font-size:24px}
  .fav .t{font-family:'Archivo'; font-weight:700; font-size:14px}
  .fav .o{margin-left:auto; font-family:'Archivo'; font-weight:800; font-size:13px; color:var(--teal); font-variant-numeric:tabular-nums}
  .fav.lead{border-color:rgba(244,198,96,.4); background:linear-gradient(180deg,var(--gold-soft),var(--panel))}
  .fav.lead .o{color:var(--gold)}

  /* ---- final four mini ---- */
  .ff{display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-top:14px}
  .ff .card{background:var(--panel); border:1px solid var(--line); border-radius:12px; padding:13px}
  .ff .lab{font-family:'Archivo'; font-weight:800; font-size:10px; letter-spacing:.18em; color:var(--violet); text-transform:uppercase}
  .ff .row{display:flex; align-items:center; gap:8px; margin-top:8px; font-size:14px}
  .ff .row .s{margin-left:auto; font-family:'Archivo'; font-weight:800; font-variant-numeric:tabular-nums}
  .ff .win{color:var(--ink)} .ff .lose{color:var(--faint)}

  .awards{display:grid; grid-template-columns:repeat(auto-fit,minmax(150px,1fr)); gap:10px; margin-top:14px}
  .award{background:var(--panel); border:1px solid var(--line); border-radius:12px; padding:13px}
  .award .l{font-family:'Archivo'; font-weight:800; font-size:10px; letter-spacing:.16em; color:var(--muted); text-transform:uppercase}
  .award .v{font-family:'Archivo'; font-weight:700; font-size:15px; margin-top:4px}
  .award .v small{font-weight:500; color:var(--muted); font-size:12px}

  /* ---- group cards ---- */
  .groups{display:grid; grid-template-columns:repeat(auto-fill,minmax(300px,1fr)); gap:14px}
  .gcard{background:var(--panel); border:1px solid var(--line); border-radius:var(--radius); overflow:hidden}
  .ghead{display:flex; align-items:center; gap:10px; padding:13px 15px; border-bottom:1px solid var(--line); background:var(--panel-2)}
  .gtag{font-family:'Archivo'; font-weight:900; font-size:13px; letter-spacing:.14em; color:var(--gold)}
  .ghead .note{margin-left:auto; font-size:10.5px; color:var(--muted); letter-spacing:.04em}
  .standings{padding:6px 8px}
  .trow{display:flex; align-items:center; gap:10px; padding:8px 7px; border-radius:9px}
  .trow .pos{width:18px; text-align:center; font-family:'Archivo'; font-weight:800; font-size:12px; color:var(--faint)}
  .trow .fl{font-size:19px; width:24px; text-align:center}
  .trow .nm{font-weight:600; font-size:13.5px}
  .trow .pts{margin-left:auto; font-family:'Archivo'; font-weight:800; font-size:13px; color:var(--muted); font-variant-numeric:tabular-nums}
  .trow .pts small{font-weight:500; color:var(--faint)}
  .trow.q1{background:rgba(55,210,198,.08)} .trow.q1 .pos{color:var(--teal)}
  .trow.q2{background:rgba(55,210,198,.05)} .trow.q2 .pos{color:var(--teal)}
  .trow.q3{background:var(--gold-soft)} .trow.q3 .pos{color:var(--gold)}
  .trow.out{opacity:.5}
  .pill{font-family:'Archivo'; font-weight:800; font-size:8.5px; letter-spacing:.08em; padding:2px 6px; border-radius:5px; text-transform:uppercase}
  .pill.adv{background:rgba(55,210,198,.16); color:var(--teal)}
  .pill.elim{background:rgba(255,92,110,.12); color:var(--coral)}

  .toggle{width:100%; text-align:left; background:transparent; border:0; border-top:1px solid var(--line);
    color:var(--muted); font-family:'Archivo'; font-weight:700; font-size:11.5px; letter-spacing:.08em;
    padding:11px 15px; cursor:pointer; display:flex; align-items:center; gap:8px; transition:.15s}
  .toggle:hover{color:var(--ink); background:var(--panel-2)}
  .toggle .chev{margin-left:auto; transition:.2s; color:var(--faint)}
  .toggle[aria-expanded="true"] .chev{transform:rotate(180deg); color:var(--teal)}
  .toggle:focus-visible{outline:2px solid var(--teal); outline-offset:-2px}
  .scores{display:none; padding:4px 10px 12px; background:rgba(10,13,26,.35)}
  .scores.show{display:block}
  .mrow{display:grid; grid-template-columns:1fr auto 1fr; align-items:center; gap:8px; padding:7px 6px; font-size:12.5px; border-bottom:1px dashed rgba(40,48,79,.7)}
  .mrow:last-child{border-bottom:0}
  .mrow .home{text-align:right} .mrow .away{text-align:left}
  .mrow .ico{font-size:15px}
  .mrow .res{font-family:'Archivo'; font-weight:900; font-size:14px; color:var(--ink); background:var(--panel-2);
    border:1px solid var(--line); border-radius:7px; padding:3px 9px; font-variant-numeric:tabular-nums; white-space:nowrap}
  .mrow .aet{display:block; font-size:8px; color:var(--coral); letter-spacing:.06em; font-weight:700; margin-top:1px}

  .legend{display:flex; gap:16px; flex-wrap:wrap; margin:4px 4px 16px; font-size:11.5px; color:var(--muted)}
  .legend span{display:inline-flex; align-items:center; gap:6px}
  .dot{width:10px; height:10px; border-radius:3px; display:inline-block}

  /* ---- knockout ---- */
  .ko-scroll{overflow-x:auto; padding-bottom:8px; -webkit-overflow-scrolling:touch}
  .ko-round{margin-bottom:8px}
  .round-h{font-family:'Archivo'; font-weight:800; font-size:12px; letter-spacing:.18em; text-transform:uppercase; color:var(--gold); margin:18px 4px 10px; display:flex; align-items:center; gap:10px}
  .round-h::after{content:''; flex:1; height:1px; background:var(--line)}
  .ties{display:grid; gap:9px; grid-template-columns:repeat(auto-fill,minmax(248px,1fr))}
  .tie{background:var(--panel); border:1px solid var(--line); border-radius:12px; overflow:hidden}
  .side{display:flex; align-items:center; gap:9px; padding:9px 12px; font-size:13.5px}
  .side .fl{font-size:18px; width:22px; text-align:center}
  .side .nm{font-weight:600}
  .side .g{margin-left:auto; font-family:'Archivo'; font-weight:900; font-size:16px; font-variant-numeric:tabular-nums; color:var(--muted)}
  .side.w{background:rgba(55,210,198,.06)}
  .side.w .nm{color:var(--ink)} .side.w .g{color:var(--teal)}
  .side.l{opacity:.52}
  .side.l .nm{font-weight:500}
  .side+.side{border-top:1px solid var(--line)}
  .tie .extra{text-align:center; font-size:9px; letter-spacing:.1em; color:var(--coral); font-weight:700; padding:3px; background:rgba(255,92,110,.06); font-family:'Archivo'}

  .final-tie{border-color:rgba(244,198,96,.5); background:linear-gradient(180deg,var(--gold-soft),var(--panel)); box-shadow:var(--shadow)}
  .final-tie .side.w .g{color:var(--gold)}
  .final-tie .crown{text-align:center; font-family:'Archivo'; font-weight:900; letter-spacing:.2em; font-size:11px; color:var(--gold); padding:8px; text-transform:uppercase}

  footer{margin-top:36px; padding-top:18px; border-top:1px solid var(--line); color:var(--faint); font-size:11.5px; line-height:1.6}

  @media (max-width:560px){
    .ff{grid-template-columns:1fr}
    .champ .final{flex-wrap:wrap; justify-content:center}
  }
  @media (prefers-reduced-motion:reduce){
    *{animation:none !important; transition:none !important}
  }

  /* ===== R32 lookup tab (scoped under #lookup) ===== */
  .tabs{flex-wrap:wrap}
  #lookup .intro{color:var(--muted); font-size:13.5px; margin:2px 2px 0; max-width:66ch}
  #lookup .h2{color:var(--gold); display:flex; align-items:center; gap:10px}
  #lookup .h2::after{content:''; flex:1; height:1px; background:var(--line)}
  #lookup .lk-card{background:var(--panel); border:1px solid var(--line); border-radius:16px; padding:18px}
  #lookup .pick-row{display:flex; align-items:center; gap:10px; flex-wrap:wrap; margin-bottom:14px}
  #lookup .count{font-family:'Archivo'; font-weight:800; font-size:13px; color:var(--muted)}
  #lookup .count b{color:var(--gold)}
  #lookup .chips{display:grid; grid-template-columns:repeat(6,1fr); gap:8px}
  @media(max-width:520px){#lookup .chips{grid-template-columns:repeat(4,1fr)}}
  #lookup .chip{font-family:'Archivo'; font-weight:800; font-size:15px; padding:12px 0 10px; text-align:center;
    background:var(--panel-2); border:1px solid var(--line); border-radius:11px; color:var(--muted); cursor:pointer; transition:.15s}
  #lookup .chip:hover{color:var(--ink); border-color:#39426b}
  #lookup .chip[aria-pressed="true"]{background:var(--gold); color:#0A0D1A; border-color:var(--gold)}
  #lookup .chip:focus-visible{outline:2px solid var(--teal); outline-offset:2px}
  #lookup .chip small{display:block; font-weight:600; font-size:9px; letter-spacing:.03em; opacity:.7; margin-top:3px}
  #lookup .btns{display:flex; gap:8px; margin-top:12px; flex-wrap:wrap}
  #lookup .b{font-family:'Archivo'; font-weight:700; font-size:12px; padding:8px 13px; border-radius:9px; border:1px solid var(--line); background:var(--panel-2); color:var(--muted); cursor:pointer}
  #lookup .b:hover{color:var(--ink)}
  #lookup .b.acc{background:rgba(55,210,198,.12); border-color:rgba(55,210,198,.35); color:var(--teal)}
  #lookup .result{margin-top:16px; display:none}
  #lookup .result.show{display:block}
  #lookup .pairs{display:grid; grid-template-columns:1fr 1fr; gap:9px}
  @media(max-width:560px){#lookup .pairs{grid-template-columns:1fr}}
  #lookup .pair{display:flex; align-items:center; gap:10px; background:var(--panel-2); border:1px solid var(--line); border-radius:11px; padding:11px 13px}
  #lookup .pair .w{font-family:'Archivo'; font-weight:900; font-size:15px; color:var(--gold); width:30px}
  #lookup .pair .vs{color:var(--faint); font-size:11px; font-family:'Archivo'; font-weight:700}
  #lookup .pair .t{font-family:'Archivo'; font-weight:800; font-size:15px; color:var(--teal); width:34px; text-align:right}
  #lookup .pair .lab{margin-left:auto; font-size:11px; color:var(--muted)}
  #lookup .empty{color:var(--faint); font-size:13px; padding:8px 2px}
  #lookup .scenario-tag{font-family:'Archivo'; font-weight:800; font-size:11px; letter-spacing:.04em; color:var(--violet); margin-bottom:10px}
  #lookup table{width:100%; border-collapse:collapse; font-size:13px; margin-top:6px}
  #lookup th,#lookup td{text-align:left; padding:9px 10px; border-bottom:1px solid var(--line)}
  #lookup th{font-family:'Archivo'; font-weight:800; font-size:10px; letter-spacing:.12em; text-transform:uppercase; color:var(--muted)}
  #lookup td.win{font-family:'Archivo'; font-weight:800; color:var(--gold)}
  #lookup .elig{color:var(--ink)} #lookup .elig b{color:var(--teal); font-weight:700}
  #lookup .ru{color:var(--muted)}
  #lookup .lhint{font-size:11.5px; color:var(--faint); margin-top:10px}
  /* ---- R32 match-type badges ---- */
  .tie-type{font-family:'Archivo'; font-weight:800; font-size:8px; letter-spacing:.1em; text-transform:uppercase;
    padding:5px 12px; border-bottom:1px solid var(--line); color:var(--muted)}
  .tie-type.t-w3{color:var(--gold); background:var(--gold-soft)}
  .tie-type.t-wr{color:var(--teal); background:rgba(55,210,198,.08)}
  .tie-type.t-rr{color:var(--violet); background:rgba(140,124,247,.10)}
  .ko-legend{display:flex; gap:8px; flex-wrap:wrap; align-items:center; margin:2px 2px 14px}
  .ko-legend .lg-label{font-size:11px; color:var(--muted); margin-right:2px}
  .ko-legend .lg{font-family:'Archivo'; font-weight:800; font-size:9px; letter-spacing:.06em; text-transform:uppercase;
    padding:5px 10px; border-radius:7px; border:1px solid var(--line)}
  .ko-legend .lg-w3{color:var(--gold); background:var(--gold-soft)}
  .ko-legend .lg-wr{color:var(--teal); background:rgba(55,210,198,.08)}
  .ko-legend .lg-rr{color:var(--violet); background:rgba(140,124,247,.10)}

  /* ---- interactive editor + live bracket ---- */
  .ed-bar{display:flex; align-items:center; gap:12px; flex-wrap:wrap; margin:0 2px 14px; padding:12px 14px; background:var(--panel); border:1px solid var(--line); border-radius:12px}
  .ed-bar .info{font-size:12.5px; color:var(--muted); max-width:48ch}
  .ed-count{font-family:'Archivo'; font-weight:800; font-size:13px; color:var(--muted)}
  .ed-count b{color:var(--gold)} .ed-count.bad b{color:var(--coral)}
  .ebtn{font-family:'Archivo'; font-weight:700; font-size:12px; padding:8px 13px; border-radius:9px; border:1px solid var(--line); background:var(--panel-2); color:var(--muted); cursor:pointer; margin-left:auto}
  .ebtn:hover{color:var(--ink); border-color:#39426b}
  #groups .trow .nm{flex:1}
  .ctrl{display:flex; gap:3px}
  .arrow{width:26px; height:26px; border:1px solid var(--line); background:var(--panel-2); color:var(--muted); border-radius:6px; cursor:pointer; font-family:'Archivo'; font-weight:800; font-size:12px; line-height:1}
  .arrow:hover:not(:disabled){color:var(--ink); border-color:#39426b}
  .arrow:disabled{opacity:.3; cursor:default}
  .q-toggle{display:inline-flex; align-items:center; gap:5px; font-family:'Archivo'; font-weight:800; font-size:9.5px; letter-spacing:.04em; text-transform:uppercase; color:var(--muted); cursor:pointer; user-select:none}
  .q-toggle.on{color:var(--gold)}
  .q-toggle input{accent-color:var(--gold); cursor:pointer}
  .ko-note{font-size:12.5px; color:var(--muted); background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:11px 13px; margin:0 2px 12px}
  .ko-note b{color:var(--ink)}
  .tie .side{width:100%; background:transparent; border:0; text-align:left; cursor:pointer; color:var(--ink); font:inherit; font-size:13.5px; padding:10px 12px; gap:9px}
  .tie .side .nm{flex:1; font-weight:600}
  .tie .side .sub{font-family:'Archivo'; font-weight:700; font-size:9px; letter-spacing:.03em; text-transform:uppercase; color:var(--faint); white-space:nowrap}
  .tie .side .pickmark{width:14px; text-align:center; color:var(--teal); font-weight:900; visibility:hidden}
  .tie .side.pick{background:rgba(55,210,198,.07)}
  .tie .side.pick .pickmark{visibility:visible}
  .tie .side:not(.pick){opacity:.6}
  .tie .side.tbd .nm{color:var(--faint); font-weight:500; font-style:italic}
  .tie .side:hover{background:var(--panel-2); opacity:1}
  .tie .side+.side{border-top:1px solid var(--line)}
  .ties-final{grid-template-columns:1fr; max-width:360px; margin:0 auto}
  /* results-applied (v6) */
  .res-note{font-size:12.5px;color:var(--muted);background:linear-gradient(180deg,rgba(55,210,198,.08),rgba(55,210,198,.03));border:1px solid rgba(55,210,198,.28);border-radius:12px;padding:12px 14px;margin:0 2px 12px}
  .res-note b{color:var(--ink)}
  .res-note .rlg{display:inline-flex;gap:8px;align-items:center;margin-left:6px}
  .fx-toggle{width:100%;text-align:left;background:transparent;border:0;border-top:1px solid var(--line);color:var(--muted);font-family:'Archivo';font-weight:700;font-size:10.5px;letter-spacing:.07em;text-transform:uppercase;padding:10px 14px;cursor:pointer;display:flex;align-items:center;gap:8px}
  .fx-toggle:hover{color:var(--ink);background:var(--panel-2)}
  .fx-toggle .chev{margin-left:auto;transition:.2s;color:var(--faint)}
  .fx-toggle[aria-expanded="true"] .chev{transform:rotate(180deg);color:var(--teal)}
  .fxwrap{display:none;padding:4px 10px 12px;background:rgba(10,13,26,.35)}
  .fxwrap.show{display:block}
  .fxrow{display:grid;grid-template-columns:1fr auto 1fr auto;align-items:center;gap:8px;padding:6px 4px;font-size:12px;border-bottom:1px dashed rgba(40,48,79,.7)}
  .fxrow:last-child{border-bottom:0}
  .fxteam{display:flex;align-items:center;gap:6px;min-width:0}
  .fxteam.h{justify-content:flex-end;text-align:right}
  .fxteam .fl{font-size:14px}
  .fxteam.w{color:var(--ink);font-weight:600}
  .fxteam:not(.w){color:var(--muted)}
  .fxsc{font-family:'Archivo';font-weight:900;font-size:13px;font-variant-numeric:tabular-nums;background:var(--panel-2);border:1px solid var(--line);border-radius:6px;padding:2px 8px;white-space:nowrap}
  .fxtag{font-family:'Archivo';font-weight:800;font-size:7.5px;letter-spacing:.07em;padding:2px 5px;border-radius:4px;white-space:nowrap}
  .fxtag.r{background:rgba(55,210,198,.16);color:var(--teal)}
  .fxtag.p{background:var(--gold-soft);color:var(--gold)}
</style>

<div class="wrap">

  <div class="mast">
    <div>
      <div class="kicker">FIFA World Cup · USA · Canada · Mexico</div>
      <h1>The <span class="yr">2026</span><br>Prediction Board</h1>
      <p class="sub">Every group, every predicted scoreline, and the full bracket to the final at MetLife Stadium on July 19 — 48 teams, 104 matches, one called champion.</p>
    </div>
    <div class="hosts">JUN 11 – JUL 19<br><b>104 matches</b></div>
  </div>

  <div class="caveat">
    <b>Honest note:</b> the exact scorelines are educated guesses for fun — football is far too low-scoring and random for anyone to reliably call 104 exact scores. The favourites tier and round-by-round calls reflect real form and the betting market at kickoff. Don't bet on them.
  </div>

  <div class="tabs" role="tablist">
    <button class="tab" role="tab" aria-selected="true" data-view="overview">Overview</button>
    <button class="tab" role="tab" aria-selected="false" data-view="groups">Group standings ✎</button>
    <button class="tab" role="tab" aria-selected="false" data-view="knockout">Knockout (live)</button>
    <button class="tab" role="tab" aria-selected="false" data-view="lookup">R32 lookup</button>
  </div>

  <!-- OVERVIEW -->
  <section class="panel-view on" id="overview">
    <div class="champ">
      <div class="tag">★ Predicted Champion ★</div>
      <div class="flag">🇪🇸</div>
      <div class="name">SPAIN</div>
      <div class="final">
        <span>🇪🇸 Spain</span>
        <span class="sc">2 – 1</span>
        <span>Argentina 🇦🇷</span>
      </div>
      <div class="meta">FINAL · MetLife Stadium, New Jersey · July 19, 2026</div>
    </div>

    <div class="h2">Title favourites — at kickoff</div>
    <div class="fav-grid">
      <div class="fav lead"><span class="f">🇪🇸</span><span class="t">Spain</span><span class="o">+450</span></div>
      <div class="fav lead"><span class="f">🇫🇷</span><span class="t">France</span><span class="o">+475</span></div>
      <div class="fav"><span class="f">🏴󠁧󠁢󠁥󠁮󠁧󠁿</span><span class="t">England</span><span class="o">+650</span></div>
      <div class="fav"><span class="f">🇧🇷</span><span class="t">Brazil</span><span class="o">+850</span></div>
      <div class="fav"><span class="f">🇵🇹</span><span class="t">Portugal</span><span class="o">+850</span></div>
      <div class="fav"><span class="f">🇦🇷</span><span class="t">Argentina</span><span class="o">+900</span></div>
      <div class="fav"><span class="f">🇩🇪</span><span class="t">Germany</span><span class="o">+1300</span></div>
      <div class="fav"><span class="f">🇳🇱</span><span class="t">Netherlands</span><span class="o">+1600</span></div>
    </div>

    <div class="h2">My final four</div>
    <div class="ff">
      <div class="card">
        <div class="lab">Semifinal 1</div>
        <div class="row"><span>🇪🇸</span><span class="win">Spain</span><span class="s">2</span></div>
        <div class="row"><span>🇫🇷</span><span class="lose">France</span><span class="s" style="color:var(--faint)">1</span></div>
      </div>
      <div class="card">
        <div class="lab">Semifinal 2</div>
        <div class="row"><span>🇦🇷</span><span class="win">Argentina</span><span class="s">2</span></div>
        <div class="row"><span>🏴󠁧󠁢󠁥󠁮󠁧󠁿</span><span class="lose">England</span><span class="s" style="color:var(--faint)">1</span></div>
      </div>
    </div>

    <div class="awards">
      <div class="award"><div class="l">Golden Boot</div><div class="v">Kylian Mbappé <small>France</small></div></div>
      <div class="award"><div class="l">Young Player</div><div class="v">Lamine Yamal <small>Spain</small></div></div>
      <div class="award"><div class="l">Dark horse to semis</div><div class="v">Morocco / Norway</div></div>
    </div>

    <p class="sub" style="margin-top:22px; max-width:62ch">
      <strong style="color:var(--ink)">The thesis:</strong> Spain has the highest floor of any side — reigning European champions, the deepest balanced midfield, and the tournament's best teenager in Yamal. They convert that into a first title since 2010, edging Messi's Argentina in a dream final. The most open World Cup in years, but the favourite holds.
    </p>
  </section>

  <!-- GROUPS (editable standings) -->
  <section class="panel-view" id="groups">
    <div class="res-note">✓ <b>Real results applied through Matchday 2</b> — Groups A, B and C are complete; the rest have one game left. Played games are locked; remaining games keep my predictions. Standings, the 8 best 3rd-placed teams and the whole knockout update from this. <span class="rlg"><span class="fxtag r">RESULT</span>=actual <span class="fxtag p">PRED</span>=prediction</span></div>
    <div class="ed-bar">
      <span class="info">Adjust anything: ↑ ↓ to reorder a group, tick a different set of 8 thirds, or open “Results &amp; fixtures” under each group.</span>
      <span class="ed-count" id="edCount">Best 3rd-placed selected: <b>8</b> / 8</span>
      <button class="ebtn" id="edReset">Reset to current</button>
    </div>
    <div class="groups" id="groupGrid"></div>
  </section>

  <!-- KNOCKOUT -->
  <section class="panel-view" id="knockout">
    <div id="koWrap"></div>
  </section>

  <!-- R32 LOOKUP -->
  <section class="panel-view" id="lookup">
    <p class="intro">Eight of the twelve third-placed teams advance, and which group winner each one faces is fixed in advance by FIFA's 495-row Annex C table. Pick the eight groups whose third-placed team qualifies to resolve the exact pairings. (The Knockout bracket now uses this official allocation.)</p>

    <div class="h2">Pick the 8 groups that send a 3rd-place team through</div>
    <div class="lk-card">
      <div class="pick-row"><span class="count">Selected: <b id="cnt">0</b> / 8</span></div>
      <div class="chips" id="chips"></div>
      <div class="btns">
        <button class="b acc" id="predBtn">Use my predicted 8 (A B C D E G I J)</button>
        <button class="b" id="clearBtn">Clear</button>
      </div>
      <div class="result" id="result">
        <div class="scenario-tag" id="scenarioTag"></div>
        <div class="pairs" id="pairs"></div>
      </div>
      <div class="empty" id="hint">Select exactly eight groups to see the eight third-place matchups.</div>
    </div>

    <div class="h2">The fixed part — which 3rd-place groups each winner can draw</div>
    <div class="lk-card">
      <table><thead><tr><th>Group winner</th><th>Faces 3rd-placed team from</th></tr></thead><tbody id="eligBody"></tbody></table>
      <p class="lhint">These five-group windows never change. The 495-row table only decides <i>which</i> eligible third lands in each slot, so all eight thirds are placed without any team meeting a group rival again.</p>
    </div>

    <div class="h2">The other 4 winners — fixed runner-up matchups</div>
    <div class="lk-card">
      <table><tbody>
        <tr><td class="win">Winner C</td><td class="ru">vs Runner-up F &nbsp;(Match 76)</td></tr>
        <tr><td class="win">Winner F</td><td class="ru">vs Runner-up C &nbsp;(Match 75)</td></tr>
        <tr><td class="win">Winner H</td><td class="ru">vs Runner-up J &nbsp;(Match 84)</td></tr>
        <tr><td class="win">Winner J</td><td class="ru">vs Runner-up H &nbsp;(Match 86)</td></tr>
      </tbody></table>
      <p class="lhint">Plus four all-runner-up ties: <b>A2 v B2</b>, <b>E2 v I2</b>, <b>K2 v L2</b>, <b>D2 v G2</b>. Winners C, F, H and J never face a third-placed team. Source: FIFA 2026 Competition Regulations, Annex C (all 495 rows validated).</p>
    </div>
  </section>

  <footer>
    Predictions reflect form and the betting market as of June 11, 2026 (kickoff). Edit standings in the Group standings tab; the Knockout tab resolves names via FIFA's official Annex C table and lets you advance each tie by tapping a team. Scorelines are for entertainment.
  </footer>
</div>

<script>
/* ===== Interactive predictor: editable standings -> live knockout (official Annex C) ===== */
const F = {
  Mexico:"\uD83C\uDDF2\uD83C\uDDFD","South Africa":"\uD83C\uDDFF\uD83C\uDDE6","Korea Republic":"\uD83C\uDDF0\uD83C\uDDF7",Czechia:"\uD83C\uDDE8\uD83C\uDDFF",
  Canada:"\uD83C\uDDE8\uD83C\uDDE6","Bosnia & H.":"\uD83C\uDDE7\uD83C\uDDE6",Qatar:"\uD83C\uDDF6\uD83C\uDDE6",Switzerland:"\uD83C\uDDE8\uD83C\uDDED",
  Brazil:"\uD83C\uDDE7\uD83C\uDDF7",Morocco:"\uD83C\uDDF2\uD83C\uDDE6",Haiti:"\uD83C\uDDED\uD83C\uDDF9",Scotland:"\uD83C\uDFF4\uDB40\uDC67\uDB40\uDC62\uDB40\uDC73\uDB40\uDC63\uDB40\uDC74\uDB40\uDC7F",
  USA:"\uD83C\uDDFA\uD83C\uDDF8",Paraguay:"\uD83C\uDDF5\uD83C\uDDFE",Australia:"\uD83C\uDDE6\uD83C\uDDFA","T\u00fcrkiye":"\uD83C\uDDF9\uD83C\uDDF7",
  Germany:"\uD83C\uDDE9\uD83C\uDDEA","Cura\u00e7ao":"\uD83C\uDDE8\uD83C\uDDFC","Ivory Coast":"\uD83C\uDDE8\uD83C\uDDEE",Ecuador:"\uD83C\uDDEA\uD83C\uDDE8",
  Netherlands:"\uD83C\uDDF3\uD83C\uDDF1",Japan:"\uD83C\uDDEF\uD83C\uDDF5",Sweden:"\uD83C\uDDF8\uD83C\uDDEA",Tunisia:"\uD83C\uDDF9\uD83C\uDDF3",
  Belgium:"\uD83C\uDDE7\uD83C\uDDEA",Egypt:"\uD83C\uDDEA\uD83C\uDDEC",Iran:"\uD83C\uDDEE\uD83C\uDDF7","New Zealand":"\uD83C\uDDF3\uD83C\uDDFF",
  Spain:"\uD83C\uDDEA\uD83C\uDDF8","Cape Verde":"\uD83C\uDDE8\uD83C\uDDFB","Saudi Arabia":"\uD83C\uDDF8\uD83C\uDDE6",Uruguay:"\uD83C\uDDFA\uD83C\uDDFE",
  France:"\uD83C\uDDEB\uD83C\uDDF7",Senegal:"\uD83C\uDDF8\uD83C\uDDF3",Iraq:"\uD83C\uDDEE\uD83C\uDDF6",Norway:"\uD83C\uDDF3\uD83C\uDDF4",
  Argentina:"\uD83C\uDDE6\uD83C\uDDF7",Algeria:"\uD83C\uDDE9\uD83C\uDDFF",Austria:"\uD83C\uDDE6\uD83C\uDDF9",Jordan:"\uD83C\uDDEF\uD83C\uDDF4",
  Portugal:"\uD83C\uDDF5\uD83C\uDDF9","DR Congo":"\uD83C\uDDE8\uD83C\uDDE9",Uzbekistan:"\uD83C\uDDFA\uD83C\uDDFF",Colombia:"\uD83C\uDDE8\uD83C\uDDF4",
  England:"\uD83C\uDFF4\uDB40\uDC67\uDB40\uDC62\uDB40\uDC65\uDB40\uDC6E\uDB40\uDC67\uDB40\uDC7F",Croatia:"\uD83C\uDDED\uD83C\uDDF7",Ghana:"\uD83C\uDDEC\uD83C\uDDED",Panama:"\uD83C\uDDF5\uD83C\uDDE6"
};
const fl = t => F[t] || "\u26BD";

/* default predicted finishing order (1st..4th) per group - fully editable */
const DEFAULT = {"A":["Mexico","South Africa","Korea Republic","Czechia"],"B":["Switzerland","Canada","Bosnia & H.","Qatar"],"C":["Brazil","Morocco","Scotland","Haiti"],"D":["USA","Australia","Paraguay","Türkiye"],"E":["Germany","Ivory Coast","Ecuador","Curaçao"],"F":["Netherlands","Japan","Sweden","Tunisia"],"G":["Egypt","Belgium","Iran","New Zealand"],"H":["Spain","Cape Verde","Uruguay","Saudi Arabia"],"I":["France","Norway","Senegal","Iraq"],"J":["Argentina","Austria","Algeria","Jordan"],"K":["Portugal","Colombia","DR Congo","Uzbekistan"],"L":["England","Croatia","Ghana","Panama"]};
const GLETTERS = "ABCDEFGHIJKL".split("");
const DEFAULT_THIRDS = ["A", "B", "D", "F", "G", "I", "J", "L"];
const FIXTURES = {"A": [["Mexico", "South Africa", 2, 0, "R"], ["Korea Republic", "Czechia", 2, 1, "R"], ["Czechia", "South Africa", 1, 1, "R"], ["Mexico", "Korea Republic", 1, 0, "R"], ["Czechia", "Mexico", 0, 3, "R"], ["South Africa", "Korea Republic", 1, 0, "R"]], "B": [["Canada", "Bosnia & H.", 1, 1, "R"], ["Qatar", "Switzerland", 1, 1, "R"], ["Switzerland", "Bosnia & H.", 4, 1, "R"], ["Canada", "Qatar", 6, 0, "R"], ["Switzerland", "Canada", 2, 1, "R"], ["Bosnia & H.", "Qatar", 3, 1, "R"]], "C": [["Brazil", "Morocco", 1, 1, "R"], ["Scotland", "Haiti", 1, 0, "R"], ["Morocco", "Scotland", 1, 0, "R"], ["Brazil", "Haiti", 3, 0, "R"], ["Scotland", "Brazil", 0, 3, "R"], ["Morocco", "Haiti", 4, 2, "R"]], "D": [["USA", "Paraguay", 4, 1, "R"], ["Australia", "Türkiye", 2, 0, "R"], ["USA", "Australia", 2, 0, "R"], ["Paraguay", "Türkiye", 1, 0, "R"], ["Türkiye", "USA", 0, 2, "P"], ["Paraguay", "Australia", 1, 2, "P"]], "E": [["Germany", "Curaçao", 7, 1, "R"], ["Ivory Coast", "Ecuador", 1, 0, "R"], ["Germany", "Ivory Coast", 2, 1, "R"], ["Ecuador", "Curaçao", 0, 0, "R"], ["Curaçao", "Ivory Coast", 0, 3, "P"], ["Ecuador", "Germany", 1, 1, "P"]], "F": [["Netherlands", "Japan", 2, 2, "R"], ["Sweden", "Tunisia", 5, 1, "R"], ["Netherlands", "Sweden", 5, 1, "R"], ["Tunisia", "Japan", 0, 4, "R"], ["Japan", "Sweden", 1, 1, "P"], ["Tunisia", "Netherlands", 1, 2, "P"]], "G": [["Belgium", "Egypt", 1, 1, "R"], ["Iran", "New Zealand", 2, 2, "R"], ["Belgium", "Iran", 0, 0, "R"], ["New Zealand", "Egypt", 1, 3, "R"], ["Egypt", "Iran", 1, 1, "P"], ["New Zealand", "Belgium", 0, 2, "P"]], "H": [["Spain", "Cape Verde", 0, 0, "R"], ["Saudi Arabia", "Uruguay", 1, 1, "R"], ["Spain", "Saudi Arabia", 4, 0, "R"], ["Uruguay", "Cape Verde", 2, 2, "R"], ["Cape Verde", "Saudi Arabia", 1, 1, "P"], ["Uruguay", "Spain", 0, 1, "P"]], "I": [["France", "Senegal", 3, 1, "R"], ["Iraq", "Norway", 1, 4, "R"], ["France", "Iraq", 3, 0, "R"], ["Norway", "Senegal", 3, 2, "R"], ["Norway", "France", 2, 2, "P"], ["Senegal", "Iraq", 2, 0, "P"]], "J": [["Argentina", "Algeria", 3, 0, "R"], ["Austria", "Jordan", 3, 1, "R"], ["Argentina", "Austria", 1, 0, "R"], ["Jordan", "Algeria", 1, 2, "R"], ["Algeria", "Austria", 1, 2, "P"], ["Jordan", "Argentina", 0, 3, "P"]], "K": [["Portugal", "DR Congo", 1, 1, "R"], ["Uzbekistan", "Colombia", 1, 3, "R"], ["Portugal", "Uzbekistan", 5, 0, "R"], ["Colombia", "DR Congo", 1, 0, "R"], ["Colombia", "Portugal", 1, 2, "P"], ["DR Congo", "Uzbekistan", 1, 1, "P"]], "L": [["England", "Croatia", 4, 2, "R"], ["Ghana", "Panama", 1, 0, "R"], ["England", "Ghana", 0, 0, "R"], ["Panama", "Croatia", 0, 1, "R"], ["Panama", "England", 0, 3, "P"], ["Croatia", "Ghana", 2, 1, "P"]]};
const RANK = {"Spain": 1, "France": 2, "Argentina": 3, "England": 4, "Brazil": 5, "Portugal": 6, "Germany": 7, "Netherlands": 8, "Belgium": 9, "Norway": 10, "Croatia": 11, "Uruguay": 12, "Morocco": 13, "Colombia": 14, "Switzerland": 15, "Japan": 16, "Senegal": 17, "Ecuador": 18, "Mexico": 19, "USA": 20, "Türkiye": 21, "Ivory Coast": 22, "Austria": 23, "Sweden": 24, "Egypt": 25, "Korea Republic": 26, "Canada": 27, "Iran": 28, "Paraguay": 29, "Czechia": 30, "Algeria": 31, "Scotland": 32, "Australia": 33, "Panama": 34, "Qatar": 35, "Saudi Arabia": 36, "Tunisia": 37, "Bosnia & H.": 38, "South Africa": 39, "DR Congo": 40, "Ghana": 41, "Uzbekistan": 42, "Cape Verde": 43, "Jordan": 44, "New Zealand": 45, "Iraq": 46, "Curaçao": 47, "Haiti": 48};
const THIRD_WINDOW = {A:"C/E/F/H/I",B:"E/F/G/I/J",D:"B/E/F/I/J",E:"A/B/C/D/F",G:"A/E/H/I/J",I:"C/D/F/G/H",K:"D/E/I/J/L",L:"E/H/I/J/K"};
const TYPELABEL = {W3:"Winner \u00d7 3rd-place",WR:"Winner \u00d7 Runner-up",RR:"Runner-up \u00d7 Runner-up"};

/* official Round-of-32..Final structure (FIFA / Wikipedia match map) */
const MATCHES = [
 {id:73,r:"Round of 32",type:"RR",s:[{ru:"A"},{ru:"B"}]},
 {id:74,r:"Round of 32",type:"W3",s:[{w:"E"},{t:"E"}]},
 {id:75,r:"Round of 32",type:"WR",s:[{w:"F"},{ru:"C"}]},
 {id:76,r:"Round of 32",type:"WR",s:[{w:"C"},{ru:"F"}]},
 {id:77,r:"Round of 32",type:"W3",s:[{w:"I"},{t:"I"}]},
 {id:78,r:"Round of 32",type:"RR",s:[{ru:"E"},{ru:"I"}]},
 {id:79,r:"Round of 32",type:"W3",s:[{w:"A"},{t:"A"}]},
 {id:80,r:"Round of 32",type:"W3",s:[{w:"L"},{t:"L"}]},
 {id:81,r:"Round of 32",type:"W3",s:[{w:"D"},{t:"D"}]},
 {id:82,r:"Round of 32",type:"W3",s:[{w:"G"},{t:"G"}]},
 {id:83,r:"Round of 32",type:"RR",s:[{ru:"K"},{ru:"L"}]},
 {id:84,r:"Round of 32",type:"WR",s:[{w:"H"},{ru:"J"}]},
 {id:85,r:"Round of 32",type:"W3",s:[{w:"B"},{t:"B"}]},
 {id:86,r:"Round of 32",type:"WR",s:[{w:"J"},{ru:"H"}]},
 {id:87,r:"Round of 32",type:"W3",s:[{w:"K"},{t:"K"}]},
 {id:88,r:"Round of 32",type:"RR",s:[{ru:"D"},{ru:"G"}]},
 {id:89,r:"Round of 16",s:[{W:74},{W:77}]},
 {id:90,r:"Round of 16",s:[{W:73},{W:75}]},
 {id:91,r:"Round of 16",s:[{W:76},{W:78}]},
 {id:92,r:"Round of 16",s:[{W:79},{W:80}]},
 {id:93,r:"Round of 16",s:[{W:83},{W:84}]},
 {id:94,r:"Round of 16",s:[{W:81},{W:82}]},
 {id:95,r:"Round of 16",s:[{W:86},{W:88}]},
 {id:96,r:"Round of 16",s:[{W:85},{W:87}]},
 {id:97,r:"Quarterfinals",s:[{W:89},{W:90}]},
 {id:98,r:"Quarterfinals",s:[{W:93},{W:94}]},
 {id:99,r:"Quarterfinals",s:[{W:91},{W:92}]},
 {id:100,r:"Quarterfinals",s:[{W:95},{W:96}]},
 {id:101,r:"Semifinals",s:[{W:97},{W:98}]},
 {id:102,r:"Semifinals",s:[{W:99},{W:100}]},
 {id:103,r:"Third place",s:[{L:101},{L:102}]},
 {id:104,r:"Final",s:[{W:101},{W:102}]}
];
const BYID = {}; MATCHES.forEach(m=>BYID[m.id]=m);

let order, thirds, overrides;
function resetState(){
  order={}; GLETTERS.forEach(g=>order[g]=DEFAULT[g].slice());
  thirds=new Set(DEFAULT_THIRDS);
  overrides={};
}
resetState();

function annexAssign(){
  if(thirds.size!==8) return null;
  const MAP=window.__annexMAP, WIN=window.__annexWIN;
  if(!MAP||!WIN) return null;
  const a=MAP[[...thirds].sort().join("")];
  if(!a) return null;
  const m={}; WIN.forEach((w,i)=>m[w]=a[i]); return m;
}
function slotTeam(spec){
  if("w" in spec)  return {name:order[spec.w][0],  sub:"Grp "+spec.w+" winner",    known:true};
  if("ru" in spec) return {name:order[spec.ru][1], sub:"Grp "+spec.ru+" runner-up", known:true};
  if("t" in spec){
    const A=annexAssign();
    if(A){ const tg=A[spec.t]; return {name:order[tg][2], sub:"3rd \u00b7 Grp "+tg, known:true}; }
    return {name:null, sub:"3rd \u00b7 "+THIRD_WINDOW[spec.t], known:false};
  }
  if("W" in spec){ const r=matchTeam(spec.W,"win");  return r.known?{name:r.name,sub:"",known:true}:{name:null,sub:"Winner M"+spec.W,known:false}; }
  if("L" in spec){ const r=matchTeam(spec.L,"lose"); return r.known?{name:r.name,sub:"",known:true}:{name:null,sub:"Loser M"+spec.L,known:false}; }
  return {name:null,sub:"?",known:false};
}
function rankOf(n){ return (n in RANK)?RANK[n]:999; }
function winnerSide(id){
  if(id in overrides) return overrides[id];
  const m=BYID[id];
  const a=slotTeam(m.s[0]), b=slotTeam(m.s[1]);
  if(a.known && b.known) return rankOf(a.name)<=rankOf(b.name)?0:1;
  if(a.known) return 0;
  if(b.known) return 1;
  return null;
}
function matchTeam(id,which){
  const s=winnerSide(id);
  if(s===null) return {known:false};
  const m=BYID[id];
  return slotTeam(which==="win"?m.s[s]:m.s[1-s]);
}

/* ---- group standings editor ---- */
function renderGroups(){
  const grid=document.getElementById("groupGrid");
  grid.innerHTML = GLETTERS.map(g=>{
    const rows=order[g].map((name,i)=>{
      const cls = i===0?"q1":i===1?"q2":(i===2&&thirds.has(g)?"q3":"out");
      const up='<button class="arrow" data-act="up" data-g="'+g+'" data-i="'+i+'"'+(i===0?" disabled":"")+'>\u2191</button>';
      const dn='<button class="arrow" data-act="dn" data-g="'+g+'" data-i="'+i+'"'+(i===3?" disabled":"")+'>\u2193</button>';
      const q = i===2 ? '<label class="q-toggle'+(thirds.has(g)?" on":"")+'"><input type="checkbox" data-act="q" data-g="'+g+'"'+(thirds.has(g)?" checked":"")+'> 3rd \u2713</label>' : '';
      return '<div class="trow '+cls+'"><span class="pos">'+(i+1)+'</span><span class="fl">'+fl(name)+'</span><span class="nm">'+name+'</span>'+q+'<span class="ctrl">'+up+dn+'</span></div>';
    }).join("");
    const fx=(FIXTURES[g]||[]).map(f=>{
      const h=f[0],a=f[1],hs=f[2],as_=f[3],stt=f[4];
      const tag = stt==="R" ? '<span class="fxtag r">RESULT</span>' : '<span class="fxtag p">PRED</span>';
      const hw=hs>as_, aw=as_>hs;
      return '<div class="fxrow"><span class="fxteam h'+(hw?" w":"")+'">'+h+' <span class="fl">'+fl(h)+'</span></span><span class="fxsc">'+hs+'\u2013'+as_+'</span><span class="fxteam a'+(aw?" w":"")+'"><span class="fl">'+fl(a)+'</span> '+a+'</span>'+tag+'</div>';
    }).join("");
    return '<div class="gcard"><div class="ghead"><span class="gtag">GROUP '+g+'</span><span class="note">results in \u00b7 \u2191 \u2193 to reorder</span></div><div class="standings">'+rows+'</div>'
      +'<button class="fx-toggle" data-g="'+g+'" aria-expanded="false">Results &amp; fixtures <span class="chev">\u2304</span></button>'
      +'<div class="fxwrap" id="fx-'+g+'">'+fx+'</div></div>';
  }).join("");
  updateCount();
}
function updateCount(){
  const el=document.getElementById("edCount"); if(!el) return;
  el.classList.toggle("bad", thirds.size!==8);
  el.innerHTML="Best 3rd-placed selected: <b>"+thirds.size+"</b> / 8";
}
function flashCount(){const el=document.getElementById("edCount"); if(!el)return; el.style.color="var(--coral)"; setTimeout(()=>el.style.color="",350);}
function wireGroups(){
  const grid=document.getElementById("groupGrid");
  grid.addEventListener("click",e=>{
    const fxb=e.target.closest(".fx-toggle");
    if(fxb){ const g=fxb.dataset.g, w=document.getElementById("fx-"+g), open=fxb.getAttribute("aria-expanded")==="true"; fxb.setAttribute("aria-expanded",String(!open)); w.classList.toggle("show",!open); return; }
    const a=e.target.closest("[data-act]"); if(!a||a.dataset.act==="q") return;
    const g=a.dataset.g, i=+a.dataset.i, j=a.dataset.act==="up"?i-1:i+1;
    if(j<0||j>3) return;
    const arr=order[g]; const tmp=arr[i]; arr[i]=arr[j]; arr[j]=tmp;
    renderGroups(); if(built.knockout) renderKO();
  });
  grid.addEventListener("change",e=>{
    const c=e.target.closest('input[data-act="q"]'); if(!c) return;
    const g=c.dataset.g;
    if(c.checked){ if(thirds.size>=8 && !thirds.has(g)){ c.checked=false; flashCount(); return; } thirds.add(g); }
    else thirds.delete(g);
    renderGroups(); if(built.knockout) renderKO();
  });
}

/* ---- live knockout ---- */
function sideHTML(m,idx){
  const st=slotTeam(m.s[idx]);
  const picked=winnerSide(m.id)===idx;
  const cls="side"+(picked?" pick":"")+(st.known?"":" tbd");
  const flag = st.known ? '<span class="fl">'+fl(st.name)+'</span>' : '<span class="fl">\u00b7</span>';
  const main = st.known ? st.name : (st.sub.indexOf("Winner")===0||st.sub.indexOf("Loser")===0 ? st.sub : "\u2014");
  let sub="";
  if(st.known && st.sub) sub='<span class="sub">'+st.sub+'</span>';
  else if(!st.known && st.sub.indexOf("3rd")===0) sub='<span class="sub">'+st.sub+'</span>';
  return '<button class="'+cls+'" data-m="'+m.id+'" data-s="'+idx+'">'+flag+'<span class="nm">'+main+'</span>'+sub+'<span class="pickmark">\u2713</span></button>';
}
function tieHTML(m){
  const isFinal=m.id===104;
  let crown="";
  if(isFinal){ const c=matchTeam(104,"win"); crown='<div class="crown">\u2605 '+(c.known?c.name+" \u2014 Champions":"Champion TBD")+' \u2605</div>'; }
  const badge=m.type?'<div class="tie-type t-'+m.type.toLowerCase()+'">'+TYPELABEL[m.type]+'</div>':"";
  let extra="";
  if(isFinal) extra='<div class="extra">MetLife Stadium, New Jersey \u00b7 July 19</div>';
  return '<div class="tie'+(isFinal?' final-tie':'')+'">'+crown+badge+sideHTML(m,0)+sideHTML(m,1)+extra+'</div>';
}
function renderKO(){
  const wrap=document.getElementById("koWrap");
  const rounds=["Round of 32","Round of 16","Quarterfinals","Semifinals","Third place","Final"];
  let html='<div class="ko-note">Built from <b>real results through Matchday 2</b> + my predictions for the remaining games. Group winners/runners-up come from your standings; the eight 3rd-placed slots resolve via the official Annex C table. Default winners follow team strength \u2014 <b>tap any team to override</b>, and reorder a group to watch it cascade.</div>';
  html+='<div class="ko-legend"><span class="lg-label">Round of 32 match types</span><span class="lg lg-w3">Winner \u00d7 3rd-place</span><span class="lg lg-wr">Winner \u00d7 Runner-up</span><span class="lg lg-rr">Runner-up \u00d7 Runner-up</span></div>';
  rounds.forEach(rn=>{
    const ms=MATCHES.filter(m=>m.r===rn);
    const title = rn==="Final" ? "The Final \u00b7 July 19" : rn;
    html+='<div class="ko-round"><div class="round-h">'+title+'</div><div class="ties'+(rn==="Final"?" ties-final":"")+'">'+ms.map(tieHTML).join("")+'</div></div>';
  });
  wrap.innerHTML=html;
}
function wireKO(){
  document.getElementById("koWrap").addEventListener("click",e=>{
    const b=e.target.closest(".side"); if(!b) return;
    overrides[+b.dataset.m]=+b.dataset.s;
    renderKO();
  });
}

/* ---- tabs ---- */
const tabs=[...document.querySelectorAll(".tab")];
const views={overview:document.getElementById("overview"),groups:document.getElementById("groups"),knockout:document.getElementById("knockout"),lookup:document.getElementById("lookup")};
let built={groups:false,knockout:false};
tabs.forEach(tab=>{
  tab.addEventListener("click",()=>{
    tabs.forEach(t=>t.setAttribute("aria-selected",String(t===tab)));
    Object.values(views).forEach(v=>v.classList.remove("on"));
    const v=tab.dataset.view; views[v].classList.add("on");
    if(v==="groups" && !built.groups){
      renderGroups(); wireGroups();
      const rb=document.getElementById("edReset");
      if(rb) rb.onclick=()=>{ resetState(); renderGroups(); if(built.knockout) renderKO(); };
      built.groups=true;
    }
    if(v==="knockout" && !built.knockout){ renderKO(); wireKO(); built.knockout=true; }
    if(v==="lookup" && window.__initLookup){ window.__initLookup(); }
    window.scrollTo({top:0,behavior:"auto"});
  });
});
</script>

<script>
/* ===== R32 lookup tab logic (isolated; lazy-built on first open) ===== */
(function(){
  const WIN=["A","B","D","E","G","I","K","L"];
  const ELIG={A:"CEFHI",B:"EFGIJ",D:"BEFIJ",E:"ABCDF",G:"AEHIJ",I:"CDFGH",K:"DEIJL",L:"EHIJK"};
  const TEAM={A:"Mexico",B:"Canada",C:"Brazil",D:"USA",E:"Germany",F:"Netherlands",G:"Belgium",H:"Spain",I:"France",J:"Argentina",K:"Portugal",L:"England"};
  const THIRD={A:"Korea Rep.",B:"Bosnia",C:"Scotland",D:"Paraguay",E:"Ivory Coast",F:"\u2014",G:"Egypt",H:"\u2014",I:"Senegal",J:"Algeria",K:"\u2014",L:"\u2014"};
  const ENC=["EFGHIJKLEJIFHGLK","DFGHIJKLHGIDJFLK","DEGHIJKLEJIDHGLK","DEFHIJKLEJIDHFLK","DEFGIJKLEGIDJFLK","DEFGHJKLEGJDHFLK","DEFGHIKLEGIDHFLK","DEFGHIJLEGJDHFLI","DEFGHIJKEGJDHFIK","CFGHIJKLHGICJFLK","CEGHIJKLEJICHGLK","CEFHIJKLEJICHFLK","CEFGIJKLEGICJFLK","CEFGHJKLEGJCHFLK","CEFGHIKLEGICHFLK","CEFGHIJLEGJCHFLI","CEFGHIJKEGJCHFIK","CDGHIJKLHGICJDLK","CDFHIJKLCJIDHFLK","CDFGIJKLCGIDJFLK","CDFGHJKLCGJDHFLK","CDFGHIKLCGIDHFLK","CDFGHIJLCGJDHFLI","CDFGHIJKCGJDHFIK","CDEHIJKLEJICHDLK","CDEGIJKLEGICJDLK","CDEGHJKLEGJCHDLK","CDEGHIKLEGICHDLK","CDEGHIJLEGJCHDLI","CDEGHIJKEGJCHDIK","CDEFIJKLCJEDIFLK","CDEFHJKLCJEDHFLK","CDEFHIKLCEIDHFLK","CDEFHIJLCJEDHFLI","CDEFHIJKCJEDHFIK","CDEFGJKLCGEDJFLK","CDEFGIKLCGEDIFLK","CDEFGIJLCGEDJFLI","CDEFGIJKCGEDJFIK","CDEFGHKLCGEDHFLK","CDEFGHJLCGJDHFLE","CDEFGHJKCGJDHFEK","CDEFGHILCGEDHFLI","CDEFGHIKCGEDHFIK","CDEFGHIJCGJDHFEI","BFGHIJKLHJBFIGLK","BEGHIJKLEJIBHGLK","BEFHIJKLEJBFIHLK","BEFGIJKLEJBFIGLK","BEFGHJKLEJBFHGLK","BEFGHIKLEGBFIHLK","BEFGHIJLEJBFHGLI","BEFGHIJKEJBFHGIK","BDGHIJKLHJBDIGLK","BDFHIJKLHJBDIFLK","BDFGIJKLIGBDJFLK","BDFGHJKLHGBDJFLK","BDFGHIKLHGBDIFLK","BDFGHIJLHGBDJFLI","BDFGHIJKHGBDJFIK","BDEHIJKLEJBDIHLK","BDEGIJKLEJBDIGLK","BDEGHJKLEJBDHGLK","BDEGHIKLEGBDIHLK","BDEGHIJLEJBDHGLI","BDEGHIJKEJBDHGIK","BDEFIJKLEJBDIFLK","BDEFHJKLEJBDHFLK","BDEFHIKLEIBDHFLK","BDEFHIJLEJBDHFLI","BDEFHIJKEJBDHFIK","BDEFGJKLEGBDJFLK","BDEFGIKLEGBDIFLK","BDEFGIJLEGBDJFLI","BDEFGIJKEGBDJFIK","BDEFGHKLEGBDHFLK","BDEFGHJLHGBDJFLE","BDEFGHJKHGBDJFEK","BDEFGHILEGBDHFLI","BDEFGHIKEGBDHFIK","BDEFGHIJHGBDJFEI","BCGHIJKLHJBCIGLK","BCFHIJKLHJBCIFLK","BCFGIJKLIGBCJFLK","BCFGHJKLHGBCJFLK","BCFGHIKLHGBCIFLK","BCFGHIJLHGBCJFLI","BCFGHIJKHGBCJFIK","BCEHIJKLEJBCIHLK","BCEGIJKLEJBCIGLK","BCEGHJKLEJBCHGLK","BCEGHIKLEGBCIHLK","BCEGHIJLEJBCHGLI","BCEGHIJKEJBCHGIK","BCEFIJKLEJBCIFLK","BCEFHJKLEJBCHFLK","BCEFHIKLEIBCHFLK","BCEFHIJLEJBCHFLI","BCEFHIJKEJBCHFIK","BCEFGJKLEGBCJFLK","BCEFGIKLEGBCIFLK","BCEFGIJLEGBCJFLI","BCEFGIJKEGBCJFIK","BCEFGHKLEGBCHFLK","BCEFGHJLHGBCJFLE","BCEFGHJKHGBCJFEK","BCEFGHILEGBCHFLI","BCEFGHIKEGBCHFIK","BCEFGHIJHGBCJFEI","BCDHIJKLHJBCIDLK","BCDGIJKLIGBCJDLK","BCDGHJKLHGBCJDLK","BCDGHIKLHGBCIDLK","BCDGHIJLHGBCJDLI","BCDGHIJKHGBCJDIK","BCDFIJKLCJBDIFLK","BCDFHJKLCJBDHFLK","BCDFHIKLCIBDHFLK","BCDFHIJLCJBDHFLI","BCDFHIJKCJBDHFIK","BCDFGJKLCGBDJFLK","BCDFGIKLCGBDIFLK","BCDFGIJLCGBDJFLI","BCDFGIJKCGBDJFIK","BCDFGHKLCGBDHFLK","BCDFGHJLCGBDHFLJ","BCDFGHJKHGBCJFDK","BCDFGHILCGBDHFLI","BCDFGHIKCGBDHFIK","BCDFGHIJHGBCJFDI","BCDEIJKLEJBCIDLK","BCDEHJKLEJBCHDLK","BCDEHIKLEIBCHDLK","BCDEHIJLEJBCHDLI","BCDEHIJKEJBCHDIK","BCDEGJKLEGBCJDLK","BCDEGIKLEGBCIDLK","BCDEGIJLEGBCJDLI","BCDEGIJKEGBCJDIK","BCDEGHKLEGBCHDLK","BCDEGHJLHGBCJDLE","BCDEGHJKHGBCJDEK","BCDEGHILEGBCHDLI","BCDEGHIKEGBCHDIK","BCDEGHIJHGBCJDEI","BCDEFJKLCJBDEFLK","BCDEFIKLCEBDIFLK","BCDEFIJLCJBDEFLI","BCDEFIJKCJBDEFIK","BCDEFHKLCEBDHFLK","BCDEFHJLCJBDHFLE","BCDEFHJKCJBDHFEK","BCDEFHILCEBDHFLI","BCDEFHIKCEBDHFIK","BCDEFHIJCJBDHFEI","BCDEFGKLCGBDEFLK","BCDEFGJLCGBDJFLE","BCDEFGJKCGBDJFEK","BCDEFGILCGBDEFLI","BCDEFGIKCGBDEFIK","BCDEFGIJCGBDJFEI","BCDEFGHLCGBDHFLE","BCDEFGHKCGBDHFEK","BCDEFGHJHGBCJFDE","BCDEFGHICGBDHFEI","AFGHIJKLHJIFAGLK","AEGHIJKLEJIAHGLK","AEFHIJKLEJIFAHLK","AEFGIJKLEJIFAGLK","AEFGHJKLEGJFAHLK","AEFGHIKLEGIFAHLK","AEFGHIJLEGJFAHLI","AEFGHIJKEGJFAHIK","ADGHIJKLHJIDAGLK","ADFHIJKLHJIDAFLK","ADFGIJKLIGJDAFLK","ADFGHJKLHGJDAFLK","ADFGHIKLHGIDAFLK","ADFGHIJLHGJDAFLI","ADFGHIJKHGJDAFIK","ADEHIJKLEJIDAHLK","ADEGIJKLEJIDAGLK","ADEGHJKLEGJDAHLK","ADEGHIKLEGIDAHLK","ADEGHIJLEGJDAHLI","ADEGHIJKEGJDAHIK","ADEFIJKLEJIDAFLK","ADEFHJKLHJEDAFLK","ADEFHIKLHEIDAFLK","ADEFHIJLHJEDAFLI","ADEFHIJKHJEDAFIK","ADEFGJKLEGJDAFLK","ADEFGIKLEGIDAFLK","ADEFGIJLEGJDAFLI","ADEFGIJKEGJDAFIK","ADEFGHKLHGEDAFLK","ADEFGHJLHGJDAFLE","ADEFGHJKHGJDAFEK","ADEFGHILHGEDAFLI","ADEFGHIKHGEDAFIK","ADEFGHIJHGJDAFEI","ACGHIJKLHJICAGLK","ACFHIJKLHJICAFLK","ACFGIJKLIGJCAFLK","ACFGHJKLHGJCAFLK","ACFGHIKLHGICAFLK","ACFGHIJLHGJCAFLI","ACFGHIJKHGJCAFIK","ACEHIJKLEJICAHLK","ACEGIJKLEJICAGLK","ACEGHJKLEGJCAHLK","ACEGHIKLEGICAHLK","ACEGHIJLEGJCAHLI","ACEGHIJKEGJCAHIK","ACEFIJKLEJICAFLK","ACEFHJKLHJECAFLK","ACEFHIKLHEICAFLK","ACEFHIJLHJECAFLI","ACEFHIJKHJECAFIK","ACEFGJKLEGJCAFLK","ACEFGIKLEGICAFLK","ACEFGIJLEGJCAFLI","ACEFGIJKEGJCAFIK","ACEFGHKLHGECAFLK","ACEFGHJLHGJCAFLE","ACEFGHJKHGJCAFEK","ACEFGHILHGECAFLI","ACEFGHIKHGECAFIK","ACEFGHIJHGJCAFEI","ACDHIJKLHJICADLK","ACDGIJKLIGJCADLK","ACDGHJKLHGJCADLK","ACDGHIKLHGICADLK","ACDGHIJLHGJCADLI","ACDGHIJKHGJCADIK","ACDFIJKLCJIDAFLK","ACDFHJKLHJFCADLK","ACDFHIKLHFICADLK","ACDFHIJLHJFCADLI","ACDFHIJKHJFCADIK","ACDFGJKLCGJDAFLK","ACDFGIKLCGIDAFLK","ACDFGIJLCGJDAFLI","ACDFGIJKCGJDAFIK","ACDFGHKLHGFCADLK","ACDFGHJLCGJDAFLH","ACDFGHJKHGJCAFDK","ACDFGHILHGFCADLI","ACDFGHIKHGFCADIK","ACDFGHIJHGJCAFDI","ACDEIJKLEJICADLK","ACDEHJKLHJECADLK","ACDEHIKLHEICADLK","ACDEHIJLHJECADLI","ACDEHIJKHJECADIK","ACDEGJKLEGJCADLK","ACDEGIKLEGICADLK","ACDEGIJLEGJCADLI","ACDEGIJKEGJCADIK","ACDEGHKLHGECADLK","ACDEGHJLHGJCADLE","ACDEGHJKHGJCADEK","ACDEGHILHGECADLI","ACDEGHIKHGECADIK","ACDEGHIJHGJCADEI","ACDEFJKLCJEDAFLK","ACDEFIKLCEIDAFLK","ACDEFIJLCJEDAFLI","ACDEFIJKCJEDAFIK","ACDEFHKLHEFCADLK","ACDEFHJLHJFCADLE","ACDEFHJKHJECAFDK","ACDEFHILHEFCADLI","ACDEFHIKHEFCADIK","ACDEFHIJHJECAFDI","ACDEFGKLCGEDAFLK","ACDEFGJLCGJDAFLE","ACDEFGJKCGJDAFEK","ACDEFGILCGEDAFLI","ACDEFGIKCGEDAFIK","ACDEFGIJCGJDAFEI","ACDEFGHLHGFCADLE","ACDEFGHKHGECAFDK","ACDEFGHJHGJCAFDE","ACDEFGHIHGECAFDI","ABGHIJKLHJBAIGLK","ABFHIJKLHJBAIFLK","ABFGIJKLIJBFAGLK","ABFGHJKLHJBFAGLK","ABFGHIKLHGBAIFLK","ABFGHIJLHJBFAGLI","ABFGHIJKHJBFAGIK","ABEHIJKLEJBAIHLK","ABEGIJKLEJBAIGLK","ABEGHJKLEJBAHGLK","ABEGHIKLEGBAIHLK","ABEGHIJLEJBAHGLI","ABEGHIJKEJBAHGIK","ABEFIJKLEJBAIFLK","ABEFHJKLEJBFAHLK","ABEFHIKLEIBFAHLK","ABEFHIJLEJBFAHLI","ABEFHIJKEJBFAHIK","ABEFGJKLEJBFAGLK","ABEFGIKLEGBAIFLK","ABEFGIJLEJBFAGLI","ABEFGIJKEJBFAGIK","ABEFGHKLEGBFAHLK","ABEFGHJLHJBFAGLE","ABEFGHJKHJBFAGEK","ABEFGHILEGBFAHLI","ABEFGHIKEGBFAHIK","ABEFGHIJHJBFAGEI","ABDHIJKLIJBDAHLK","ABDGIJKLIJBDAGLK","ABDGHJKLHJBDAGLK","ABDGHIKLIGBDAHLK","ABDGHIJLHJBDAGLI","ABDGHIJKHJBDAGIK","ABDFIJKLIJBDAFLK","ABDFHJKLHJBDAFLK","ABDFHIKLHIBDAFLK","ABDFHIJLHJBDAFLI","ABDFHIJKHJBDAFIK","ABDFGJKLFJBDAGLK","ABDFGIKLIGBDAFLK","ABDFGIJLFJBDAGLI","ABDFGIJKFJBDAGIK","ABDFGHKLHGBDAFLK","ABDFGHJLHGBDAFLJ","ABDFGHJKHGBDAFJK","ABDFGHILHGBDAFLI","ABDFGHIKHGBDAFIK","ABDFGHIJHGBDAFIJ","ABDEIJKLEJBAIDLK","ABDEHJKLEJBDAHLK","ABDEHIKLEIBDAHLK","ABDEHIJLEJBDAHLI","ABDEHIJKEJBDAHIK","ABDEGJKLEJBDAGLK","ABDEGIKLEGBAIDLK","ABDEGIJLEJBDAGLI","ABDEGIJKEJBDAGIK","ABDEGHKLEGBDAHLK","ABDEGHJLHJBDAGLE","ABDEGHJKHJBDAGEK","ABDEGHILEGBDAHLI","ABDEGHIKEGBDAHIK","ABDEGHIJHJBDAGEI","ABDEFJKLEJBDAFLK","ABDEFIKLEIBDAFLK","ABDEFIJLEJBDAFLI","ABDEFIJKEJBDAFIK","ABDEFHKLHEBDAFLK","ABDEFHJLHJBDAFLE","ABDEFHJKHJBDAFEK","ABDEFHILHEBDAFLI","ABDEFHIKHEBDAFIK","ABDEFHIJHJBDAFEI","ABDEFGKLEGBDAFLK","ABDEFGJLEGBDAFLJ","ABDEFGJKEGBDAFJK","ABDEFGILEGBDAFLI","ABDEFGIKEGBDAFIK","ABDEFGIJEGBDAFIJ","ABDEFGHLHGBDAFLE","ABDEFGHKHGBDAFEK","ABDEFGHJHGBDAFEJ","ABDEFGHIHGBDAFEI","ABCHIJKLIJBCAHLK","ABCGIJKLIJBCAGLK","ABCGHJKLHJBCAGLK","ABCGHIKLIGBCAHLK","ABCGHIJLHJBCAGLI","ABCGHIJKHJBCAGIK","ABCFIJKLIJBCAFLK","ABCFHJKLHJBCAFLK","ABCFHIKLHIBCAFLK","ABCFHIJLHJBCAFLI","ABCFHIJKHJBCAFIK","ABCFGJKLCJBFAGLK","ABCFGIKLIGBCAFLK","ABCFGIJLCJBFAGLI","ABCFGIJKCJBFAGIK","ABCFGHKLHGBCAFLK","ABCFGHJLHGBCAFLJ","ABCFGHJKHGBCAFJK","ABCFGHILHGBCAFLI","ABCFGHIKHGBCAFIK","ABCFGHIJHGBCAFIJ","ABCEIJKLEJBAICLK","ABCEHJKLEJBCAHLK","ABCEHIKLEIBCAHLK","ABCEHIJLEJBCAHLI","ABCEHIJKEJBCAHIK","ABCEGJKLEJBCAGLK","ABCEGIKLEGBAICLK","ABCEGIJLEJBCAGLI","ABCEGIJKEJBCAGIK","ABCEGHKLEGBCAHLK","ABCEGHJLHJBCAGLE","ABCEGHJKHJBCAGEK","ABCEGHILEGBCAHLI","ABCEGHIKEGBCAHIK","ABCEGHIJHJBCAGEI","ABCEFJKLEJBCAFLK","ABCEFIKLEIBCAFLK","ABCEFIJLEJBCAFLI","ABCEFIJKEJBCAFIK","ABCEFHKLHEBCAFLK","ABCEFHJLHJBCAFLE","ABCEFHJKHJBCAFEK","ABCEFHILHEBCAFLI","ABCEFHIKHEBCAFIK","ABCEFHIJHJBCAFEI","ABCEFGKLEGBCAFLK","ABCEFGJLEGBCAFLJ","ABCEFGJKEGBCAFJK","ABCEFGILEGBCAFLI","ABCEFGIKEGBCAFIK","ABCEFGIJEGBCAFIJ","ABCEFGHLHGBCAFLE","ABCEFGHKHGBCAFEK","ABCEFGHJHGBCAFEJ","ABCEFGHIHGBCAFEI","ABCDIJKLIJBCADLK","ABCDHJKLHJBCADLK","ABCDHIKLHIBCADLK","ABCDHIJLHJBCADLI","ABCDHIJKHJBCADIK","ABCDGJKLCJBDAGLK","ABCDGIKLIGBCADLK","ABCDGIJLCJBDAGLI","ABCDGIJKCJBDAGIK","ABCDGHKLHGBCADLK","ABCDGHJLHGBCADLJ","ABCDGHJKHGBCADJK","ABCDGHILHGBCADLI","ABCDGHIKHGBCADIK","ABCDGHIJHGBCADIJ","ABCDFJKLCJBDAFLK","ABCDFIKLCIBDAFLK","ABCDFIJLCJBDAFLI","ABCDFIJKCJBDAFIK","ABCDFHKLHFBCADLK","ABCDFHJLCJBDAFLH","ABCDFHJKHJBCAFDK","ABCDFHILHFBCADLI","ABCDFHIKHFBCADIK","ABCDFHIJHJBCAFDI","ABCDFGKLCGBDAFLK","ABCDFGJLCGBDAFLJ","ABCDFGJKCGBDAFJK","ABCDFGILCGBDAFLI","ABCDFGIKCGBDAFIK","ABCDFGIJCGBDAFIJ","ABCDFGHLCGBDAFLH","ABCDFGHKHGBCAFDK","ABCDFGHJHGBCAFDJ","ABCDFGHIHGBCAFDI","ABCDEJKLEJBCADLK","ABCDEIKLEIBCADLK","ABCDEIJLEJBCADLI","ABCDEIJKEJBCADIK","ABCDEHKLHEBCADLK","ABCDEHJLHJBCADLE","ABCDEHJKHJBCADEK","ABCDEHILHEBCADLI","ABCDEHIKHEBCADIK","ABCDEHIJHJBCADEI","ABCDEGKLEGBCADLK","ABCDEGJLEGBCADLJ","ABCDEGJKEGBCADJK","ABCDEGILEGBCADLI","ABCDEGIKEGBCADIK","ABCDEGIJEGBCADIJ","ABCDEGHLHGBCADLE","ABCDEGHKHGBCADEK","ABCDEGHJHGBCADEJ","ABCDEGHIHGBCADEI","ABCDEFKLCEBDAFLK","ABCDEFJLCJBDAFLE","ABCDEFJKCJBDAFEK","ABCDEFILCEBDAFLI","ABCDEFIKCEBDAFIK","ABCDEFIJCJBDAFEI","ABCDEFHLHFBCADLE","ABCDEFHKHEBCAFDK","ABCDEFHJHJBCAFDE","ABCDEFHIHEBCAFDI","ABCDEFGLCGBDAFLE","ABCDEFGKCGBDAFEK","ABCDEFGJCGBDAFEJ","ABCDEFGICGBDAFEI","ABCDEFGHHGBCAFDE"];
  const MAP={}; for(const s of ENC){ MAP[s.slice(0,8)]=s.slice(8); } window.__annexMAP=MAP; window.__annexWIN=WIN;
  const LGROUPS="ABCDEFGHIJKL".split("");
  let sel=new Set(); let built=false;

  function flash(){const c=document.getElementById("cnt"); if(!c)return; c.style.color="var(--coral)"; setTimeout(()=>c.style.color="",350);}
  function toggle(g,b){
    if(sel.has(g)){sel.delete(g); b.setAttribute("aria-pressed","false");}
    else{ if(sel.size>=8){flash(); return;} sel.add(g); b.setAttribute("aria-pressed","true"); }
    render();
  }
  function render(){
    document.getElementById("cnt").textContent=sel.size;
    const res=document.getElementById("result"), hint=document.getElementById("hint");
    if(sel.size!==8){res.classList.remove("show"); hint.style.display="block";
      hint.textContent = sel.size<8 ? "Select exactly eight groups to see the eight third-place matchups." : ""; return;}
    hint.style.display="none";
    const key=[...sel].sort().join("");
    const assign=MAP[key];
    const usingPred = key==="ABCDEGIJ";
    document.getElementById("scenarioTag").textContent =
      "Scenario: thirds from groups "+[...sel].sort().join(" ")+(usingPred?"  \u00b7  my predicted bracket":"");
    document.getElementById("pairs").innerHTML = WIN.map((w,i)=>{
      const third=assign[i];
      const namePart = usingPred ? '<span class="lab">'+TEAM[w]+" v "+THIRD[third]+"</span>" : "";
      return '<div class="pair"><span class="w">1'+w+'</span><span class="vs">vs</span><span class="t">3'+third+"</span>"+namePart+"</div>";
    }).join("");
    res.classList.add("show");
  }
  function build(){
    const chips=document.getElementById("chips");
    LGROUPS.forEach(g=>{
      const b=document.createElement("button");
      b.className="chip"; b.setAttribute("aria-pressed","false"); b.dataset.g=g;
      b.innerHTML=g+"<small>"+(TEAM[g]||"").toUpperCase()+"</small>";
      b.onclick=()=>toggle(g,b); chips.appendChild(b);
    });
    document.getElementById("clearBtn").onclick=()=>{sel.clear(); document.querySelectorAll("#lookup .chip").forEach(c=>c.setAttribute("aria-pressed","false")); render();};
    document.getElementById("predBtn").onclick=()=>{
      sel=new Set("ABCDEGIJ".split(""));
      document.querySelectorAll("#lookup .chip").forEach(c=>c.setAttribute("aria-pressed", sel.has(c.dataset.g)?"true":"false"));
      render();
    };
    document.getElementById("eligBody").innerHTML = WIN.map(w=>{
      const e=ELIG[w].split("").map(x=>"<b>"+x+"</b>").join(" / ");
      return '<tr><td class="win">Winner '+w+'</td><td class="elig">3rd from '+e+"</td></tr>";
    }).join("");
  }
  window.__initLookup=function(){ if(built) return; built=true; build(); };
})();
</script>
