# Setup: SEO vs GEO Demo — pro nového collaboratora

Toto jsou instrukce pro nastavení lokálního prostředí pro práci na projektu **SEO vs GEO Demo**. Projekt je interaktivní edukativní web porovnávající SEO a GEO optimalizaci obsahu.

**Live web:** https://seo-vs-geo-demo.netlify.app
**GitHub repo:** https://github.com/jorgesedlista/seo-vs-geo-demo

---

## Co potřebuješ mít nainstalované

Před začátkem ověř, že máš:
- **Git** (`git --version`)
- **Node.js** (`node --version`)
- **npm** (`npm --version`)
- **GitHub účet** s přijatou pozvánkou do repo (username: koprifka)

Pokud něco chybí, nainstaluj to.

---

## Krok 1: Naklonuj repo

```bash
git clone https://github.com/jorgesedlista/seo-vs-geo-demo.git
cd seo-vs-geo-demo
```

---

## Krok 2: Nainstaluj Netlify CLI

```bash
npm install -g netlify-cli
```

---

## Krok 3: Přihlas se do svého Netlify účtu

Pokud ještě nemáš Netlify účet, vytvoř si ho zdarma na https://app.netlify.com (stačí přes GitHub login).

```bash
netlify login
```

Otevře se prohlížeč, přihlas se.

---

## Krok 4: Vytvoř si vlastní preview site

Spusť v adresáři projektu:

```bash
netlify sites:create --name seo-geo-preview-katka
```

(Název si zvol libovolně, musí být unikátní.)

Potom propoj lokální složku s tímto site:

```bash
netlify link --name seo-geo-preview-katka
```

---

## Krok 5: Ověř, že vše funguje

```bash
netlify deploy --dir=. --prod
```

Měla bys vidět URL tvého preview site, např. `https://seo-geo-preview-katka.netlify.app`. Otevři ji v prohlížeči a ověř, že stránka funguje.

---

## Jak pracovat na projektu

### Stáhni nejnovější verzi
```bash
cd seo-vs-geo-demo
git pull
```

### Edituj s Claudem
```bash
claude
```
Claude si přečte CLAUDE.md v repo a bude vědět, jak projekt funguje — jaký je design system, jak přidávat hotspoty, jak editovat tooltipy atd.

### Zobraz si preview
```bash
netlify deploy --dir=. --prod
```
Otevři svou preview URL v prohlížeči.

### Pošli změny na GitHub
```bash
git add index.html
git commit -m "popis co jsi změnila"
git push
```

Jirka si tvoje změny stáhne a nasadí na produkční URL, až budou připravené.

---

## Struktura projektu

```
seo-vs-geo-demo/
├── index.html      ← Celý web v jednom souboru (HTML + CSS + JS)
├── CLAUDE.md       ← Dokumentace pro Clauda (design system, jak editovat)
├── netlify.toml    ← Konfigurace deploye
└── .gitignore
```

Žádný build, žádné závislosti, žádný framework. Edituje se jen `index.html`.

---

## Důležité

- **Produkční URL** (seo-vs-geo-demo.netlify.app) deployuje Jirka
- **Tvoje preview URL** je jen pro tebe — ukazuješ na ní svoje rozpracované změny
- Před pushnutím vždy udělej `git pull`, aby ses vyhnula konfliktům
- Všechny instrukce pro editování obsahu, hotspotů a tooltipů najdeš v `CLAUDE.md` v repo
