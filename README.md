<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Diário do Além — chocollate</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300..900;1,9..144,300..900&family=Lora:ital,wght@0,400..700;1,400..700&family=Jost:wght@300..600&display=swap" rel="stylesheet">
<style>
  :root{
    --void:#110a17;
    --abyss:#1c1126;
    --abyss-2:#281634;
    --line:#3a2740;
    --amethyst:#a675ee;
    --amethyst-soft:#8456cf;
    --amethyst-dim:#4d3470;
    --crimson:#c0405c;
    --mist:#cdb6e6;
    --parchment:#f4ecf8;
    --stem:#43314c;
  }

  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    margin:0;
    min-height:100vh;
    background:var(--void);
    color:var(--parchment);
    font-family:'Lora',serif;
    overflow-x:hidden;
    position:relative;
  }

  /* ---------- ambient shards ---------- */
  .shards{position:fixed;inset:0;z-index:0;pointer-events:none;overflow:hidden;}
  .shard{
    position:absolute;
    width:22px;height:64px;
    background:linear-gradient(160deg,#8a3550,#3a1422);
    clip-path:polygon(50% 0%,100% 38%,58% 100%,42% 100%,0% 38%);
    opacity:.16;
    animation:drift 18s ease-in-out infinite;
  }
  .shard.amethyst{background:linear-gradient(160deg,#9d6fe6,#3c2a57);}
  .shard:nth-child(1){top:8%;left:6%;width:18px;height:50px;animation-duration:21s;}
  .shard:nth-child(2){top:62%;left:3%;width:26px;height:72px;animation-duration:26s;animation-delay:-4s;}
  .shard:nth-child(3){top:18%;left:92%;width:20px;height:58px;animation-duration:19s;animation-delay:-9s;}
  .shard:nth-child(4){top:74%;left:90%;width:30px;height:80px;animation-duration:24s;animation-delay:-2s;}
  .shard:nth-child(5){top:40%;left:50%;width:16px;height:44px;animation-duration:22s;animation-delay:-12s;opacity:.10;}
  .shard:nth-child(6){top:88%;left:30%;width:20px;height:56px;animation-duration:20s;animation-delay:-6s;}
  .shard:nth-child(7){top:4%;left:46%;width:18px;height:50px;animation-duration:23s;animation-delay:-15s;}
  @keyframes drift{
    0%,100%{transform:translateY(0) rotate(0deg);}
    50%{transform:translateY(-26px) rotate(10deg);}
  }

  /* ---------- shared layout ---------- */
  .view{position:relative;z-index:1;animation:viewIn .6s ease both;}
  .view.hidden{display:none;}
  @keyframes viewIn{from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);}}

  /* ---------- hero / cover ---------- */
  .hero{
    display:grid;
    grid-template-columns:minmax(240px,360px) 1fr;
    align-items:center;
    gap:clamp(2.5rem,6vw,5.5rem);
    max-width:1180px;
    margin:0 auto;
    padding:clamp(3rem,8vw,6rem) clamp(1.5rem,5vw,3rem) clamp(3.5rem,8vw,5rem);
  }
  .cover-wrap{position:relative;}
  .cover-glow{
    position:absolute;inset:-15%;
    background:radial-gradient(circle at 50% 35%,var(--amethyst-dim),transparent 70%);
    filter:blur(46px);
    opacity:.7;
    z-index:-1;
  }
  .cover-frame{
    position:relative;
    clip-path:polygon(7% 0%,100% 0%,100% 93%,93% 100%,0% 100%,0% 7%);
    background:linear-gradient(135deg,var(--amethyst),var(--crimson));
    padding:3px;
  }
  .cover-frame img{
    filter:saturate(1.08) contrast(1.05);
display:block;width:100%;height:auto;
    clip-path:polygon(7% 0%,100% 0%,100% 93%,93% 100%,0% 100%,0% 7%);
  }
  .vine-corner{position:absolute;width:128px;height:184px;overflow:visible;}
  .vine-tl{top:-34px;left:-46px;}
  .vine-br{bottom:-34px;right:-46px;transform:rotate(180deg);}

  .hero-text{position:relative;}
  .eyebrow{
    font-family:'Jost',sans-serif;font-weight:500;
    font-size:.72rem;letter-spacing:.32em;text-transform:uppercase;
    color:var(--amethyst);margin:0 0 .6rem;
  }
  h1.title{
    font-family:'Fraunces',serif;font-weight:600;
    font-variation-settings:'opsz' 144,'SOFT' 10,'WONK' 1;
    font-size:clamp(2.6rem,6.2vw,4.4rem);
    line-height:1.05;letter-spacing:-.01em;
    margin:0;color:var(--parchment);
  }
  .title-rule{
    width:84px;height:3px;margin:1rem 0 1.1rem;
    background:linear-gradient(90deg,var(--crimson),var(--amethyst));
  }
  .hero-text .by{
    font-family:'Jost',sans-serif;font-weight:300;font-style:italic;
    font-size:1rem;letter-spacing:.08em;
    color:var(--mist);margin:0 0 1.4rem;
  }
  .hero-text .by::before{content:'escrito por ';font-style:normal;opacity:.7;}
  blockquote{
    font-family:'Fraunces',serif;font-style:italic;font-weight:400;
    font-size:1.18rem;line-height:1.65;
    color:var(--mist);
    border-left:2px solid var(--crimson);
    padding-left:1.1rem;margin:0;max-width:30ch;
  }
  .cta{
    display:inline-flex;align-items:center;gap:.65rem;
    font-family:'Jost',sans-serif;font-weight:500;font-size:.92rem;
    letter-spacing:.12em;text-transform:uppercase;
    color:var(--parchment);
    background:linear-gradient(135deg,var(--amethyst-soft),var(--crimson));
    border:none;cursor:pointer;
    padding:.95rem 1.9rem;margin-top:2rem;
    clip-path:polygon(5% 0,100% 0,100% 68%,95% 100%,0 100%,0 32%);
    transition:transform .25s ease,box-shadow .25s ease;
  }
  .cta:hover{transform:translateY(-2px);box-shadow:0 10px 32px -10px var(--amethyst);}
  .cta svg{width:18px;height:18px;flex-shrink:0;}

  /* ---------- index ---------- */
  .index{max-width:740px;margin:0 auto;padding:0 clamp(1.5rem,5vw,3rem) 6rem;}
  .vine-divider{display:flex;justify-content:center;margin:0 auto 1rem;width:100%;max-width:480px;}
  .vine-divider svg{width:100%;height:42px;}
  .index-head{text-align:center;margin-bottom:2.2rem;}
  .index-head .eyebrow{justify-content:center;display:block;text-align:center;}
  .index-head h2{
    font-family:'Fraunces',serif;font-weight:600;font-size:1.9rem;
    margin:.4rem 0 0;letter-spacing:.04em;color:var(--parchment);
  }
  ul.chapter-list{list-style:none;margin:0;padding:0;border-top:1px solid var(--line);}
  .chapter-item button{
    all:unset;
    display:flex;align-items:center;gap:1.1rem;
    width:100%;padding:1.05rem .6rem;
    cursor:pointer;border-bottom:1px solid var(--line);
    transition:background .25s ease,padding-left .25s ease;
  }
  .chapter-item button:hover{background:var(--abyss-2);}
  .chapter-item.interludio button{padding-left:2.4rem;}
  .chapter-item.interludio button:hover{padding-left:2.7rem;}
  .chapter-icon{
    flex-shrink:0;width:26px;height:26px;opacity:.45;
    transition:opacity .25s ease,transform .25s ease,filter .25s ease;
  }
  .chapter-item button:hover .chapter-icon{
    opacity:1;transform:scale(1.18) rotate(-6deg);
    filter:drop-shadow(0 0 7px var(--amethyst));
  }
  .chapter-meta{display:flex;flex-direction:column;gap:.2rem;text-align:left;}
  .chapter-meta .num{
    font-family:'Jost',sans-serif;font-size:.68rem;font-weight:500;
    letter-spacing:.24em;text-transform:uppercase;color:var(--amethyst);
  }
  .chapter-meta .ttl{
    font-family:'Fraunces',serif;font-size:1.18rem;color:var(--parchment);
  }
  .chapter-item.interludio .num{color:var(--mist);}
  .chapter-item.interludio .ttl{font-style:italic;font-size:1.04rem;color:var(--mist);}
  .chapter-arrow{
    margin-left:auto;color:var(--crimson);font-family:'Jost',sans-serif;
    opacity:0;transform:translateX(-8px);
    transition:opacity .25s ease,transform .25s ease;
  }
  .chapter-item button:hover .chapter-arrow{opacity:1;transform:translateX(0);}

  .home-footer{
    text-align:center;font-family:'Jost',sans-serif;font-size:.74rem;
    letter-spacing:.28em;text-transform:uppercase;color:var(--stem);
    padding-bottom:3rem;
  }

  /* ---------- reader ---------- */
  #reader{max-width:660px;margin:0 auto;padding:clamp(2rem,5vw,3.2rem) clamp(1.25rem,5vw,2rem) 6rem;}
  .reader-nav{display:flex;justify-content:space-between;align-items:center;gap:1rem;}
  .back-btn{
    font-family:'Jost',sans-serif;font-size:.8rem;letter-spacing:.1em;
    color:var(--mist);background:none;border:1px solid var(--line);
    padding:.55rem 1.1rem;cursor:pointer;border-radius:1px;
    transition:border-color .2s ease,color .2s ease;
  }
  .back-btn:hover{border-color:var(--amethyst);color:var(--amethyst);}
  .reader-label{
    font-family:'Jost',sans-serif;font-size:.7rem;font-weight:500;
    letter-spacing:.3em;text-transform:uppercase;color:var(--amethyst);
    text-align:right;
  }
  .reader-title{
    font-family:'Fraunces',serif;font-weight:600;
    font-size:clamp(1.8rem,5.5vw,2.5rem);
    text-align:center;line-height:1.2;
    margin:1.6rem 0 2.4rem;color:var(--parchment);
  }
  #reader-content p{
    font-family:'Lora',serif;font-size:1.08rem;line-height:1.95;
    color:var(--parchment);margin:0 0 1.05rem;
  }
  .reader-controls{
    display:flex;justify-content:space-between;align-items:center;
    margin-top:3.2rem;gap:1rem;
  }
  .reader-controls button{
    font-family:'Jost',sans-serif;font-size:.82rem;letter-spacing:.08em;
    color:var(--parchment);background:none;border:1px solid var(--line);
    padding:.75rem 1.5rem;cursor:pointer;border-radius:1px;
    transition:border-color .2s ease,color .2s ease,transform .2s ease;
  }
  .reader-controls button:hover:not(:disabled){
    border-color:var(--crimson);color:var(--crimson);transform:translateY(-1px);
  }
  .reader-controls button:disabled{opacity:.3;cursor:default;}

  /* ---------- vine svg animation ---------- */
  .stem{fill:none;stroke:var(--stem);stroke-width:2.5;stroke-linecap:round;
    stroke-dasharray:1100;stroke-dashoffset:1100;
    animation:growStem 1.6s ease-out forwards;}
  .gem-anim{opacity:0;transform-origin:center;transform-box:fill-box;
    animation:bloomGem .7s ease-out forwards;animation-delay:1.1s;}
  .thorn{fill:#5a3f63;}
  @keyframes growStem{to{stroke-dashoffset:0;}}
  @keyframes bloomGem{from{opacity:0;transform:scale(.35);}to{opacity:1;transform:scale(1);}}

  @media (prefers-reduced-motion:reduce){
    .shard{animation:none!important;}
    .view{animation:none!important;}
    .stem{animation:none!important;stroke-dashoffset:0;}
    .gem-anim{animation:none!important;opacity:1;transform:scale(1);}
    .cta:hover{transform:none;}
  }

  @media (max-width:860px){
    .hero{grid-template-columns:1fr;text-align:center;}
    .hero-text{display:flex;flex-direction:column;align-items:center;}
    .title-rule{margin:1rem auto 1.1rem;}
    blockquote{text-align:left;}
    .vine-corner{display:none;}
    .cover-wrap{max-width:320px;margin:0 auto;}
  }
</style>

<style>
body::before{
content:'';
position:fixed;
left:0;top:0;bottom:0;
width:120px;
pointer-events:none;
opacity:.18;
background:
radial-gradient(circle at 30px 120px,#9d6fe6 0 8px,transparent 10px),
radial-gradient(circle at 60px 280px,#9d6fe6 0 7px,transparent 9px),
radial-gradient(circle at 25px 520px,#9d6fe6 0 8px,transparent 10px);
filter:blur(.2px);
}
body::after{
content:'';
position:fixed;
right:0;top:0;bottom:0;
width:120px;
pointer-events:none;
opacity:.18;
background:
radial-gradient(circle at 90px 180px,#9d6fe6 0 8px,transparent 10px),
radial-gradient(circle at 50px 420px,#9d6fe6 0 7px,transparent 9px),
radial-gradient(circle at 95px 700px,#9d6fe6 0 8px,transparent 10px);
}
.hero{
filter:drop-shadow(0 0 25px rgba(166,117,238,.15));
}
.cover-frame{
box-shadow:0 0 40px rgba(166,117,238,.25);
}
.chapter-item button:hover{
box-shadow:inset 0 0 18px rgba(166,117,238,.12);
}
</style>

</head>
<body>

<div class="shards" aria-hidden="true">
  <div class="shard"></div>
  <div class="shard amethyst"></div>
  <div class="shard"></div>
  <div class="shard amethyst"></div>
  <div class="shard"></div>
  <div class="shard amethyst"></div>
  <div class="shard"></div>
</div>

<!-- shared SVG defs: faceted violet "gem-flower" + thorns -->
<svg aria-hidden="true" focusable="false" style="position:absolute;width:0;height:0;overflow:hidden">
  <defs>
    <linearGradient id="gemGrad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0" stop-color="#dcc2ff"/>
      <stop offset="1" stop-color="#7b4fc4"/>
    </linearGradient>
    <path id="petal" d="M24 24 L31 4 L38 18 Z"/>
    <symbol id="gem" viewBox="0 0 48 48">
      <g fill="url(#gemGrad)">
        <use href="#petal" xlink:href="#petal" transform="rotate(0 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(72 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(144 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(216 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(288 24 24)"/>
      </g>
      <path d="M24 16 L32 24 L24 32 L16 24 Z" fill="#f4e9ff"/>
      <path d="M24 19.5 L28.5 24 L24 28.5 L19.5 24 Z" fill="#c0405c"/>
    </symbol>
    <symbol id="thorn" viewBox="0 0 16 16">
      <path d="M8 1 L15 15 L1 15 Z" fill="#5a3f63"/>
      <path d="M8 1 L11.5 15 L1 15 Z" fill="#3c2945"/>
    </symbol>
  </defs>
</svg>

<!-- ================= HOME ================= -->
<main id="home" class="view">

  <section class="hero">
    <div class="cover-wrap">
      <div class="cover-glow"></div>
      <div class="cover-frame">
        <img src="data:image/png;base64,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:none!important;}
    .stem{animation:none!important;stroke-dashoffset:0;}
    .gem-anim{animation:none!important;opacity:1;transform:scale(1);}
    .cta:hover{transform:none;}
  }

  @media (max-width:860px){
    .hero{grid-template-columns:1fr;text-align:center;}
    .hero-text{display:flex;flex-direction:column;align-items:center;}
    .title-rule{margin:1rem auto 1.1rem;}
    blockquote{text-align:left;}
    .vine-corner{display:none;}
    .cover-wrap{max-width:320px;margin:0 auto;}
  }
</style>
</head>
<body>

<div class="shards" aria-hidden="true">
  <div class="shard"></div>
  <div class="shard amethyst"></div>
  <div class="shard"></div>
  <div class="shard amethyst"></div>
  <div class="shard"></div>
  <div class="shard amethyst"></div>
  <div class="shard"></div>
</div>

<!-- shared SVG defs: faceted violet "gem-flower" + thorns -->
<svg aria-hidden="true" focusable="false" style="position:absolute;width:0;height:0;overflow:hidden">
  <defs>
    <linearGradient id="gemGrad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0" stop-color="#dcc2ff"/>
      <stop offset="1" stop-color="#7b4fc4"/>
    </linearGradient>
    <path id="petal" d="M24 24 L31 4 L38 18 Z"/>
    <symbol id="gem" viewBox="0 0 48 48">
      <g fill="url(#gemGrad)">
        <use href="#petal" xlink:href="#petal" transform="rotate(0 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(72 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(144 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(216 24 24)"/>
        <use href="#petal" xlink:href="#petal" transform="rotate(288 24 24)"/>
      </g>
      <path d="M24 16 L32 24 L24 32 L16 24 Z" fill="#f4e9ff"/>
      <path d="M24 19.5 L28.5 24 L24 28.5 L19.5 24 Z" fill="#c0405c"/>
    </symbol>
    <symbol id="thorn" viewBox="0 0 16 16">
      <path d="M8 1 L15 15 L1 15 Z" fill="#5a3f63"/>
      <path d="M8 1 L11.5 15 L1 15 Z" fill="#3c2945"/>
    </symbol>
  </defs>
</svg>

<!-- ================= HOME ================= -->
<main id="home" class="view">

  <section class="hero">
    <div class="cover-wrap">
      <div class="cover-glow"></div>
      <div class="cover-frame">
        <img src="data:image/jpeg;base64,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
