---
layout: page
title: 我的文件
full-width: true
permalink: /docs/
docs-groups:
  - label: MCU
    slug: mcu
    docs:
      - id: stm32g431
        title: STM32G431
        include: "docs/mcu/stm32g431.md"
      - id: stm32h503
        title: STM32H503
        include: "docs/mcu/stm32h503.md"
  - label: 工具
    slug: tools
    docs:
      - id: canedge
        title: CANedge
        include: "docs/tools/canedge.md"
---

<style>
.docs-shell { padding: 32px 0 56px; }
.docs-grid {
  display: grid;
  grid-template-columns: 250px minmax(0, 1fr) 280px;
  gap: 28px;
}
.doc-sidebar {
  background: #f5f7fb;
  border-radius: 14px;
  padding: 18px 14px 22px;
  position: sticky;
  top: 88px;
  height: fit-content;
}
.doc-sidebar__title {
  font-size: 18px;
  font-weight: 700;
  margin-bottom: 12px;
  color: #22344a;
}
.doc-sidebar__section { margin-top: 10px; }
.doc-sidebar__toggle {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 8px;
  border: none;
  border-radius: 8px;
  background: transparent;
  color: #394a5a;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.16s ease;
}
.doc-sidebar__toggle:hover { background: #eef2f8; }
.doc-sidebar__caret { transition: transform 0.16s ease; }
.doc-sidebar__section.collapsed .doc-sidebar__caret { transform: rotate(-90deg); }
.doc-list {
  margin: 6px 0 0;
  display: grid;
  gap: 10px;
  position: relative;
  padding-left: 26px;
}
.doc-sidebar__section.collapsed .doc-list { display: none; }
.doc-list::before {
  content: "";
  position: absolute;
  top: 0;
  left: 9px;
  width: 2px;
  height: 100%;
  background: linear-gradient(#dfe5ee, #dfe5ee);
  border-radius: 2px;
}
.doc-link {
  display: flex;
  align-items: center;
  width: 100%;
  padding: 0;
  border: none;
  background: transparent;
  color: #3c5066;
  font-weight: 600;
  cursor: pointer;
  transition: color 0.14s ease;
  position: relative;
}
.doc-link::before {
  content: "";
  position: absolute;
  left: -17px;
  top: 50%;
  width: 14px;
  height: 2px;
  background: #dfe5ee;
  transform: translateY(-50%);
}
.doc-link:hover { color: #1f3b57; }
.doc-link.active {
  color: #d48a00;
}
.doc-content { padding: 0 10px; }
.doc-body { display: none; }
.doc-body.active { display: block; }
.doc-body h2, .doc-body h3 { scroll-margin-top: 90px; }
.doc-meta {
  font-size: 13px;
  color: #7b8794;
  margin-bottom: 18px;
}
.doc-nav {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
  margin: 36px 0 8px;
}
.doc-nav__btn {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 14px;
  border: 1px solid #e3e9f4;
  border-radius: 12px;
  background: #f7fafc;
  color: #2b3c4e;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.14s ease;
}
.doc-nav__btn:hover { border-color: #d9e4f5; background: #eef3fb; }
.doc-nav__btn:disabled {
  opacity: 0.55;
  cursor: not-allowed;
}
.doc-nav__label { font-size: 12px; color: #7b8794; }
.doc-nav__title { font-size: 15px; }
.doc-nav__icon { color: #d48a00; }
.doc-toc {
  border: 1px solid #e3e9f4;
  border-radius: 14px;
  padding: 18px 16px;
  position: sticky;
  top: 88px;
  height: fit-content;
  background: #fff;
}
.doc-toc__title {
  font-weight: 700;
  font-size: 16px;
  color: #1f3b57;
  margin-bottom: 12px;
}
.doc-toc__item { margin: 4px 0; }
.doc-toc__item a {
  color: #2b3c4e;
  text-decoration: none;
  font-size: 14px;
  transition: color 0.12s ease;
}
.doc-toc__item a:hover { color: #d48a00; }
.doc-toc__item--h3 { margin-left: 12px; font-size: 13px; }
@media (max-width: 1199px) {
  .docs-grid { grid-template-columns: 220px minmax(0, 1fr); }
  .doc-toc { display: none; }
}
@media (max-width: 991px) {
  .docs-grid { grid-template-columns: 1fr; }
  .doc-sidebar { position: relative; top: 0; }
}
</style>

{% assign first_group = page.docs-groups | first %}
{% assign first_doc = first_group.docs | first %}

<div class="container-fluid docs-shell">
  <div class="docs-grid">
    <aside class="doc-sidebar">
      <div class="doc-sidebar__title">技術文件</div>

      {% for group in page.docs-groups %}
      <div class="doc-sidebar__section{% unless forloop.first %}{% endunless %}" data-group="{{ group.slug }}">
        <button class="doc-sidebar__toggle" data-toggle-group="{{ group.slug }}">
          <span>{{ group.label }}</span>
          <span class="doc-sidebar__caret">▾</span>
        </button>
        <div class="doc-list">
          {% for doc in group.docs %}
          <button class="doc-link{% if forloop.first and forloop.parentloop.first %} active{% endif %}" data-doc-target="{{ doc.id }}" data-group="{{ group.slug }}">
            {{ doc.title }}
          </button>
          {% endfor %}
        </div>
      </div>
      {% endfor %}
    </aside>

    <section class="doc-content">
      {% for group in page.docs-groups %}
        {% for doc in group.docs %}
          <div class="doc-body{% if forloop.first and forloop.parentloop.first %} active{% endif %}" data-doc-id="{{ doc.id }}" data-group="{{ group.slug }}">
            <div class="doc-meta"> · 類別：{{ group.label }}</div>
            {% capture doc_md %}{% include {{ doc.include }} %}{% endcapture %}
            {{ doc_md | markdownify }}
          </div>
        {% endfor %}
      {% endfor %}
      <div class="doc-nav">
        <button class="doc-nav__btn" id="doc-prev">
          <span>
            <div class="doc-nav__label">Previous</div>
            <div class="doc-nav__title" data-prev-title>—</div>
          </span>
          <span class="doc-nav__icon">←</span>
        </button>
        <button class="doc-nav__btn" id="doc-next">
          <span>
            <div class="doc-nav__label">Next</div>
            <div class="doc-nav__title" data-next-title>—</div>
          </span>
          <span class="doc-nav__icon">→</span>
        </button>
      </div>
    </section>

    <aside class="doc-toc">
      <div class="doc-toc__title">本頁大綱</div>
      <nav id="doc-toc-list"></nav>
    </aside>
  </div>
</div>

<script>
(function() {
  const links = Array.from(document.querySelectorAll('.doc-link'));
  const bodies = Array.from(document.querySelectorAll('.doc-body'));
  const sections = Array.from(document.querySelectorAll('.doc-sidebar__section'));
  const toggles = Array.from(document.querySelectorAll('[data-toggle-group]'));
  const tocContainer = document.getElementById('doc-toc-list');
  const navPrev = document.getElementById('doc-prev');
  const navNext = document.getElementById('doc-next');
  const prevTitleEl = document.querySelector('[data-prev-title]');
  const nextTitleEl = document.querySelector('[data-next-title]');
  const docOrder = links.map((btn) => ({
    id: btn.dataset.docTarget,
    title: btn.textContent.trim()
  }));

  function slugify(text) {
    return text.toLowerCase()
      .replace(/[^a-z0-9\u4e00-\u9fa5\s-]/g, '')
      .trim()
      .replace(/\s+/g, '-');
  }

  function buildToc(activeBody) {
    if (!tocContainer) return;
    tocContainer.innerHTML = '';
    if (!activeBody) return;

    const headings = activeBody.querySelectorAll('h2, h3');
    headings.forEach((heading) => {
      if (!heading.id) {
        const fallbackId = 'section-' + Math.random().toString(36).slice(2, 8);
        heading.id = slugify(heading.textContent) || fallbackId;
      }
      const link = document.createElement('a');
      link.href = '#' + heading.id;
      link.textContent = heading.textContent;

      const item = document.createElement('div');
      item.className = 'doc-toc__item doc-toc__item--' + heading.tagName.toLowerCase();
      item.appendChild(link);
      tocContainer.appendChild(item);
    });
  }

  function setActive(id) {
    links.forEach((btn) => {
      const isActive = btn.dataset.docTarget === id;
      btn.classList.toggle('active', isActive);
    });
    bodies.forEach((body) => {
      const isActive = body.dataset.docId === id;
      body.classList.toggle('active', isActive);
    });

    const activeBody = bodies.find((b) => b.dataset.docId === id);
    if (activeBody) {
      buildToc(activeBody);
      const group = activeBody.dataset.group;
      sections.forEach((section) => {
        if (section.dataset.group === group) {
          section.classList.remove('collapsed');
        }
      });
      if (id) history.replaceState({}, '', '#' + id);
      updateNav(id);
    }
  }

  function updateNav(currentId) {
    const idx = docOrder.findIndex((d) => d.id === currentId);
    const prev = idx > 0 ? docOrder[idx - 1] : null;
    const next = idx >= 0 && idx < docOrder.length - 1 ? docOrder[idx + 1] : null;

    if (prevTitleEl) prevTitleEl.textContent = prev ? prev.title : '—';
    if (nextTitleEl) nextTitleEl.textContent = next ? next.title : '—';

    if (navPrev) {
      navPrev.disabled = !prev;
      navPrev.dataset.target = prev ? prev.id : '';
    }
    if (navNext) {
      navNext.disabled = !next;
      navNext.dataset.target = next ? next.id : '';
    }
  }

  links.forEach((btn) => {
    btn.addEventListener('click', (e) => {
      e.preventDefault();
      setActive(btn.dataset.docTarget);
    });
  });

  toggles.forEach((btn) => {
    btn.addEventListener('click', () => {
      const section = btn.closest('.doc-sidebar__section');
      section.classList.toggle('collapsed');
    });
  });

  [navPrev, navNext].forEach((btn) => {
    if (!btn) return;
    btn.addEventListener('click', (e) => {
      e.preventDefault();
      const target = btn.dataset.target;
      if (target) setActive(target);
    });
  });

  const initialId = window.location.hash ? window.location.hash.substring(1) : links[0]?.dataset.docTarget;
  setActive(initialId);
})();
</script>
