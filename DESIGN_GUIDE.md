# DESIGN GUIDE — Painel MH Contabil-Fiscal

Este arquivo é a referência visual obrigatória para todos os HTMLs do projeto.
**Sempre leia este guia antes de criar ou editar qualquer HTML.**

---

## ⚠️ REGRA CRÍTICA — Escala Tipográfica v2 (obrigatória em todos os HTMLs)

> **Esta escala é OBRIGATÓRIA.** Nunca usar `font-size` com valor fixo direto no CSS.
> Sempre declarar as variáveis abaixo no `:root` e referenciar via `var(--fs-*)`.
> Fontes pequenas foram um problema recorrente — nunca descer abaixo de 12px.

```css
:root {
  --fs-micro:  12px;   /* badges, topbar-badge, tool-label               */
  --fs-small:  13px;   /* hints de upload, th de tabela, notas           */
  --fs-body:   15px;   /* texto geral, td, selects, inputs, botões, desc */
  --fs-step:   16px;   /* títulos de etapas, títulos de card             */
  --fs-title:  36px;   /* tool-title (Cormorant Garamond)                */
  --fs-val:    28px;   /* valores monetários nos cards (Cormorant)       */
}
```

### Tabela de uso por elemento

| Elemento                        | Variável       | Valor  |
|---------------------------------|----------------|--------|
| `tool-label`, badges, topbar    | `--fs-micro`   | 12px   |
| `th` de tabela, hints, notas    | `--fs-small`   | 13px   |
| `td`, inputs, selects, botões   | `--fs-body`    | 15px   |
| Títulos de etapas e cards       | `--fs-step`    | 16px   |
| `tool-title` (Cormorant)        | `--fs-title`   | 36px   |
| Valores nos cards de resumo     | `--fs-val`     | 28px   |

---

## Fontes

```html
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
```

- **Corpo / UI:** `'DM Sans', sans-serif` — pesos 300, 400, 500
- **Títulos principais / valores monetários:** `'Cormorant Garamond', serif` — pesos 300–600, itálico disponível
- **Nunca usar** outras fontes ou pesos fora desses

---

## Variáveis CSS — copie exatamente no `:root`

```css
:root {
  --cream:        #f5f0e8;
  --cream2:       #ede7d9;
  --cream3:       #e4dccb;
  --gold:         #a8895a;
  --gold2:        #c4a870;
  --gold3:        #d4bc8e;
  --brown:        #6b4f2e;
  --brown2:       #8a6640;
  --bege:         #a8895a;
  --bege-claro:   #c4a870;
  --bege-bg:      rgba(168,137,90,0.10);
  --bege-border:  rgba(168,137,90,0.25);
  --bg:           #f5f0e8;   /* fundo da página */
  --bg2:          #fff;      /* cards, painéis */
  --bg3:          #ede7d9;   /* campos, áreas internas */
  --border:       rgba(168,137,90,0.15);
  --border2:      rgba(168,137,90,0.28);
  --text1:        #2c1f0e;   /* texto principal */
  --text2:        #5a4228;   /* texto secundário */
  --text3:        #9a7d5a;   /* texto auxiliar */
  --text4:        #c4aa88;   /* labels, placeholders */
  --verde-bg:     rgba(74,124,89,0.08);
  --verde-text:   #3d7a52;
  --vermelho-bg:  rgba(180,60,60,0.08);
  --vermelho-text:#a03030;
  --amarelo-text: #8a6200;
  --azul-text:    #1a4a8a;
  --azul-bg:      rgba(26,74,138,0.08);
}
```

---

## Base do documento

```css
* { margin: 0; padding: 0; box-sizing: border-box; }
body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--text1);
  min-height: 100vh;
}
```

---

## Dependências JS (sempre via CDN)

```html
<!-- SheetJS — leitura de Excel -->
<script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>

<!-- PDF.js — somente em ferramentas que lêem PDF -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
```

---

## Topbar (barra superior fixa)

