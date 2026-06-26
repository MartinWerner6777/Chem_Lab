[index(11).html](https://github.com/user-attachments/files/29395487/index.11.html)
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>ChemLab – Interaktive Chemie-Lernplattform</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;0,9..144,500;1,9..144,300&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&display=swap" rel="stylesheet">
<style>

*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f6f5f1;--bg2:#fff;--bg3:#efece7;--bg4:#e6e3de;
  --t1:#1a1917;--t2:#5c5a56;--t3:#9c9a96;--t4:#c8c5be;
  --bdr:#e2dfd8;--bdr2:#ccc9c2;
  --acc:#1a5c3a;--acl:#e6f2ec;--acd:#2d8a5a;
  --bl:#1a3d7a;--bll:#e6edf8;
  --rd:#7a1a1a;--rdl:#fce8e8;
  --am:#7a4800;--aml:#fdf2e0;
  --pu:#3d1a7a;--pul:#ede8f8;
  --te:#0a5050;--tel:#e0f4f4;
  --shadow:0 2px 12px rgba(0,0,0,.08);
  --shadow-lg:0 8px 32px rgba(0,0,0,.16);
  --r:12px;--rlg:18px;
  --tr:all .2s cubic-bezier(.4,0,.2,1);
}
.dk{
  --bg:#0a0a08;--bg2:#141412;--bg3:#1e1e1b;--bg4:#282825;
  --t1:#f0ece4;--t2:#a0a09a;--t3:#606058;--t4:#3a3830;
  --bdr:#222220;--bdr2:#32322e;
}
html,body{font-family:'DM Sans',system-ui,sans-serif;background:var(--bg);color:var(--t1);font-size:13px;overflow:hidden;height:100%;transition:background .3s,color .3s}

/* ── INFINITY ZOOM UNIVERSE ── */
#universe{position:fixed;inset:0;overflow:hidden;perspective:1200px;perspective-origin:50% 50%}
#zoom-world{position:absolute;inset:0;transform-style:preserve-3d;transition:transform 1.1s cubic-bezier(.77,0,.175,1)}

/* ── LAYERS ── */
.layer{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;transform-style:preserve-3d;pointer-events:none;opacity:0;transition:opacity .6s}
.layer.active{pointer-events:all;opacity:1}
.layer.entering{opacity:1}

/* ── HUD (always on top) ── */
#hud{position:fixed;top:0;left:0;right:0;height:52px;background:rgba(246,245,241,.92);backdrop-filter:blur(12px);border-bottom:0.5px solid var(--bdr);display:flex;align-items:center;gap:10px;padding:0 20px;z-index:1000;transition:background .3s}
.dk #hud{background:rgba(10,10,8,.92)}
.hud-logo{font-family:'Fraunces',serif;font-size:17px;color:var(--t1);flex-shrink:0;display:flex;align-items:center;gap:8px;cursor:pointer}
.hud-logo-ico{width:28px;height:28px;background:var(--acc);border-radius:7px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:13px;font-style:italic}
.hud-logo span{color:var(--acc)}
.hud-breadcrumb{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--t3)}
.hud-breadcrumb .crumb{cursor:pointer;transition:color .15s;padding:3px 7px;border-radius:6px}
.hud-breadcrumb .crumb:hover{color:var(--t1);background:var(--bg3)}
.hud-breadcrumb .crumb.active{color:var(--acc);font-weight:500}
.hud-breadcrumb .sep{opacity:.4}
.hud-right{margin-left:auto;display:flex;gap:8px;align-items:center}
.hud-btn{width:30px;height:30px;border-radius:7px;background:var(--bg3);border:0.5px solid var(--bdr);display:flex;align-items:center;justify-content:center;cursor:pointer;color:var(--t2);font-size:14px;transition:var(--tr)}
.hud-btn:hover{background:var(--bg4);color:var(--t1)}
.srch-wrap{flex:1;max-width:340px;position:relative}
.srch-in{width:100%;height:30px;background:var(--bg3);border:0.5px solid var(--bdr);border-radius:7px;padding:0 10px 0 28px;font-size:12.5px;color:var(--t1);outline:none;font-family:inherit;transition:var(--tr)}
.srch-in:focus{border-color:var(--acc);background:var(--bg2)}
.srch-ic{position:absolute;left:8px;top:50%;transform:translateY(-50%);font-size:13px;color:var(--t3);pointer-events:none}
.srch-dd{position:absolute;top:34px;left:0;right:0;background:var(--bg2);border:0.5px solid var(--bdr2);border-radius:var(--r);z-index:200;overflow:hidden;box-shadow:var(--shadow-lg);display:none}
.srch-item{padding:8px 12px;font-size:12.5px;cursor:pointer;display:flex;align-items:center;gap:9px;border-bottom:0.5px solid var(--bdr)}
.srch-item:last-child{border-bottom:none}.srch-item:hover{background:var(--bg3)}

/* ── ZOOM NAV HINT ── */
#zoom-hint{position:fixed;bottom:24px;left:50%;transform:translateX(-50%);background:rgba(0,0,0,.6);color:#fff;font-size:12px;padding:8px 16px;border-radius:20px;z-index:900;pointer-events:none;transition:opacity .4s;backdrop-filter:blur(8px)}
#zoom-hint.hidden{opacity:0}

/* ── BACK BUTTON ── */
#back-btn{position:fixed;bottom:28px;right:28px;background:var(--bg2);border:0.5px solid var(--bdr2);border-radius:14px;padding:11px 18px;font-size:13.5px;font-weight:500;color:var(--t1);cursor:pointer;z-index:9999;display:none;align-items:center;gap:8px;box-shadow:0 4px 20px rgba(0,0,0,.15);transition:all .2s;font-family:'DM Sans',system-ui,sans-serif}
#back-btn:hover{background:var(--bg3);transform:translateY(-2px);box-shadow:0 6px 24px rgba(0,0,0,.2)}
#back-btn.show{display:flex!important}

/* ── LAYER 0: HOME GALAXY ── */
#layer-home{background:var(--bg)}
.galaxy-bg{position:absolute;inset:0;overflow:hidden}
.galaxy-bg::before{content:'';position:absolute;inset:-50%;background:radial-gradient(ellipse at 50% 50%,var(--acl) 0%,transparent 60%);opacity:.4}
.home-center{text-align:center;position:relative;z-index:2;padding:0 20px}
.home-title{font-family:'Fraunces',serif;font-size:clamp(32px,6vw,72px);color:var(--t1);margin-bottom:12px;line-height:1.1}
.home-title span{color:var(--acc);font-style:italic}
.home-sub{font-size:clamp(14px,2vw,18px);color:var(--t2);margin-bottom:48px;max-width:520px;line-height:1.7}
.home-modules{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;max-width:680px;margin:0 auto}
.module-orbit{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:16px;padding:20px;cursor:pointer;transition:all .25s;position:relative;overflow:hidden}
.module-orbit::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,transparent 60%,var(--acl) 100%);opacity:0;transition:opacity .25s}
.module-orbit:hover{transform:translateY(-4px) scale(1.02);box-shadow:var(--shadow-lg);border-color:var(--bdr2)}
.module-orbit:hover::before{opacity:1}
.mo-ico{font-size:28px;margin-bottom:10px}
.mo-name{font-size:14px;font-weight:500;color:var(--t1);margin-bottom:4px}
.mo-desc{font-size:11.5px;color:var(--t3);line-height:1.5}
.mo-arrow{position:absolute;bottom:12px;right:12px;width:22px;height:22px;background:var(--acl);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;color:var(--acc);opacity:0;transition:opacity .2s}
.module-orbit:hover .mo-arrow{opacity:1}
.scroll-hint{display:flex;flex-direction:column;align-items:center;gap:8px;margin-top:40px;color:var(--t3);font-size:12px;animation:bounce 2s infinite}
.scroll-hint-arrow{font-size:20px}
@keyframes bounce{0%,100%{transform:translateY(0)}50%{transform:translateY(6px)}}

/* ── LAYER 1: CONTENT PANEL ── */
#layer-content{background:var(--bg)}
.content-panel{width:100%;height:100%;overflow-y:auto;padding:72px 24px 80px;max-width:1100px;margin:0 auto}
.content-panel::-webkit-scrollbar{width:4px}
.content-panel::-webkit-scrollbar-thumb{background:var(--bdr2);border-radius:2px}

