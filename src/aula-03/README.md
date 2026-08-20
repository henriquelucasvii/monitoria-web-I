#  Resolução

Este documento explica, atividade por atividade, o que cada exercício resolvido está ensinando. A ideia é que você não apenas copie o código, mas entenda **por que** ele funciona.

---

## Atividade 1 — Conectando HTML e CSS

### O que este exercício ensina
Como **ligar** um arquivo CSS externo a um arquivo HTML usando a tag `<link>`:

```html
<link rel="stylesheet" href="style.css">
```

Essa linha vai dentro do `<head>` e diz ao navegador: *"antes de mostrar essa página, aplique também os estilos definidos em `style.css`"*.

### O que o CSS faz
```css
h1 {
    color: red;
    font-family: 'Montserrat', sans-serif;
    font-size: 100px;
}
```
Aqui usamos um **seletor de tag** (`h1`), que aplica o estilo a **todos** os elementos `<h1>` da página. Repare no `font-family`: sempre colocamos uma fonte alternativa (`sans-serif`) depois da fonte desejada, caso o navegador não consiga carregar a `Montserrat`.

---

## Atividade 2 — Os três tipos de seletores CSS

### O que este exercício ensina
A diferença entre os **três seletores mais usados** em CSS e a ordem de prioridade entre eles:

| Seletor | Sintaxe | Aplica em |
|---|---|---|
| **Tag** | `h1 { }` | Todos os elementos daquele tipo |
| **ID** | `#title { }` | Um único elemento (o `id` deve ser único na página) |
| **Classe** | `.paragrafo { }` | Qualquer elemento com essa classe (pode repetir) |

No HTML:
```html
<h1 id="title">Atividade 2 - Seletores</h1>
<p class="paragrafo">Paragráfo </p>
```

---

## Atividade 3 — Box Model (modelo de caixas)

### O que este exercício ensina
Todo elemento HTML é, na prática, uma **caixa retangular**. O CSS controla essa caixa com quatro propriedades principais:

```css
.caixa {
    background-color: cyan;
    padding: 150px;  /* espaço INTERNO, entre o conteúdo e a borda */
    margin: 20px;    /* espaço EXTERNO, entre a caixa e os outros elementos */
    width: 40px;
    height: 60px;
}
```

### Por que a caixa parece muito maior que 40x60px?
Isso é o ponto-chave do exercício! Por padrão, o `padding` **soma** ao tamanho definido em `width`/`height`. Ou seja, a caixa final fica assim:

- **Largura real:** `40px (width) + 150px (padding-left) + 150px (padding-right)` = **340px**
- **Altura real:** `60px (height) + 150px (padding-top) + 150px (padding-bottom)` = **360px**

```
┌─────────────── padding ───────────────┐
│                                        │
│         ┌──────────────┐              │
│ padding │  width x height │  padding  │
│         └──────────────┘              │
│                                        │
└─────────────── padding ───────────────┘
```

---

## Atividade 4 — Introdução ao Flexbox

### O que este exercício ensina
Como colocar elementos **lado a lado** e distribuí-los no espaço disponível usando **Flexbox**.

```css
.container {
    display: flex;                   /* ativa o flexbox no container */
    justify-content: space-between;  /* distribui o espaço ENTRE as caixas */
    align-items: center;             /* centraliza verticalmente */
    width: 80vw;
    margin: 50px auto;
}
```

- `display: flex` transforma o `.container` em um **flex container**: a partir daí, todos os filhos diretos dele (as `.caixa`) viram **itens flexíveis**, alinhados em linha por padrão.
- `justify-content` controla o alinhamento no **eixo horizontal** (eixo principal).
- `align-items` controla o alinhamento no **eixo vertical** (eixo transversal).
- `margin: 50px auto` centraliza o próprio `.container` na página (o `auto` nas laterais divide o espaço sobrando igualmente).


---

## Atividade 5 — Flexbox com `gap` e Responsividade

### O que este exercício ensina

```css
.container {
    display: flex;
    justify-content: center;
    margin: 20px;
    gap: 50px;
}
```

`gap` cria um espaçamento **entre** os itens do flexbox, sem precisar usar `margin` em cada `.card` individualmente. É mais simples e evita o problema de margem "dobrada" entre elementos vizinhos.

### Responsividade com `@media`
```css
@media (max-width: 768px) {
    .container {
        flex-direction: column;
        align-items: center;
    }
}
```

Essa é a parte mais importante do exercício: o `@media (max-width: 768px)` diz *"aplique esse bloco de CSS apenas quando a tela tiver 768px de largura ou menos"* (ou seja, tablets e celulares).

Dentro dele, `flex-direction: column` faz os `.card` pararem de ficar lado a lado e passarem a ficar **um embaixo do outro** — um comportamento mais adequado para telas estreitas.