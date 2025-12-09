---
layout: page
permalink: /publications/
title: publications
description: Peer-Reviewed Journals & Conference Proceedings, Policy Reports, and Preprints
nav: true
nav_order: 1
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<style>
/* Basic tab styles - scoped to publications page */
.publications { margin-top: 1rem; }
.pub-tabs { display:flex; gap:0.5rem; flex-wrap:wrap; margin-bottom:0.75rem; }
.pub-tab { appearance:none; background:transparent; border:1px solid var(--muted-color, #ddd); padding:0.5rem 0.75rem; border-radius:6px; cursor:pointer; font-weight:600; color:var(--text-color, #222); }
.pub-tab:focus { outline:3px solid rgba(50,115,220,0.2); outline-offset:2px; }
.pub-tab.active { background:var(--accent, #b16d6c); color:white; border-color:var(--accent, #b16d6c); }
.pub-panels { margin-top:0.5rem; }
.pub-panel { display:block; }
.pub-panel[hidden] { display:none; }
/* Small responsive tweak */
@media (max-width:520px){ .pub-tabs{ gap:0.25rem } .pub-tab{ padding:0.4rem 0.5rem; font-size:0.95rem } }
</style>

<div class="publications">

<div class="pub-tabs" role="tablist" aria-label="Publications categories">
  <button class="pub-tab active" data-target="#pub-all" role="tab" aria-selected="true">All</button>
  <button class="pub-tab" data-target="#pub-journals" role="tab" aria-selected="false">Journals</button>
  <button class="pub-tab" data-target="#pub-proceedings" role="tab" aria-selected="false">Conference Proceedings</button>
  <button class="pub-tab" data-target="#pub-reports" role="tab" aria-selected="false">Policy Reports</button>
  <button class="pub-tab" data-target="#pub-preprints" role="tab" aria-selected="false">Preprints</button>
</div>

<div class="pub-panels">
  <section id="pub-all" class="pub-panel" role="tabpanel" aria-hidden="false">
    {% bibliography --prefix="all" %}
  </section>

  <section id="pub-journals" class="pub-panel" role="tabpanel" aria-hidden="true" hidden>
    {% bibliography --prefix="journals" -q @*[keywords=J] %}
  </section>

  <section id="pub-proceedings" class="pub-panel" role="tabpanel" aria-hidden="true" hidden>
    {% bibliography --prefix="proceedings" -q @*[keywords=C] %}
  </section>

  <section id="pub-reports" class="pub-panel" role="tabpanel" aria-hidden="true" hidden>
    {% bibliography --prefix="reports" -q @*[keywords=report] %}
  </section>

  <section id="pub-preprints" class="pub-panel" role="tabpanel" aria-hidden="true" hidden>
    {% bibliography --prefix="preprints" -q @*[keywords=preprint] %}
  </section>
</div>

</div>

<script>
  (function(){
    if (typeof document === 'undefined') return;
    const tabs = Array.from(document.querySelectorAll('.pub-tab'));
    const panels = Array.from(document.querySelectorAll('.pub-panel'));
    if (!tabs.length || !panels.length) return;

    function activate(tab){
      tabs.forEach(t=>{
        const isActive = t === tab;
        t.classList.toggle('active', isActive);
        t.setAttribute('aria-selected', isActive ? 'true' : 'false');
        if (isActive) t.focus();
      });
      const target = tab.getAttribute('data-target');
      panels.forEach(p=>{
        const show = ('#'+p.id) === target;
        p.hidden = !show;
        p.setAttribute('aria-hidden', (!show).toString());
      });
    }

    // click
    tabs.forEach(t=> t.addEventListener('click', ()=> activate(t)) );

    // keyboard navigation: left/right to move, enter/space to activate
    tabs.forEach((t, idx)=>{
      t.addEventListener('keydown', (ev)=>{
        if (ev.key === 'ArrowRight' || ev.key === 'ArrowDown'){
          ev.preventDefault();
          const next = tabs[(idx+1) % tabs.length]; next.focus();
        } else if (ev.key === 'ArrowLeft' || ev.key === 'ArrowUp'){
          ev.preventDefault();
          const prev = tabs[(idx-1+tabs.length) % tabs.length]; prev.focus();
        } else if (ev.key === 'Enter' || ev.key === ' ') {
          ev.preventDefault(); activate(t);
        }
      });
    });

    // ensure first tab/panel state
    const initial = tabs.find(t=> t.classList.contains('active')) || tabs[0];
    activate(initial);
  })();
</script>