/* ── SHARED CONTENT STYLES ── */
.sec-hd{font-size:11px;font-weight:500;color:var(--t3);margin-bottom:10px;display:flex;align-items:center;gap:8px;letter-spacing:.06em;text-transform:uppercase}
.sec-hd::after{content:'';flex:1;height:0.5px;background:var(--bdr)}
.btn{display:inline-flex;align-items:center;gap:6px;padding:7px 14px;border-radius:7px;font-size:12.5px;cursor:pointer;font-family:inherit;transition:var(--tr);border:0.5px solid var(--bdr2);background:var(--bg2);color:var(--t1)}
.btn:hover{background:var(--bg3)}.btn.pri{background:var(--acc);border-color:var(--acc);color:#fff}.btn.pri:hover{opacity:.9}
.inp{width:100%;height:34px;background:var(--bg3);border:0.5px solid var(--bdr);border-radius:7px;padding:0 11px;font-size:12.5px;color:var(--t1);font-family:inherit;outline:none;transition:var(--tr)}
.inp:focus{border-color:var(--acc);background:var(--bg2)}
.warn-box{background:var(--rdl);border:0.5px solid #e0a0a0;border-radius:7px;padding:9px 11px;font-size:12px;color:var(--rd);display:flex;gap:7px;align-items:flex-start;margin-top:8px}
/* PSE */
.el-tooltip{position:fixed;background:var(--bg2);border:0.5px solid var(--bdr2);border-radius:8px;padding:9px 11px;font-size:12px;color:var(--t1);z-index:2000;pointer-events:none;box-shadow:var(--shadow-lg);max-width:190px;display:none}
.el-tooltip.show{display:block}
.pt-filter-row{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:8px}
.ptf{font-size:10.5px;padding:3px 8px;border-radius:10px;border:0.5px solid var(--bdr);background:var(--bg2);color:var(--t2);cursor:pointer;transition:var(--tr);white-space:nowrap}
.ptf:hover{background:var(--bg3)}.ptf.on{color:#fff;border-color:transparent}
.pt-legend{display:flex;gap:7px;flex-wrap:wrap;margin-bottom:8px}
.leg{display:flex;align-items:center;gap:4px;font-size:10px;color:var(--t2);cursor:pointer;padding:2px 5px;border-radius:5px}
.leg:hover{background:var(--bg3)}.leg-dot{width:8px;height:8px;border-radius:2px;flex-shrink:0}
.pt-scroll{overflow-x:auto;padding-bottom:8px}
.ptable{display:grid;grid-template-columns:repeat(18,1fr);gap:2px;min-width:560px}
.el{border-radius:4px;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:2px 1px;aspect-ratio:1;min-height:27px;transition:transform .1s,opacity .1s;border:0.5px solid transparent}
.el:hover{transform:scale(1.22);z-index:30;box-shadow:var(--shadow-lg)}.el.sel{box-shadow:0 0 0 2px var(--acc);z-index:15;transform:scale(1.05)}.el.dimmed{opacity:.18}
.el.gap{cursor:default;background:transparent!important;border-color:transparent!important}.el.gap:hover{transform:none;box-shadow:none}
.el-z{font-size:5.5px;align-self:flex-start;line-height:1;padding-left:1.5px;opacity:.7}
.el-s{font-size:10px;font-weight:600;line-height:1}
.el-n{font-size:4.5px;line-height:1;text-align:center;max-width:26px;overflow:hidden;white-space:nowrap;text-overflow:ellipsis;opacity:.6}
.pse-detail-wrap{display:grid;grid-template-columns:1fr 220px;gap:14px;margin-top:14px}
.pse-detail{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:var(--r);padding:14px}
.pse-quick{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:var(--r);padding:14px}
.pse-sym-row{display:flex;gap:12px;align-items:flex-start;margin-bottom:12px}
.pse-sym-box{width:60px;height:60px;border-radius:10px;display:flex;flex-direction:column;align-items:center;justify-content:center;flex-shrink:0}
.prop-grid{display:grid;grid-template-columns:1fr 1fr;gap:5px;margin-bottom:12px}
.prop{background:var(--bg3);border-radius:6px;padding:7px 9px}
.prop-l{font-size:9px;color:var(--t3);text-transform:uppercase;letter-spacing:.06em;margin-bottom:2px}
.prop-v{font-size:12px;font-weight:500;color:var(--t1)}
.dp-sec{font-size:9.5px;font-weight:500;color:var(--t3);letter-spacing:.07em;text-transform:uppercase;margin:10px 0 5px;display:flex;align-items:center;gap:5px}
.dp-sec::after{content:'';flex:1;height:0.5px;background:var(--bdr)}
.dp-desc{font-size:12px;color:var(--t2);line-height:1.7;margin-bottom:8px}
.dp-list{list-style:none;display:flex;flex-direction:column;gap:2px}
.dp-list li{font-size:11.5px;color:var(--t2);padding:3px 8px;background:var(--bg3);border-radius:5px;border-left:2px solid var(--acc);margin-bottom:2px}
.rxn-item{font-size:11px;color:var(--t2);padding:5px 8px;background:var(--bg3);border-radius:5px;border-left:2px solid var(--bl);font-family:monospace;margin-bottom:3px}
.key-box{background:var(--acl);border-radius:7px;padding:7px 10px;font-size:11.5px;color:var(--acc);border-left:2px solid var(--acc);margin-bottom:6px;font-style:italic}
.shell-wrap{display:flex;justify-content:center;padding:10px;background:var(--bg3);border-radius:8px;margin-bottom:10px}
/* Wiki */
.wiki-grid{display:grid;gap:8px}
.wiki-card{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:var(--r);padding:13px 15px;cursor:pointer;transition:var(--tr);display:flex;gap:11px;align-items:flex-start}
.wiki-card:hover{border-color:var(--bdr2);background:var(--bg3)}
.wiki-ico{width:34px;height:34px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;background:var(--bg3)}
.wiki-card h3{font-size:13px;font-weight:500;color:var(--t1);margin-bottom:3px}
.wiki-card p{font-size:12px;color:var(--t3);line-height:1.5}
.wiki-tags{display:flex;gap:4px;flex-wrap:wrap;margin-top:6px}
.wiki-tag{font-size:10px;padding:2px 7px;border-radius:7px;background:var(--bg3);color:var(--t2)}
.art h2{font-family:'Fraunces',serif;font-size:20px;color:var(--t1);margin-bottom:6px}
.art-meta{font-size:11.5px;color:var(--t3);margin-bottom:16px;display:flex;gap:10px}
.art h3{font-size:14px;font-weight:500;color:var(--t1);margin:16px 0 6px;padding-bottom:5px;border-bottom:0.5px solid var(--bdr)}
.art p{font-size:13px;color:var(--t2);line-height:1.78;margin-bottom:11px}
.art ul,.art ol{padding-left:18px;margin-bottom:11px}
.art li{font-size:13px;color:var(--t2);line-height:1.7;margin-bottom:3px}
.art code{background:var(--bg3);border:0.5px solid var(--bdr);border-radius:4px;padding:1px 5px;font-family:monospace;font-size:11.5px;color:var(--acc)}
.art blockquote{border-left:2px solid var(--acc);padding-left:12px;margin:12px 0;font-style:italic;color:var(--t3);font-size:13px}
.merksatz{background:var(--acl);border:0.5px solid var(--bdr2);border-radius:7px;padding:10px 13px;margin:12px 0;font-size:13px;color:var(--acc)}
.merksatz::before{content:'Merksatz: ';font-weight:500}
.formula-box{background:var(--bg3);border-radius:7px;padding:9px 13px;margin:9px 0;font-family:monospace;font-size:12.5px;color:var(--t1);border-left:2px solid var(--bl)}
/* Struc */
.struc-wrap{display:grid;grid-template-columns:180px 1fr 175px;gap:0;border:0.5px solid var(--bdr);border-radius:var(--rlg);overflow:hidden;background:var(--bg2)}
.struc-left,.struc-right{background:var(--bg3);display:flex;flex-direction:column;overflow:hidden}
.struc-right{border-left:0.5px solid var(--bdr)}.struc-left{border-right:0.5px solid var(--bdr)}
.struc-center{display:flex;flex-direction:column}
.struc-panel-hd{padding:9px 12px 5px;font-size:10px;font-weight:500;color:var(--t3);letter-spacing:.07em;text-transform:uppercase;border-bottom:0.5px solid var(--bdr)}
.struc-scroll{flex:1;overflow-y:auto;padding:4px}
.struc-scroll::-webkit-scrollbar{width:3px}.struc-scroll::-webkit-scrollbar-thumb{background:var(--bdr2);border-radius:2px}
.tool-grid{display:grid;grid-template-columns:1fr 1fr;gap:2px;padding:4px}
.tbtn{display:flex;align-items:center;gap:5px;padding:5px 7px;border-radius:5px;cursor:pointer;font-size:11px;color:var(--t2);transition:var(--tr);border:none;background:none;width:100%;text-align:left;font-family:inherit}
.tbtn:hover{background:var(--bg4);color:var(--t1)}.tbtn.on{background:var(--acl);color:var(--acc)}
.atom-pip{width:11px;height:11px;border-radius:50%;flex-shrink:0}
/* NEW STRUKTURZEICHNER */
.snew-wrap{display:grid;grid-template-columns:190px 1fr 195px;gap:0;border:0.5px solid var(--bdr);border-radius:14px;overflow:hidden;background:var(--bg2);min-height:520px}
.snew-left{background:var(--bg3);border-right:0.5px solid var(--bdr);display:flex;flex-direction:column;overflow:hidden}
.snew-center{display:flex;flex-direction:column;background:var(--bg2)}
.snew-right{background:var(--bg3);border-left:0.5px solid var(--bdr);display:flex;flex-direction:column;overflow:hidden}
.snew-sec-hd{font-size:9.5px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:var(--t3);padding:10px 12px 5px;border-bottom:0.5px solid var(--bdr)}
.snew-atoms{display:flex;flex-direction:column;gap:2px;padding:6px}
.snew-atom{display:flex;align-items:center;gap:8px;padding:6px 8px;border-radius:8px;border:0.5px solid transparent;background:var(--bg2);cursor:pointer;transition:all .15s;text-align:left;width:100%}
.snew-atom:hover{background:var(--bg4);border-color:var(--bdr2)}
.snew-atom.on{background:var(--acl);border-color:var(--acd)}
.sa-pip{width:10px;height:10px;border-radius:50%;flex-shrink:0}
.sa-sym{font-size:13px;font-weight:600;color:var(--t1);line-height:1}
.sa-name{font-size:9.5px;color:var(--t3);line-height:1;margin-top:1px}
.snew-bonds{display:flex;flex-direction:column;gap:2px;padding:0 6px 6px}
.snew-bond{padding:5px 10px;border-radius:7px;border:0.5px solid var(--bdr);background:var(--bg2);color:var(--t2);font-size:11.5px;cursor:pointer;text-align:left;transition:all .15s;font-family:monospace;width:100%}
.snew-bond:hover{background:var(--bg4)}.snew-bond.on{background:var(--acl);border-color:var(--acd);color:var(--acc)}
.snew-bond.danger{color:#e53935}.snew-bond.danger:hover{background:#ffeaea}
.snew-lib{flex:1;overflow-y:auto;padding:4px 6px}
.snew-lib::-webkit-scrollbar{width:3px}.snew-lib::-webkit-scrollbar-thumb{background:var(--bdr2);border-radius:2px}
.sl-cat{font-size:9px;font-weight:600;text-transform:uppercase;letter-spacing:.08em;color:var(--t4);padding:8px 4px 3px}
.sl-mol{display:flex;align-items:center;gap:7px;width:100%;padding:5px 6px;border-radius:7px;border:none;background:none;cursor:pointer;color:var(--t2);font-family:inherit;font-size:11.5px;text-align:left;transition:all .12s}
.sl-mol:hover{background:var(--bg4)}.sl-mol-ico{font-size:14px;flex-shrink:0}.sl-mol-name{line-height:1.3}.sl-mol-f{font-size:9.5px;color:var(--t3);font-family:monospace}
.snew-libadd{margin:6px;padding:7px;border-radius:8px;border:0.5px dashed var(--bdr2);background:none;color:var(--t3);font-size:11.5px;cursor:pointer;transition:all .15s;font-family:inherit;width:calc(100% - 12px)}
.snew-libadd:hover{background:var(--bg4);color:var(--t2)}
.snew-toolbar{display:flex;align-items:center;gap:4px;padding:7px 10px;border-bottom:0.5px solid var(--bdr);flex-wrap:wrap}
.snew-tbtn{width:30px;height:28px;border-radius:7px;border:0.5px solid var(--bdr);background:var(--bg3);color:var(--t2);font-size:13px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .12s;font-family:monospace}
.snew-tbtn:hover{background:var(--bg4)}.snew-tbtn.on{background:var(--acl);border-color:var(--acd);color:var(--acc)}.snew-tbtn.danger{color:#e53935}
.snew-mode-badge{margin-left:auto;font-size:10.5px;color:var(--t3);background:var(--bg3);border:0.5px solid var(--bdr);padding:3px 10px;border-radius:20px}
.snew-canvas-wrap{flex:1;position:relative;min-height:300px}
.mol-canvas{display:block;cursor:crosshair;width:100%;height:100%;min-height:280px}
.snew-tip{padding:6px 12px;font-size:11.5px;color:var(--t3);background:var(--bg3);border-top:0.5px solid var(--bdr);display:flex;align-items:center;gap:6px}
.snew-loadbar{display:flex;gap:6px;padding:8px 10px;border-top:0.5px solid var(--bdr)}
.snew-loadbar input{flex:1;height:32px;border:0.5px solid var(--bdr);border-radius:8px;padding:0 10px;font-size:12px;background:var(--bg3);color:var(--t1);font-family:monospace;outline:none}
.snew-loadbar input:focus{border-color:var(--acc)}
.snew-loadbar button{height:32px;padding:0 16px;border-radius:8px;font-size:12px;cursor:pointer;background:var(--acc);color:#fff;border:none;font-family:inherit;font-weight:500}
.snew-footer-chips{display:flex;gap:6px;padding:7px 10px;border-top:0.5px solid var(--bdr);flex-wrap:wrap}
.snew-chip{font-size:10px;color:var(--t3);padding:3px 8px;border-radius:6px;background:var(--bg3);border:0.5px solid var(--bdr)}
.snew-suggestions{padding:6px;display:flex;flex-direction:column;gap:4px;max-height:220px;overflow-y:auto}
.suggest-card{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:7px;padding:9px 10px;cursor:pointer;transition:var(--tr)}
.suggest-card:hover{border-color:var(--bdr2)}.suggest-card.hl{border-color:#c0ddd0;background:var(--acl)}
.sc-hd{display:flex;align-items:center;gap:6px;margin-bottom:3px}
.snew-molinfo{padding:8px 10px;font-size:12px;color:var(--t2);flex:1;overflow-y:auto}
.snew-info-row{display:flex;justify-content:space-between;padding:4px 0;border-bottom:0.5px solid var(--bdr);font-size:11.5px}
.snew-info-row:last-child{border-bottom:none}
.snew-info-lbl{color:var(--t3)}.snew-info-val{font-weight:500;font-family:monospace}
@media(max-width:640px){.snew-wrap{grid-template-columns:1fr!important;min-height:auto}.snew-right{display:none}.snew-left{max-height:200px}}
.mol-group-lbl{font-size:9px;color:var(--t3);text-transform:uppercase;letter-spacing:.06em;padding:7px 8px 2px}
.mol-btn{padding:5px 8px;border-radius:5px;cursor:pointer;font-size:11px;color:var(--t2);transition:var(--tr);border:none;background:none;text-align:left;width:100%;font-family:inherit;display:flex;flex-direction:column;gap:1px}
.mol-btn:hover{background:var(--bg4);color:var(--t1)}.mol-btn span{font-size:9.5px;color:var(--t3)}
.struc-topbar{display:flex;align-items:center;gap:5px;padding:7px 10px;border-bottom:0.5px solid var(--bdr);flex-wrap:wrap}
.act-btn{display:inline-flex;align-items:center;gap:4px;padding:4px 9px;border-radius:5px;font-size:11px;cursor:pointer;border:0.5px solid var(--bdr);background:var(--bg2);color:var(--t2);transition:var(--tr);font-family:inherit}
.act-btn:hover{background:var(--bg3)}.act-btn.on{background:var(--acl);color:var(--acc);border-color:var(--acd)}.act-btn.danger:hover{background:var(--rdl);color:var(--rd);border-color:var(--rd)}
.cvs-wrap{flex:1;position:relative;min-height:280px}
.mol-canvas{display:block;cursor:crosshair;width:100%;height:100%;min-height:280px}
.struc-fbar{display:flex;gap:6px;padding:7px 10px;border-top:0.5px solid var(--bdr)}
.struc-fbar input{flex:1;height:30px;border:0.5px solid var(--bdr);border-radius:6px;padding:0 9px;font-size:12px;background:var(--bg3);color:var(--t1);font-family:monospace;outline:none}
.struc-fbar input:focus{border-color:var(--acc)}
.struc-fbar button{height:30px;padding:0 12px;border-radius:6px;font-size:12px;cursor:pointer;background:var(--acc);color:#fff;border:none;font-family:inherit}
.fbar-info{padding:5px 10px;font-size:11px;color:var(--t2);border-top:0.5px solid var(--bdr);background:var(--bg3);min-height:28px}
.suggest-card{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:7px;padding:9px 10px;margin-bottom:5px;cursor:pointer;transition:var(--tr)}
.suggest-card:hover{border-color:var(--bdr2)}.suggest-card.hl{border-color:#c0ddd0;background:var(--acl)}
.sc-hd{display:flex;align-items:center;gap:6px;margin-bottom:3px}
.sc-ico{width:22px;height:22px;border-radius:4px;display:flex;align-items:center;justify-content:center;font-size:12px;flex-shrink:0}
.sc-title{font-size:12px;font-weight:500;color:var(--t1)}.sc-desc{font-size:11px;color:var(--t3);line-height:1.5}
.mol-info-row{display:flex;align-items:center;justify-content:space-between;padding:4px 0;border-bottom:0.5px solid var(--bdr)}
.mol-info-row:last-child{border-bottom:none}
.mol-info-l{font-size:10.5px;color:var(--t3)}.mol-info-v{font-size:11px;font-weight:500;color:var(--t1)}
/* Rxn */
.rxn-wrap{display:grid;grid-template-columns:1fr 1fr;gap:16px}
.rxn-right{overflow-y:auto;max-height:480px}
.rxn-right::-webkit-scrollbar{width:3px}.rxn-right::-webkit-scrollbar-thumb{background:var(--bdr2);border-radius:2px}
.rxn-in-row{display:flex;gap:7px;margin-bottom:7px}
.rxn-hint{font-size:11px;color:var(--t3);margin-bottom:10px}
.cat-tabs{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:7px}
.cat-tab{font-size:11px;padding:3px 9px;border-radius:10px;border:0.5px solid var(--bdr);background:var(--bg2);color:var(--t2);cursor:pointer;transition:var(--tr)}
.cat-tab:hover{background:var(--bg3)}.cat-tab.on{background:var(--acl);color:var(--acc);border-color:#c0ddd0}
.ex-grid{display:grid;gap:3px}
.ex-btn{padding:5px 8px;border-radius:6px;border:0.5px solid var(--bdr);background:var(--bg2);color:var(--t2);cursor:pointer;font-size:11px;font-family:monospace;text-align:left;transition:var(--tr);line-height:1.4}
.ex-btn:hover{background:var(--bg3);border-color:var(--bdr2)}
.rxn-result{background:var(--bg3);border-radius:var(--r);padding:14px}
.rxn-eq{font-size:17px;font-weight:500;color:var(--t1);margin-bottom:9px;line-height:1.4;font-family:'Fraunces',serif}
.rxn-tags{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:11px}
.tag{font-size:10px;padding:3px 8px;border-radius:8px;font-weight:500}
.tag-g{background:var(--acl);color:var(--acc)}.tag-b{background:var(--bll);color:var(--bl)}.tag-a{background:var(--aml);color:var(--am)}
.step{padding:5px 9px;background:var(--bg2);border-radius:5px;margin-bottom:4px;border-left:2px solid var(--acd);font-size:12px;color:var(--t2);line-height:1.6}
.step-n{color:var(--acc);font-weight:500;margin-right:5px}
.ox-box{background:var(--bll);border-radius:7px;padding:9px 11px;margin-top:9px}
.ox-title{font-size:9.5px;font-weight:500;color:var(--bl);text-transform:uppercase;letter-spacing:.06em;margin-bottom:5px}
.ox-row{display:flex;align-items:center;gap:6px;margin-bottom:3px;font-size:11.5px;color:var(--bl);flex-wrap:wrap}
.ox-el{font-weight:500}.ox-chg{font-size:10px;padding:1px 6px;border-radius:5px;font-weight:500}
.ox-ox{background:var(--rdl);color:var(--rd)}.ox-rd{background:var(--acl);color:var(--acc)}.ox-neu{background:var(--bg4);color:var(--t2)}
.dh-box{background:var(--aml);border-radius:7px;padding:7px 10px;margin-top:7px;font-size:12px;color:var(--am)}
.rxn-empty{display:flex;flex-direction:column;align-items:center;gap:8px;padding:28px 14px;text-align:center}
.rxn-empty i{font-size:30px;color:var(--t4)}.rxn-empty p{font-size:12px;color:var(--t3);line-height:1.6}
/* Quiz */
.quiz-wrap{max-width:620px;margin:0 auto}
.quiz-header{text-align:center;margin-bottom:24px}
.quiz-header h2{font-family:'Fraunces',serif;font-size:22px;color:var(--t1);margin-bottom:5px}
.quiz-header p{font-size:13px;color:var(--t3)}
.quiz-mode-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:20px}
.quiz-mode{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:var(--r);padding:16px;cursor:pointer;transition:var(--tr);text-align:center}
.quiz-mode:hover{border-color:var(--bdr2);transform:translateY(-1px);box-shadow:var(--shadow)}
.qm-ico{font-size:26px;margin-bottom:8px}
.quiz-mode h3{font-size:13px;font-weight:500;color:var(--t1);margin-bottom:3px}
.quiz-mode p{font-size:11.5px;color:var(--t3)}
.quiz-progress{background:var(--bg3);border-radius:20px;height:6px;margin-bottom:20px;overflow:hidden}
.quiz-progress-bar{height:100%;background:var(--acc);border-radius:20px;transition:width .4s ease}
.quiz-card{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:var(--rlg);padding:22px 24px;margin-bottom:14px}
.quiz-q-num{font-size:11px;color:var(--t3);margin-bottom:8px;text-transform:uppercase;letter-spacing:.06em}
.quiz-q{font-family:'Fraunces',serif;font-size:18px;color:var(--t1);margin-bottom:18px;line-height:1.4}
.quiz-element-hint{display:inline-flex;flex-direction:column;align-items:center;justify-content:center;width:70px;height:70px;border-radius:10px;margin-bottom:14px;font-family:'Fraunces',serif}
.quiz-el-z{font-size:10px;opacity:.7}.quiz-el-s{font-size:30px;line-height:1}.quiz-el-m{font-size:8px;opacity:.6}
.quiz-answers{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.qa{padding:11px 14px;border-radius:8px;border:0.5px solid var(--bdr);background:var(--bg3);cursor:pointer;font-size:13px;color:var(--t1);transition:var(--tr);text-align:left;font-family:inherit;width:100%}
.qa:hover:not(:disabled){background:var(--bg4);border-color:var(--bdr2)}
.qa.correct{background:var(--acl);border-color:var(--acd);color:var(--acc);font-weight:500}
.qa.wrong{background:var(--rdl);border-color:#e0a0a0;color:var(--rd)}.qa:disabled{cursor:default}
.quiz-feedback{margin-top:12px;padding:10px 13px;border-radius:8px;font-size:13px;display:none}
.quiz-feedback.show{display:block}.quiz-feedback.correct{background:var(--acl);color:var(--acc)}.quiz-feedback.wrong{background:var(--rdl);color:var(--rd)}
.quiz-nav{display:flex;align-items:center;justify-content:space-between;margin-top:10px}
.quiz-score-label{font-size:12px;color:var(--t3)}
.quiz-result{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:var(--rlg);padding:28px;text-align:center}
.quiz-result h2{font-family:'Fraunces',serif;font-size:24px;color:var(--t1);margin-bottom:6px}
.quiz-result p{font-size:14px;color:var(--t2);margin-bottom:18px}
.quiz-score-big{font-family:'Fraunces',serif;font-size:52px;color:var(--acc);margin:14px 0}
.quiz-stars{font-size:28px;margin-bottom:12px}
/* Learn */
.learn-h1{font-family:'Fraunces',serif;font-size:20px;color:var(--t1);margin-bottom:4px}
.learn-sub{font-size:12.5px;color:var(--t3);margin-bottom:18px}
.learn-card{background:var(--bg2);border:0.5px solid var(--bdr);border-radius:var(--r);padding:14px 16px;margin-bottom:10px}
.learn-card h3{font-family:'Fraunces',serif;font-size:15px;color:var(--t1);margin-bottom:6px}
.learn-card p{font-size:12.5px;color:var(--t2);line-height:1.75}
.learn-card ul{padding-left:16px;margin-top:6px}
.learn-card li{font-size:12.5px;color:var(--t2);line-height:1.7;margin-bottom:3px}
.type-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px;margin-top:8px}
.type-box{background:var(--bg3);border-radius:8px;padding:9px 10px;text-align:center}
.ticon{font-size:20px;margin-bottom:4px}
.type-box h4{font-size:12px;font-weight:500;color:var(--t1);margin-bottom:2px}
.type-box p{font-size:10.5px;color:var(--t3);line-height:1.5}
.gt{width:100%;border-collapse:collapse;margin-top:8px}
.gt th{font-size:10px;font-weight:500;color:var(--t3);text-transform:uppercase;letter-spacing:.06em;padding:5px 7px;text-align:left;border-bottom:0.5px solid var(--bdr)}
.gt td{font-size:11.5px;color:var(--t2);padding:5px 7px;border-bottom:0.5px solid var(--bdr)}
.gt tr:last-child td{border-bottom:none}.gt tr:hover td{background:var(--bg3)}
/* Page header */
.page-hdr{margin-bottom:24px}
.page-hdr h1{font-family:'Fraunces',serif;font-size:clamp(22px,4vw,34px);color:var(--t1);margin-bottom:6px}
.page-hdr p{font-size:13.5px;color:var(--t2);line-height:1.6}


@keyframes slideInRight {
  from { transform: translateX(60px); opacity: 0; }
  to   { transform: translateX(0);    opacity: 1; }
}
#back-btn.show { animation: slideInRight 0.35s cubic-bezier(.4,0,.2,1) both; }

#scroll-progress {
  position: fixed;
  left: 20px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 8px;
  z-index: 800;
  transition: opacity .3s;
}
#scroll-progress.hidden { opacity: 0; pointer-events: none; }
.sp-dot {
  width: 8px; height: 8px; border-radius: 50%;
  background: var(--bdr2);
  cursor: pointer;
  transition: all .2s;
  border: 1.5px solid transparent;
}
.sp-dot.active {
  background: var(--acc);
  transform: scale(1.4);
  border-color: var(--acd);
}
.sp-dot:hover { background: var(--acd); transform: scale(1.3); }


/* NAV DOTS */
#scroll-progress{position:fixed;left:20px;top:50%;transform:translateY(-50%);display:flex;flex-direction:column;gap:10px;z-index:800;transition:opacity .4s}
#scroll-progress.on-home{opacity:.35}
#scroll-progress.on-module{opacity:1}
.sp-dot{position:relative;width:8px;height:8px;border-radius:50%;background:var(--bdr2);cursor:pointer;transition:all .25s cubic-bezier(.4,0,.2,1);border:1.5px solid transparent;flex-shrink:0}
.sp-dot.active{background:var(--acc);transform:scale(1.5);border-color:var(--acd);box-shadow:0 0 0 3px var(--acl)}
.sp-dot:hover{background:var(--acd);transform:scale(1.35)}
.sp-dot::after{content:attr(title);position:absolute;left:18px;top:50%;transform:translateY(-50%) translateX(-4px);background:var(--t1);color:var(--bg);font-size:10.5px;white-space:nowrap;padding:3px 8px;border-radius:5px;opacity:0;pointer-events:none;transition:opacity .15s,transform .15s}
.sp-dot:hover::after{opacity:1;transform:translateY(-50%) translateX(0)}

/* FLOATING MOLECULES */
#mol-bg{position:fixed;inset:0;pointer-events:none;z-index:0;overflow:hidden}
.mol-float{position:absolute;opacity:0;animation:molFloat linear infinite;will-change:transform,opacity}
@keyframes molFloat{0%{transform:translateY(100vh) rotate(0deg);opacity:0}8%{opacity:.1}92%{opacity:.1}100%{transform:translateY(-120px) rotate(360deg);opacity:0}}

/* XP WIDGET */
#xp-widget{display:flex;align-items:center;gap:8px;padding:4px 10px;background:var(--bg3);border:0.5px solid var(--bdr2);border-radius:10px;cursor:pointer;transition:var(--tr)}
#xp-widget:hover{background:var(--bg4)}
.xp-icon{font-size:14px}
.xp-info{display:flex;flex-direction:column;gap:2px}
.xp-label{font-size:10.5px;font-weight:500;color:var(--t1);white-space:nowrap}
.xp-bar-wrap{width:70px;height:4px;background:var(--bdr);border-radius:2px;overflow:hidden}
.xp-bar{height:100%;background:var(--acc);border-radius:2px;transition:width .6s}
.xp-sub{font-size:9.5px;color:var(--t3);white-space:nowrap}
#xp-popup{position:fixed;top:60px;right:16px;width:270px;background:var(--bg2);border:0.5px solid var(--bdr2);border-radius:var(--rlg);box-shadow:var(--shadow-lg);z-index:2000;padding:16px;display:none}
#xp-popup.show{display:block}
.xp-pop-header{display:flex;align-items:center;gap:10px;margin-bottom:12px}
.xp-pop-avatar{width:40px;height:40px;border-radius:10px;background:var(--acl);border:2px solid var(--acc);display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}
.xp-pop-name{font-size:14px;font-weight:500;color:var(--t1)}
.xp-pop-level{font-size:11px;color:var(--acc);font-weight:500}
.xp-pop-bar-wrap{height:7px;background:var(--bg3);border-radius:4px;overflow:hidden;margin-bottom:4px}
.xp-pop-bar{height:100%;background:var(--acc);border-radius:4px;transition:width .8s}
.xp-pop-xplabel{font-size:11px;color:var(--t3);margin-bottom:12px}
.badges-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:6px}
.badge{background:var(--bg3);border:0.5px solid var(--bdr);border-radius:8px;padding:7px 5px;text-align:center}
.badge.earned{background:var(--acl);border-color:var(--acd)}
.badge-ico{font-size:16px;margin-bottom:2px}
.badge-lbl{font-size:9px;color:var(--t2);line-height:1.3}
.badge.earned .badge-lbl{color:var(--acc);font-weight:500}
.badge.locked{opacity:.35;filter:grayscale(1)}
#xp-toast{position:fixed;bottom:80px;right:24px;background:var(--acc);color:#fff;border-radius:10px;padding:9px 15px;font-size:13px;font-weight:500;z-index:3000;display:none;align-items:center;gap:8px}
#xp-toast.show{display:flex}

/* FACT CARD */
.fact-card{background:var(--acl);border:0.5px solid var(--acd);border-radius:var(--rlg);padding:16px 18px;margin-bottom:18px}
.fact-badge{display:inline-flex;align-items:center;gap:5px;background:var(--acc);color:#fff;font-size:10px;font-weight:600;padding:3px 9px;border-radius:8px;margin-bottom:8px;text-transform:uppercase;letter-spacing:.04em}
.fact-text{font-family:'Fraunces',serif;font-size:14.5px;color:var(--t1);line-height:1.65;font-style:italic}
.fact-source{font-size:10.5px;color:var(--t3);margin-top:7px}
.fact-nav{display:flex;gap:5px;margin-top:10px}
.fact-dot{width:6px;height:6px;border-radius:50%;background:var(--bdr2);cursor:pointer;transition:background .2s}
.fact-dot.on{background:var(--acc)}

/* FOOTER */
.site-footer{background:var(--bg2);border-top:0.5px solid var(--bdr);padding:24px 28px 20px;margin-top:28px}
.footer-inner{max-width:1100px;margin:0 auto;display:grid;grid-template-columns:1.2fr 1fr 1fr;gap:20px;align-items:start}
.footer-brand{font-family:'Fraunces',serif;font-size:17px;color:var(--t1);margin-bottom:5px;display:flex;align-items:center;gap:7px}
.footer-brand-ico{width:24px;height:24px;background:var(--acc);border-radius:5px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:11px;font-style:italic}
.footer-sub{font-size:11.5px;color:var(--t3);line-height:1.6}
.footer-col h4{font-size:10.5px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.07em;margin-bottom:9px}
.footer-link{display:block;font-size:12px;color:var(--t3);text-decoration:none;margin-bottom:5px;cursor:pointer;transition:color .15s;background:none;border:none;font-family:inherit;text-align:left;padding:0}
.footer-link:hover{color:var(--acc)}
.footer-bottom{max-width:1100px;margin:14px auto 0;padding-top:12px;border-top:0.5px solid var(--bdr);display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px}
.footer-copy{font-size:11px;color:var(--t4)}
.footer-chips{display:flex;gap:5px}
.footer-chip{font-size:10px;padding:2px 7px;border-radius:6px;background:var(--bg3);color:var(--t3);border:0.5px solid var(--bdr)}

/* ENHANCED HOVER */
.module-orbit:hover{transform:translateY(-5px) scale(1.025)!important;box-shadow:0 14px 36px rgba(26,92,58,.13)!important;border-color:var(--acd)!important}
.el:hover{box-shadow:0 0 0 2px var(--acc),0 6px 16px rgba(26,92,58,.2)!important}
@keyframes slideInRight{from{transform:translateX(60px);opacity:0}to{transform:translateX(0);opacity:1}}
#back-btn.show{animation:slideInRight .35s cubic-bezier(.4,0,.2,1) both}

/* MOBILE */
@media(max-width:640px){
  .home-modules{grid-template-columns:1fr 1fr!important}
  .content-panel{padding:64px 14px 80px!important}
  .pse-detail-wrap{grid-template-columns:1fr!important}
  .rxn-wrap{grid-template-columns:1fr!important}
  .quiz-answers{grid-template-columns:1fr!important}
  .quiz-mode-grid{grid-template-columns:1fr 1fr!important}
  .footer-inner{grid-template-columns:1fr!important}
  .footer-bottom{flex-direction:column;align-items:flex-start}
  #xp-widget .xp-bar-wrap{display:none}
}
@media(max-width:400px){.home-modules{grid-template-columns:1fr!important}}

</style>
</head>
<body>


<div id="universe">
  <div id="zoom-world">
    <!-- LAYER 0: HOME -->
    <div class="layer active" id="layer-home">
      <div class="galaxy-bg"></div>
      <div class="home-center">
        <div style="font-family:'Fraunces',serif;font-size:clamp(38px,7vw,80px);color:var(--t1);line-height:1.05;margin-bottom:14px">
          Chem<span style="color:var(--acc);font-style:italic">Lab</span>
        </div>
        <div style="font-size:clamp(14px,2vw,18px);color:var(--t2);margin-bottom:44px;max-width:500px;line-height:1.7">
          Deine interaktive Chemie-Lernplattform —<br>Periodensystem, Wiki, Tools und mehr.
        </div>
        <div class="home-modules">
          <div class="module-orbit" onclick="zoomTo('pse')">
            <div class="mo-ico">🔬</div>
            <div class="mo-name">Periodensystem</div>
            <div class="mo-desc">118 Elemente interaktiv erkunden</div>
            <div class="mo-arrow">→</div>
          </div>
          <div class="module-orbit" onclick="zoomTo('wiki')">
            <div class="mo-ico">📚</div>
            <div class="mo-name">Chemie-Wiki</div>
            <div class="mo-desc">5 ausführliche Artikel</div>
            <div class="mo-arrow">→</div>
          </div>
          <div class="module-orbit" onclick="zoomTo('learn')">
            <div class="mo-ico">🎓</div>
            <div class="mo-name">Lernbereich</div>
            <div class="mo-desc">PSE-Grundlagen einfach erklärt</div>
            <div class="mo-arrow">→</div>
          </div>
          <div class="module-orbit" onclick="zoomTo('struc')">
            <div class="mo-ico">✏️</div>
            <div class="mo-name">Strukturzeichner</div>
            <div class="mo-desc">Moleküle zeichnen & erkunden</div>
            <div class="mo-arrow">→</div>
          </div>
          <div class="module-orbit" onclick="zoomTo('rxn')">
            <div class="mo-ico">⚖️</div>
            <div class="mo-name">Reaktionsrechner</div>
            <div class="mo-desc">23 Gleichungen ausgleichen</div>
            <div class="mo-arrow">→</div>
          </div>
          <div class="module-orbit" onclick="zoomTo('quiz')">
            <div class="mo-ico">🧠</div>
            <div class="mo-name">Quiz</div>
            <div class="mo-desc">Wissen testen in 3 Kategorien</div>
            <div class="mo-arrow">→</div>
          </div>
          <div class="module-orbit" onclick="zoomTo('info')">
            <div class="mo-ico">ℹ️</div>
            <div class="mo-name">Info & Impressum</div>
            <div class="mo-desc">Kontakt, Impressum, Über ChemLab</div>
            <div class="mo-arrow">→</div>
          </div>
        </div>
        <div class="scroll-hint">
          <div class="scroll-hint-arrow">↓</div>
          <div>Scrollen oder Kachel anklicken zum Einzoomen</div>
        </div>
      </div>
    </div>
    <!-- LAYER 1: CONTENT -->
    <div class="layer" id="layer-content">
      <div class="content-panel" id="content-panel"></div>
    </div>
  </div>
</div>

<!-- HUD -->
<div id="hud">
  <div class="hud-logo" onclick="zoomHome()" title="Zurück zur Startseite" style="text-decoration:none">
    <div class="hud-logo-ico">C</div>
    <span>Chem<span>Lab</span></span>
  </div>
  <div id="hud-back" style="display:none;align-items:center;gap:6px;padding:5px 12px;background:var(--bg3);border:0.5px solid var(--bdr2);border-radius:8px;cursor:pointer;font-size:12.5px;color:var(--t2);margin-left:4px;transition:all .15s" onclick="zoomHome()" onmouseover="this.style.background='var(--bg4)'" onmouseout="this.style.background='var(--bg3)'">
    🏠 Startseite
  </div>
  <div class="hud-breadcrumb" id="breadcrumb" style="display:none">
    <span class="sep">›</span>
    <span class="crumb active" id="crumb-current"></span>
  </div>
  <div class="srch-wrap" style="margin-left:16px">
    <span class="srch-ic">🔍</span>
    <input class="srch-in" id="srch" placeholder="Suchen… (Elemente, Module, Stoffe)" oninput="doSearch(this.value)" onblur="setTimeout(hideDd,180)" onfocus="doSearch(this.value)" autocomplete="off">
    <div class="srch-dd" id="srch-dd"></div>
  </div>
  <div class="hud-right">
    <div id="xp-widget" onclick="toggleXpPopup()" title="Dein Fortschritt">
      <div class="xp-icon">&#x1F9EA;</div>
      <div class="xp-info">
        <div class="xp-label" id="xp-level-label">Lv.1 Novize</div>
        <div class="xp-bar-wrap"><div class="xp-bar" id="xp-bar" style="width:0%"></div></div>
        <div class="xp-sub" id="xp-sub-label">0 / 100 XP</div>
      </div>
    </div>
    <div class="hud-btn" onclick="toggleDark()" title="Dunkelmodus" id="dk-btn" style="font-size:16px">🌙</div>
  </div>
</div>

<!-- BACK BUTTON -->
<button id="back-btn" onclick="zoomHome()" aria-label="Zurück zur Startseite">
  🏠 Zurück
</button>

<!-- ZOOM HINT -->
<div id="zoom-hint">↓ Scrollen zum Einzoomen · Klick auf Kachel zum Öffnen</div>


<!-- SCROLL PROGRESS DOTS -->
<div id="mol-bg"></div>
<div id="xp-popup">
  <div class="xp-pop-header">
    <div class="xp-pop-avatar">&#x1F9EA;</div>
    <div>
      <div class="xp-pop-name">ChemLab</div>
      <div class="xp-pop-level" id="xp-pop-level">Level 1 - Novize</div>
    </div>
  </div>
  <div class="xp-pop-bar-wrap"><div class="xp-pop-bar" id="xp-pop-bar" style="width:0%"></div></div>
  <div class="xp-pop-xplabel" id="xp-pop-label">0 / 100 XP</div>
  <div class="sec-hd" style="margin-bottom:8px">Abzeichen</div>
  <div class="badges-grid" id="badges-grid"></div>
</div>
<div id="xp-toast">&#11088; <span id="xp-toast-msg"></span></div>
<div id="scroll-progress" class="on-home">
  <div class="sp-dot" onclick="zoomTo('pse')"    title="Periodensystem"></div>
  <div class="sp-dot" onclick="zoomTo('wiki')"   title="Chemie-Wiki"></div>
  <div class="sp-dot" onclick="zoomTo('learn')"  title="Lernbereich"></div>
  <div class="sp-dot" onclick="zoomTo('struc')"  title="Strukturzeichner"></div>
  <div class="sp-dot" onclick="zoomTo('rxn')"    title="Reaktionsrechner"></div>
  <div class="sp-dot" onclick="zoomTo('quiz')"   title="Quiz"></div>
  <div class="sp-dot" onclick="zoomTo('info')"   title="Info & Impressum"></div>
</div>

<!-- TOOLTIP -->
<div class="el-tooltip" id="tooltip"></div>

<script>


const CATS={alkali:{l:'Alkalimetalle',bg:'#EF5350'},alkaline:{l:'Erdalkalimetalle',bg:'#FFA726'},trans:{l:'Übergangsmetalle',bg:'#42A5F5'},post:{l:'Metalle',bg:'#66BB6A'},met:{l:'Halbmetalle',bg:'#AB47BC'},non:{l:'Nichtmetalle',bg:'#26C6DA'},hal:{l:'Halogene',bg:'#FFA726'},noble:{l:'Edelgase',bg:'#EC407A'},lan:{l:'Lanthanide',bg:'#7E57C2'},act:{l:'Actinide',bg:'#26A69A'}};
const catCol=c=>CATS[c]?.bg||'#888';
const catBg=c=>catCol(c)+'40';
const catBdr=c=>catCol(c)+'99';

const EL_DETAIL={
1:{cfg:'1s¹',shells:[1],rxn:['H₂+½O₂→H₂O','N₂+3H₂⇌2NH₃','H₂+Cl₂→2HCl'],cpd:['H₂O','HCl','H₂SO₄','NH₃'],uses:'Raketentreibstoff, Brennstoffzellen, Ammoniaksynthese, Hydrierung',desc:'Leichtestes und häufigstes Element im Universum (~75 % der Baryonenmasse). Jede Sonne ist hauptsächlich Wasserstoff.',key:'Isotope: ¹H Protium (Stabil), ²H Deuterium (Stabil), ³H Tritium (β⁻-Strahler, HWZ 12,3 a).',history:'Erstmals 1766 von Henry Cavendish als „brennbare Luft" isoliert. Antoine Lavoisier erkannte 1783, dass es bei Verbrennung mit Sauerstoff Wasser ergibt, und nannte es Hydrogen (griech. „Wassererzeuger").',warn:null},
2:{cfg:'1s²',shells:[2],rxn:[],cpd:[],uses:'MRT-Kühlung (Supraleiter), Luftballons, Tauchergas (Heliox), Schutzgas',desc:'Edelgas, geht keine Verbindungen ein. Niedrigster Siedepunkt aller Elemente (−268,9 °C).',key:'Einziges Element ohne Festphase bei Normaldruck — bleibt selbst am absoluten Nullpunkt flüssig.',history:'1868 im Spektrum der Sonne entdeckt (Pierre Janssen, Norman Lockyer) — 27 Jahre bevor es auf der Erde isoliert wurde (William Ramsay, 1895). Benannt nach Helios, dem griechischen Sonnengott.',warn:null},
3:{cfg:'[He] 2s¹',shells:[2,1],rxn:['2Li+2H₂O→2LiOH+H₂','2Li+O₂→Li₂O'],cpd:['LiOH','Li₂CO₃','LiCl','Li₃PO₄'],uses:'Li-Ionen-Akkus, Medikamente gegen Bipolarstörung, Glas, Legierungen',desc:'Leichtestes Metall der Erde (ρ=0,53 g/cm³). Schwimmt auf Wasser und reagiert damit.',key:'Li-Ionen-Akkus ermöglichen Smartphones, Laptops und Elektroautos.',history:'1817 von Johan August Arfwedson in Stockholm aus dem Mineral Petalit isoliert. Humphry Davy bestätigte es als Metall. Name: griech. lithos = Stein, da als erstes Alkalimetall aus Gestein gewonnen.',warn:'Unter Mineralöl lagern! Reagiert mit Wasser und Luft.'},
4:{cfg:'[He] 2s²',shells:[2,2],rxn:['2Be+O₂→2BeO','Be+2HCl→BeCl₂+H₂'],cpd:['BeO','BeCl₂','Be(OH)₂'],uses:'Raumfahrt (Legierungen), Kernreaktoren, Röntgenfenster, Werkzeugstahl',desc:'Leichtestes Erdalkalimetall. Berylliumoxid hat eine höhere Wärmeleitfähigkeit als die meisten Metalle.',key:'Be-Cu-Legierungen sind federhart, nicht magnetisch und schlagen keinen Funken — ideal für Werkzeuge in explosionsgefährdeten Bereichen.',history:'1798 von Louis-Nicolas Vauquelin in Beryll und Smaragd entdeckt. Isoliert 1828 gleichzeitig von Friedrich Wöhler und Antoine Bussy. Name: Beryllium vom Mineral Beryll.',warn:'Hochgiftig und kanzerogen! Berylliumstaub verursacht Berylliose.'},
5:{cfg:'[He] 2s² 2p¹',shells:[2,3],rxn:['4B+3O₂→2B₂O₃','B₂H₆+3O₂→B₂O₃+3H₂O'],cpd:['H₃BO₃','B₂O₃','NaBH₄','BF₃'],uses:'Borsilikatglas (Pyrex), Halbleiter, Düngung, Neutronenabsorber in AKW',desc:'Halbmetall, Halbleiter. Bornitrid (BN) ist in kubischer Form so hart wie Diamant.',key:'Borax (Na₂B₄O₇) war eines der ersten industriell genutzten Reinigungsmittel.',history:'1808 gleichzeitig von Humphry Davy in London und Joseph Gay-Lussac & Louis Thénard in Paris isoliert. Name: arabisch bauraq = Borax.',warn:null},
6:{cfg:'[He] 2s² 2p²',shells:[2,4],rxn:['C+O₂→CO₂','2C+O₂→2CO','C+2H₂→CH₄'],cpd:['CO₂','CH₄','C₆H₁₂O₆','CaCO₃','C₆₀'],uses:'Basis aller organischen Verbindungen, Stahl (Kohlenstoffstahl), Diamant, Graphit, Aktivkohle',desc:'Grundlage des Lebens auf der Erde. Über 10 Millionen organische Verbindungen bekannt.',key:'¹⁴C-Datierung (Radiokohlenstoff): HWZ 5730 a. Ermöglicht Altersbestimmung bis ~50.000 Jahre.',history:'Kohlenstoff als Ruß und Holzkohle seit der Frühzeit bekannt. Als Element erkannt durch Lavoisier (1789). Diamant als Kohlenstoff identifiziert 1796 durch Smithson Tennant.',warn:null},
7:{cfg:'[He] 2s² 2p³',shells:[2,5],rxn:['N₂+3H₂⇌2NH₃','4NH₃+5O₂→4NO+6H₂O','N₂+O₂→2NO (Blitz)'],cpd:['NH₃','HNO₃','NO₂','N₂O','KNO₃'],uses:'Düngemittel (via NH₃), flüssiger N₂ (Kryotechnik), Sprengstoff (TNT, Nitroglycerol), Elektronik',desc:'78 % der Erdatmosphäre. N≡N-Dreifachbindung (945 kJ/mol) extrem stabil.',key:'Stickstoff-Fixierung: Haber-Bosch (industriell) und Nitrogenase-Enzyme (biologisch in Leguminosen).',history:'1772 von Daniel Rutherford als „dephlogistierte Luft" entdeckt. Zeitgleich von Scheele, Cavendish und Priestley untersucht. Name: griech. nitron (Salpeter) + genes (erzeugen).',warn:'Flüssiger N₂ (−196 °C): Kälteverbrennungen! Kann Sauerstoff verdrängen — Erstickungsgefahr.'},
8:{cfg:'[He] 2s² 2p⁴',shells:[2,6],rxn:['2H₂+O₂→2H₂O','4Fe+3O₂→2Fe₂O₃','S+O₂→SO₂'],cpd:['H₂O','O₃','SiO₂','Fe₂O₃','CO₂'],uses:'Atmung, Verbrennung, Stahlerzeugung, Medizin, Raketen (LOX)',desc:'21 % der Erdatmosphäre (als O₂). Elektronegativität EN=3,44 — dritthöchste aller Elemente.',key:'Ozon (O₃) in der Stratosphäre (20–40 km) absorbiert 97–99 % der UV-B/C-Strahlung.',history:'1774 von Carl Wilhelm Scheele entdeckt (unveröffentlicht) und gleichzeitig von Joseph Priestley (publiziert). Lavoisier nannte es Oxygenium (griech. „Säureerzeuger") — fälschlicherweise glaubend, es sei in allen Säuren.',warn:null},
9:{cfg:'[He] 2s² 2p⁵',shells:[2,7],rxn:['F₂+H₂→2HF','2F₂+2H₂O→O₂+4HF'],cpd:['HF','CaF₂','NaF','PTFE (Teflon)','SF₆','UF₆'],uses:'Teflon, Zahnpasta (Kariesschutz), Urananreicherung (UF₆), Kältemittel',desc:'Reaktivstes aller Elemente. Höchste EN aller Elemente (3,98). Greift fast alle Stoffe an.',key:'C–F-Bindung (485 kJ/mol) ist eine der stärksten Einfachbindungen — macht Teflon chemisch inert.',history:'Flussspat (CaF₂) seit dem 16. Jh. bekannt. Elementares Fluor erst 1886 von Henri Moissan isoliert — viele Chemiker hatten es vorher versucht und sich dabei vergiftet. Nobelpreis für Moissan 1906.',warn:'Extrem ätzend! HF greift Glas und Knochen an. F₂ reagiert mit fast allem — auch mit Wasser.'},
10:{cfg:'[He] 2s² 2p⁶',shells:[2,8],rxn:[],cpd:[],uses:'Leuchtstoffröhren (orange-rotes Licht), Laser, Tauchergas (Neonox)',desc:'Edelgas. Im Universum dritthäufigstes Element (nach H und He). Auf der Erde sehr selten.',key:'Neonröhren leuchten orange-rot — andere Farben kommen von Argon, Quecksilber oder Phosphor.',history:'1898 von William Ramsay und Morris Travers durch fraktionierte Destillation von flüssiger Luft entdeckt. Name: griech. neos = neu.',warn:null},
11:{cfg:'[Ne] 3s¹',shells:[2,8,1],rxn:['2Na+2H₂O→2NaOH+H₂','4Na+O₂→2Na₂O'],cpd:['NaCl','NaOH','Na₂CO₃','NaHCO₃','Na₂SO₄'],uses:'Kochsalz (NaCl), Seifenherstellung (NaOH), Natriumdampflampen, Legierungen',desc:'Weiches Alkalimetall (ritzt sich mit Fingernagel). Reagiert heftig mit Wasser und Luft.',key:'Na⁺/K⁺-Pumpe in Nervenzellen erzeugt elektrische Potenziale — essenziell für Nervenimpulse.',history:'1807 von Humphry Davy durch Elektrolyse von geschmolzenem Natriumhydroxid isoliert. Name: arabisch natrun (Soda/Natriumkarbonat).',warn:'Unter Mineralöl lagern. Reagiert mit Wasser: 2Na + 2H₂O → 2NaOH + H₂↑ (brennbar!).'},
12:{cfg:'[Ne] 3s²',shells:[2,8,2],rxn:['2Mg+O₂→2MgO','Mg+2HCl→MgCl₂+H₂','Mg+CO₂→MgO+C'],cpd:['MgO','MgCl₂','Mg(OH)₂','MgSO₄'],uses:'Leichtlegierungen (Flugzeug, Kfz), Feuerwerkskörper (weißes Licht), Chlorophyll, Antazida',desc:'Zentralatom im Chlorophyll — ohne Mg keine Photosynthese, kein pflanzliches Leben.',key:'Mg-Legierungen sind 33 % leichter als Aluminium und werden in Smartphones und Laptops eingesetzt.',history:'1755 von Joseph Black als eigenständiges Element erkannt (vorher als Kalk verwechselt). 1808 von Humphry Davy durch Elektrolyse isoliert. Name: Magnesia, Stadt in Griechenland.',warn:'Brennendes Mg NICHT mit Wasser löschen! Mg + H₂O → MgO + H₂ (Knallgasgefahr!). Auch CO₂ wird von Mg verbrannt.'},
13:{cfg:'[Ne] 3s² 3p¹',shells:[2,8,3],rxn:['4Al+3O₂→2Al₂O₃','2Al+6HCl→2AlCl₃+3H₂','2Al+Fe₂O₃→Al₂O₃+2Fe (Thermit)'],cpd:['Al₂O₃','AlCl₃','Al(OH)₃','Al₂(SO₄)₃'],uses:'Verpackungen, Flugzeugbau, Bauindustrie, Kochgeschirr, Kabel, Alufolie',desc:'Häufigstes Metall der Erdkruste (8,1 %). Leicht, korrosionsbeständig durch Al₂O₃-Passivschicht.',key:'Im 19. Jahrhundert war Al wertvoller als Gold — Napoleon ließ Besteck daraus fertigen. Erst die Elektrolyse (1886) machte es billig.',history:'1825 von Hans Christian Ørsted erstmals rein isoliert (elektrochemisch). 1886 unabhängig voneinander von Charles Hall (USA) und Paul Héroult (Frankreich) durch Schmelzflusselektrolyse (Hall-Héroult-Verfahren) erzeugt.',warn:null},
14:{cfg:'[Ne] 3s² 3p²',shells:[2,8,4],rxn:['Si+O₂→SiO₂','Si+2Cl₂→SiCl₄','SiO₂+2C→Si+2CO↑'],cpd:['SiO₂','SiC','Na₂SiO₃','SiH₄'],uses:'Halbleiter (CPU, Solarzellen), Glas (SiO₂), Silikone, Beton (SiO₂)',desc:'Zweithäufigstes Element der Erdkruste (27,7 %). Basis der modernen Elektronik.',key:'Ein moderner CPU-Chip enthält mehr als 10 Milliarden Transistoren auf einem Stück Silicium von der Größe eines Fingernagels.',history:'1824 von Jöns Jacob Berzelius rein dargestellt (nach früheren unreinen Versuchen von Davy 1808). Name: lateinisch silex = Kieselstein.',warn:null},
15:{cfg:'[Ne] 3s² 3p³',shells:[2,8,5],rxn:['4P+5O₂→P₄O₁₀','P₄+6Cl₂→4PCl₃','P+HNO₃→H₃PO₄'],cpd:['H₃PO₄','P₂O₅','PCl₃','PCl₅','Ca₃(PO₄)₂'],uses:'Düngemittel (Phosphat), Waschmittel, DNA/RNA-Rückgrat, Streichholzköpfe, Zündmittel',desc:'Essenzielles Element für Leben — Bestandteil von DNA, RNA, ATP und Zellmembranen (Phospholipide).',key:'ATP (Adenosintriphosphat): Das Phosphat-basierte Energiemolekül jeder Zelle — der „Treibstoff des Lebens".',history:'1669 von Hennig Brand in Hamburg entdeckt: Er kochte riesige Mengen Urin ein, um Gold zu suchen — und fand stattdessen weißen Phosphor, der im Dunkeln leuchtet. Erstes Element mit bekanntem Entdecker.',warn:'Weißer Phosphor: extrem giftig und selbstentzündlich. Roter Phosphor: deutlich stabiler.'},
16:{cfg:'[Ne] 3s² 3p⁴',shells:[2,8,6],rxn:['S+O₂→SO₂','SO₃+H₂O→H₂SO₄','2H₂S+3O₂→2SO₂+2H₂O'],cpd:['H₂SO₄','SO₂','H₂S','Na₂SO₄','FeS₂'],uses:'H₂SO₄-Produktion (meistproduzierte Chemikalie), Vulkanisierung von Kautschuk, Batterien, Dünger',desc:'Schwefel war in der Antike bekannt als „Brimstone" (Höllenfeuer). H₂SO₄ ist die meistproduzierte Chemikalie weltweit.',key:'Der H₂SO₄-Verbrauch eines Landes korreliert stark mit seinem Industrialisierungsgrad — wird als Wirtschaftsindikator verwendet.',history:'Im Altertum bekannt (Bibel, Homer). Als Element definiert von Lavoisier (1789). Vorkommen: elementar in vulkanischen Gebieten (Sizilien war Hauptproduzent bis 1900).',warn:'H₂S: riecht nach faulen Eiern, extrem giftig ab 100 ppm. SO₂: Hauptursache des sauren Regens.'},
17:{cfg:'[Ne] 3s² 3p⁵',shells:[2,8,7],rxn:['Cl₂+H₂→2HCl','Cl₂+2NaOH→NaCl+NaOCl+H₂O','Cl₂+2KI→2KCl+I₂'],cpd:['HCl','NaCl','NaOCl','Cl₂','PVC','CCl₄'],uses:'Wasserdesinfektion, PVC (meistproduzierter Kunststoff), Bleichmittel, Lösungsmittel',desc:'Gelbgrünes Giftgas. Als Desinfektionsmittel hat Chlor mehr Menschenleben gerettet als jedes andere Mittel.',key:'PVC (Polyvinylchlorid) ist einer der weltweit meistproduzierten Kunststoffe — Rohre, Fensterrahmen, Kabel.',history:'1774 von Carl Wilhelm Scheele entdeckt. Name: griech. chloros = gelbgrün. Davy erkannte 1810, dass es ein Element ist (nicht „de-phlogistierte Salzsäure" wie Scheele dachte).',warn:'Giftig! Cl₂ war im 1. Weltkrieg als Kampfgas eingesetzt. Nicht mit Ammoniak mischen — erzeugt Chloramin (giftig)!'},
18:{cfg:'[Ne] 3s² 3p⁶',shells:[2,8,8],rxn:[],cpd:[],uses:'Schutzgas (Schweißen), Füllgas (Glühbirnen, Fenster), Tauchergas, Plasmabildschirme',desc:'Häufigstes Edelgas in der Erdatmosphäre (0,93 %). Chemisch völlig inert.',key:'Ar macht mehr als 99 % aller Edelgase der Erdatmosphäre aus. Entsteht durch radioaktiven Zerfall von ⁴⁰K.',history:'1894 von Lord Rayleigh und William Ramsay entdeckt: Sie bemerkten, dass Stickstoff aus Luft etwas dichter ist als synthetischer — die Differenz war Argon. Name: griech. argos = träge.',warn:null},
19:{cfg:'[Ar] 4s¹',shells:[2,8,8,1],rxn:['2K+2H₂O→2KOH+H₂','4K+O₂→2K₂O'],cpd:['KCl','KOH','KNO₃','K₂SO₄','K₂CO₃'],uses:'Düngemittel (K als Pflanzennährstoff), Medizin, Feuerwerkskörper (lila Farbe), Schießpulver',desc:'Essenziell für Nervensystem und Herz. K⁺ reguliert Zellpotenzial und Herzrhythmus.',key:'⁴⁰K ist radioaktiv (HWZ 1,25 Mrd. Jahre) — im menschlichen Körper finden ~4400 K-Zerfälle/Sekunde statt.',history:'1807 von Humphry Davy durch Elektrolyse von geschmolzenem KOH isoliert — erstes Metall, das elektrochemisch gewonnen wurde. Name: deutsch „Kalium" (von arabisch qali = Asche).',warn:'Reagiert sehr heftig mit Wasser — heftiger als Natrium! Unter Mineralöl lagern.'},
20:{cfg:'[Ar] 4s²',shells:[2,8,8,2],rxn:['Ca+2H₂O→Ca(OH)₂+H₂','CaCO₃→CaO+CO₂','CaO+H₂O→Ca(OH)₂'],cpd:['CaCO₃','Ca(OH)₂','CaSO₄','CaCl₂','Ca₃(PO₄)₂'],uses:'Knochen/Zähne, Zement, Kalk, Dünger, Weichmacher, Lebensmittelzusatz',desc:'Häufigstes Metall im menschlichen Körper (~1 kg). 99 % in Knochen und Zähnen.',key:'Kalk (CaO) ist seit 7000 Jahren eine der wichtigsten Chemikalien: Mörtel, Zement, Glasherstellung.',history:'Seit der Antike als Kalk bekannt. Als eigenständiges Metall 1808 von Humphry Davy durch Elektrolyse isoliert. Name: lateinisch calx = Kalk.',warn:null},
26:{cfg:'[Ar] 3d⁶ 4s²',shells:[2,8,14,2],rxn:['4Fe+3O₂→2Fe₂O₃','Fe+S→FeS','Fe+2HCl→FeCl₂+H₂'],cpd:['Fe₂O₃','Fe₃O₄','FeCl₃','FeS₂','Fe(CO)₅'],uses:'Stahl (Kohlenstoffstahl, Edelstahl), Bauwesen, Magnete, Hämoglobin, Katalysatoren',desc:'Häufigstes Element im Erdkern (32 % der Erdmasse). Ferromagnetisch unter 770 °C (Curie-Punkt).',key:'Fe²⁺ im Hämoglobin bindet O₂ reversibel — ein Gramm Hämoglobin bindet 1,36 ml O₂.',history:'Seit mind. 5000 Jahren genutzt (Eisenzeit ab ca. 1200 v.Chr.). Meteoriten-Eisen wurde schon früher verwendet (Tutanchamun hatte einen Eisendolch aus Meteorit). Name: germanisch isan = fest.',warn:'Rosten (Fe₂O₃) verursacht weltweit Schäden von über 2,5 Billionen Dollar jährlich.'},
27:{cfg:'[Ar] 3d⁷ 4s²',shells:[2,8,15,2],rxn:['Co+2HCl→CoCl₂+H₂','3Co+2O₂→Co₂O₃+CoO'],cpd:['CoCl₂','CoO','Co₂O₃','Vitamin B₁₂'],uses:'Superlegierungen (Turbinen), Permanentmagnete (Samarium-Cobalt), Blau-Pigment, Vitamin B₁₂',desc:'Kobalt gibt Glas und Keramik eine tiefblaue Farbe (Kobaltblau). Zentralatom in Vitamin B₁₂.',key:'Kobalt ist eines der strategischen kritischen Rohstoffe — 70 % der Weltproduktion kommen aus der DR Kongo.',history:'1735 von Georg Brandt in Stockholm isoliert. Bergmänner nannten störende silberhaltige Erze „Kobold" — daraus wurde Co. Name: deutsch Kobold (böser Geist der Bergleute).',warn:null},
28:{cfg:'[Ar] 3d⁸ 4s²',shells:[2,8,16,2],rxn:['Ni+2HCl→NiCl₂+H₂','Ni+4CO→Ni(CO)₄'],cpd:['NiO','NiCl₂','NiSO₄','Ni(CO)₄'],uses:'Edelstahl (V2A), Münzen (5-Cent), Nickel-Cadmium-Akkus, Katalysatoren (Hydrierung), Schmuck',desc:'Dritthäufigstes Element im Erdkern (nach Fe und O). Silbrig-weißes, korrosionsbeständiges Metall.',key:'Ni(CO)₄ (Nickelcarbonyl) ist eine der giftigsten bekannten Verbindungen und wird zur Nickelreinigung genutzt (Mond-Verfahren).',history:'1751 von Axel Fredrik Cronstedt entdeckt, als er aus einem kupferfarbenen Erz kein Kupfer gewinnen konnte. Bergmänner nannten das Erz „Kupfernickel" (vom Berggeist Nickel). Isoliert aus Niccolite (NiAs).',warn:'Ni(CO)₄ extrem toxisch. Nickelkontakt kann Kontaktallergien auslösen.'},
29:{cfg:'[Ar] 3d¹⁰ 4s¹',shells:[2,8,18,1],rxn:['Cu+2AgNO₃→Cu(NO₃)₂+2Ag','2Cu+O₂→2CuO','Cu+2H₂SO₄(konz)→CuSO₄+SO₂+2H₂O'],cpd:['CuSO₄','CuO','Cu₂O','CuCO₃·Cu(OH)₂ (Grünspan)'],uses:'Elektrische Leitungen (50% der Cu-Produktion), Rohre, Bronze (Cu+Sn), Messing (Cu+Zn), Münzen',desc:'Bester bezahlbarer elektrischer Leiter (σ=59,6 MS/m). Seit ~9000 Jahren metallurgisch genutzt.',key:'Kupfer tötet Bakterien und Viren innerhalb von 2 Stunden — „Oligodynamischer Effekt". Daher Cu-Handläufe in Krankenhäusern.',history:'Eines der ersten vom Menschen genutzten Metalle (Kupferzeit: 5000–3000 v.Chr.). Name: lateinisch cuprum, von Zypern (Cyprus) — größte antike Kupfermine. Symbol Cu von Cuprum.',warn:null},
30:{cfg:'[Ar] 3d¹⁰ 4s²',shells:[2,8,18,2],rxn:['2Zn+O₂→2ZnO','Zn+2HCl→ZnCl₂+H₂','Zn+H₂SO₄→ZnSO₄+H₂'],cpd:['ZnO','ZnCl₂','ZnSO₄','ZnS'],uses:'Galvanisierung (Verzinkung), Messing, Sonnencreme (ZnO), Antioxidans, Batterien (Zn-C, Zn-Luft)',desc:'Essenzielles Spurenelement — ~300 Enzyme benötigen Zink als Kofaktor. Wichtig für Immunsystem.',key:'Zinkoxid (ZnO) ist weißes Pigment und UV-Blocker in Sonnencremes. Leitet kein Strom, aber Licht durch nanostrukturierte Formen.',history:'Zink-Legierungen seit 1000 v.Chr. (Messing). Elementares Zink 1746 von Andreas Marggraf isoliert. Name: mittelhochdeutsch Zinke = Zahn (wegen kristalliner Form).',warn:null},
31:{cfg:'[Ar] 3d¹⁰ 4s² 4p¹',shells:[2,8,18,3],rxn:['4Ga+3O₂→2Ga₂O₃'],cpd:['Ga₂O₃','GaAs','GaN','GaP'],uses:'Halbleiter (GaAs-Solarzellen, LEDs), Spezielle Legierungen, Thermometer (Galinstan)',desc:'Schmilzt bei 29,8 °C — in der Hand flüssig. Gallinstan (Ga-In-Sn-Legierung) ersetzt Quecksilber.',key:'GaN (Galliumnitrid) ist Basis effizienter LED-Beleuchtung und Hochfrequenz-Elektronik in Smartphones.',history:'1875 von Paul Emile Lecoq de Boisbaudran entdeckt — exakt wie von Mendeleev 1871 aus dem PSE vorhergesagt (Masse, Dichte, Eigenschaften). Größter Triumph des Periodensystems. Name: Gallia = Gallien (Frankreich).',warn:null},
32:{cfg:'[Ar] 3d¹⁰ 4s² 4p²',shells:[2,8,18,4],rxn:['Ge+O₂→GeO₂','Ge+2Cl₂→GeCl₄'],cpd:['GeO₂','GeCl₄','GeH₄'],uses:'Halbleiter (erste Transistoren), Infrarotoptik, Glasfaserkabel, Katalysatoren',desc:'Erste Transistoren (1947, Bell Labs) bestanden aus Germanium. Heute weitgehend durch Silicium ersetzt.',key:'Ebenfalls von Mendeleev als „Eka-Silicium" vorhergesagt und 1886 von Clemens Winkler exakt bestätigt.',history:'1886 von Clemens Winkler in Freiberg in einem silberhaltigen Mineral entdeckt. Name: Germanium nach dem Vaterland des Entdeckers (Deutschland).',warn:null},
35:{cfg:'[Ar] 3d¹⁰ 4s² 4p⁵',shells:[2,8,18,7],rxn:['Br₂+2KI→2KBr+I₂','Br₂+H₂→2HBr'],cpd:['HBr','NaBr','AgBr','CH₃Br'],uses:'Flammschutzmittel, Desinfektionsmittel, Fotofilm (AgBr), Medikamente',desc:'Einziges nicht-metallisches Element, das bei RT flüssig ist. Stechend riechendes, braun-rotes Halogen.',key:'AgBr ist lichtempfindlich — Basis der analogen Fotografie für über 150 Jahre.',history:'1826 gleichzeitig von Antoine Jérôme Balard (Frankreich) und Carl Jacob Löwig (Deutschland) entdeckt. Name: griech. bromos = Gestank.',warn:'Ätzend! Hautkontakt verursacht schmerzhafte Verätzungen. Dämpfe reizen Atemwege.'},
47:{cfg:'[Kr] 4d¹⁰ 5s¹',shells:[2,8,18,18,1],rxn:['Ag+Cl⁻→AgCl↓','2Ag+O₃→Ag₂O+O₂'],cpd:['AgCl','AgNO₃','AgBr','Ag₂S'],uses:'Schmuck, Besteck, Fotografie (AgBr), Elektronik (höchste Leitfähigkeit), Medizin (antibakteriell)',desc:'Höchste elektrische und thermische Leitfähigkeit aller Metalle (σ=63 MS/m).',key:'Silbernitrat (AgNO₃) fleckt Haut schwarz-braun und ist nicht abwaschbar — oxidiert Proteine dauerhaft.',history:'Seit mindestens 5000 Jahren bekannt (Silberzeit). Silber-Minen in Spanien und Griechenland finanzierten antike Reiche. Symbol Ag von lateinisch argentum. Argentinien ist nach Silber benannt.',warn:null},
50:{cfg:'[Kr] 4d¹⁰ 5s² 5p²',shells:[2,8,18,18,4],rxn:['Sn+2HCl→SnCl₂+H₂','Sn+O₂→SnO₂'],cpd:['SnO₂','SnCl₂','SnCl₄','Sn(OH)₂'],uses:'Lötzinn (Sn-Pb oder Sn-Ag), Bronze (Cu-Sn), Weißblech, Orgelpfeifen, Konservierungsdosen',desc:'Zwei stabile Allotrope: Weißzinn (β, metallisch) und Grauzinn (α, spröde, <13,2 °C).',key:'„Zinnpest": Unter −13,2 °C wandelt sich Weißzinn in Grauzinn um (bröckelt) — soll Napoleons Russlandfeldzug mitverursacht haben (Knöpfe und Dosen versagten).',history:'Seit 3500 v.Chr. bekannt (Bronzezeit: Cu+Sn). Name: englisch tin, Symbol Sn von lateinisch stannum.',warn:null},
56:{cfg:'[Xe] 6s²',shells:[2,8,18,18,8,2],rxn:['Ba+2H₂O→Ba(OH)₂+H₂','Ba+O₂→BaO₂'],cpd:['BaSO₄','BaCl₂','BaO','Ba(OH)₂'],uses:'Röntgenkontrastmittel (BaSO₄), Grünes Feuerwerkslicht (Ba-Salze), Vakuumröhren',desc:'Schwerste stabile Erdalkalimetall. BaSO₄ ist röntgenopak und für Magen-Darm-Untersuchungen ideal.',key:'BaSO₄ (Bariumsulfat) ist trotz allgemeiner Bariumgiftigkeit ungiftig — es löst sich in Wasser kaum (Ksp = 1,1×10⁻¹⁰).',history:'1808 von Humphry Davy durch Elektrolyse isoliert. Name: griech. barys = schwer.',warn:'Lösliche Ba-Verbindungen (BaCl₂) sind giftig!'},
79:{cfg:'[Xe] 4f¹⁴ 5d¹⁰ 6s¹',shells:[2,8,18,32,18,1],rxn:['Au+HNO₃+4HCl→H[AuCl₄]+NO+2H₂O (Königswasser)'],cpd:['AuCl₃','HAuCl₄','Au₂O₃'],uses:'Schmuck, Elektronik (Kontakte, Leiterplatten), Nanomedizin, Raumfahrt (Wärmeschutz)',desc:'Reaktionsträgestes Metall — nur in Königswasser (3 HCl + 1 HNO₃) löslich. Symbol Au von lateinisch aurum.',key:'Die gelbe Farbe von Gold ist ein relativistischer Quanteneffekt: Elektronen bewegen sich mit 58 % der Lichtgeschwindigkeit — ohne Relativitätstheorie wäre Gold silbrig-weiß.',history:'Seit Jahrtausenden bekannt (Goldmasken der Ägypter, ca. 3000 v.Chr.). In freier Form in der Natur gefunden. Der Goldrausch 1848 in Kalifornien veränderte die Geschichte. Alchemisten suchten Jahrhunderte nach seiner Synthese.',warn:null},
80:{cfg:'[Xe] 4f¹⁴ 5d¹⁰ 6s²',shells:[2,8,18,32,18,2],rxn:['Hg+S→HgS','2HgO→2Hg+O₂ (Priestleys Experiment)'],cpd:['HgCl₂','HgS (Zinnober)','Hg₂Cl₂','CH₃Hg⁺'],uses:'Leuchtstofflampen, hist. Thermometer (ersetzt durch Gallium), Amalgam-Zahnfüllungen (umstritten)',desc:'Einziges Metall, das bei Raumtemperatur flüssig ist (Schmp. −38,83 °C). Dichte: 13,6 g/cm³.',key:'Zinnober (HgS) war der teuerste rote Farbstoff der Antike — Pompeji hatte ganze Räume damit dekoriert.',history:'Im Altertum in ägyptischen Gräbern gefunden (ca. 1500 v.Chr.). Mittelalterliche Alchemisten hielten es für den „Urstoff" aller Metalle. Symbol Hg von lateinisch hydrargyrum = Wassersilber.',warn:'Hochgiftig! Methylquecksilber (CH₃Hg⁺) akkumuliert in Nahrungsketten. Minamata-Katastrophe 1956: 2000 Tote durch Quecksilbervergiftung in Japan.'},
82:{cfg:'[Xe] 4f¹⁴ 5d¹⁰ 6s² 6p²',shells:[2,8,18,32,18,4],rxn:['Pb+2HCl→PbCl₂+H₂','PbO₂+4HCl→PbCl₄+2H₂O'],cpd:['PbO₂','PbSO₄','PbO','Pb(CH₃)₄'],uses:'Blei-Akkumulatoren (Starterbatterien), Strahlenschutz (Röntgen), hist. Rohre, Schrot, Lot',desc:'Schwermetalll. Weich, leicht formbar, Röntgenstrahlen absorbierend. Schmp. nur 327 °C.',key:'Bleirohre im Römischen Reich wurden für Wasserleitungen genutzt. Einige Historiker sehen chronische Bleivergiftung als Mitursache des Niedergangs.',history:'Seit ca. 7000 Jahren genutzt — eines der ältesten verarbeiteten Metalle. Symbol Pb von lateinisch plumbum (daher auch „Klempner" aus plumber). Alchimisten glaubten, Blei sei das „unreifste" Metall und wollten es in Gold umwandeln.',warn:'Neurotoxisch! Irreversible Hirnschäden, besonders bei Kindern. Bleipetrol (Tetraethylblei) bis 2000 im Benzin — EU-Verbot 2000.'},
92:{cfg:'[Rn] 5f³ 6d¹ 7s²',shells:[2,8,18,32,21,9,2],rxn:['U+3F₂→UF₆','UO₂+4HF→UF₄+2H₂O'],cpd:['UO₂','UF₆','U₃O₈','UO₂(NO₃)₂'],uses:'Kernkraftwerke (Brennstoff), Strahlenschutzglas (früher), Uranverglasung (Vaseline-Glas), militärisch',desc:'Schwerstes natürliches Element. ²³⁸U: HWZ 4,47 Milliarden Jahre — fast so alt wie die Erde selbst.',key:'Ein Kilogramm ²³⁵U (spaltbar) setzt bei vollständiger Kernspaltung so viel Energie frei wie 3.000 Tonnen Steinkohle.',history:'1789 von Martin Klaproth in Pechblende entdeckt. Nach dem Planeten Uranus benannt (erst 1781 entdeckt). Erst 1938 entdeckten Otto Hahn, Lise Meitner und Fritz Straßmann die Kernspaltung — veränderte die Welt.',warn:'Radioaktiv (α-Strahlung) UND chemisch giftig (Schwermetall). Abgereichertes Uran in Panzermunition und Panzerungen.'},
};

const BASE=[
{z:1,s:'H',n:'Wasserstoff',m:1.008,g:1,p:1,c:'non',ph:'Gas',en:2.20,melt:-259.1,boil:-252.9},
{z:2,s:'He',n:'Helium',m:4.003,g:18,p:1,c:'noble',ph:'Gas',en:null,melt:null,boil:-268.9},
{z:3,s:'Li',n:'Lithium',m:6.941,g:1,p:2,c:'alkali',ph:'Fest',en:0.98,melt:180.5,boil:1342},
{z:4,s:'Be',n:'Beryllium',m:9.012,g:2,p:2,c:'alkaline',ph:'Fest',en:1.57,melt:1287,boil:2469},
{z:5,s:'B',n:'Bor',m:10.81,g:13,p:2,c:'met',ph:'Fest',en:2.04,melt:2076,boil:3927},
{z:6,s:'C',n:'Kohlenstoff',m:12.011,g:14,p:2,c:'non',ph:'Fest',en:2.55,melt:3550,boil:4827},
{z:7,s:'N',n:'Stickstoff',m:14.007,g:15,p:2,c:'non',ph:'Gas',en:3.04,melt:-210,boil:-195.8},
{z:8,s:'O',n:'Sauerstoff',m:15.999,g:16,p:2,c:'non',ph:'Gas',en:3.44,melt:-218.8,boil:-183},
{z:9,s:'F',n:'Fluor',m:18.998,g:17,p:2,c:'hal',ph:'Gas',en:3.98,melt:-219.6,boil:-188.1},
{z:10,s:'Ne',n:'Neon',m:20.18,g:18,p:2,c:'noble',ph:'Gas',en:null,melt:-248.6,boil:-246.1},
{z:11,s:'Na',n:'Natrium',m:22.99,g:1,p:3,c:'alkali',ph:'Fest',en:0.93,melt:97.8,boil:883},
{z:12,s:'Mg',n:'Magnesium',m:24.305,g:2,p:3,c:'alkaline',ph:'Fest',en:1.31,melt:650,boil:1090},
{z:13,s:'Al',n:'Aluminium',m:26.982,g:13,p:3,c:'post',ph:'Fest',en:1.61,melt:660.3,boil:2519},
{z:14,s:'Si',n:'Silicium',m:28.086,g:14,p:3,c:'met',ph:'Fest',en:1.90,melt:1414,boil:3265},
{z:15,s:'P',n:'Phosphor',m:30.974,g:15,p:3,c:'non',ph:'Fest',en:2.19,melt:44.2,boil:280.5},
{z:16,s:'S',n:'Schwefel',m:32.06,g:16,p:3,c:'non',ph:'Fest',en:2.58,melt:112.8,boil:444.6},
{z:17,s:'Cl',n:'Chlor',m:35.45,g:17,p:3,c:'hal',ph:'Gas',en:3.16,melt:-101.5,boil:-34.04},
{z:18,s:'Ar',n:'Argon',m:39.948,g:18,p:3,c:'noble',ph:'Gas',en:null,melt:-189.3,boil:-185.8},
{z:19,s:'K',n:'Kalium',m:39.098,g:1,p:4,c:'alkali',ph:'Fest',en:0.82,melt:63.5,boil:759},
{z:20,s:'Ca',n:'Calcium',m:40.078,g:2,p:4,c:'alkaline',ph:'Fest',en:1.0,melt:842,boil:1484},
{z:21,s:'Sc',n:'Scandium',m:44.956,g:3,p:4,c:'trans',ph:'Fest',en:1.36,melt:1541,boil:2836},
{z:22,s:'Ti',n:'Titan',m:47.867,g:4,p:4,c:'trans',ph:'Fest',en:1.54,melt:1668,boil:3287},
{z:23,s:'V',n:'Vanadium',m:50.942,g:5,p:4,c:'trans',ph:'Fest',en:1.63,melt:1910,boil:3407},
{z:24,s:'Cr',n:'Chrom',m:51.996,g:6,p:4,c:'trans',ph:'Fest',en:1.66,melt:1907,boil:2671},
{z:25,s:'Mn',n:'Mangan',m:54.938,g:7,p:4,c:'trans',ph:'Fest',en:1.55,melt:1246,boil:2061},
{z:26,s:'Fe',n:'Eisen',m:55.845,g:8,p:4,c:'trans',ph:'Fest',en:1.83,melt:1538,boil:2862},
{z:27,s:'Co',n:'Cobalt',m:58.933,g:9,p:4,c:'trans',ph:'Fest',en:1.88,melt:1495,boil:2927},
{z:28,s:'Ni',n:'Nickel',m:58.693,g:10,p:4,c:'trans',ph:'Fest',en:1.91,melt:1455,boil:2913},
{z:29,s:'Cu',n:'Kupfer',m:63.546,g:11,p:4,c:'trans',ph:'Fest',en:1.90,melt:1085,boil:2562},
{z:30,s:'Zn',n:'Zink',m:65.38,g:12,p:4,c:'post',ph:'Fest',en:1.65,melt:419.5,boil:907},
{z:31,s:'Ga',n:'Gallium',m:69.723,g:13,p:4,c:'post',ph:'Fest',en:1.81,melt:29.8,boil:2204},
{z:32,s:'Ge',n:'Germanium',m:72.63,g:14,p:4,c:'met',ph:'Fest',en:2.01,melt:938.3,boil:2833},
{z:33,s:'As',n:'Arsen',m:74.922,g:15,p:4,c:'met',ph:'Fest',en:2.18,melt:817,boil:614},
{z:34,s:'Se',n:'Selen',m:78.971,g:16,p:4,c:'non',ph:'Fest',en:2.55,melt:221,boil:685},
{z:35,s:'Br',n:'Brom',m:79.904,g:17,p:4,c:'hal',ph:'Flüssig',en:2.96,melt:-7.3,boil:58.8},
{z:36,s:'Kr',n:'Krypton',m:83.798,g:18,p:4,c:'noble',ph:'Gas',en:null,melt:-157.4,boil:-153.2},
{z:37,s:'Rb',n:'Rubidium',m:85.468,g:1,p:5,c:'alkali',ph:'Fest',en:0.82,melt:39.3,boil:688},
{z:38,s:'Sr',n:'Strontium',m:87.62,g:2,p:5,c:'alkaline',ph:'Fest',en:0.95,melt:777,boil:1382},
{z:39,s:'Y',n:'Yttrium',m:88.906,g:3,p:5,c:'trans',ph:'Fest',en:1.22,melt:1522,boil:3345},
{z:40,s:'Zr',n:'Zirconium',m:91.224,g:4,p:5,c:'trans',ph:'Fest',en:1.33,melt:1855,boil:4409},
{z:41,s:'Nb',n:'Niob',m:92.906,g:5,p:5,c:'trans',ph:'Fest',en:1.6,melt:2477,boil:4744},
{z:42,s:'Mo',n:'Molybdän',m:95.96,g:6,p:5,c:'trans',ph:'Fest',en:2.16,melt:2623,boil:4639},
{z:43,s:'Tc',n:'Technetium',m:98,g:7,p:5,c:'trans',ph:'Fest',en:1.9,melt:2157,boil:4265},
{z:44,s:'Ru',n:'Ruthenium',m:101.07,g:8,p:5,c:'trans',ph:'Fest',en:2.2,melt:2334,boil:4150},
{z:45,s:'Rh',n:'Rhodium',m:102.906,g:9,p:5,c:'trans',ph:'Fest',en:2.28,melt:1964,boil:3695},
{z:46,s:'Pd',n:'Palladium',m:106.42,g:10,p:5,c:'trans',ph:'Fest',en:2.2,melt:1555,boil:2963},
{z:47,s:'Ag',n:'Silber',m:107.868,g:11,p:5,c:'trans',ph:'Fest',en:1.93,melt:961.8,boil:2162},
{z:48,s:'Cd',n:'Cadmium',m:112.414,g:12,p:5,c:'post',ph:'Fest',en:1.69,melt:321.1,boil:767},
{z:49,s:'In',n:'Indium',m:114.818,g:13,p:5,c:'post',ph:'Fest',en:1.78,melt:156.6,boil:2072},
{z:50,s:'Sn',n:'Zinn',m:118.71,g:14,p:5,c:'post',ph:'Fest',en:1.96,melt:231.9,boil:2602},
{z:51,s:'Sb',n:'Antimon',m:121.76,g:15,p:5,c:'met',ph:'Fest',en:2.05,melt:630.6,boil:1587},
{z:52,s:'Te',n:'Tellur',m:127.6,g:16,p:5,c:'met',ph:'Fest',en:2.1,melt:449.5,boil:988},
{z:53,s:'I',n:'Iod',m:126.904,g:17,p:5,c:'hal',ph:'Fest',en:2.66,melt:113.7,boil:184.3},
{z:54,s:'Xe',n:'Xenon',m:131.293,g:18,p:5,c:'noble',ph:'Gas',en:null,melt:-111.8,boil:-108},
{z:55,s:'Cs',n:'Caesium',m:132.905,g:1,p:6,c:'alkali',ph:'Fest',en:0.79,melt:28.5,boil:671},
{z:56,s:'Ba',n:'Barium',m:137.327,g:2,p:6,c:'alkaline',ph:'Fest',en:0.89,melt:727,boil:1897},
{z:57,s:'La',n:'Lanthan',m:138.905,g:0,p:6,c:'lan',ph:'Fest',en:1.1,melt:920,boil:3464},
{z:58,s:'Ce',n:'Cer',m:140.116,g:0,p:6,c:'lan',ph:'Fest',en:1.12,melt:795,boil:3443},
{z:59,s:'Pr',n:'Praseodym',m:140.908,g:0,p:6,c:'lan',ph:'Fest',en:1.13,melt:935,boil:3520},
{z:60,s:'Nd',n:'Neodym',m:144.242,g:0,p:6,c:'lan',ph:'Fest',en:1.14,melt:1024,boil:3074},
{z:61,s:'Pm',n:'Promethium',m:145,g:0,p:6,c:'lan',ph:'Fest',en:1.13,melt:1042,boil:3000},
{z:62,s:'Sm',n:'Samarium',m:150.36,g:0,p:6,c:'lan',ph:'Fest',en:1.17,melt:1072,boil:1794},
{z:63,s:'Eu',n:'Europium',m:151.964,g:0,p:6,c:'lan',ph:'Fest',en:1.2,melt:826,boil:1529},
{z:64,s:'Gd',n:'Gadolinium',m:157.25,g:0,p:6,c:'lan',ph:'Fest',en:1.2,melt:1312,boil:3273},
{z:65,s:'Tb',n:'Terbium',m:158.925,g:0,p:6,c:'lan',ph:'Fest',en:1.2,melt:1356,boil:3230},
{z:66,s:'Dy',n:'Dysprosium',m:162.5,g:0,p:6,c:'lan',ph:'Fest',en:1.22,melt:1407,boil:2567},
{z:67,s:'Ho',n:'Holmium',m:164.93,g:0,p:6,c:'lan',ph:'Fest',en:1.23,melt:1461,boil:2700},
{z:68,s:'Er',n:'Erbium',m:167.259,g:0,p:6,c:'lan',ph:'Fest',en:1.24,melt:1529,boil:2868},
{z:69,s:'Tm',n:'Thulium',m:168.934,g:0,p:6,c:'lan',ph:'Fest',en:1.25,melt:1545,boil:1950},
{z:70,s:'Yb',n:'Ytterbium',m:173.04,g:0,p:6,c:'lan',ph:'Fest',en:1.1,melt:824,boil:1196},
{z:71,s:'Lu',n:'Lutetium',m:174.967,g:0,p:6,c:'lan',ph:'Fest',en:1.27,melt:1652,boil:3402},
{z:72,s:'Hf',n:'Hafnium',m:178.49,g:4,p:6,c:'trans',ph:'Fest',en:1.3,melt:2233,boil:4603},
{z:73,s:'Ta',n:'Tantal',m:180.948,g:5,p:6,c:'trans',ph:'Fest',en:1.5,melt:3017,boil:5458},
{z:74,s:'W',n:'Wolfram',m:183.84,g:6,p:6,c:'trans',ph:'Fest',en:2.36,melt:3422,boil:5555},
{z:75,s:'Re',n:'Rhenium',m:186.207,g:7,p:6,c:'trans',ph:'Fest',en:1.9,melt:3186,boil:5596},
{z:76,s:'Os',n:'Osmium',m:190.23,g:8,p:6,c:'trans',ph:'Fest',en:2.2,melt:3033,boil:5012},
{z:77,s:'Ir',n:'Iridium',m:192.217,g:9,p:6,c:'trans',ph:'Fest',en:2.2,melt:2446,boil:4428},
{z:78,s:'Pt',n:'Platin',m:195.084,g:10,p:6,c:'trans',ph:'Fest',en:2.28,melt:1768.3,boil:3825},
{z:79,s:'Au',n:'Gold',m:196.967,g:11,p:6,c:'trans',ph:'Fest',en:2.54,melt:1064.2,boil:2970},
{z:80,s:'Hg',n:'Quecksilber',m:200.592,g:12,p:6,c:'trans',ph:'Flüssig',en:2.0,melt:-38.83,boil:356.7},
{z:81,s:'Tl',n:'Thallium',m:204.383,g:13,p:6,c:'post',ph:'Fest',en:1.62,melt:304,boil:1473},
{z:82,s:'Pb',n:'Blei',m:207.2,g:14,p:6,c:'post',ph:'Fest',en:2.33,melt:327.5,boil:1749},
{z:83,s:'Bi',n:'Bismut',m:208.98,g:15,p:6,c:'post',ph:'Fest',en:2.02,melt:271.5,boil:1564},
{z:84,s:'Po',n:'Polonium',m:209,g:16,p:6,c:'met',ph:'Fest',en:2.0,melt:254,boil:962},
{z:85,s:'At',n:'Astat',m:210,g:17,p:6,c:'hal',ph:'Fest',en:2.2,melt:302,boil:337},
{z:86,s:'Rn',n:'Radon',m:222,g:18,p:6,c:'noble',ph:'Gas',en:null,melt:-71,boil:-61.7},
{z:87,s:'Fr',n:'Francium',m:223,g:1,p:7,c:'alkali',ph:'Fest',en:0.7,melt:27,boil:677},
{z:88,s:'Ra',n:'Radium',m:226,g:2,p:7,c:'alkaline',ph:'Fest',en:0.9,melt:700,boil:1737},
{z:89,s:'Ac',n:'Actinium',m:227,g:0,p:7,c:'act',ph:'Fest',en:1.1,melt:1050,boil:3200},
{z:90,s:'Th',n:'Thorium',m:232.038,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:1750,boil:4788},
{z:91,s:'Pa',n:'Protactinium',m:231.036,g:0,p:7,c:'act',ph:'Fest',en:1.5,melt:1572,boil:4000},
{z:92,s:'U',n:'Uran',m:238.029,g:3,p:7,c:'act',ph:'Fest',en:1.38,melt:1135,boil:4131},
{z:93,s:'Np',n:'Neptunium',m:237,g:0,p:7,c:'act',ph:'Fest',en:1.36,melt:644,boil:4000},
{z:94,s:'Pu',n:'Plutonium',m:244,g:0,p:7,c:'act',ph:'Fest',en:1.28,melt:640,boil:3228},
{z:95,s:'Am',n:'Americium',m:243,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:1176,boil:2011},
{z:96,s:'Cm',n:'Curium',m:247,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:1340,boil:3110},
{z:97,s:'Bk',n:'Berkelium',m:247,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:1050,boil:null},
{z:98,s:'Cf',n:'Californium',m:251,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:900,boil:null},
{z:99,s:'Es',n:'Einsteinium',m:252,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:860,boil:null},
{z:100,s:'Fm',n:'Fermium',m:257,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:1527,boil:null},
{z:101,s:'Md',n:'Mendelevium',m:258,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:827,boil:null},
{z:102,s:'No',n:'Nobelium',m:259,g:0,p:7,c:'act',ph:'Fest',en:1.3,melt:827,boil:null},
{z:103,s:'Lr',n:'Lawrencium',m:266,g:3,p:7,c:'act',ph:'Fest',en:1.3,melt:1627,boil:null},
{z:104,s:'Rf',n:'Rutherfordium',m:267,g:4,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:105,s:'Db',n:'Dubnium',m:268,g:5,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:106,s:'Sg',n:'Seaborgium',m:271,g:6,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:107,s:'Bh',n:'Bohrium',m:272,g:7,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:108,s:'Hs',n:'Hassium',m:270,g:8,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:109,s:'Mt',n:'Meitnerium',m:276,g:9,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:110,s:'Ds',n:'Darmstadtium',m:281,g:10,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:111,s:'Rg',n:'Roentgenium',m:280,g:11,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:112,s:'Cn',n:'Copernicium',m:285,g:12,p:7,c:'trans',ph:'?',en:null,melt:null,boil:null},
{z:113,s:'Nh',n:'Nihonium',m:284,g:13,p:7,c:'post',ph:'?',en:null,melt:null,boil:null},
{z:114,s:'Fl',n:'Flerovium',m:289,g:14,p:7,c:'post',ph:'?',en:null,melt:null,boil:null},
{z:115,s:'Mc',n:'Moscovium',m:288,g:15,p:7,c:'post',ph:'?',en:null,melt:null,boil:null},
{z:116,s:'Lv',n:'Livermorium',m:293,g:16,p:7,c:'post',ph:'?',en:null,melt:null,boil:null},
{z:117,s:'Ts',n:'Tenness',m:294,g:17,p:7,c:'hal',ph:'?',en:null,melt:null,boil:null},
{z:118,s:'Og',n:'Oganesson',m:294,g:18,p:7,c:'noble',ph:'?',en:null,melt:null,boil:null},
];
const EL=BASE.map(b=>({...b,...(EL_DETAIL[b.z]||{cfg:'–',shells:[],rxn:[],cpd:[],uses:'Synthetisch.',desc:'Synthetisch hergestelltes Element.',key:null,warn:null})}));
const EL_MAP=Object.fromEntries(EL.map(e=>[e.z,e]));

const PT_ROWS=[
  [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
  [3,4,0,0,0,0,0,0,0,0,0,0,5,6,7,8,9,10],
  [11,12,0,0,0,0,0,0,0,0,0,0,13,14,15,16,17,18],
  [19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36],
  [37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54],
  [55,56,-1,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86],
  [87,88,-2,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118],
  [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
  [0,0,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,0],
  [0,0,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,0],
];

const WIKI={
redox:{t:'Redoxreaktionen',ico:'⚡',desc:'Elektronenübertragung und Oxidationszahlen',tags:['Grundlagen','Elektrochemie'],html:`<h2>Redoxreaktionen</h2><div class="art-meta"><span>⏱ 8 min</span><span>Elektrochemie</span></div><p>Redoxreaktionen sind chemische Reaktionen, bei denen Elektronen zwischen Reaktionspartnern übertragen werden.</p><h3>Grundprinzip</h3><ul><li><strong>Oxidation:</strong> Elektronenabgabe → Oxidationszahl steigt</li><li><strong>Reduktion:</strong> Elektronenaufnahme → Oxidationszahl sinkt</li></ul><div class="merksatz">OIL RIG – Oxidation Is Loss, Reduction Is Gain</div><h3>Beispiel: Knallgasreaktion</h3><div class="formula-box">2 H₂ + O₂ → 2 H₂O &nbsp; ΔH = –572 kJ/mol</div><p>H: 0→+1 (Oxidation). O: 0→–2 (Reduktion).</p><div class="merksatz">Oxidation und Reduktion laufen immer gleichzeitig ab.</div>`},
electro:{t:'Elektrochemie',ico:'🔋',desc:'Galvanische Zellen, Elektrolyse, Spannungsreihe',tags:['Redox','Anwendung'],html:`<h2>Elektrochemie</h2><div class="art-meta"><span>⏱ 10 min</span><span>Redox</span></div><p>Zusammenhang zwischen Redoxreaktionen und elektrischem Strom.</p><h3>Daniell-Element</h3><ul><li>Anode (–): Zn → Zn²⁺ + 2e⁻</li><li>Kathode (+): Cu²⁺ + 2e⁻ → Cu</li><li>E° = +1,10 V</li></ul><div class="formula-box">E = E° + (RT/nF) · ln([Ox]/[Red])</div><h3>Elektrolyse</h3><p>Nicht-spontane Redoxreaktion durch Strom: Chlor-Alkali, Al-Gewinnung, Galvanik, grüner H₂.</p><div class="merksatz">Je negativer E°, desto stärker das Reduktionsmittel.</div>`},
acids:{t:'Säuren & Basen',ico:'🧪',desc:'pH-Wert, Protolyse und Pufferlösungen',tags:['Gleichgewicht','pH'],html:`<h2>Säuren und Basen</h2><div class="art-meta"><span>⏱ 9 min</span><span>Gleichgewicht</span></div><h3>Definitionen</h3><ul><li><strong>Arrhenius:</strong> Säure→H⁺, Base→OH⁻</li><li><strong>Brønsted-Lowry:</strong> Säure=H⁺-Donor, Base=H⁺-Akzeptor</li><li><strong>Lewis:</strong> allgemeinste Definition</li></ul><div class="formula-box">pH = –log₁₀[H₃O⁺] &nbsp;&nbsp; pH + pOH = 14</div><div class="merksatz">Jede pH-Einheit = 10-fache Konzentrationsänderung!</div><div class="formula-box">Henderson-Hasselbalch: pH = pKₐ + log([A⁻]/[HA])</div>`},
organic:{t:'Organische Chemie',ico:'🌿',desc:'Kohlenwasserstoffe und funktionelle Gruppen',tags:['Organik','Struktur'],html:`<h2>Organische Chemie</h2><div class="art-meta"><span>⏱ 12 min</span><span>Organik</span></div><p>Organische Chemie = Chemie der Kohlenstoffverbindungen.</p><h3>Kohlenwasserstoffe</h3><ul><li><strong>Alkane</strong> CₙH₂ₙ₊₂: gesättigt (CH₄, C₂H₆)</li><li><strong>Alkene</strong> CₙH₂ₙ: C=C (Ethen)</li><li><strong>Alkine</strong> CₙH₂ₙ₋₂: C≡C (Ethin)</li><li><strong>Arene:</strong> π-System (Benzol C₆H₆)</li></ul><h3>Funktionelle Gruppen</h3><ul><li>–OH: Alkohole &nbsp;–COOH: Carbonsäuren &nbsp;–NH₂: Amine</li><li>–CHO: Aldehyde &nbsp;–CO–: Ketone &nbsp;–COO–: Ester</li></ul><div class="merksatz">Funktionelle Gruppen bestimmen die Eigenschaften.</div>`},
bonding:{t:'Bindungsarten',ico:'🔗',desc:'Ionisch, kovalent, metallisch, Van-der-Waals',tags:['Grundlagen','Struktur'],html:`<h2>Chemische Bindungsarten</h2><div class="art-meta"><span>⏱ 7 min</span><span>Grundlagen</span></div><h3>Ionenbindung</h3><p>Metall+Nichtmetall. Elektronenübertragung. Hohe Smp., spröde.</p><div class="formula-box">Na + Cl → Na⁺Cl⁻ (NaCl, ΔH = –411 kJ/mol)</div><h3>Kovalente Bindung</h3><p>Gemeinsame e⁻-Paare. Einfach- (σ), Doppel- (σ+π), Dreifach (σ+2π).</p><h3>Metallische Bindung</h3><p>Metallionen im Elektronensee. Leitfähig, duktil, glänzend.</p><h3>Van-der-Waals</h3><ul><li>H-Brücken: X–H···Y (stärkste sekundäre Kraft)</li><li>Dipol-Dipol, London-Dispersion</li></ul><div class="merksatz">Wasser (Sdp. 100°C trotz M=18) → starke H-Brücken!</div>`}
};

const RXN_DB=[
{cat:'Verbrennung',eq:'CH4 + O2 → CO2 + H2O',name:'Methanverbrennung',bal:'CH₄ + 2 O₂ → CO₂ + 2 H₂O',dh:'–890 kJ/mol',steps:['C aus CH₄ → CO₂','4H → 2H₂O','O-Bilanz: 2O₂ ✓'],ox:[{el:'C',from:'-4',to:'+4',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Verbrennung',eq:'C + O2 → CO2',name:'Kohlenstoffverbrennung',bal:'C + O₂ → CO₂',dh:'–394 kJ/mol',steps:['1C=1C in CO₂ ✓','O₂=2O=CO₂ ✓','Ausgeglichen!'],ox:[{el:'C',from:'0',to:'+4',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Verbrennung',eq:'S + O2 → SO2',name:'Schwefelverbrennung',bal:'S + O₂ → SO₂',dh:'–296 kJ/mol',steps:['1S=SO₂ ✓','O₂=2O ✓','Ausgeglichen!'],ox:[{el:'S',from:'0',to:'+4',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Verbrennung',eq:'C3H8 + O2 → CO2 + H2O',name:'Propanverbrennung',bal:'C₃H₈ + 5 O₂ → 3 CO₂ + 4 H₂O',dh:'–2220 kJ/mol',steps:['3C→3CO₂','8H→4H₂O','O: 10=5O₂ ✓'],ox:[{el:'C',from:'-8/3',to:'+4',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Synthese',eq:'N2 + H2 → NH3',name:'Haber-Bosch (Ammoniak)',bal:'N₂ + 3 H₂ → 2 NH₃',dh:'–92 kJ/mol',steps:['2NH₃ für N₂','6H→3H₂','2N+6H ✓'],ox:[{el:'N',from:'0',to:'-3',t:'rd'},{el:'H',from:'0',to:'+1',t:'ox'}]},
{cat:'Synthese',eq:'H2 + Cl2 → HCl',name:'HCl-Synthese',bal:'H₂ + Cl₂ → 2 HCl',dh:'–184 kJ/mol',steps:['H₂→2H, Cl₂→2Cl','1H+1Cl→HCl','2HCl ✓'],ox:[{el:'H',from:'0',to:'+1',t:'ox'},{el:'Cl',from:'0',to:'-1',t:'rd'}]},
{cat:'Synthese',eq:'SO2 + O2 → SO3',name:'Kontaktverfahren',bal:'2 SO₂ + O₂ → 2 SO₃',dh:'–198 kJ/mol',steps:['S:2=2 ✓','O:4+2=6 ✓','Ausgeglichen!'],ox:[{el:'S',from:'+4',to:'+6',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Metallreaktionen',eq:'Fe + O2 → Fe2O3',name:'Eisenoxidation (Rosten)',bal:'4 Fe + 3 O₂ → 2 Fe₂O₃',dh:'–1648 kJ/mol',steps:['Fe₂O₃ hat 2Fe→2Fe₂O₃ für 4Fe','6O→3O₂','4Fe+6O ✓'],ox:[{el:'Fe',from:'0',to:'+3',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Metallreaktionen',eq:'Na + H2O → NaOH + H2',name:'Natrium + Wasser',bal:'2 Na + 2 H₂O → 2 NaOH + H₂',dh:'–368 kJ/mol',steps:['Na→Na⁺+e⁻','2H⁺+2e⁻→H₂','2NaOH+H₂ ✓'],ox:[{el:'Na',from:'0',to:'+1',t:'ox'},{el:'H',from:'+1',to:'0',t:'rd'}]},
{cat:'Metallreaktionen',eq:'Mg + O2 → MgO',name:'Magnesiumverbrennung',bal:'2 Mg + O₂ → 2 MgO',dh:'–1204 kJ/mol',steps:['O₂→2O→2MgO','2Mg+O₂→2MgO ✓'],ox:[{el:'Mg',from:'0',to:'+2',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Metallreaktionen',eq:'Al + HCl → AlCl3 + H2',name:'Aluminium + Salzsäure',bal:'2 Al + 6 HCl → 2 AlCl₃ + 3 H₂',dh:'–1060 kJ/mol',steps:['Al→Al³⁺+3e⁻','6H⁺→3H₂','2AlCl₃ ✓'],ox:[{el:'Al',from:'0',to:'+3',t:'ox'},{el:'H',from:'+1',to:'0',t:'rd'}]},
{cat:'Metallreaktionen',eq:'Zn + H2SO4 → ZnSO4 + H2',name:'Zink + Schwefelsäure',bal:'Zn + H₂SO₄ → ZnSO₄ + H₂',dh:'–153 kJ/mol',steps:['Zn→Zn²⁺+2e⁻','2H⁺→H₂','SO₄²⁻ unverändert ✓'],ox:[{el:'Zn',from:'0',to:'+2',t:'ox'},{el:'H',from:'+1',to:'0',t:'rd'}]},
{cat:'Metallreaktionen',eq:'Cu + AgNO3 → CuNO32 + Ag',name:'Kupfer + Silbernitrat',bal:'Cu + 2 AgNO₃ → Cu(NO₃)₂ + 2 Ag',dh:'–100 kJ/mol',steps:['Cu→Cu²⁺+2e⁻','2Ag⁺→2Ag','NO₃⁻ unverändert ✓'],ox:[{el:'Cu',from:'0',to:'+2',t:'ox'},{el:'Ag',from:'+1',to:'0',t:'rd'}]},
{cat:'Säure-Base',eq:'HCl + NaOH → NaCl + H2O',name:'Neutralisation',bal:'HCl + NaOH → NaCl + H₂O',dh:'–57 kJ/mol',steps:['H⁺+OH⁻→H₂O','1:1 ✓'],ox:[{el:'H',from:'+1',to:'+1',t:'neu'},{el:'Na',from:'+1',to:'+1',t:'neu'}]},
{cat:'Säure-Base',eq:'H2SO4 + 2NaOH → Na2SO4 + H2O',name:'Schwefelsäure + NaOH',bal:'H₂SO₄ + 2 NaOH → Na₂SO₄ + 2 H₂O',dh:'–114 kJ/mol',steps:['H₂SO₄ zweiprotonig→2OH⁻','Ausgeglichen ✓'],ox:[{el:'S',from:'+6',to:'+6',t:'neu'}]},
{cat:'Säure-Base',eq:'CaCO3 + HCl → CaCl2 + CO2 + H2O',name:'Kalk + Salzsäure',bal:'CaCO₃ + 2 HCl → CaCl₂ + CO₂ + H₂O',dh:'–15 kJ/mol',steps:['CaCO₃+2H⁺→Ca²⁺+CO₂+H₂O','CaCl₂ ✓'],ox:[{el:'Ca',from:'+2',to:'+2',t:'neu'}]},
{cat:'Elektrochemie',eq:'Zn + CuSO4 → ZnSO4 + Cu',name:'Daniell-Element',bal:'Zn + CuSO₄ → ZnSO₄ + Cu',dh:'–212 kJ/mol',steps:['Zn→Zn²⁺+2e⁻ (Anode)','Cu²⁺+2e⁻→Cu (Kathode)','SO₄²⁻ Spektator ✓'],ox:[{el:'Zn',from:'0',to:'+2',t:'ox'},{el:'Cu',from:'+2',to:'0',t:'rd'}]},
{cat:'Elektrochemie',eq:'2H2O → 2H2 + O2',name:'Wasserelektrolyse',bal:'2 H₂O → 2 H₂ + O₂',dh:'+572 kJ/mol',steps:['Kathode: 4H⁺+4e⁻→2H₂','Anode: 2H₂O→O₂+4H⁺+4e⁻','Ausgeglichen ✓'],ox:[{el:'H',from:'+1',to:'0',t:'rd'},{el:'O',from:'-2',to:'0',t:'ox'}]},
{cat:'Industrieprozesse',eq:'CaCO3 → CaO + CO2',name:'Kalkbrennen',bal:'CaCO₃ → CaO + CO₂',dh:'+178 kJ/mol',steps:['Thermische Zersetzung ~900°C','1:1:1 ausgeglichen ✓'],ox:[{el:'Ca',from:'+2',to:'+2',t:'neu'},{el:'C',from:'+4',to:'+4',t:'neu'}]},
{cat:'Industrieprozesse',eq:'Fe2O3 + CO → Fe + CO2',name:'Hochofenprozess',bal:'Fe₂O₃ + 3 CO → 2 Fe + 3 CO₂',dh:'–25 kJ/mol',steps:['2Fe→Rechts','3CO für 3O','3CO₂ ✓'],ox:[{el:'Fe',from:'+3',to:'0',t:'rd'},{el:'C',from:'+2',to:'+4',t:'ox'}]},
{cat:'Industrieprozesse',eq:'4NH3 + 5O2 → 4NO + 6H2O',name:'Ostwald-Prozess',bal:'4 NH₃ + 5 O₂ → 4 NO + 6 H₂O',dh:'–906 kJ/mol',steps:['N:–3→+2','H:12H→6H₂O','O:10O=4+6 ✓'],ox:[{el:'N',from:'-3',to:'+2',t:'ox'},{el:'O',from:'0',to:'-2',t:'rd'}]},
{cat:'Organik',eq:'C2H4 + H2 → C2H6',name:'Ethen-Hydrierung',bal:'C₂H₄ + H₂ → C₂H₆',dh:'–137 kJ/mol',steps:['Addition an C=C','Pt/Ni-Katalysator','1:1:1 ✓'],ox:[{el:'C',from:'-2',to:'-3',t:'rd'},{el:'H',from:'0',to:'+1',t:'ox'}]},
{cat:'Organik',eq:'CH3COOH + C2H5OH → CH3COOC2H5 + H2O',name:'Veresterung',bal:'CH₃COOH + C₂H₅OH ⇌ CH₃COOC₂H₅ + H₂O',dh:'–8 kJ/mol',steps:['Gleichgewichtsreaktion','OH+H→H₂O','Esterbindung ✓'],ox:[{el:'C',from:'0',to:'0',t:'neu'}]},
];

const MOLECULES=[
{cat:'Alkane',name:'Methan',formula:'CH₄',atoms:[{s:'C',x:0,y:0},{s:'H',x:-40,y:0},{s:'H',x:40,y:0},{s:'H',x:0,y:-40},{s:'H',x:0,y:40}],bonds:[[0,1,1],[0,2,1],[0,3,1],[0,4,1]]},
{cat:'Alkane',name:'Ethan',formula:'C₂H₆',atoms:[{s:'C',x:-25,y:0},{s:'C',x:25,y:0},{s:'H',x:-55,y:-22},{s:'H',x:-55,y:22},{s:'H',x:-25,y:-40},{s:'H',x:55,y:-22},{s:'H',x:55,y:22},{s:'H',x:25,y:-40}],bonds:[[0,1,1],[0,2,1],[0,3,1],[0,4,1],[1,5,1],[1,6,1],[1,7,1]]},
{cat:'Alkane',name:'Propan',formula:'C₃H₈',atoms:[{s:'C',x:-50,y:0},{s:'C',x:0,y:0},{s:'C',x:50,y:0},{s:'H',x:-50,y:-38},{s:'H',x:-82,y:18},{s:'H',x:-82,y:-18},{s:'H',x:0,y:-38},{s:'H',x:0,y:38},{s:'H',x:50,y:-38},{s:'H',x:82,y:18},{s:'H',x:82,y:-18}],bonds:[[0,1,1],[1,2,1],[0,3,1],[0,4,1],[0,5,1],[1,6,1],[1,7,1],[2,8,1],[2,9,1],[2,10,1]]},
{cat:'Alkene',name:'Ethen',formula:'C₂H₄',atoms:[{s:'C',x:-22,y:0},{s:'C',x:22,y:0},{s:'H',x:-50,y:-26},{s:'H',x:-50,y:26},{s:'H',x:50,y:-26},{s:'H',x:50,y:26}],bonds:[[0,1,2],[0,2,1],[0,3,1],[1,4,1],[1,5,1]]},
{cat:'Alkine',name:'Ethin',formula:'C₂H₂',atoms:[{s:'C',x:-22,y:0},{s:'C',x:22,y:0},{s:'H',x:-56,y:0},{s:'H',x:56,y:0}],bonds:[[0,1,3],[0,2,1],[1,3,1]]},
{cat:'Arene',name:'Benzol',formula:'C₆H₆',ring6:true},
{cat:'Alkohole',name:'Methanol',formula:'CH₃OH',atoms:[{s:'C',x:-20,y:0},{s:'O',x:22,y:0},{s:'H',x:52,y:0},{s:'H',x:-20,y:-38},{s:'H',x:-52,y:18},{s:'H',x:-52,y:-18}],bonds:[[0,1,1],[1,2,1],[0,3,1],[0,4,1],[0,5,1]]},
{cat:'Alkohole',name:'Ethanol',formula:'C₂H₅OH',atoms:[{s:'C',x:-38,y:0},{s:'C',x:2,y:0},{s:'O',x:38,y:0},{s:'H',x:68,y:0},{s:'H',x:-38,y:-38},{s:'H',x:-70,y:18},{s:'H',x:-70,y:-18},{s:'H',x:2,y:-38},{s:'H',x:2,y:38}],bonds:[[0,1,1],[1,2,1],[2,3,1],[0,4,1],[0,5,1],[0,6,1],[1,7,1],[1,8,1]]},
{cat:'Carbonsäuren',name:'Essigsäure',formula:'CH₃COOH',atoms:[{s:'C',x:-38,y:0},{s:'C',x:2,y:0},{s:'O',x:34,y:-26},{s:'O',x:34,y:26},{s:'H',x:62,y:26},{s:'H',x:-38,y:-38},{s:'H',x:-70,y:18},{s:'H',x:-70,y:-18}],bonds:[[0,1,1],[1,2,2],[1,3,1],[3,4,1],[0,5,1],[0,6,1],[0,7,1]]},
{cat:'Sonstige',name:'Aceton',formula:'(CH₃)₂CO',atoms:[{s:'C',x:-50,y:0},{s:'C',x:0,y:0},{s:'O',x:0,y:-40},{s:'C',x:50,y:0},{s:'H',x:-50,y:-38},{s:'H',x:-82,y:18},{s:'H',x:-82,y:-18},{s:'H',x:50,y:-38},{s:'H',x:82,y:18},{s:'H',x:82,y:-18}],bonds:[[0,1,1],[1,2,2],[1,3,1],[0,4,1],[0,5,1],[0,6,1],[3,7,1],[3,8,1],[3,9,1]]},
{cat:'Sonstige',name:'Glucose',formula:'C₆H₁₂O₆',glucose:true},
{cat:'Sonstige',name:'Harnstoff',formula:'(NH₂)₂CO',atoms:[{s:'C',x:0,y:0},{s:'O',x:0,y:-40},{s:'N',x:-40,y:28},{s:'N',x:40,y:28},{s:'H',x:-66,y:8},{s:'H',x:-40,y:62},{s:'H',x:66,y:8},{s:'H',x:40,y:62}],bonds:[[0,1,2],[0,2,1],[0,3,1],[2,4,1],[2,5,1],[3,6,1],[3,7,1]]},
];

const ATOM_COLORS={C:'#546E7A',H:'#1E88E5',O:'#E53935',N:'#43A047',S:'#FB8C00',Cl:'#00897B',P:'#9C27B0'};
const ATOM_R={C:14,H:11,O:14,N:13,S:14,Cl:16};
const MAX_VAL={C:4,N:3,O:2,S:2,Cl:1,F:1,H:1,Br:1,I:1,P:5,B:3};

// ── Freie Valenzen ──────────────────────────────────────────────
function sFreeVal(atom){
  const mv=MAX_VAL[atom.s]||0;
  const used=_S.bonds.filter(b=>b.a===atom||b.b===atom).reduce((s,b)=>s+b.order,0);
  return Math.max(0,mv-used);
}
// ── Nächstes Atom mit freier Valenz ─────────────────────────────
function sNearFree(x,y,exclude,minFree){
  minFree=minFree||1;
  let best=null,bestD=Infinity;
  for(const a of _S.atoms){
    if(a===exclude)continue;
    if(sFreeVal(a)<minFree)continue;
    const d=Math.hypot(a.x-x,a.y-y);
    if(d<72&&d<bestD){bestD=d;best=a;}
  }
  return best;
}

// ── Molekülerkennung ────────────────────────────────────────────
const MOL_NAMES={
  'H2':'Wasserstoff','O2':'Sauerstoff','N2':'Stickstoff','Cl2':'Chlorgas',
  'HCl':'Chlorwasserstoff','H2O':'Wasser','NH3':'Ammoniak',
  'CH4':'Methan','C2H6':'Ethan','C3H8':'Propan','C4H10':'Butan',
  'C5H12':'Pentan','C6H14':'Hexan','C7H16':'Heptan','C8H18':'Octan',
  'C2H4':'Ethen','C3H6':'Propen','C4H8':'Buten',
  'C2H2':'Ethin','C3H4':'Propin',
  'C6H6':'Benzol','C7H8':'Toluol','C8H10':'Xylol','C6H12':'Cyclohexan',
  'CH3OH':'Methanol','C2H5OH':'Ethanol','C2H6O':'Ethanol',
  'C3H7OH':'Propanol','C3H8O':'Propanol','C4H9OH':'Butanol',
  'CH2O':'Formaldehyd','C2H4O':'Acetaldehyd','C3H6O':'Aceton',
  'CH2O2':'Ameisensäure','C2H4O2':'Essigsäure','C3H6O2':'Propansäure',
  'CH3Cl':'Chlormethan','C2H5Cl':'Chlorethan','CHCl3':'Chloroform','CCl4':'Tetrachlormethan',
  'H2S':'Schwefelwasserstoff','SO2':'Schwefeldioxid','CO':'Kohlenmonoxid','CO2':'Kohlendioxid',
  'C6H12O6':'Glucose','C12H22O11':'Saccharose','C3H8O3':'Glycerin',
  'CH4N2O':'Harnstoff','C2H6O2':'Ethylenglycol',
  'HNO3':'Salpetersäure','H2SO4':'Schwefelsäure','H3PO4':'Phosphorsäure',
  'NaOH':'Natriumhydroxid','KOH':'Kaliumhydroxid','Ca(OH)2':'Calciumhydroxid',
};
function sMolName(f){return MOL_NAMES[f]||null;}

const QUIZ_Q={
elements:[
{q:'Welches Element hat das Symbol Fe?',el:26,answers:['Eisen','Fluor','Francium','Fermium'],correct:0,exp:'Fe kommt vom lateinischen "ferrum" (Eisen).'},
{q:'Ordnungszahl von Gold?',el:79,answers:['78','79','80','81'],correct:1,exp:'Gold (Au) hat die Ordnungszahl 79.'},
{q:'Leichtestes Element?',el:1,answers:['Helium','Lithium','Wasserstoff','Beryllium'],correct:2,exp:'Wasserstoff (H, Z=1) ist das leichteste Element.'},
{q:'Höchste Elektronegativität?',el:9,answers:['Sauerstoff','Stickstoff','Chlor','Fluor'],correct:3,exp:'Fluor hat EN=3,98 – die höchste aller Elemente.'},
{q:'Welches Element ist bei RT flüssig (außer Hg)?',el:35,answers:['Iod','Brom','Chlor','Phosphor'],correct:1,exp:'Brom ist neben Hg das einzige bei RT flüssige Element.'},
{q:'Elektronen von Natrium (Na)?',el:11,answers:['10','11','12','13'],correct:1,exp:'Natrium (Z=11) hat 11 Elektronen.'},
{q:'Häufigstes Edelgas in der Atmosphäre?',el:18,answers:['Helium','Neon','Argon','Krypton'],correct:2,exp:'Argon macht 0,93% der Erdatmosphäre aus.'},
{q:'Atommasse von Kohlenstoff?',el:6,answers:['11','12','13','14'],correct:1,exp:'Kohlenstoff hat die Atommasse 12,011 u.'},
{q:'Welches Element ist im Hämoglobin?',el:26,answers:['Kupfer','Zink','Eisen','Mangan'],correct:2,exp:'Fe²⁺ ist das Zentralion im Hämoglobin.'},
{q:'Symbol für Kalium?',el:19,answers:['Ka','K','Kal','Kt'],correct:1,exp:'Kalium hat das Symbol K (vom lat. "kalium").'},
],
reactions:[
{q:'Produkte der vollst. Verbrennung von Methan?',answers:['CO+H₂O','CO₂+H₂O','CO₂+H₂','CH₄O'],correct:1,exp:'CH₄+2O₂→CO₂+2H₂O.'},
{q:'Reaktion von Na mit H₂O?',answers:['NaO+H₂','NaOH+H₂','Na₂O+H₂O','NaH+O₂'],correct:1,exp:'2Na+2H₂O→2NaOH+H₂.'},
{q:'Was ist Oxidation?',answers:['Aufnahme von Elektronen','Abgabe von Elektronen','Aufnahme von Protonen','Abgabe von Neutronen'],correct:1,exp:'Oxidation = Elektronenabgabe (OIL).'},
{q:'Was entsteht an der Kathode bei Wasserelektrolyse?',answers:['Sauerstoff','Ozon','Wasserstoff','Wasser'],correct:2,exp:'Kathode: 4H⁺+4e⁻→2H₂.'},
{q:'Was ist der Haber-Bosch-Prozess?',answers:['H₂SO₄-Synthese','NH₃-Synthese','Fe-Reduktion','Al-Gewinnung'],correct:1,exp:'N₂+3H₂⇌2NH₃.'},
{q:'Hauptursache sauren Regens?',answers:['CO₂','NO','SO₂','NH₃'],correct:2,exp:'SO₂+H₂O→H₂SO₃.'},
{q:'Was ist ein Puffer?',answers:['Gemisch starker Säuren','pH-stabilisierendes Gemisch','konzentrierte Lauge','Salz'],correct:1,exp:'Schwache Säure+Konjugatbase stabilisiert pH.'},
{q:'Welche Reaktion ist EXOTHERM?',answers:['CaCO₃→CaO+CO₂','2H₂O→2H₂+O₂','2Na+2H₂O→2NaOH+H₂','Fotosynthese'],correct:2,exp:'Na+H₂O: stark exotherm (ΔH<0).'},
],
theory:[
{q:'Was gibt die Periode im PSE an?',answers:['Neutronen','Elektronen','besetzte Schalen','Valenzelektronen'],correct:2,exp:'Periode = Anzahl der besetzten Elektronenschalen.'},
{q:'Gemeinsames Merkmal einer Gruppe?',answers:['Gleiche Atommasse','Gleiche Protonenzahl','Gleiche Valenzelektronen','Gleicher Aggregatzustand'],correct:2,exp:'Gleiche Valenzelektronenzahl → ähnliche Eigenschaften.'},
{q:'Was ist Elektronegativität?',answers:['Elektronen abgeben','Elektronen anziehen','Anzahl der Elektronen','Verhältnis p/e'],correct:1,exp:'EN = Fähigkeit, Bindungselektronen anzuziehen.'},
{q:'Bindung zwischen zwei Nichtmetallen?',answers:['Ionenbindung','Metallische Bindung','Kovalente Bindung','Van-der-Waals'],correct:2,exp:'Zwei Nichtmetalle: kovalente Bindungen.'},
{q:'Was ist die Oktettregel?',answers:['Atome wollen 10e⁻','8 Valenzelektronen','Atome haben 8 Protonen','8 Bindungen'],correct:1,exp:'Atome streben nach 8 Valenzelektronen.'},
]};

/* ═══════════════════════════════════════════
   INFINITY ZOOM ENGINE
═══════════════════════════════════════════ */
let CURRENT_PAGE = 'home';
let DARK = false;
let PSE_FILTER = 'all';
let PSE_SEL = null;
let RXN_CAT = null;
let WIKI_KEY = null;
let QZ = {mode:null,cat:'elements',q:0,score:0,answered:false,done:false};
let _S = {tool:'C',atoms:[],bonds:[],undoStack:[],sel:null,hover:null,drag:null,dragOfs:{x:0,y:0},grid:true,snap:true,isDown:false,mouse:{x:0,y:0}};

const PAGE_NAMES = {
  home:'Startseite', pse:'Periodensystem', wiki:'Chemie-Wiki',
  learn:'Lernbereich', struc:'Strukturzeichner', rxn:'Reaktionsrechner', quiz:'Quiz', info:'Info & Impressum'
};

function zoomTo(page) {
  const world        = document.getElementById('zoom-world');
  const homeLayer    = document.getElementById('layer-home');
  const contentLayer = document.getElementById('layer-content');
  const panel        = document.getElementById('content-panel');
  const fromHome     = CURRENT_PAGE === 'home';

  CURRENT_PAGE = page;

  if (fromHome) {
    // ── Home → Modul ──
    world.style.transform = 'scale(2.5) translateZ(200px)';
    homeLayer.style.opacity = '0';
    homeLayer.style.transition = 'opacity 0.5s';

    setTimeout(() => {
      homeLayer.classList.remove('active');
      homeLayer.style.opacity = '';
      homeLayer.style.transition = '';

      // Clear panel BEFORE making layer visible
      panel.innerHTML = '';
      contentLayer.classList.add('active');
      contentLayer.style.opacity = '0';

      panel.innerHTML = renderPage(page);
      if (page === 'struc') initCanvas();
      panel.scrollTop = 0;

      world.style.transition = 'none';
      world.style.transform = 'scale(0.6) translateZ(-200px)';

      requestAnimationFrame(() => {
        contentLayer.style.transition = 'opacity 0.35s';
        contentLayer.style.opacity = '1';
        world.style.transition = 'transform 0.9s cubic-bezier(.77,0,.175,1)';
        world.style.transform = 'scale(1) translateZ(0)';
        setTimeout(() => {
          contentLayer.style.opacity = '';
          contentLayer.style.transition = '';
        }, 400);
      });
    }, 500);

  } else {
    // ── Modul → Modul ── (fix: fade out, swap content, fade in)
    contentLayer.style.transition = 'opacity 0.2s';
    contentLayer.style.opacity = '0';

    setTimeout(() => {
      // Clear old content completely before writing new
      panel.innerHTML = '';
      panel.innerHTML = renderPage(page);
      if (page === 'struc') initCanvas();
      panel.scrollTop = 0;

      contentLayer.style.transition = 'opacity 0.25s';
      contentLayer.style.opacity = '1';
      setTimeout(() => {
        contentLayer.style.opacity = '';
        contentLayer.style.transition = '';
      }, 280);
    }, 220);
  }

  // Update HUD immediately
  document.getElementById('breadcrumb').style.display = 'flex';
  document.getElementById('crumb-current').textContent = PAGE_NAMES[page] || page;
  document.getElementById('back-btn').classList.add('show');
  const hudBack = document.getElementById('hud-back'); if(hudBack) hudBack.style.display='flex';
  document.getElementById('zoom-hint').classList.add('hidden');

  // Nav dots + XP + nav hint
  _navDots(page);
  _trackVisit(page);
  var _ni = MODULES_ORDER.indexOf(page);
  var _hp = _ni <= 0 ? 'Startseite' : MODULE_NAMES[_ni-1];
  var _hn = _ni >= MODULES_ORDER.length-1 ? 'Startseite' : MODULE_NAMES[_ni+1];
  var _hint = document.getElementById('zoom-hint');
  if(_hint){ _hint.textContent = '\u2191 '+_hp+' \u00b7 Scrollen \u00b7 '+_hn+' \u2193'; _hint.classList.remove('hidden'); clearTimeout(_hint._ht); _hint._ht = setTimeout(function(){ _hint.classList.add('hidden'); }, 4000); }
}

function zoomHome() {
  const world = document.getElementById('zoom-world');
  const homeLayer = document.getElementById('layer-home');
  const contentLayer = document.getElementById('layer-content');

  // Zoom out
  world.style.transform = 'scale(0.4) translateZ(-300px)';
  contentLayer.style.opacity = '0';
  contentLayer.style.transition = 'opacity 0.4s';

  setTimeout(() => {
    contentLayer.classList.remove('active');
    contentLayer.style.opacity = '';
    contentLayer.style.transition = '';
    homeLayer.classList.add('active');
    homeLayer.style.opacity = '0';
    world.style.transition = 'none';
    world.style.transform = 'scale(1.8) translateZ(150px)';

    requestAnimationFrame(() => {
      homeLayer.style.transition = 'opacity 0.5s';
      homeLayer.style.opacity = '1';
      world.style.transition = 'transform 0.9s cubic-bezier(.77,0,.175,1)';
      world.style.transform = 'scale(1) translateZ(0)';
    });

    CURRENT_PAGE = 'home';
    PSE_SEL = null;
    WIKI_KEY = null;
    document.getElementById('breadcrumb').style.display = 'none';
    document.getElementById('back-btn').classList.remove('show');
    const hudBackEl = document.getElementById('hud-back'); if(hudBackEl) hudBackEl.style.display='none';
    document.getElementById('zoom-hint').classList.remove('hidden');
    // Reset scroll state via helper
    _resetHS();
    _navDots('home');
    _transitioning = false;
    _edgeAccum = 0;
    const hint = document.getElementById('zoom-hint');
    if(hint) hint.textContent = '\u2193 Scrollen zum Einzoomen \u00b7 Klick auf Kachel zum \u00d6ffnen';
  }, 400);
}

// ── SCROLL-TO-ZOOM ENGINE ──
// Maps scroll position to zoom depth on home screen

function toggleDark() {
  DARK = !DARK;
  document.getElementById('app') && document.getElementById('app').classList.toggle('dk', DARK);
  document.documentElement.classList.toggle('dk', DARK);
  const btn = document.getElementById('dk-btn');
  if (btn) btn.textContent = DARK ? '☀️' : '🌙';
}

/* ═══ SEARCH ═══ */
const SRCH_IDX = [
  // Module
  {l:'Periodensystem',s:'118 Elemente interaktiv',c:'Modul',ico:'🔬',a:()=>zoomTo('pse')},
  {l:'Chemie-Wiki',s:'Artikel zu Reaktionen, Bindungen',c:'Modul',ico:'📚',a:()=>zoomTo('wiki')},
  {l:'Lernbereich',s:'PSE-Grundlagen einfach erklärt',c:'Modul',ico:'🎓',a:()=>zoomTo('learn')},
  {l:'Strukturzeichner',s:'Moleküle zeichnen & erkunden',c:'Modul',ico:'✏️',a:()=>zoomTo('struc')},
  {l:'Reaktionsrechner',s:'Gleichungen ausgleichen',c:'Modul',ico:'⚖️',a:()=>zoomTo('rxn')},
  {l:'Quiz',s:'Wissen in 8 Kategorien testen',c:'Modul',ico:'🧠',a:()=>zoomTo('quiz')},
  {l:'Info & Impressum',s:'Kontakt, Über ChemLab',c:'Modul',ico:'ℹ️',a:()=>zoomTo('info')},
  // Alle Elemente (auch ohne Detail-Seite)
  ...EL.map(e=>({l:e.n,s:e.s+' · Z='+e.z+' · '+e.g,c:'Element',ico:'⚛️',a:()=>{PSE_SEL=e;zoomTo('pse');}})),
  // Wiki-Artikel
  ...Object.entries(WIKI).map(([k,v])=>({l:v.t,s:v.desc||'',c:'Wiki',ico:'📖',a:()=>{WIKI_KEY=k;zoomTo('wiki');}})),
  // Moleküle aus Bibliothek
  ...MOLECULES.map(m=>({l:m.name,s:m.formula+' · '+m.cat,c:'Molekül',ico:'🧬',a:()=>{zoomTo('struc');setTimeout(()=>loadMol(m),600);}})),
];
let _srchActs = [];

function doSearch(q) {
  const dd = document.getElementById('srch-dd');
  const ql = q.trim().toLowerCase();
  // On empty focus: show modules as default suggestions
  if (!ql) {
    const mods = SRCH_IDX.filter(d=>d.c==='Modul');
    _srchActs = mods;
    dd.innerHTML = '<div style="padding:6px 12px;font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.06em">Module</div>' +
      mods.map((r,i)=>`<div class="srch-item" onmousedown="pickSrch(${i})">
        <span style="font-size:15px">${r.ico}</span>
        <div><div style="font-weight:500">${r.l}</div><div style="font-size:10.5px;color:var(--t3)">${r.s}</div></div>
      </div>`).join('');
    dd.style.display = 'block';
    return;
  }
  const res = SRCH_IDX.filter(d=>
    d.l.toLowerCase().includes(ql) ||
    d.s.toLowerCase().includes(ql) ||
    (d.c==='Element' && d.l.toLowerCase().startsWith(ql))
  ).slice(0,10);
  _srchActs = res;
  if (!res.length) {
    dd.innerHTML = '<div style="padding:10px 12px;font-size:12px;color:var(--t3)">Keine Ergebnisse für „'+q+'"</div>';
    dd.style.display = 'block';
    return;
  }
  // Group by category
  const groups = {};
  res.forEach(r=>{ if(!groups[r.c]) groups[r.c]=[]; groups[r.c].push(r); });
  dd.innerHTML = Object.entries(groups).map(([cat,items])=>
    `<div style="padding:5px 12px 2px;font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.06em">${cat}</div>`+
    items.map(r=>{
      const i=_srchActs.indexOf(r);
      // Highlight match
      const hl=r.l.replace(new RegExp('('+ql+')','gi'),'<mark style="background:var(--acl);color:var(--acc);border-radius:2px">$1</mark>');
      return `<div class="srch-item" onmousedown="pickSrch(${i})">
        <span style="font-size:15px">${r.ico}</span>
        <div><div>${hl}</div><div style="font-size:10.5px;color:var(--t3)">${r.s}</div></div>
        <span style="margin-left:auto;font-size:10px;background:var(--bg3);color:var(--t3);padding:2px 7px;border-radius:8px;flex-shrink:0">${r.c}</span>
      </div>`;
    }).join('')
  ).join('');
  dd.style.display = 'block';
}
function pickSrch(i) { if(_srchActs[i]){_srchActs[i].a();document.getElementById('srch').value='';hideDd();} }
function hideDd() { document.getElementById('srch-dd').style.display='none'; }

/* ═══ PAGE ROUTER ═══ */
function renderPage(p) {
  if (p==='pse')   return renderPSE();
  if (p==='wiki')  return WIKI_KEY ? renderArt() : renderWikiList();
  if (p==='learn') return renderLearn();
  if (p==='struc') return renderStruc();
  if (p==='rxn')   return renderRxn();
  if (p==='quiz')  return renderQuiz();
  return '';
}

/* ═══ SHARED RE-RENDER (for in-page nav) ═══ */
function rerender() {
  const panel = document.getElementById('content-panel');
  if (!panel) return;
  panel.innerHTML = renderPage(CURRENT_PAGE);
  if (CURRENT_PAGE === 'struc') initCanvas();
}

/* ═══ PSE ═══ */
function shellSVG(shells,sym,col) {
  if(!shells||!shells.length) return `<svg width="100" height="100"><text x="50" y="56" text-anchor="middle" font-size="22" fill="${col}" font-family="Fraunces,serif">${sym}</text></svg>`;
  const cx=50,cy=50;
  let s=`<svg width="100" height="100" viewBox="0 0 100 100">`;
  s+=`<circle cx="${cx}" cy="${cy}" r="10" fill="${col}" opacity=".9"/>`;
  s+=`<text x="${cx}" y="${cy+4}" text-anchor="middle" font-size="7" fill="#fff" font-family="DM Sans,sans-serif">${sym}</text>`;
  shells.forEach((n,i)=>{
    const r=12+(i+1)*9; if(r>48)return;
    s+=`<circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="${col}30" stroke-width="0.5"/>`;
    const max=Math.min(n,24);
    for(let j=0;j<max;j++){const a=2*Math.PI*j/max-Math.PI/2;s+=`<circle cx="${(cx+r*Math.cos(a)).toFixed(1)}" cy="${(cy+r*Math.sin(a)).toFixed(1)}" r="2.2" fill="${col}" opacity=".85"/>`;}
  });
  return s+'</svg>';
}

function renderPSE() {
  const cats=Object.keys(CATS);
  const ftags=['all',...cats].map(k=>{
    const col=k!=='all'?catCol(k):''; const on=PSE_FILTER===k;
    return `<div class="ptf${on?' on':''}" style="${on&&k!=='all'?'background:'+col+';color:#fff':''}" onclick="PSE_FILTER='${k}';rerender()">${k==='all'?'Alle':CATS[k].l}</div>`;
  }).join('');
  const legend=cats.map(k=>`<div class="leg" onclick="PSE_FILTER='${k}';rerender()"><div class="leg-dot" style="background:${catCol(k)}"></div>${CATS[k].l}</div>`).join('');
  let cells='';
  PT_ROWS.forEach(row=>{row.forEach(z=>{
    if(z===0){cells+=`<div style="min-height:27px"></div>`;return;}
    if(z<0){cells+=`<div class="el gap"></div>`;return;}
    const el=EL_MAP[z]; if(!el){cells+=`<div></div>`;return;}
    const col=catCol(el.c);
    const dim=PSE_FILTER!=='all'&&PSE_FILTER!==el.c;
    const isSel=PSE_SEL&&PSE_SEL.z===z;
    const hasD=!!EL_DETAIL[z];
    cells+=`<div class="el${dim?' dimmed':''}${isSel?' sel':''}" style="background:${catBg(el.c)};border-color:${catBdr(el.c)}"
      ${hasD?`onmouseenter="pHover(event,${z})" onmouseleave="pHoverOut()"`:''} onclick="${hasD?`pseSel(${z})`:''}" title="${el.n}">
      <div class="el-z" style="color:${col}">${z}</div>
      <div class="el-s" style="color:${col}">${el.s}</div>
      <div class="el-n" style="color:${col}">${el.n}</div>
    </div>`;
  });});
  const sel=PSE_SEL;
  const detailHtml=sel?buildElDetail(sel):`<div style="text-align:center;padding:20px;color:var(--t3);font-size:12.5px">Klicke auf ein farbiges Element für Details</div>`;
  return `<div class="page-hdr"><h1>🔬 Periodensystem</h1><p>Alle 118 Elemente – klicke auf ein Element für Details, Schalenmodell und Reaktionen.</p></div>
  <div class="pt-filter-row">${ftags}</div>
  <div class="pt-legend">${legend}</div>
  <div class="pt-scroll"><div class="ptable" style="grid-template-columns:repeat(18,1fr)">${cells}</div></div>
  ${sel?`<div class="pse-detail-wrap"><div class="pse-detail">${detailHtml}</div>
  <div class="pse-quick"><div style="font-size:11px;font-weight:500;color:var(--t3);margin-bottom:10px;text-transform:uppercase;letter-spacing:.06em">Kategorien</div>
  ${Object.entries(CATS).map(([k,v])=>`<div style="display:flex;align-items:center;gap:6px;padding:4px 0;border-bottom:0.5px solid var(--bdr);cursor:pointer" onclick="PSE_FILTER='${k}';rerender()"><div style="width:8px;height:8px;border-radius:2px;background:${v.bg};flex-shrink:0"></div><span style="font-size:11.5px;color:var(--t2)">${v.l}</span></div>`).join('')}
  </div></div>`:detailHtml}`;
}

function pseSel(z) { PSE_SEL=EL_MAP[z]; rerender(); }
function pHover(e,z) {
  const el=EL_MAP[z]; if(!el)return;
  const t=document.getElementById('tooltip');
  t.innerHTML=`<div style="display:flex;gap:7px;align-items:center;margin-bottom:4px"><div style="font-family:'Fraunces',serif;font-size:20px;color:${catCol(el.c)}">${el.s}</div><div><div style="font-weight:500">${el.n}</div><div style="font-size:10.5px;color:var(--t3)">Z=${el.z}${el.m?' · '+el.m+' u':''}</div></div></div><div style="font-size:11px;color:var(--t2)">${CATS[el.c]?.l||el.c} · ${el.ph}</div>${el.en!=null?`<div style="font-size:10.5px;color:var(--t3);margin-top:2px">EN: ${el.en}</div>`:''}`;
  const r=e.target.getBoundingClientRect();
  let left=r.right+6,top=r.top-4;
  if(left+200>window.innerWidth) left=r.left-210;
  t.style.left=left+'px'; t.style.top=top+'px'; t.classList.add('show');
}
function pHoverOut() { document.getElementById('tooltip').classList.remove('show'); }

function buildElDetail(el) {
  const col=catCol(el.c);
  return `<div class="pse-sym-row">
    <div class="pse-sym-box" style="background:${catBg(el.c)};border:0.5px solid ${catBdr(el.c)}">
      <div style="font-size:9px;opacity:.7;color:${col}">${el.z}</div>
      <div style="font-family:'Fraunces',serif;font-size:28px;line-height:1;color:${col}">${el.s}</div>
      <div style="font-size:7px;opacity:.6;color:${col}">${el.m?el.m+' u':'–'}</div>
    </div>
    <div><div style="font-family:'Fraunces',serif;font-size:17px;color:var(--t1);margin-bottom:3px">${el.n}</div>
    <div style="font-size:11.5px;color:var(--t2)">${CATS[el.c]?.l||el.c}<br>Periode ${el.p}${el.g?' · Gruppe '+el.g:''}<br>${el.ph}</div></div>
  </div>
  <div class="prop-grid">
    <div class="prop"><div class="prop-l">Ordnungszahl</div><div class="prop-v">${el.z}</div></div>
    <div class="prop"><div class="prop-l">Atommasse</div><div class="prop-v">${el.m?el.m+' u':'–'}</div></div>
    <div class="prop"><div class="prop-l">Konfig.</div><div class="prop-v" style="font-size:10px">${el.cfg||'–'}</div></div>
    <div class="prop"><div class="prop-l">Schmelzpunkt</div><div class="prop-v">${el.melt!=null?el.melt+' °C':'–'}</div></div>
    <div class="prop"><div class="prop-l">Siedepunkt</div><div class="prop-v">${el.boil!=null?el.boil+' °C':'–'}</div></div>
    <div class="prop"><div class="prop-l">Elektroneg.</div><div class="prop-v">${el.en!=null?el.en:'–'}</div></div>
  </div>
  <div class="dp-sec">Schalenmodell</div>
  <div class="shell-wrap">${shellSVG(el.shells,el.s,col)}</div>
  ${el.desc?`<div class="dp-sec">Beschreibung</div><div class="dp-desc">${el.desc}</div>`:''}
  ${el.key?`<div class="key-box">${el.key}</div>`:''}
  ${el.history?`<div class="dp-sec">📜 Geschichte & Entdeckung</div><div class="dp-desc" style="background:var(--acl);border:0.5px solid var(--acd);border-radius:8px;padding:10px 12px;line-height:1.7">${el.history}</div>`:''}
  ${el.rxn&&el.rxn.length?`<div class="dp-sec">Reaktionen</div>${el.rxn.map(r=>`<div class="rxn-item">${r}</div>`).join('')}`:''}
  ${el.cpd&&el.cpd.length?`<div class="dp-sec">Verbindungen</div><ul class="dp-list">${el.cpd.map(c=>`<li>${c}</li>`).join('')}</ul>`:''}
  ${el.uses?`<div class="dp-sec">Verwendung</div><div class="dp-desc">${el.uses}</div>`:''}
  ${el.warn?`<div class="warn-box">⚠️ <div><strong>Achtung:</strong> ${el.warn}</div></div>`:''}`;
}

/* ═══ WIKI ═══ */
function renderWikiList() {
  return `<div class="page-hdr"><h1>📚 Chemie-Wiki</h1><p>Ausführliche Artikel mit Formeln, Beispielen und Merksätzen.</p></div>
  <div class="wiki-grid">${Object.entries(WIKI).map(([k,a])=>`
    <div class="wiki-card" onclick="WIKI_KEY='${k}';rerender()">
      <div class="wiki-ico">${a.ico}</div>
      <div style="flex:1"><h3>${a.t}</h3><p>${a.desc}</p>
      <div class="wiki-tags">${a.tags.map(t=>`<span class="wiki-tag">${t}</span>`).join('')}</div></div>
      <i class="ti ti-chevron-right" style="color:var(--t3);font-size:14px;flex-shrink:0;margin-top:2px"></i>
    </div>`).join('')}</div>`;
}
function renderArt() {
  const a=WIKI[WIKI_KEY]; if(!a)return renderWikiList();
  return `<div style="display:inline-flex;align-items:center;gap:5px;font-size:12px;color:var(--t3);cursor:pointer;padding:4px 9px;border-radius:7px;margin-bottom:16px;transition:var(--tr)" onclick="WIKI_KEY=null;rerender()" onmouseover="this.style.background='var(--bg3)'" onmouseout="this.style.background=''"><i class="ti ti-arrow-left"></i> Zurück zur Übersicht</div>
  <div class="art">${a.html}</div>`;
}

/* ═══ LEARN ═══ */
function renderLearn() {
  return `<div class="page-hdr"><h1>🎓 Lernbereich</h1><p>PSE-Grundlagen einfach erklärt – für Schülerinnen und Schüler.</p></div>
  <div class="learn-card"><h3>🗓 Aufbau des Periodensystems</h3>
  <p>Das PSE ordnet alle 118 Elemente nach ihrer <strong>Ordnungszahl</strong>. Es hat <strong>7 Perioden</strong> (Zeilen) und <strong>18 Gruppen</strong> (Spalten).</p>
  <ul><li><strong>Periode:</strong> Anzahl der besetzten Elektronenschalen</li><li><strong>Gruppe:</strong> Gleiche Valenzelektronenzahl → ähnliche Eigenschaften</li><li><strong>Ordnungszahl = Protonenzahl = Elektronenzahl</strong></li></ul></div>
  <div class="learn-card"><h3>⚡ Wichtige Gruppen</h3>
  <table class="gt"><tr><th>Gruppe</th><th>Name</th><th>Valenz-e⁻</th><th>Beispiele</th></tr>
  <tr><td>1</td><td>Alkalimetalle</td><td>1</td><td>Li, Na, K</td></tr>
  <tr><td>2</td><td>Erdalkalimetalle</td><td>2</td><td>Mg, Ca, Ba</td></tr>
  <tr><td>17</td><td>Halogene</td><td>7</td><td>F, Cl, Br, I</td></tr>
  <tr><td>18</td><td>Edelgase</td><td>8 (stabil)</td><td>He, Ne, Ar</td></tr>
  <tr><td>3–12</td><td>Übergangsmetalle</td><td>variabel</td><td>Fe, Cu, Au</td></tr></table></div>
  <div class="learn-card"><h3>🔬 Metalle · Nichtmetalle · Halbmetalle</h3>
  <div class="type-grid">
    <div class="type-box"><div class="ticon">🔩</div><h4>Metalle</h4><p>Glänzend, leitfähig, formbar. ~80% aller Elemente.</p></div>
    <div class="type-box"><div class="ticon">💨</div><h4>Nichtmetalle</h4><p>Meist Gase, nicht leitfähig. Rechts im PSE.</p></div>
    <div class="type-box"><div class="ticon">⚡</div><h4>Halbmetalle</h4><p>Halbleiter: bedingt leitfähig (Si, Ge).</p></div>
  </div></div>
  <div class="learn-card"><h3>📈 Trends im PSE</h3>
  <ul><li><strong>EN →</strong> steigt von links nach rechts (höchste: F=3,98)</li>
  <li><strong>Atomradius →</strong> nimmt von links nach rechts ab</li>
  <li><strong>Reaktivität Metalle ↓</strong> steigt in einer Gruppe nach unten</li></ul></div>
  <div class="learn-card"><h3>💡 Merksätze</h3>
  <ul><li><em>„Periodenanzahl = Schalenanzahl"</em></li>
  <li><em>„Gruppennummer (HG) = Valenzelektronen"</em></li>
  <li><em>„Edelgase (Gr. 18) → volle Außenschale → unreaktiv"</em></li>
  <li><em>„OIL RIG: Oxidation Is Loss, Reduction Is Gain"</em></li></ul></div>`;
}

/* ═══ STRUKTURZEICHNER ═══ */
function renderStruc() {
  const cats=[...new Set(MOLECULES.map(m=>m.cat))];
  const molList=cats.map(cat=>`
    <div class="sl-cat">${cat}</div>
    ${MOLECULES.filter(m=>m.cat===cat).map(m=>`
      <button class="sl-mol" onclick='loadMol(${JSON.stringify(m)})'>
        <span class="sl-mol-ico">⬡</span>
        <span class="sl-mol-name">${m.name}<br><span class="sl-mol-f">${m.formula}</span></span>
      </button>`).join('')}`).join('');

  return `<div class="page-hdr" style="margin-bottom:12px"><h1>✏️ Strukturzeichner</h1><p>Zeichne Moleküle auf der Leinwand oder lade ein Preset aus der Bibliothek.</p></div>
  <div class="snew-wrap">

    <!-- LINKE SPALTE: Werkzeuge + Bibliothek -->
    <div class="snew-left">
      <div class="snew-sec-hd">WERKZEUGE</div>
      <div class="snew-atoms">
        <button class="snew-atom on" id="tbtn-C"  onclick="sTool('C')"  style="--ac:#546E7A"><span class="sa-pip" style="background:#546E7A"></span><div><div class="sa-sym">C</div><div class="sa-name">Kohlenstoff</div></div></button>
        <button class="snew-atom"    id="tbtn-H"  onclick="sTool('H')"  style="--ac:#1E88E5"><span class="sa-pip" style="background:#1E88E5"></span><div><div class="sa-sym">H</div><div class="sa-name">Wasserstoff</div></div></button>
        <button class="snew-atom"    id="tbtn-O"  onclick="sTool('O')"  style="--ac:#E53935"><span class="sa-pip" style="background:#E53935"></span><div><div class="sa-sym">O</div><div class="sa-name">Sauerstoff</div></div></button>
        <button class="snew-atom"    id="tbtn-N"  onclick="sTool('N')"  style="--ac:#43A047"><span class="sa-pip" style="background:#43A047"></span><div><div class="sa-sym">N</div><div class="sa-name">Stickstoff</div></div></button>
        <button class="snew-atom"    id="tbtn-S"  onclick="sTool('S')"  style="--ac:#FB8C00"><span class="sa-pip" style="background:#FB8C00"></span><div><div class="sa-sym">S</div><div class="sa-name">Schwefel</div></div></button>
        <button class="snew-atom"    id="tbtn-Cl" onclick="sTool('Cl')" style="--ac:#00897B"><span class="sa-pip" style="background:#00897B"></span><div><div class="sa-sym">Cl</div><div class="sa-name">Chlor</div></div></button>
      </div>
      <div class="snew-bonds">
        <button class="snew-bond" id="tbtn-b1"   onclick="sTool('b1')">─ Einfach</button>
        <button class="snew-bond" id="tbtn-b2"   onclick="sTool('b2')">═ Doppel</button>
        <button class="snew-bond" id="tbtn-b3"   onclick="sTool('b3')">≡ Dreifach</button>
        <button class="snew-bond" id="tbtn-move" onclick="sTool('move')">✥ Bewegen</button>
        <button class="snew-bond danger" id="tbtn-erase" onclick="sTool('erase')">✕ Löschen</button>
      </div>

      <div class="snew-sec-hd" style="margin-top:12px">BIBLIOTHEK</div>
      <div class="snew-lib">${molList}</div>
      <button class="snew-libadd">+ Eigene Bibliothek</button>
    </div>

    <!-- MITTLERE SPALTE: Leinwand -->
    <div class="snew-center">
      <div class="snew-toolbar">
        <button class="snew-tbtn${_S.grid?' on':''}" id="sbtn-grid" onclick="sGrid()" title="Raster">⊞</button>
        <button class="snew-tbtn${_S.snap?' on':''}" id="sbtn-snap" onclick="sSnap()" title="Einrasten">⊕</button>
        <button class="snew-tbtn" onclick="sAutoH()" title="H-Atome ergänzen">H⁺</button>
        <button class="snew-tbtn" onclick="sCenter()" title="Zentrieren">⊙</button>
        <button class="snew-tbtn" onclick="sUndo()" title="Rückgängig">↩</button>
        <button class="snew-tbtn danger" onclick="sClear()" title="Alles löschen">🗑</button>
        <span class="snew-mode-badge" id="s-mode">C-Atom</span>
      </div>
      <div class="snew-canvas-wrap"><canvas class="mol-canvas" id="mol-cv"></canvas></div>
      <div class="snew-tip" id="s-fbar">💡 Tipp: Klicke auf ein Atom, um es zu verändern. Ziehe, um die Ansicht zu bewegen.</div>
      <div class="snew-loadbar">
        <input id="s-fi" placeholder="Molekül: Ethanol, Benzol, CH4 …" autocomplete="off" onkeydown="if(event.key==='Enter')sLoad()">
        <button onclick="sLoad()">Laden</button>
      </div>
      <div class="snew-footer-chips" style="display:none"></div>
    </div>

    <!-- RECHTE SPALTE: Smart Suggestions + Molekül-Info -->
    <div class="snew-right">
      <div class="snew-sec-hd">SMART SUGGESTIONS</div>
      <div id="s-suggest" class="snew-suggestions"></div>

      <div class="snew-sec-hd" style="margin-top:14px">MOLEKÜL-INFO</div>
      <div id="s-info" class="snew-molinfo">
        <div style="font-size:12px;color:var(--t3);padding:8px 0">Noch kein Molekül gezeichnet.</div>
      </div>
    </div>

  </div>`;
}

function initCanvas(){
  const cv=document.getElementById('mol-cv'); if(!cv)return;
  const cont=cv.parentElement;
  function resize(){cv.width=cont.offsetWidth||420;cv.height=cont.offsetHeight||340;sDraw();}
  resize(); if(window._cvObs)window._cvObs.disconnect(); window._cvObs=new ResizeObserver(resize); window._cvObs.observe(cont);
  cv.onmousedown=e=>{
    const p=sPos(e,cv);_S.isDown=true;const hit=sNear(p.x,p.y);

    // BEWEGEN
    if(_S.tool==='move'){if(hit){sSaveU();_S.drag=hit;_S.dragOfs={x:p.x-hit.x,y:p.y-hit.y};cv.style.cursor='grabbing';}return;}

    // LÖSCHEN
    if(_S.tool==='erase'){
      if(hit){sSaveU();_S.bonds=_S.bonds.filter(b=>b.a!==hit&&b.b!==hit);_S.atoms=_S.atoms.filter(a=>a!==hit);}
      else{const bh=sNearB(p.x,p.y);if(bh){sSaveU();_S.bonds=_S.bonds.filter(b=>b!==bh);}}
      sDraw();sSuggest();return;
    }

    // BINDUNG ZEICHNEN (b1/b2/b3) — MIT VALENZ-CHECK
    if(['b1','b2','b3'].includes(_S.tool)){
      const ord=_S.tool==='b1'?1:_S.tool==='b2'?2:3;
      if(hit){
        if(!_S.sel){_S.sel=hit;}
        else if(_S.sel!==hit){
          const fA=sFreeVal(_S.sel),fB=sFreeVal(hit);
          if(fA>=ord&&fB>=ord){
            sSaveU();
            const ex=_S.bonds.find(b=>(b.a===_S.sel&&b.b===hit)||(b.b===_S.sel&&b.a===hit));
            if(ex)ex.order=ord;else _S.bonds.push({a:_S.sel,b:hit,order:ord});
          } else {
            const fb=document.getElementById('s-fbar');
            if(fb)fb.innerHTML=`<span style="color:#e53935">⚠ Valenz überschritten: ${_S.sel.s} (${fA} frei) ↔ ${hit.s} (${fB} frei)</span>`;
          }
          _S.sel=null;sDraw();sSuggest();
        } else {_S.sel=null;}
        sDraw();
      }
      return;
    }

    // ATOM PLATZIEREN — MIT AUTO-BINDUNG ZUM NÄCHSTEN FREIEN ATOM
    if(!['C','H','O','N','S','Cl','F','P','B'].includes(_S.tool))return;
    const sym=_S.tool;
    if(hit){
      // Auf bestehendes Atom geklickt → Element wechseln
      if(hit.s!==sym){sSaveU();hit.s=sym;}
      sDraw();sSuggest();return;
    }
    sSaveU();
    const sn=sSnapA(p.x,p.y)||sSnapG(p.x,p.y);
    const na={s:sym,...sn};
    _S.atoms.push(na);
    // Auto-Verbinden: nächstes Atom mit freier Valenz (respektiert Chemie)
    const myMax=MAX_VAL[sym]||0;
    if(myMax>0){
      const near=sNearFree(na.x,na.y,na,1);
      if(near&&!_S.bonds.find(b=>(b.a===near&&b.b===na)||(b.b===near&&b.a===na))){
        _S.bonds.push({a:near,b:na,order:1});
      }
    }
    sDraw();sSuggest();
  };
  cv.onmousemove=e=>{const p=sPos(e,cv);_S.mouse=p;_S.hover=sNear(p.x,p.y);if(_S.drag&&_S.isDown){_S.drag.x=p.x-_S.dragOfs.x;_S.drag.y=p.y-_S.dragOfs.y;}sDraw();};
  cv.onmouseup=()=>{_S.drag=null;_S.isDown=false;cv.style.cursor=_S.tool==='move'?'grab':'crosshair';};
  cv.onmouseleave=()=>{_S.drag=null;_S.hover=null;_S.isDown=false;sDraw();};
  sDraw();sSuggest();
}
function sPos(e,cv){const r=cv.getBoundingClientRect();return{x:(e.clientX-r.left)*cv.width/r.width,y:(e.clientY-r.top)*cv.height/r.height};}
function sNear(x,y){for(let i=_S.atoms.length-1;i>=0;i--){const a=_S.atoms[i];if(Math.hypot(a.x-x,a.y-y)<=(ATOM_R[a.s]||14)+5)return a;}return null;}
function sNearB(x,y){for(const b of _S.bonds){const mx=(b.a.x+b.b.x)/2,my=(b.a.y+b.b.y)/2;if(Math.hypot(mx-x,my-y)<14)return b;}return null;}
function sSnapG(x,y){if(!_S.snap)return{x,y};const g=26;return{x:Math.round(x/g)*g,y:Math.round(y/g)*g};}
function sSnapA(x,y){if(!_S.snap)return null;const BL=52;for(const a of _S.atoms){const d=Math.hypot(a.x-x,a.y-y);if(d>2&&d<BL*1.4){const ang=Math.atan2(y-a.y,x-a.x);return{x:a.x+BL*Math.cos(ang),y:a.y+BL*Math.sin(ang)};}}return null;}
function sSaveU(){_S.undoStack.push(JSON.stringify({atoms:_S.atoms.map((a,i)=>({...a})),bonds:_S.bonds.map(b=>({order:b.order,ai:_S.atoms.indexOf(b.a),bi:_S.atoms.indexOf(b.b)}))}))}
function sUndo(){if(!_S.undoStack.length)return;const sn=JSON.parse(_S.undoStack.pop());const na=sn.atoms.map(a=>({...a}));_S.atoms=na;_S.bonds=sn.bonds.map(b=>({...b,a:na[b.ai],b:na[b.bi]}));_S.sel=null;sDraw();sSuggest();}
function sTool(t){_S.tool=t;_S.sel=null;
  // Clear all tool buttons (both old and new classes)
  document.querySelectorAll('.tbtn,.snew-atom,.snew-bond').forEach(b=>b.classList.remove('on'));
  const tb=document.getElementById('tbtn-'+t);if(tb)tb.classList.add('on');
  const cv=document.getElementById('mol-cv');if(cv)cv.style.cursor=t==='move'?'grab':t==='erase'?'not-allowed':'crosshair';
  const mb=document.getElementById('s-mode');if(mb)mb.textContent={C:'C-Atom',H:'H-Atom',O:'O-Atom',N:'N-Atom',S:'S-Atom',Cl:'Cl-Atom',b1:'Einfachbindung',b2:'Doppelbindung',b3:'Dreifachbindung',move:'Bewegen',erase:'Löschen'}[t]||t;
  sDraw();
}
function sGrid(){_S.grid=!_S.grid;document.getElementById('sbtn-grid')?.classList.toggle('on',_S.grid);sDraw();}
function sSnap(){_S.snap=!_S.snap;document.getElementById('sbtn-snap')?.classList.toggle('on',_S.snap);}
function sClear(){sSaveU();_S.atoms=[];_S.bonds=[];_S.sel=null;sDraw();sSuggest();}
function sCenter(){if(!_S.atoms.length)return;const cv=document.getElementById('mol-cv');if(!cv)return;const mx=_S.atoms.reduce((s,a)=>s+a.x,0)/_S.atoms.length,my=_S.atoms.reduce((s,a)=>s+a.y,0)/_S.atoms.length;const ox=cv.width/2-mx,oy=cv.height/2-my;_S.atoms.forEach(a=>{a.x+=ox;a.y+=oy;});sDraw();}
function sAutoH(){sSaveU();_S.atoms.forEach(a=>{const mv=MAX_VAL[a.s];if(!mv)return;const bv=_S.bonds.filter(b=>b.a===a||b.b===a).reduce((s,b)=>s+b.order,0);const need=mv-bv;if(need<=0)return;const exA=_S.bonds.filter(b=>b.a===a||b.b===a).map(b=>Math.atan2((b.a===a?b.b.y-a.y:b.a.y-a.y),(b.a===a?b.b.x-a.x:b.a.x-a.x)));for(let i=0;i<need;i++){let best=(i+0.5)*Math.PI*2/need;let maxD=0;for(let t=0;t<24;t++){const ta=t*Math.PI/12;const d=exA.reduce((m,ea)=>Math.min(m,Math.abs(ta-ea)),Math.PI);if(d>maxD){maxD=d;best=ta;}}const h={s:'H',x:a.x+34*Math.cos(best),y:a.y+34*Math.sin(best)};_S.atoms.push(h);_S.bonds.push({a,b:h,order:1});}});sDraw();sSuggest();}
function sDraw(){
  const cv=document.getElementById('mol-cv');if(!cv)return;
  const ctx=cv.getContext('2d');const W=cv.width,H=cv.height;
  ctx.clearRect(0,0,W,H);ctx.fillStyle=DARK?'#1a1a17':'#ffffff';ctx.fillRect(0,0,W,H);
  if(_S.grid){const g=26;ctx.strokeStyle=DARK?'#2a2a27':'#e8e5df';ctx.lineWidth=0.5;for(let x=0;x<W;x+=g){ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,H);ctx.stroke();}for(let y=0;y<H;y+=g){ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(W,y);ctx.stroke();}}
  if(_S.atoms.length===0){ctx.fillStyle='#c8c5be';ctx.font='12px DM Sans,sans-serif';ctx.textAlign='center';ctx.textBaseline='middle';ctx.fillText('Werkzeug wählen → klicken oder Molekül laden',W/2,H/2);return;}
  if(['b1','b2','b3'].includes(_S.tool)&&_S.sel){ctx.strokeStyle='#a8d5c0';ctx.lineWidth=1.2;ctx.setLineDash([4,3]);ctx.beginPath();ctx.moveTo(_S.sel.x,_S.sel.y);ctx.lineTo(_S.mouse.x||_S.sel.x,_S.mouse.y||_S.sel.y);ctx.stroke();ctx.setLineDash([]);}
  _S.bonds.forEach(b=>{const dx=b.b.x-b.a.x,dy=b.b.y-b.a.y,len=Math.hypot(dx,dy);if(len<1)return;const nx=-dy/len,ny=dx/len;ctx.strokeStyle=DARK?'#9a9690':'#4a4840';ctx.lineWidth=1.8;ctx.lineCap='round';const offs=b.order===1?[0]:b.order===2?[-4,4]:[-6,0,6];offs.forEach(o=>{ctx.beginPath();ctx.moveTo(b.a.x+nx*o,b.a.y+ny*o);ctx.lineTo(b.b.x+nx*o,b.b.y+ny*o);ctx.stroke();});});
  if(_S.sel){ctx.strokeStyle='#4CAF5099';ctx.lineWidth=2;ctx.setLineDash([3,3]);ctx.beginPath();ctx.arc(_S.sel.x,_S.sel.y,(ATOM_R[_S.sel.s]||14)+5,0,2*Math.PI);ctx.stroke();ctx.setLineDash([]);}
  _S.atoms.forEach(a=>{const r=ATOM_R[a.s]||14;const col=ATOM_COLORS[a.s]||'#888';const isH=a===_S.hover,isSel=a===_S.sel;ctx.beginPath();ctx.arc(a.x,a.y,r,0,2*Math.PI);ctx.fillStyle=isSel?col+'55':(isH?col+'40':col+'25');ctx.fill();ctx.strokeStyle=isSel?'#43A047':col;ctx.lineWidth=isSel?2:(isH?2:1.5);ctx.stroke();ctx.fillStyle=DARK?'#f0ece4':col;ctx.font=`500 ${a.s.length>1?9.5:12}px DM Sans,sans-serif`;ctx.textAlign='center';ctx.textBaseline='middle';ctx.fillText(a.s,a.x,a.y);});
  const ct={};_S.atoms.forEach(a=>{ct[a.s]=(ct[a.s]||0)+1;});
  const order=['C','H','N','O','S','Cl','F','P','B'];
  const f=order.filter(e=>ct[e]).map(e=>`${e}${ct[e]>1?ct[e]:''}`).join('')+Object.keys(ct).filter(e=>!order.includes(e)).map(e=>`${e}${ct[e]>1?ct[e]:''}`).join('');
  const mw=Object.entries(ct).reduce((s,[el,n])=>s+n*({'H':1,'C':12,'O':16,'N':14,'S':32,'Cl':35.5,'F':19,'P':31,'B':10.8}[el]||10),0);
  const molName=sMolName(f);
  const fb=document.getElementById('s-fbar');
  if(fb)fb.innerHTML=`${molName?`<strong style="color:var(--acc)">${molName}</strong> &nbsp;`:''}<strong style="font-family:monospace">${f||'–'}</strong> &nbsp;<span style="color:var(--t3)">${_S.atoms.length} Atome · ${_S.bonds.length} Bindungen · M≈${mw.toFixed(1)} g/mol</span>`;
  const si=document.getElementById('s-info');
  if(si&&_S.atoms.length){
    si.innerHTML=
      (molName?`<div style="font-size:14px;font-weight:600;color:var(--acc);margin-bottom:6px">✅ ${molName}</div>`:`<div style="font-size:12px;color:var(--t3);margin-bottom:6px">Unbekannte Verbindung</div>`)+
      `<div class="snew-info-row"><span class="snew-info-lbl">Summenformel</span><span class="snew-info-val">${f||'–'}</span></div>`+
      ['C','H','O','N','S','Cl'].filter(e=>ct[e]).map(e=>`<div class="snew-info-row"><span class="snew-info-lbl">${e}-Atome</span><span class="snew-info-val">${ct[e]}</span></div>`).join('')+
      `<div class="snew-info-row"><span class="snew-info-lbl">Atome gesamt</span><span class="snew-info-val">${_S.atoms.length}</span></div>`+
      `<div class="snew-info-row"><span class="snew-info-lbl">Bindungen</span><span class="snew-info-val">${_S.bonds.length}</span></div>`+
      `<div class="snew-info-row"><span class="snew-info-lbl">Molmasse</span><span class="snew-info-val">${mw.toFixed(2)} g/mol</span></div>`;
  } else if(si){
    si.innerHTML='<div style="font-size:12px;color:var(--t3);padding:8px 0">Noch kein Molekül gezeichnet.</div>';
  }
}
const _SG={empty:[{i:'⚗',t:'Starte mit C',d:'C ist das Grundgerüst organischer Moleküle.',hl:true,a:null}],singleC:[{i:'➕',t:'Kette verlängern',d:'Weiteres C → Ethan',a:'loadMol(MOLECULES.find(m=>m.name==="Ethan"))'},{i:'🔴',t:'O anfügen',d:'→ Alkohol/Keton',a:null},{i:'🔵',t:'H ergänzen',d:'Methyl vervollständigen',a:'sAutoH()'}],twoC:[{i:'➕',t:'H ergänzen',d:'→ Ethan vollständig',a:'sAutoH()'},{i:'⬡',t:'Doppelbindung',d:'C=C → Ethen',a:"sTool('b2')"}],threeC:[{i:'➕',t:'H ergänzen',d:'→ Propan',a:'sAutoH()'},{i:'🔴',t:'C=O',d:'→ Aldehyd/Säure',a:"sTool('b2')"}],hasO:[{i:'🔵',t:'OH vervollst.',d:'O+H → OH-Gruppe',a:"sTool('H')"},{i:'🔴',t:'C=O',d:'Carbonylgruppe',a:"sTool('b2')"}],hasDouble:[{i:'🔵',t:'Addition möglich',d:'Doppelbindungen sind reaktiv',a:null},{i:'⬡',t:'Benzol laden',d:'Aromatischer Ring',a:"loadMol(MOLECULES.find(m=>m.name==='Benzol'))"}],complete:[{i:'✅',t:'Valenz gesättigt',d:'Alle Atome haben max. Valenz.',hl:true,a:null}]};
function sSuggest(){const sp=document.getElementById('s-suggest');if(!sp)return;let key='empty';if(_S.atoms.length){const cs=_S.atoms.filter(a=>a.s==='C').length;const hasO=_S.atoms.some(a=>a.s==='O');const hasD=_S.bonds.some(b=>b.order>=2);const allSat=_S.atoms.every(a=>{const mv=MAX_VAL[a.s];if(!mv)return true;return _S.bonds.filter(b=>b.a===a||b.b===a).reduce((s,b)=>s+b.order,0)>=mv;});if(allSat&&_S.atoms.length>4)key='complete';else if(hasD)key='hasDouble';else if(hasO)key='hasO';else if(cs>=3)key='threeC';else if(cs===2)key='twoC';else if(cs===1)key='singleC';}sp.innerHTML=(_SG[key]||[]).map(s=>`<div class="suggest-card${s.hl?' hl':''}"${s.a?` onclick="${s.a}"`:''}><div class="sc-hd"><div class="sc-ico">${s.i}</div><div class="sc-title">${s.t}</div></div><div class="sc-desc">${s.d}</div>${s.a?'<div style="font-size:10.5px;color:var(--acc);margin-top:4px">↗ Anwenden</div>':''}</div>`).join('');}
function loadMol(mol){if(!mol)return;sSaveU();_S.atoms=[];_S.bonds=[];_S.sel=null;const cv=document.getElementById('mol-cv');const W=cv?cv.width:400,H=cv?cv.height:300,cx=W/2,cy=H/2;if(mol.glucose){const rr=68,cs=[];for(let i=0;i<6;i++){const a=i*Math.PI/3-Math.PI/2;cs.push({s:'C',x:cx+rr*Math.cos(a),y:cy+rr*Math.sin(a)});}_S.atoms=[...cs];for(let i=0;i<6;i++)_S.bonds.push({a:cs[i],b:cs[(i+1)%6],order:1});[{s:'O',idx:0,dx:0,dy:-52},{s:'O',idx:1,dx:44,dy:-28},{s:'O',idx:2,dx:44,dy:28},{s:'O',idx:3,dx:0,dy:52},{s:'C',idx:4,dx:-44,dy:28}].forEach(({s,idx,dx,dy})=>{const ra=cs[idx];const na={s,x:ra.x+dx,y:ra.y+dy};_S.atoms.push(na);_S.bonds.push({a:ra,b:na,order:1});});sDraw();sSuggest();return;}if(mol.ring6){const r=58,cs=[];for(let i=0;i<6;i++){const a=i*Math.PI/3-Math.PI/2;cs.push({s:'C',x:cx+r*Math.cos(a),y:cy+r*Math.sin(a)});}_S.atoms=[...cs];for(let i=0;i<6;i++)_S.bonds.push({a:cs[i],b:cs[(i+1)%6],order:i%2===0?2:1});for(let i=0;i<6;i++){const a=i*Math.PI/3-Math.PI/2;const h={s:'H',x:cx+(r+30)*Math.cos(a),y:cy+(r+30)*Math.sin(a)};_S.atoms.push(h);_S.bonds.push({a:cs[i],b:h,order:1});}sDraw();sSuggest();return;}const sc=Math.min((W-80)/(mol.atoms.reduce((m,a)=>Math.max(m,Math.abs(a.x)),0.1)*2+20),(H-60)/(mol.atoms.reduce((m,a)=>Math.max(m,Math.abs(a.y)),0.1)*2+20),1.6);_S.atoms=mol.atoms.map(({s,x,y})=>({s,x:cx+x*sc,y:cy+y*sc}));_S.bonds=mol.bonds.map(([ai,bi,ord])=>({a:_S.atoms[ai],b:_S.atoms[bi],order:ord}));sDraw();sSuggest();}
function sLoad(){const v=document.getElementById('s-fi')?.value.trim().toUpperCase().replace(/\s/g,'');if(!v)return;const map={'METHANOL':'Methanol','ETHANOL':'Ethanol','ETHAN':'Ethan','METHAN':'Methan','PROPAN':'Propan','ETHEN':'Ethen','ETHIN':'Ethin','BENZOL':'Benzol','ACETON':'Aceton','GLUCOSE':'Glucose','HARNSTOFF':'Harnstoff','CH4':'Methan','C2H6':'Ethan','C3H8':'Propan','C2H4':'Ethen','C2H2':'Ethin','C6H6':'Benzol','CH3OH':'Methanol','C2H5OH':'Ethanol','C6H12O6':'Glucose'};const mol=MOLECULES.find(m=>m.name.toUpperCase()===v||m.name===(map[v]||''));if(mol){loadMol(mol);document.getElementById('s-fi').value='';}}

/* ═══ REAKTIONSRECHNER ═══ */
function renderRxn(){
  const cats=[...new Set(RXN_DB.map(r=>r.cat))];
  if(!RXN_CAT)RXN_CAT=cats[0];
  const exs=RXN_DB.filter(r=>r.cat===RXN_CAT);
  return `<div class="page-hdr"><h1>⚖️ Reaktionsrechner</h1><p>23 Reaktionen · Oxidationszahlen · Enthalpie · Schritt-Erklärung</p></div>
  <div class="rxn-wrap"><div>
    <div class="rxn-in-row"><input class="inp" id="rxn-in" placeholder="z.B. Fe + O2 → Fe2O3" style="font-family:monospace" onkeydown="if(event.key==='Enter')rxnGo()"><button class="btn pri" onclick="rxnGo()">Ausgleichen</button></div>
    <div class="cat-tabs">${cats.map(c=>`<div class="cat-tab${c===RXN_CAT?' on':''}" onclick="RXN_CAT='${c}';rerender()">${c}</div>`).join('')}</div>
    <div class="ex-grid">${exs.map(r=>`<button class="ex-btn" onclick="document.getElementById('rxn-in').value='${r.eq}';rxnGo()"><span style="font-weight:500;color:var(--t1);font-family:inherit">${r.name}</span><br>${r.eq}</button>`).join('')}</div>
  </div>
  <div class="rxn-right" id="rxn-out"><div class="rxn-empty"><i class="ti ti-flask"></i><p>Gleichung eingeben oder Beispiel wählen.</p></div></div></div>`;
}
function rxnGo(){
  const raw=document.getElementById('rxn-in')?.value.trim();if(!raw)return;
  const norm=raw.replace(/\s/g,'').toLowerCase().replace(/[→=>-]+/g,'→');
  const match=RXN_DB.find(r=>r.eq.replace(/\s/g,'').toLowerCase().replace(/[→=>-]+/g,'→')===norm)||RXN_DB.find(r=>raw.toLowerCase().split(/[\s→=+]+/).some(w=>w.length>1&&r.eq.toLowerCase().includes(w)));
  const out=document.getElementById('rxn-out');if(!out)return;
  if(!match){out.innerHTML=`<div class="rxn-empty"><i class="ti ti-search-off"></i><p>Nicht gefunden. Bitte ein Beispiel wählen.</p></div>`;return;}
  const oxRows=match.ox.map(o=>`<div class="ox-row"><span class="ox-el">${o.el}</span><span style="color:var(--t3)">:</span><span>${o.from}</span><span style="color:var(--t3)">→</span><span>${o.to}</span><span class="ox-chg ${o.t==='ox'?'ox-ox':o.t==='rd'?'ox-rd':'ox-neu'}">${o.t==='ox'?'Oxidation':o.t==='rd'?'Reduktion':'unverändert'}</span></div>`).join('');
  out.innerHTML=`<div class="rxn-result"><div style="font-size:10.5px;color:var(--t3);margin-bottom:3px">Ausgeglichene Gleichung:</div><div class="rxn-eq">${match.bal}</div>
  <div class="rxn-tags"><span class="tag tag-g">${match.cat}</span><span class="tag tag-b">${match.name}</span>${match.dh?`<span class="tag tag-a">ΔH=${match.dh}</span>`:''}</div>
  <div style="font-size:11px;font-weight:500;color:var(--t2);margin-bottom:6px">Ausgleichsschritte:</div>${match.steps.map((s,i)=>`<div class="step"><span class="step-n">${i+1}.</span>${s}</div>`).join('')}
  <div class="ox-box"><div class="ox-title">Oxidationszahlen</div>${oxRows}</div>
  ${match.dh?`<div class="dh-box">ΔH=${match.dh} — ${match.dh.startsWith('+')?'endotherm':'exotherm'}</div>`:''}</div>`;
}

/* ═══ QUIZ ═══ */
function renderQuiz(){if(!QZ.mode)return renderQuizStart();if(QZ.done)return renderQuizResult();return renderQuizQ();}
function renderQuizStart(){return `<div class="page-hdr"><h1>🧠 Chemie-Quiz</h1><p>Teste dein Wissen in drei Kategorien.</p></div><div class="quiz-mode-grid"><div class="quiz-mode" onclick="QZ={mode:'quiz',cat:'elements',q:0,score:0,answered:false,done:false};rerender()"><div class="qm-ico">⚗</div><h3>Elemente</h3><p>Symbole, Ordnungszahlen, Eigenschaften</p></div><div class="quiz-mode" onclick="QZ={mode:'quiz',cat:'reactions',q:0,score:0,answered:false,done:false};rerender()"><div class="qm-ico">⚡</div><h3>Reaktionen</h3><p>Verbrennung, Redox, Neutralisation</p></div><div class="quiz-mode" onclick="QZ={mode:'quiz',cat:'theory',q:0,score:0,answered:false,done:false};rerender()"><div class="qm-ico">📚</div><h3>Theorie</h3><p>PSE-Aufbau, Bindungsarten, Trends</p></div></div>`;}
function renderQuizQ(){const qs=QUIZ_Q[QZ.cat];const q=qs[QZ.q];const total=qs.length;const prog=Math.round((QZ.q/total)*100);let elHint='';if(q.el){const el=EL_MAP[q.el];if(el)elHint=`<div class="quiz-element-hint" style="background:${catBg(el.c)};border:0.5px solid ${catBdr(el.c)};color:${catCol(el.c)}"><div class="quiz-el-z">${el.z}</div><div class="quiz-el-s">${el.s}</div><div class="quiz-el-m">${el.m?el.m+' u':'–'}</div></div>`;}
return `<div class="quiz-wrap"><div class="quiz-progress"><div class="quiz-progress-bar" style="width:${prog}%"></div></div><div class="quiz-card"><div class="quiz-q-num">Frage ${QZ.q+1}/${total} · ${QZ.cat==='elements'?'Elemente':QZ.cat==='reactions'?'Reaktionen':'Theorie'}</div>${elHint}<div class="quiz-q">${q.q}</div><div class="quiz-answers">${q.answers.map((a,i)=>`<button class="qa" id="qa-${i}" onclick="quizAns(${i})">${a}</button>`).join('')}</div><div class="quiz-feedback" id="qfb"></div></div><div class="quiz-nav"><div class="quiz-score-label">Punkte: ${QZ.score}/${QZ.q}</div><button class="btn${QZ.answered?' pri':''}" id="qnext" onclick="quizNext()" ${QZ.answered?'':'disabled'} style="${QZ.answered?'':'opacity:.4'}">Nächste Frage →</button></div></div>`;}
function quizAns(idx){if(QZ.answered)return;QZ.answered=true;const q=QUIZ_Q[QZ.cat][QZ.q];const isRight=idx===q.correct;if(isRight)QZ.score++;document.querySelectorAll('.qa').forEach((b,i)=>{b.disabled=true;if(i===q.correct)b.classList.add('correct');else if(i===idx&&!isRight)b.classList.add('wrong');});const fb=document.getElementById('qfb');if(fb){fb.textContent=(isRight?'✓ Richtig! ':'✗ Falsch. ')+q.exp;fb.className='quiz-feedback show '+(isRight?'correct':'wrong');}const nxt=document.getElementById('qnext');if(nxt){nxt.disabled=false;nxt.style.opacity='1';nxt.classList.add('pri');}}
function quizNext(){const qs=QUIZ_Q[QZ.cat];if(QZ.q+1>=qs.length){QZ.done=true;rerender();return;}QZ.q++;QZ.answered=false;rerender();}
function renderQuizResult(){const qs=QUIZ_Q[QZ.cat];const total=qs.length;const pct=Math.round(QZ.score/total*100);const stars=pct>=90?'⭐⭐⭐':pct>=70?'⭐⭐':pct>=50?'⭐':'';const msg=pct>=90?'Ausgezeichnet!':pct>=70?'Sehr gut!':pct>=50?'Gut – weiter üben!':'Weiter üben!';return `<div class="quiz-wrap"><div class="quiz-result"><div class="quiz-stars">${stars}</div><h2>${msg}</h2><div class="quiz-score-big">${QZ.score}/${total}</div><p>${pct}% korrekt</p><div style="display:flex;gap:8px;justify-content:center;flex-wrap:wrap"><button class="btn pri" onclick="QZ={mode:'quiz',cat:'${QZ.cat}',q:0,score:0,answered:false,done:false};rerender()">Nochmal</button><button class="btn" onclick="QZ.mode=null;QZ.done=false;rerender()">Kategorie wählen</button></div></div></div>`;}

/* ═══ HINT AUTO-HIDE ═══ */
setTimeout(()=>{const h=document.getElementById('zoom-hint');if(h)h.classList.add('hidden');},10000);



// ════════════════════════════════════════════════════════════════
// INFINITY SCROLL ENGINE
// ════════════════════════════════════════════════════════════════
let _scrollY = 0, _scrollTarget = 0, _scrollRaf = null;
let _transitioning = false, _highlightIdx = -1, _edgeAccum = 0;
const MODULES_ORDER = ['pse','wiki','learn','struc','rxn','quiz','info'];
const MODULE_NAMES = ['Periodensystem','Chemie-Wiki','Lernbereich','Strukturzeichner','Reaktionsrechner','Quiz','Info & Impressum'];

function _goNext() {
  if (_transitioning) return;
  _transitioning = true; setTimeout(function(){ _transitioning = false; }, 900);
  var idx = MODULES_ORDER.indexOf(CURRENT_PAGE);
  if (idx === -1) { _resetHS(); zoomTo(MODULES_ORDER[0]); }
  else if (idx < MODULES_ORDER.length - 1) { zoomTo(MODULES_ORDER[idx + 1]); }
  else { zoomHome(); }
}
function _goPrev() {
  if (_transitioning) return;
  _transitioning = true; setTimeout(function(){ _transitioning = false; }, 900);
  var idx = MODULES_ORDER.indexOf(CURRENT_PAGE);
  if (idx === -1) { _resetHS(); zoomTo(MODULES_ORDER[MODULES_ORDER.length - 1]); }
  else if (idx === 0) { zoomHome(); }
  else { zoomTo(MODULES_ORDER[idx - 1]); }
}
function _resetHS() {
  _scrollY = 0; _scrollTarget = 0; _highlightIdx = -1;
  if (_scrollRaf) { cancelAnimationFrame(_scrollRaf); _scrollRaf = null; }
  document.querySelectorAll('.module-orbit').forEach(function(m){ m.style.transform=''; m.style.boxShadow=''; m.style.borderColor=''; });
  document.querySelectorAll('.sp-dot').forEach(function(d){ d.classList.remove('active'); });
}
function _navDots(page) {
  var sp = document.getElementById('scroll-progress');
  var dots = document.querySelectorAll('.sp-dot');
  if (!sp) return;
  if (!page || page === 'home') { sp.className = 'on-home'; dots.forEach(function(d){ d.classList.remove('active'); }); }
  else { sp.className = 'on-module'; var idx = MODULES_ORDER.indexOf(page); dots.forEach(function(d,i){ d.classList.toggle('active', i === idx); }); }
}
function _panelEdge(dir) {
  var p = document.getElementById('content-panel');
  if (!p) return dir > 0 ? 'bottom' : 'top';
  if (dir > 0) return (p.scrollTop + p.clientHeight >= p.scrollHeight - 4) ? 'bottom' : 'middle';
  return p.scrollTop <= 4 ? 'top' : 'middle';
}
document.addEventListener('wheel', function(e) {
  var delta = e.deltaMode === 1 ? e.deltaY * 30 : e.deltaY;
  if (CURRENT_PAGE === 'home') {
    e.preventDefault();
    _scrollTarget += delta * 0.8;
    _scrollTarget = Math.max(-200, Math.min(_scrollTarget, MODULES_ORDER.length * 180 + 60));
    if (_scrollTarget < -160 && !_transitioning) { _scrollTarget = 0; _scrollY = 0; _goPrev(); return; }
    if (!_scrollRaf) _scrollRaf = requestAnimationFrame(_scrollTick);
    return;
  }
  var edge = _panelEdge(delta);
  if (edge === 'middle') { _edgeAccum = 0; return; }
  e.preventDefault();
  _edgeAccum += Math.abs(delta);
  if (_edgeAccum >= 180) { _edgeAccum = 0; if (delta > 0) _goNext(); else _goPrev(); }
}, { passive: false, capture: true });

function _scrollTick() {
  _scrollY += (_scrollTarget - _scrollY) * 0.12;
  if (Math.abs(_scrollTarget - _scrollY) < 0.4) _scrollY = _scrollTarget;
  var world = document.getElementById('zoom-world');
  var modules = document.querySelectorAll('.module-orbit');
  var hint = document.getElementById('zoom-hint');
  var dots = document.querySelectorAll('.sp-dot');
  if (_scrollY <= 0) {
    _scrollY = 0;
    world.style.transform = 'scale(1) translateZ(0)';
    _highlightIdx = -1;
    modules.forEach(function(m){ m.style.transform=''; m.style.boxShadow=''; m.style.borderColor=''; });
    if (hint) { hint.textContent = '\u2193 Scrollen zum Einzoomen \u00b7 Klick auf Kachel zum \u00d6ffnen'; hint.classList.remove('hidden'); }
    _navDots('home'); _scrollRaf = null; return;
  }
  var zl = 1 + Math.min(_scrollY / 3000, 0.4);
  var tz = Math.min(_scrollY / 8, 60);
  world.style.transform = 'scale(' + zl + ') translateZ(' + tz + 'px)';
  var idx = Math.floor(_scrollY / 180);
  var frac = (_scrollY % 180) / 180;
  var ci = Math.min(idx, MODULES_ORDER.length - 1);
  if (ci !== _highlightIdx) {
    modules.forEach(function(m){ m.style.transform=''; m.style.boxShadow=''; m.style.borderColor=''; });
    if (modules[ci]) { modules[ci].style.transform='translateY(-8px) scale(1.06)'; modules[ci].style.boxShadow='0 12px 40px rgba(26,92,58,.25)'; modules[ci].style.borderColor='var(--acd)'; }
    _highlightIdx = ci;
    if (hint) { hint.textContent = '\u21b5 Enter oder Klick \u2192 ' + MODULE_NAMES[ci]; hint.classList.remove('hidden'); }
    dots.forEach(function(d,i){ d.classList.toggle('active', i === ci); });
  }
  if (frac > 0.88 && !_transitioning && idx < MODULES_ORDER.length) { _resetHS(); zoomTo(MODULES_ORDER[idx]); return; }
  if (Math.abs(_scrollTarget - _scrollY) > 0.1) _scrollRaf = requestAnimationFrame(_scrollTick);
  else _scrollRaf = null;
}

// Touch
var _ty=0,_tly=0,_tea=0;
document.addEventListener('touchstart', function(e){ _ty=e.touches[0].clientY; _tly=_ty; _tea=0; },{passive:true});
document.addEventListener('touchmove', function(e){
  var dy=_tly-e.touches[0].clientY; _tly=e.touches[0].clientY;
  if(CURRENT_PAGE==='home'){ _scrollTarget+=dy*1.5; _scrollTarget=Math.max(-200,Math.min(_scrollTarget,MODULES_ORDER.length*180+60)); if(!_scrollRaf) _scrollRaf=requestAnimationFrame(_scrollTick); return; }
  var edge=_panelEdge(dy); if(edge==='middle'){_tea=0;return;} _tea+=Math.abs(dy); if(_tea>=80){_tea=0;if(dy>0)_goNext();else _goPrev();}
},{passive:true});
document.addEventListener('touchend', function(){
  if(CURRENT_PAGE!=='home') return;
  _scrollTarget=Math.max(0,Math.round(_scrollTarget/180))*180;
  if(!_scrollRaf) _scrollRaf=requestAnimationFrame(_scrollTick);
},{passive:true});
window.addEventListener('keydown', function(e){
  if(e.key==='Escape'){zoomHome();return;}
  if(CURRENT_PAGE==='home'){
    if((e.key==='Enter'||e.key===' ')&&_highlightIdx>=0){e.preventDefault();zoomTo(MODULES_ORDER[_highlightIdx]);}
    if(e.key==='ArrowDown'){e.preventDefault();_scrollTarget+=180;if(!_scrollRaf)_scrollRaf=requestAnimationFrame(_scrollTick);}
    if(e.key==='ArrowUp'){e.preventDefault();_scrollTarget-=180;if(!_scrollRaf)_scrollRaf=requestAnimationFrame(_scrollTick);}
  } else {
    if(e.key==='ArrowRight'||e.key==='PageDown'){e.preventDefault();_goNext();}
    if(e.key==='ArrowLeft'||e.key==='PageUp'){e.preventDefault();_goPrev();}
  }
});

// ════════════════════════════════════════════════════════════════
// GAMIFICATION — XP / LEVEL / BADGES
// ════════════════════════════════════════════════════════════════
var XP_LEVELS=[
  {min:0,   max:100,  label:'Stufe 1 - Chemieschüler',    short:'⚗ Chemieschüler'},
  {min:100, max:250,  label:'Stufe 2 - Lab-Assistent',    short:'🔬 Lab-Assistent'},
  {min:250, max:500,  label:'Stufe 3 - Laborant',         short:'🧪 Laborant'},
  {min:500, max:850,  label:'Stufe 4 - Forscher',         short:'🔭 Forscher'},
  {min:850, max:1300, label:'Stufe 5 - Wissenschaftler',  short:'🧬 Wissenschaftler'},
  {min:1300,max:99999,label:'Stufe 6 - Chemieprofessor',  short:'🎓 Chemieprofessor'},
];
var BADGE_DEFS=[
  {id:'quiz5',      ico:'🏆',lbl:'Quiz-Starter',    desc:'5 Fragen beantwortet'},
  {id:'quiz25',     ico:'🥇',lbl:'Quiz-Profi',       desc:'25 Fragen beantwortet'},
  {id:'pse_visit',  ico:'⚗️',lbl:'PSE-Erkunder',    desc:'Periodensystem besucht'},
  {id:'wiki_read',  ico:'📚',lbl:'Lernprofi',        desc:'Wiki gelesen'},
  {id:'struc_use',  ico:'✏️',lbl:'Molekülzeichner',  desc:'Strukturzeichner genutzt'},
  {id:'rxn_use',    ico:'⚡',lbl:'Reaktionsforscher',desc:'Reaktionsrechner genutzt'},
  {id:'all_modules',ico:'🌟',lbl:'Allrounder',       desc:'Alle Module besucht'},
  {id:'darkmode',   ico:'🌙',lbl:'Nachtforscher',    desc:'Dunkelmodus aktiviert'},
  {id:'xp500',      ico:'🔬',lbl:'Wissenschaftler',  desc:'500 XP erreicht'},
];
var _XP={
  total: parseInt(localStorage.getItem('cl_xp')||'0'),
  badges: JSON.parse(localStorage.getItem('cl_badges')||'[]'),
  visits: JSON.parse(localStorage.getItem('cl_visits')||'[]'),
  qa: parseInt(localStorage.getItem('cl_qa')||'0'),
};
function _saveXP(){ localStorage.setItem('cl_xp',_XP.total); localStorage.setItem('cl_badges',JSON.stringify(_XP.badges)); localStorage.setItem('cl_visits',JSON.stringify(_XP.visits)); localStorage.setItem('cl_qa',_XP.qa); }
function _getLv(xp){ for(var i=XP_LEVELS.length-1;i>=0;i--) if(xp>=XP_LEVELS[i].min) return Object.assign({idx:i},XP_LEVELS[i]); return Object.assign({idx:0},XP_LEVELS[0]); }
function _xpPct(xp){ var lv=_getLv(xp); if(lv.idx>=XP_LEVELS.length-1) return 100; return Math.min(100,Math.round(((xp-lv.min)/(lv.max-lv.min))*100)); }
function _updateXpUI(){
  var lv=_getLv(_XP.total), pct=_xpPct(_XP.total), tn=lv.idx<XP_LEVELS.length-1?lv.max-_XP.total:0;
  var ll=document.getElementById('xp-level-label'); if(ll) ll.textContent=lv.short;
  var bar=document.getElementById('xp-bar'); if(bar) bar.style.width=pct+'%';
  var sub=document.getElementById('xp-sub-label'); if(sub) sub.textContent=_XP.total+' XP'+(tn>0?' \u00b7 noch '+tn:'');
  var pl=document.getElementById('xp-pop-level'); if(pl) pl.textContent=lv.label;
  var pb=document.getElementById('xp-pop-bar'); if(pb) pb.style.width=pct+'%';
  var pll=document.getElementById('xp-pop-label'); if(pll) pll.textContent=tn>0?_XP.total+' / '+lv.max+' XP':'Max. Level erreicht!';
  var grid=document.getElementById('badges-grid');
  if(grid) grid.innerHTML=BADGE_DEFS.map(function(b){ var e=_XP.badges.includes(b.id); return '<div class="badge '+(e?'earned':'locked')+'" title="'+b.desc+'"><div class="badge-ico">'+b.ico+'</div><div class="badge-lbl">'+b.lbl+'</div></div>'; }).join('');
}
function _toast(msg){ var t=document.getElementById('xp-toast'),m=document.getElementById('xp-toast-msg'); if(!t||!m) return; m.textContent=msg; t.classList.add('show'); clearTimeout(t._t); t._t=setTimeout(function(){ t.classList.remove('show'); },2800); }
function addXP(amt,reason){
  var prevLv=_getLv(_XP.total).idx; _XP.total+=amt; var newLv=_getLv(_XP.total).idx;
  _saveXP(); _updateXpUI(); _toast('+'+amt+' XP \u00b7 '+reason);
  if(newLv>prevLv) setTimeout(function(){ _toast('\uD83C\uDF89 Level Up! '+_getLv(_XP.total).label); },1400);
  _checkBadges();
}
function _earnBadge(id){ if(_XP.badges.includes(id)) return; var b=BADGE_DEFS.find(function(x){ return x.id===id; }); if(!b) return; _XP.badges.push(id); _saveXP(); _updateXpUI(); _toast(b.ico+' Abzeichen: '+b.lbl); }
function _checkBadges(){ if(_XP.qa>=5)_earnBadge('quiz5'); if(_XP.qa>=25)_earnBadge('quiz25'); if(_XP.total>=500)_earnBadge('xp500'); if(_XP.visits.includes('pse'))_earnBadge('pse_visit'); if(_XP.visits.includes('wiki'))_earnBadge('wiki_read'); if(_XP.visits.includes('struc'))_earnBadge('struc_use'); if(_XP.visits.includes('rxn'))_earnBadge('rxn_use'); if(['pse','wiki','learn','struc','rxn','quiz'].every(function(m){ return _XP.visits.includes(m); }))_earnBadge('all_modules'); }
function toggleXpPopup(){ var p=document.getElementById('xp-popup'); if(p) p.classList.toggle('show'); _updateXpUI(); }
function _trackVisit(p){ if(!_XP.visits.includes(p)){ _XP.visits.push(p); _saveXP(); addXP(15,p.toUpperCase()+' erkundet'); } }
document.addEventListener('click',function(e){ var p=document.getElementById('xp-popup'),w=document.getElementById('xp-widget'); if(p&&p.classList.contains('show')&&!p.contains(e.target)&&w&&!w.contains(e.target)) p.classList.remove('show'); });

// ════════════════════════════════════════════════════════════════
// WRAPPERS: zoomTo / zoomHome / renderPage / quizAns
// ════════════════════════════════════════════════════════════════
var _op=renderPage, _oqa=quizAns;

// XP + nav hints are called directly from inside zoomTo above
// Just patch renderPage and quizAns here:

renderPage=function(p){
  if(p==='info') return renderInfo();
  var withFact=['wiki','learn','rxn','quiz'];
  var fact=withFact.includes(p)?_renderFact():'';
  return fact+_op(p);
};

function renderInfo(){
  var yr=new Date().getFullYear();
  return '<div class="page-hdr"><h1>ℹ️ Info & Impressum</h1><p>Alles über ChemLab und Kontakt.</p></div>'+
  '<div style="display:grid;grid-template-columns:1fr 1fr;gap:18px;margin-bottom:24px">'+

  '<div class="wiki-card" style="padding:20px">'+
  '<div style="font-size:22px;margin-bottom:10px">📄</div>'+
  '<h3 style="margin-bottom:10px;font-size:15px">Impressum</h3>'+
  '<div style="font-size:13px;color:var(--t2);line-height:1.9">'+
  '<strong>Angaben gemäß § 5 TMG</strong><br>'+
  'Martin Werner<br>'+
  'Privates Schulprojekt<br>'+
  'Nicht-kommerziell<br><br>'+
  '<strong>Haftungshinweis</strong><br>'+
  'Trotz sorgfältiger Kontrolle übernehmen wir keine Haftung für die Inhalte externer Links. '+
  'Für den Inhalt verlinkter Seiten sind ausschließlich deren Betreiber verantwortlich.'+
  '</div></div>'+

  '<div class="wiki-card" style="padding:20px">'+
  '<div style="font-size:22px;margin-bottom:10px">✉️</div>'+
  '<h3 style="margin-bottom:10px;font-size:15px">Kontakt</h3>'+
  '<div style="font-size:13px;color:var(--t2);line-height:1.9">'+
  '<strong>E-Mail</strong><br>'+
  '<a href="mailto:mango10@snafu.de" style="color:var(--acc);text-decoration:none">mango10@snafu.de</a><br><br>'+
  '<strong>Erstellt von</strong><br>Martin Werner<br><br>'+
  '<strong>Projekt</strong><br>ChemLab – Interaktive Chemie-Lernplattform'+
  '</div></div>'+

  '</div>'+

  '<div class="wiki-card" style="padding:20px;margin-bottom:18px">'+
  '<div style="font-size:22px;margin-bottom:10px">🧪</div>'+
  '<h3 style="margin-bottom:10px;font-size:15px">Über ChemLab</h3>'+
  '<div style="font-size:13px;color:var(--t2);line-height:1.8">'+
  'ChemLab ist eine interaktive Chemie-Lernplattform, die als privates Schulprojekt entstanden ist. '+
  'Sie bietet ein interaktives Periodensystem mit allen 118 Elementen, ein Chemie-Wiki, '+
  'einen Strukturzeichner, einen Reaktionsrechner und ein Quiz mit 97 Fragen in 8 Kategorien.'+
  '<div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:14px">'+
  '<span class="footer-chip">118 Elemente</span>'+
  '<span class="footer-chip">97 Quizfragen</span>'+
  '<span class="footer-chip">8 Quiz-Kategorien</span>'+
  '<span class="footer-chip">8 Module</span>'+
  '</div></div></div>'+

  '<div class="wiki-card" style="padding:20px">'+
  '<div style="font-size:22px;margin-bottom:10px">🔗</div>'+
  '<h3 style="margin-bottom:10px;font-size:15px">Schnellnavigation</h3>'+
  '<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:8px">'+
  ['pse','wiki','learn','struc','rxn','quiz'].map(function(m){
    var icons={pse:'🔬',wiki:'📚',learn:'🎓',struc:'✏️',rxn:'⚖️',quiz:'🧠'};
    var names={pse:'Periodensystem',wiki:'Chemie-Wiki',learn:'Lernbereich',struc:'Strukturzeichner',rxn:'Reaktionsrechner',quiz:'Quiz'};
    return '<button class="btn" style="width:100%;justify-content:flex-start;gap:8px" onclick="zoomTo(\''+m+'\')">'+icons[m]+' '+names[m]+'</button>';
  }).join('')+
  '</div></div>'+
  '<div style="text-align:center;color:var(--t4);font-size:11px;margin-top:24px;padding-top:16px;border-top:0.5px solid var(--bdr)">'+
  '© '+yr+' ChemLab · Martin Werner · Privates Schulprojekt</div>';
}

quizAns=function(idx){
  var q=QUIZ_Q[QZ.cat][QZ.q];
  if(q.correct===idx) addXP(10,'Richtige Antwort');
  else addXP(2,'Frage versucht');
  _XP.qa++; _saveXP(); _checkBadges();
  _oqa(idx);
};

// ════════════════════════════════════════════════════════════════
// CHEMIE-FAKT
// ════════════════════════════════════════════════════════════════
var FACTS=[
  {t:'Gallium (Ga, Z=31) schmilzt bei nur 29,8 °C — schon in deiner Hand wird es flüssig. Das liegt an seiner ungewöhnlichen Kristallstruktur: Gallium-Atome bilden Paare (Ga₂), die untereinander schwächer anziehen als andere Metalle. Entdeckt 1875 von Lecoq de Boisbaudran — exakt wie Mendeleev es drei Jahre zuvor aus dem PSE vorhergesagt hatte.',s:'Ga, Z=31 · Schmp. 29,8 °C · Gruppe 13'},
  {t:'Graphen (eine einzelne Kohlenstoffschicht in Honigwabenstruktur, sp²-hybridisiert) ist 200-mal stärker als Stahl, leitet Strom besser als Kupfer und ist mit bloßem Auge unsichtbar. Entdeckt 2004 mit Tesafilm von Andre Geim und Konstantin Novoselov — Nobelpreis Physik 2010. Ein Quadratmeter Graphen wiegt 0,77 Milligramm.',s:'C, Z=6 · sp²-Hybridisierung · Nobelpreis 2010'},
  {t:'Fluorwasserstoffsäure (HF) löst Glas auf: F⁻ reagiert mit SiO₂ zu flüchtigem SiF₄ (SiO₂ + 4HF → SiF₄↑ + 2H₂O). Paradox: Chemisch ist HF eine schwache Säure (pKs = 3,17) — Essigsäure ist ähnlich stark. Trotzdem ist HF lebensgefährlich, weil Fluorid-Ionen durch die Haut dringen und im Gewebe Calciumionen binden, was Herzrhythmusstörungen verursachen kann.',s:'HF · pKs 3,17 · SiO₂ + 4HF → SiF₄ + 2H₂O'},
  {t:'Das Haber-Bosch-Verfahren (N₂ + 3H₂ ⇌ 2NH₃) wurde 1909 von Fritz Haber entdeckt. Das Besondere: Die N≡N-Dreifachbindung hat 945 kJ/mol Bindungsenergie — eine der stärksten überhaupt. Ein Eisenkatalysator bei 400–500 °C und 200 bar bricht sie auf. Ohne dieses Verfahren könnten nur halb so viele Menschen von der Erde ernährt werden, da Kunstdünger unmöglich wäre.',s:'N₂ + 3H₂ ⇌ 2NH₃ · Fe-Katalysator · 400–500 °C · 200 bar'},
  {t:'Wasserstoff (H, Z=1) macht ~75 % der Baryonenmasse des Universums aus. In Sternen wie unserer Sonne laufen Kernfusionsreaktionen ab: 4¹H → ⁴He + 2e⁺ + 2ν + 26,7 MeV Energie. Die Sonne setzt dabei 3,8 × 10²⁶ Watt frei und verbraucht 600 Millionen Tonnen Wasserstoff — pro Sekunde.',s:'H, Z=1 · 4¹H → ⁴He + 26,7 MeV · Sonne: 4,6 Mrd. Jahre alt'},
  {t:'Osmium (Os, Z=76) ist das dichteste Element aller: 22,59 g/cm³. Ein Würfel mit 10 cm Kantenlänge wiegt 22,6 kg. Zum Vergleich: Blei hat 11,3, Eisen 7,9 g/cm³. Die extreme Dichte entsteht durch die hexagonale dichteste Kugelpackung der schweren Atome (Atommasse 192). Entdeckt 1803 von Smithson Tennant — gleichzeitig mit Iridium.',s:'Os, Z=76 · 22,59 g/cm³ · hcp-Kristall · entdeckt 1803'},
  {t:'Diamant und Graphit: gleiche Atome (C, Z=6), völlig verschiedene Eigenschaften. Diamant: sp³-Hybridisierung, jedes C mit 4 anderen tetraedrisch verbunden → 3D-Netz, härtester natürlicher Stoff (Mohs 10). Graphit: sp²-Hybridisierung, hexagonale Schichten durch Van-der-Waals-Kräfte → gleitend weich (Mohs 1–2), elektrisch leitend. Beide sind stabile Allotrope des Kohlenstoffs.',s:'C, Z=6 · sp³ (Diamant, Mohs 10) vs. sp² (Graphit, Mohs 1–2)'},
  {t:'Helium (He, Z=2) ist das einzige Element, das unter Normaldruck selbst am absoluten Nullpunkt (0 K = −273,15 °C) flüssig bleibt. Der Grund ist Quantenmechanik: Die Nullpunktsenergie der leichten He-Atome ist so groß, dass kein Gitter sie halten kann. Erst ab 25 bar erstarrt es. Unter 2,17 K (Lambda-Punkt) wird flüssiges ⁴He zum Superfluid: Es kriecht Wände hoch und hat null Viskosität.',s:'He, Z=2 · Superfluid unter 2,17 K · Sdp. −268,9 °C'},
  {t:'Phosphor wurde 1669 von Hennig Brand in Hamburg entdeckt — als erstes Element mit bekanntem Entdecker. Er wollte aus Urin Gold gewinnen und kochte hunderte Liter ein. Heraus kam weißer Phosphor, der im Dunkeln leuchtet (Chemolumineszenz durch langsame Oxidation). Phosphor ist essenziell für das Leben: DNA, RNA, ATP und Zellmembranen (Phospholipide) enthalten alle Phosphat.',s:'P, Z=15 · entdeckt 1669 · DNA/RNA-Rückgrat · ATP-Energie'},
  {t:'Kohlenstoff-14 (¹⁴C) entsteht in der oberen Atmosphäre durch kosmische Strahlung: ¹⁴N + n → ¹⁴C + p. Lebewesen nehmen ¹⁴C über die Nahrung auf; nach dem Tod hört die Aufnahme auf. ¹⁴C zerfällt mit einer Halbwertszeit von 5730 Jahren (β⁻-Zerfall). Aus dem ¹⁴C/¹²C-Verhältnis lässt sich das Alter organischer Materialien bis ~50.000 Jahre bestimmen — die Radiokarbondatierung.',s:'¹⁴C · HWZ 5730 a · β⁻-Zerfall · Altersbestimmung bis 50.000 a'},
  {t:'Gold (Au, Z=79) hat eine gelbe Farbe aus einem relativistischen Quanteneffekt: Die inneren s-Elektronen bewegen sich mit ~58 % der Lichtgeschwindigkeit, werden dadurch schwerer und ihre Orbitale schrumpfen. Das verschiebt Übergangsenergien ins sichtbare Blau — Gold absorbiert Blaulicht und wirkt daher gelb. Ohne Relativitätstheorie wäre Gold silbrig-weiß wie Silber.',s:'Au, Z=79 · relativistischer Effekt · nur löslich in Königswasser (3:1 HCl/HNO₃)'},
  {t:'Aluminium war im 19. Jahrhundert wertvoller als Gold — Napoleon III. ließ seine Staatsgäste mit Aluminiumbesteck speisen, während einfache Gäste Gold und Silber bekamen. Das änderte sich 1886 schlagartig: Charles Hall (USA) und Paul Héroult (Frankreich) entdeckten unabhängig voneinander die Schmelzflusselektrolyse (Hall-Héroult-Verfahren). Seither ist Al das preiswerteste Konstruktionsmetall.',s:'Al, Z=13 · Hall-Héroult 1886 · häufigstes Metall der Erdkruste (8,1 %)'},
  {t:'Chlor (Cl₂) hat im 1. Weltkrieg als Giftgas verheerende Wirkung gezeigt (Ypern 1915). Dasselbe Element hat aber als Desinfektionsmittel in Trinkwasser und Schwimmbädern mehr Menschenleben gerettet als jedes Medikament. Die Reaktion mit Wasser: Cl₂ + H₂O ⇌ HCl + HOCl. Hypochlorige Säure (HOCl) tötet Bakterien durch Oxidation der Zellmembranproteine.',s:'Cl, Z=17 · Cl₂ + H₂O ⇌ HCl + HOCl · Desinfektionswirkung'},
  {t:'Das Periodensystem war eine Prophezeiung: Mendeleev ließ 1869 bewusst Lücken für noch unbekannte Elemente und sagte deren Eigenschaften voraus. "Eka-Aluminium" (Gallium, 1875), "Eka-Bor" (Scandium, 1879) und "Eka-Silicium" (Germanium, 1886) wurden exakt wie vorhergesagt entdeckt — mit Dichte, Schmelzpunkt und Reaktivität fast auf den Punkt. Das war der ultimative Beweis für das System.',s:'Mendeleev 1869 · Gallium, Scandium, Germanium korrekt vorhergesagt'},
  {t:'Natrium und Kalium sind lebenswichtig für jeden Nervenimpuls: Die Na⁺/K⁺-ATPase-Pumpe transportiert aktiv 3 Na⁺ nach außen und 2 K⁺ nach innen — gegen den Konzentrationsgradienten, unter ATP-Verbrauch. Das erzeugt das Membranpotenzial von −70 mV. Öffnen sich Na⁺-Kanäle, strömt Na⁺ ein → Aktionspotenzial (+40 mV) → Nervenimpuls mit ~100 m/s.',s:'Na, Z=11 · K, Z=19 · Membranpotenzial −70 mV → +40 mV'},
  {t:'Schwefelsäure (H₂SO₄) ist die meistproduzierte Chemikalie der Welt: ~250 Millionen Tonnen jährlich. Sie wird so viel produziert, dass Ökonomen den H₂SO₄-Verbrauch als Indikator für den Industrialisierungsgrad eines Landes nutzen. 60 % gehen in die Düngemittelproduktion (Phosphataufschluss), der Rest in Metallverarbeitung, Batterien und Chemiesynthese.',s:'H₂SO₄ · 250 Mio. t/Jahr · Industrieindikator'},
  {t:'Radioaktivität wurde 1896 von Henri Becquerel zufällig entdeckt: Er legte Uranmineralien auf fotografische Platten — auch im Dunkeln schwärzten sie sich. Marie und Pierre Curie isolierten 1898 Polonium und Radium. Marie Curie gewann den Nobelpreis zweimal (Physik 1903, Chemie 1911). Sie starb 1934 an aplastischer Anämie durch jahrelange Strahlenexposition.',s:'Becquerel 1896 · Marie Curie · 2× Nobelpreis · Polonium & Radium'},
  {t:'Eisen (Fe, Z=26) ist das häufigste Element im Erdkern (80 %) und das vierthäufigste in der Erdkruste. Im Blut bindet Fe²⁺ im Hämoglobin reversibel Sauerstoff: Ein Hämoglobin-Molekül hat 4 Häm-Gruppen und kann 4 O₂ tragen. Kohlenmonoxid (CO) verdrängt O₂ mit 200-facher Affinität — deshalb ist CO so gefährlich: Es blockiert den Sauerstofftransport.',s:'Fe, Z=26 · Hämoglobin · CO 200× stärkere Bindung als O₂'},
  {t:'Quecksilber (Hg, Z=80) ist das einzige Metall, das bei Raumtemperatur flüssig ist (Schmp. −38,83 °C). Die Minamata-Katastrophe (Japan, 1956) zeigte die verheerenden Folgen: Eine Chemiefabrik leitete methylierte Quecksilberverbindungen (CH₃Hg⁺) ins Meer. Fische akkumulierten es (Bioakkumulation), Menschen erkrankten an schweren Nervenschäden. Über 2000 Todesfälle.',s:'Hg, Z=80 · Schmp. −38,83 °C · Minamata 1956 · Bioakkumulation'},
  {t:'Ozon (O₃) in der Stratosphäre (20–40 km Höhe) absorbiert 97–99 % der UV-B- und UV-C-Strahlung. Die Reaktion: O₃ + UV → O₂ + O·. FCKW (Fluorchlorkohlenwasserstoffe) wie CCl₂F₂ zersetzen Ozon katalytisch: Cl· + O₃ → ClO + O₂ — ein Cl-Atom kann 100.000 O₃-Moleküle zerstören! Das Montreal-Protokoll (1987) verbot FCKW weltweit — die Ozonschicht erholt sich seitdem.',s:'O₃ · UV-Schutz · FCKW-Katalyse · Montreal-Protokoll 1987'},
];

var _fi=Math.floor((Date.now()/(1000*60*60*24*7))%FACTS.length);
function _renderFact(){
  var f=FACTS[_fi];
  var dots=FACTS.map(function(_,i){ return '<div class="fact-dot'+(i===_fi?' on':'')+'" onclick="_fi='+i+';_rerenderFact()"></div>'; }).join('');
  return '<div class="fact-card"><div class="fact-badge">&#x1F9E0; Chemie-Fakt</div><div class="fact-text">'+f.t+'</div><div class="fact-source">'+f.s+'</div><div class="fact-nav">'+dots+'</div></div>';
}
function _rerenderFact(){
  document.querySelectorAll('.fact-card').forEach(function(c){
    c.querySelector('.fact-text').textContent=FACTS[_fi].t;
    c.querySelector('.fact-source').textContent=FACTS[_fi].s;
    c.querySelector('.fact-nav').innerHTML=FACTS.map(function(_,i){ return '<div class="fact-dot'+(i===_fi?' on':'')+'" onclick="_fi='+i+';_rerenderFact()"></div>'; }).join('');
  });
}

// ════════════════════════════════════════════════════════════════
// EXTENDED QUIZ (8 Kategorien)
// ════════════════════════════════════════════════════════════════
Object.assign(QUIZ_Q,{
alkane:[
{q:'Allgemeine Summenformel der Alkane?',answers:['CnH2n','CnH2n+2','CnH2n-2','CnHn'],correct:1,exp:'Alkane: CnH2n+2 (gesaettigt).'},
{q:'Alkan mit 1 C-Atom?',answers:['Ethan','Propan','Methan','Butan'],correct:2,exp:'CH4 = Methan.'},
{q:'Bindungen in Alkanen?',answers:['C=C','C-C Einfachbindungen','C≡C','Aromatisch'],correct:1,exp:'Nur sp3-C, Einfachbindungen.'},
{q:'Alkan mit 4 C-Atomen?',answers:['Propan','Butan','Pentan','Hexan'],correct:1,exp:'C4H10 = Butan.'},
{q:'Typische Reaktion von Alkanen?',answers:['Elektrophile Addition','Radikalische Substitution','Nucleophile Substitution','Eliminierung'],correct:1,exp:'Radikalische Substitution.'},
{q:'Produkte vollstaendiger Verbrennung?',answers:['CO+H2','CO2+H2O','C+H2O','H2+O2'],correct:1,exp:'CnH2n+2 + O2 → CO2 + H2O'},
{q:'Hybridisierung von C in Alkanen?',answers:['sp','sp2','sp3','sp3d'],correct:2,exp:'sp3: Tetraeder.'},
{q:'Alkan mit 3 C-Atomen?',answers:['Methan','Ethan','Propan','Butan'],correct:2,exp:'C3H8 = Propan.'},
],
proteins:[
{q:'Grundbausteine von Proteinen?',answers:['Fettsaeuren','Nucleotide','Aminosaeuren','Monosaccharide'],correct:2,exp:'Proteinen sind Polypeptide aus Aminosaeuren.'},
{q:'Was ist eine Peptidbindung?',answers:['NH2-Bindung','CO-NH-Bindung','Esterbindung','Disulfid'],correct:1,exp:'CO-NH entsteht durch Kondensation.'},
{q:'Wie viele proteinogene AS?',answers:['10','20','30','64'],correct:1,exp:'20 Standard-Aminosaeuren.'},
{q:'Was ist Primaerstruktur?',answers:['3D-Faltung','Helix','Aminosaeure-Sequenz','Quartaer'],correct:2,exp:'Lineare AS-Sequenz.'},
{q:'Was ist eine Alpha-Helix?',answers:['Primaer','Sekundaer','Tertiaer','Quartaer'],correct:1,exp:'Sekundaerstruktur, stabilisiert durch H-Bruecken.'},
{q:'Was ist Denaturierung?',answers:['Peptidbindungsspaltung','Verlust der Raumstruktur','Synthese','Reduktion'],correct:1,exp:'Verlust der raeumlichen Struktur.'},
{q:'Welche AS bildet Disulfidbruecken?',answers:['Glycin','Alanin','Cystein','Serin'],correct:2,exp:'Cystein: -SH Gruppen → -S-S-.'},
{q:'Was ist ein Enzym?',answers:['Strukturprotein','Biologischer Katalysator','Transportprotein','Hormon'],correct:1,exp:'Proteine, die Reaktionen katalysieren.'},
],
carbs:[
{q:'Formel der Monosaccharide?',answers:['(CH2O)n','CnH2nO2','CnHnOn','C6H12O6'],correct:0,exp:'(CH2O)n, z.B. Glucose n=6.'},
{q:'Glucose und Fructose sind?',answers:['Verschiedene Formeln','Verschiedene C-Zahl','Konstitutionsisomere','Gleiche Struktur'],correct:2,exp:'Beide C6H12O6, verschiedene Struktur.'},
{q:'Glucose + Fructose ergibt?',answers:['Maltose','Lactose','Saccharose','Cellobiose'],correct:2,exp:'Saccharose = Rohrzucker.'},
{q:'Speicherform von Glucose im Koerper?',answers:['Cellulose','Staerke','Glykogen','Saccharose'],correct:2,exp:'Glykogen in Leber und Muskel.'},
{q:'Unterschied Staerke/Cellulose?',answers:['Verschiedene Zucker','Alpha- vs. Beta-Bindung','Kettenlaenge','Verzweigung'],correct:1,exp:'Staerke alpha-1,4; Cellulose beta-1,4.'},
{q:'Was zeigt die Fehlingprobe?',answers:['Proteine','Reduzierende Zucker','Fette','Staerke'],correct:1,exp:'Cu2+ → Cu2O (rot) bei red. Zuckern.'},
{q:'Strukturfestigkeit der Zellwand?',answers:['Glykogen','Staerke','Chitin','Cellulose'],correct:3,exp:'Cellulose = häufigstes Biopolymer.'},
{q:'C-Atome in Ribose?',answers:['3','4','5','6'],correct:2,exp:'Ribose C5H10O5, Pentose, RNA-Baustein.'},
],
acids:[
{q:'Broensted-Saeure ist?',answers:['Elektronenpaardonor','Protonendonor','Elektronenpaarakzeptor','Protonenakzeptor'],correct:1,exp:'Saeure gibt H+ ab.'},
{q:'pH von 0,01 M HCl?',answers:['1','2','7','12'],correct:1,exp:'pH = -log(0.01) = 2.'},
{q:'Saeure in Essig?',answers:['Salzsaeure','Schwefelsaeure','Essigsaeure','Zitronensaeure'],correct:2,exp:'Essigsaeure CH3COOH.'},
{q:'Was ist amphoter?',answers:['Nur Saeure','Nur Base','Beides moeglich','Weder noch'],correct:2,exp:'Kann als Saeure oder Base reagieren.'},
{q:'Was bedeutet kleiner pKs?',answers:['Schwaechere Saeure','Staerkere Saeure','Neutral','Starke Base'],correct:1,exp:'pKs = -log(Ks). Kleiner = staerker.'},
{q:'pH + pOH bei 25 Grad?',answers:['7','14','1','0'],correct:1,exp:'Kw = 10^-14, also pH + pOH = 14.'},
{q:'Was ist NaOH?',answers:['Schwache Saeure','Starke Saeure','Schwache Base','Starke Base'],correct:3,exp:'Vollstaendige Dissoziation zu Na+ + OH-.'},
{q:'Neutraler pH-Wert?',answers:['0','7','14','1'],correct:1,exp:'pH 7: [H+] = [OH-].'},
],
lipids:[
{q:'Bausteine von Triglyceriden?',answers:['Aminosaeuren+Glycerin','Fettsaeuren+Glycerin','Glucose+Fettsaeuren','Fettsaeuren+Phosphat'],correct:1,exp:'3 Fettsaeuren + Glycerin via Esterbindung.'},
{q:'Unterschied gesaettigt/ungesaettigt?',answers:['Anzahl C','C=C-Doppelbindungen','Loeslichkeit','OH-Gruppen'],correct:1,exp:'Ungesaettigt: mind. eine C=C.'},
{q:'Warum sind ungesaettigte Fette fluessig?',answers:['Weniger C','Cis-Knicke = weniger Packung','Mehr O','Ionisch'],correct:1,exp:'Cis-Doppelbindungen stoeren Packung.'},
{q:'Was ist Verseifung?',answers:['Oxidation','Hydrolyse mit Lauge','H2-Addition','Verbrennung'],correct:1,exp:'Fett + NaOH → Glycerin + Seife.'},
{q:'Was sind Phospholipide?',answers:['Fette mit Phosphat','Zucker-Fett','Protein-Fett','Cholesterin'],correct:0,exp:'Glycerin + 2 Fettsaeuren + Phosphat.'},
{q:'Essentielle Fettsaeuren?',answers:['Vom Koerper herstellbar','Muessen zugefuehrt werden','Nur in Tieren','Gesaettigt'],correct:1,exp:'Koerper kann sie nicht selbst synthetisieren.'},
{q:'Fettgewebe besteht aus?',answers:['Hepatozyten','Myozyten','Adipozyten','Chondrozyten'],correct:2,exp:'Adipozyten speichern Triglyceride.'},
],
});

var QUIZ_CATS={
  elements:  {ico:'⚗',  label:'Elemente',       desc:'Symbole, Ordnungszahlen'},
  reactions: {ico:'⚡', label:'Reaktionen',      desc:'Verbrennung, Redox'},
  theory:    {ico:'📚', label:'Theorie & PSE',   desc:'Bindungsarten, Atombau'},
  alkane:    {ico:'⛽', label:'Alkane',          desc:'Gesaettigte KW'},
  proteins:  {ico:'🧬', label:'Proteine',        desc:'Aminosaeuren, Faltung'},
  carbs:     {ico:'🍞', label:'Kohlenhydrate',   desc:'Zucker, Staerke, Cellulose'},
  acids:     {ico:'🧪', label:'Saeuren & Basen', desc:'pH, Puffer, Titration'},
  lipids:    {ico:'🫙', label:'Lipide & Fette',  desc:'Fettsaeuren, Verseifung'},
};

var _oRQS=renderQuizStart;
renderQuizStart=function(){
  var cats=Object.entries(QUIZ_CATS).map(function(e){
    var k=e[0],v=e[1];
    return '<div class="quiz-mode" onclick="QZ={mode:\'quiz\',cat:\''+k+'\',q:0,score:0,answered:false,done:false};rerender()"><div class="qm-ico">'+v.ico+'</div><h3>'+v.label+'</h3><p>'+v.desc+' &middot; '+((QUIZ_Q[k]||[]).length)+' Fragen</p></div>';
  }).join('');
  return '<div class="page-hdr"><h1>&#x1F9E0; Chemie-Quiz</h1><p>W&#xe4;hle ein Themengebiet.</p></div><div class="quiz-mode-grid" style="grid-template-columns:repeat(auto-fill,minmax(155px,1fr))">'+cats+'</div>';
};

var _oRQQ=renderQuizQ;
renderQuizQ=function(){
  var cl=(QUIZ_CATS[QZ.cat]||{}).label||QZ.cat;
  var qs=QUIZ_Q[QZ.cat],q=qs[QZ.q],total=qs.length,prog=Math.round((QZ.q/total)*100);
  var elHint='';
  if(q.el){var el=EL_MAP[q.el];if(el)elHint='<div class="quiz-element-hint" style="background:'+catBg(el.c)+';border:0.5px solid '+catBdr(el.c)+';color:'+catCol(el.c)+'"><div class="quiz-el-z">'+el.z+'</div><div class="quiz-el-s">'+el.s+'</div><div class="quiz-el-m">'+(el.m?el.m+' u':'–')+'</div></div>';}
  var ans=q.answers.map(function(a,i){ return '<button class="qa" id="qa-'+i+'" onclick="quizAns('+i+')">'+a+'</button>'; }).join('');
  return '<div class="quiz-wrap"><div class="quiz-progress"><div class="quiz-progress-bar" style="width:'+prog+'%"></div></div><div class="quiz-card"><div class="quiz-q-num">Frage '+(QZ.q+1)+'/'+total+' \u00b7 '+cl+'</div>'+elHint+'<div class="quiz-q">'+q.q+'</div><div class="quiz-answers">'+ans+'</div><div class="quiz-feedback" id="qfb"></div></div><div class="quiz-nav"><div class="quiz-score-label">Punkte: '+QZ.score+'/'+QZ.q+'</div><button class="btn'+(QZ.answered?' pri':'')+'" id="qnext" onclick="quizNext()" '+(QZ.answered?'':'disabled')+' style="'+(QZ.answered?'':'opacity:.4')+'">N\u00e4chste Frage \u2192</button></div></div>';
};

// ════════════════════════════════════════════════════════════════
// INIT (nach DOM)
// ════════════════════════════════════════════════════════════════
document.addEventListener('DOMContentLoaded', function(){
  _updateXpUI();
  _navDots('home');
  var icons=['⚗️','🔬','⚛️','🧬','💊','🧪','🔭','💡','⚡','🌡️'];
  var mb=document.getElementById('mol-bg');
  if(mb){ for(var i=0;i<12;i++){
    var el=document.createElement('div'); el.className='mol-float';
    el.textContent=icons[Math.floor(Math.random()*icons.length)];
    var sz=14+Math.random()*12, lft=Math.random()*96, dur=24+Math.random()*28, dly=-(Math.random()*dur);
    el.style.cssText='left:'+lft+'%;font-size:'+sz+'px;animation-duration:'+dur+'s;animation-delay:'+dly+'s';
    mb.appendChild(el);
  }}
});

</script>
</body>
</html>