```css
.topbar {
  display: flex; align-items: center; gap: 12px;
  padding: 0.85rem 2rem;
  background: #fff;
  border-bottom: 0.5px solid var(--border2);
  position: sticky; top: 0; z-index: 10;
}
.btn-back {
  background: none; border: 0.5px solid var(--border2); color: var(--text3);
  padding: 5px 12px; border-radius: 2px; font-size: 12px; cursor: pointer;
  font-family: 'DM Sans', sans-serif; text-decoration: none;
  display: inline-flex; align-items: center; gap: 5px; transition: all 0.2s;
}
.btn-back:hover { color: var(--text1); border-color: var(--bege); }
.topbar-title { font-size: 13px; color: var(--text2); font-weight: 500; }
.topbar-badge {
  margin-left: auto; font-size: 9px; font-weight: 500;
  background: var(--bege-bg); color: var(--bege-claro);
  border: 0.5px solid var(--bege-border);
  padding: 3px 9px; border-radius: 20px;
  letter-spacing: 0.06em; text-transform: uppercase;
}
```

```html
<div class="topbar">
  <a href="index.html" class="btn-back">← Painel</a>
  <span class="topbar-div" style="color:var(--text4)">|</span>
  <span class="topbar-title">Nome da Ferramenta</span>
  <span class="topbar-badge">SETOR CONTÁBIL</span>
</div>
```

---

## Área principal

```css
.main { max-width: 1200px; margin: 0 auto; padding: 2rem; }
```

---

## Cabeçalho da ferramenta

```css
.tool-label  { font-size: 10px; color: var(--text4); letter-spacing: 0.12em; text-transform: uppercase; margin-bottom: 6px; }
.tool-title  { font-family: 'Cormorant Garamond', serif; font-size: 30px; font-weight: 400; color: var(--text1); }
.tool-title em { font-style: italic; color: var(--bege-claro); }
.tool-desc   { font-size: 13px; color: var(--text3); margin-top: 6px; line-height: 1.6; }
```

```html
<div class="tool-header">
  <div class="tool-label">SETOR CONTÁBIL — NOME DA SEÇÃO</div>
  <h1 class="tool-title">Título da <em>Ferramenta</em></h1>
  <p class="tool-desc">Descrição breve da funcionalidade.</p>
</div>
```

---

## Botões

```css
/* Primário — ação principal */
.btn-primary {
  background: var(--bege); color: #fff; border: none;
  border-radius: 2px; padding: 8px 16px;
  font-size: 13px; font-weight: 600; cursor: pointer;
  font-family: 'DM Sans', sans-serif; transition: all 0.2s;
}
.btn-primary:hover { background: var(--bege-claro); }

/* Secundário — ação auxiliar */
.btn-secondary {
  background: none; border: 0.5px solid var(--border2); color: var(--text2);
  border-radius: 2px; padding: 8px 16px;
  font-size: 13px; cursor: pointer;
  font-family: 'DM Sans', sans-serif; transition: all 0.2s;
}
.btn-secondary:hover { border-color: var(--bege); color: var(--text1); }

/* Saldo anterior — ação de conciliação específica */
.btn-conciliar-saldo {
  background: var(--brown); color: #fff; border: none; border-radius: 2px;
  padding: 8px 18px; font-size: 13px; font-weight: 600; cursor: pointer;
  font-family: 'DM Sans', sans-serif; transition: all 0.2s;
}
.btn-conciliar-saldo:hover { background: var(--brown2); }
```

---

## Upload / Importação

```css
.upload-section {
  background: var(--bg2); border: 0.5px dashed var(--border2);
  border-radius: 2px; padding: 2rem; margin-bottom: 1.5rem;
}
.upload-box {
  border: 0.5px dashed var(--border2); border-radius: 2px;
  padding: 1.5rem; text-align: center; cursor: pointer;
  transition: all 0.2s; background: var(--bg3);
}
.upload-box:hover { border-color: var(--bege); background: var(--bege-bg); }
.upload-title { font-size: 13px; font-weight: 500; color: var(--text2); margin-bottom: 4px; }
.upload-hint  { font-size: 11px; color: var(--text4); }
```

---

## Tabela de lançamentos

```css
.lanc-table { width: 100%; border-collapse: collapse; margin-top: 10px; }
.lanc-table th {
  font-size: 9px; letter-spacing: 0.08em; text-transform: uppercase;
  color: var(--text3); font-weight: 500; padding: 10px 12px;
  text-align: left; border-bottom: 0.5px solid var(--border2);
  background: var(--cream2);
}
.lanc-table td {
  font-size: 12px; color: var(--text2); padding: 8px 12px;
  border-bottom: 0.5px solid rgba(184,153,106,0.05); cursor: pointer;
}
.lanc-table tr:hover               { background: rgba(184,153,106,0.07); }
.lanc-table tr.conciliado          { opacity: 0.35; background: rgba(74,124,89,0.06); }
.lanc-table tr.conciliado td       { color: var(--verde-text) !important; font-weight: 400 !important; }
.lanc-table tr.nao-conciliado      { background: rgba(180,60,60,0.04); }
.lanc-table tr.nao-conciliado td   { color: var(--vermelho-text) !important; font-weight: 700; }
.lanc-table tr.selecionado         { background: rgba(184,153,106,0.18) !important; }
.lanc-table tr.selecionado td      { color: var(--gold2) !important; font-weight: 700 !important; }
```

---

## Cards de resumo (métricas)

```css
.cards-resumo {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(200px,1fr));
  gap: 10px; margin-bottom: 1.5rem;
}
.card-resumo {
  background: var(--bg2); border: 0.5px solid var(--border);
  border-radius: 2px; padding: 1rem;
}
.card-resumo-label { font-size: 10px; color: var(--text4); letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 6px; }
.card-resumo-valor { font-family: 'Cormorant Garamond', serif; font-size: 22px; font-weight: 500; }
.card-resumo-sub   { font-size: 10px; color: var(--text4); margin-top: 3px; }
.val-d { color: var(--vermelho-text); }   /* débito */
.val-c { color: var(--verde-text); }      /* crédito */
.val-s { color: var(--amarelo-text); }    /* saldo */
```

---

## Etapas de conciliação (stepper)

```css
.etapa-box { background: var(--bg2); border: 0.5px solid var(--border2); border-radius: 2px; margin-bottom: 1rem; overflow: hidden; }
.etapa-box.etapa-concluida { border-color: var(--verde-text); }
.etapa-header { display: flex; align-items: center; gap: 1rem; padding: 1rem 1.25rem; flex-wrap: wrap; }
.etapa-num { width: 32px; height: 32px; border-radius: 50%; flex-shrink: 0; background: var(--gold); color: #fff; display: flex; align-items: center; justify-content: center; font-size: 14px; font-weight: 700; }
.etapa-num-locked { background: var(--border2); color: var(--text4); }
.etapa-num-done   { background: var(--verde-text); color: #fff; }
.etapa-titulo { font-size: 14px; font-weight: 600; color: var(--text1); }
.etapa-sub    { font-size: 11px; color: var(--text4); margin-top: 2px; }
.etapa-resultado { padding: 0.75rem 1.25rem; border-top: 0.5px solid var(--border); font-size: 12px; background: rgba(74,124,89,0.05); color: var(--verde-text); }
.etapa-resultado.aviso { background: rgba(140,98,0,0.06); color: var(--amarelo-text); }
```

---

## Filter bar (barra de filtros)

```css
.filter-bar {
  display: flex; flex-wrap: wrap; gap: 1rem; align-items: flex-end;
  background: var(--bg2); border: 0.5px solid var(--border);
  border-radius: 2px; padding: 1rem 1.25rem; margin-bottom: 1rem;
}
.filter-label { font-size: 9px; text-transform: uppercase; letter-spacing: 0.1em; color: var(--text4); }
.filter-input {
  background: var(--cream); border: 0.5px solid var(--border2); color: var(--text2);
  padding: 6px 10px; border-radius: 2px; font-size: 12px; outline: none;
  font-family: 'DM Sans', sans-serif; min-width: 180px;
}
.filter-input:focus { border-color: var(--gold); }

/* Botões toggle (Todos / Pendentes / Conciliados) */
.ftog {
  background: none; border: 0.5px solid var(--border2); color: var(--text3);
  padding: 5px 12px; font-size: 11px; cursor: pointer;
  font-family: 'DM Sans', sans-serif; transition: all 0.2s;
}
.ftog:first-child { border-radius: 2px 0 0 2px; }
.ftog:last-child  { border-radius: 0 2px 2px 0; }
.ftog:not(:first-child) { border-left: none; }
.ftog.active { background: var(--gold); color: #fff; border-color: var(--gold); }
```

---

## Badges de grupo / filial

```css
.badge-filial {
  font-size: 9px; padding: 2px 6px; border-radius: 4px;
  background: var(--bg3); border: 0.5px solid var(--border2); color: var(--text3);
}
.grupo-tag {
  font-size: 9px; padding: 2px 7px; border-radius: 10px;
  background: var(--bege-bg); color: var(--bege); border: 0.5px solid var(--bege-border);
  font-weight: 600; letter-spacing: 0.04em;
}
.grupo-tag.saldo-ant { background: rgba(107,79,46,0.12); color: var(--brown2); border-color: rgba(107,79,46,0.3); }
```

---

## Status / resultado de operações

```css
/* Verde — sucesso / conciliado */
background: var(--verde-bg); color: var(--verde-text);
border: 0.5px solid rgba(74,124,89,0.2);

/* Vermelho — erro / pendente */
background: var(--vermelho-bg); color: var(--vermelho-text);
border: 0.5px solid rgba(180,60,60,0.2);

/* Amarelo — aviso / atenção */
background: rgba(140,98,0,0.08); color: var(--amarelo-text);
border: 0.5px solid rgba(140,98,0,0.2);

/* Azul — informação */
background: var(--azul-bg); color: var(--azul-text);
border: 0.5px solid rgba(26,74,138,0.2);
```

---

## Regras gerais de design

- **Border-radius:** sempre `2px` em painéis, inputs e botões. Exceção: badges/pílulas usam `border-radius: 20px`, avatares circulares usam `50%`
- **Bordas:** sempre `0.5px solid` — nunca `1px` exceto em estados ativos especiais
- **Espaçamento:** `padding: 1rem 1.25rem` em painéis internos; `padding: 2rem` na `.main`
- **Valores monetários:** sempre em `Cormorant Garamond`, tamanho mínimo 18px
- **Labels de seção:** sempre em maiúsculas + `letter-spacing: 0.08em`+ `font-size: 9–10px` + `color: var(--text4)`
- **Título com itálico dourado:** `<h1 class="tool-title">Verbo de <em>substantivo</em></h1>`
- **Nunca usar sombras** (`box-shadow`) exceto no float `.selection-info`
- **Sem gradientes** em nenhum elemento
- **Scroll na tabela:** sempre `overflow-x: auto` no container, nunca na página toda

---

## Estrutura mínima de um HTML novo

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nome da Ferramenta — MH Consultoria</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
:root {
  /* ... colar todas as variáveis acima ... */
}
body { font-family: 'DM Sans', sans-serif; background: var(--bg); color: var(--text1); min-height: 100vh; }
</style>
</head>
<body>

<div class="topbar">
  <a href="index.html" class="btn-back">← Painel</a>
  <span style="color:var(--text4)">|</span>
  <span class="topbar-title">SETOR CONTÁBIL — NOME</span>
  <span class="topbar-badge">MH CONTABIL</span>
</div>

<div class="main">
  <div class="tool-header">
    <div class="tool-label">SETOR CONTÁBIL — SEÇÃO</div>
    <h1 class="tool-title">Título da <em>Ferramenta</em></h1>
    <p class="tool-desc">Descrição da ferramenta.</p>
  </div>

  <!-- conteúdo -->
</div>

</body>
</html>
```

---

*Última atualização: extraído dos arquivos razao-fornecedores.html, razao-tributos.html e encontro-contas.html do projeto Painel MH Contabil-Fiscal.*
