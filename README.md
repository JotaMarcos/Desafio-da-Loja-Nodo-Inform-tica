# Desafio da Loja Nodo Informática

Site institucional com catálogo e montagem de pedido para a **Nodo Informática**, uma loja fictícia de computadores, redes e proteção de dados para pequenas e médias empresas.

Projeto feito com **HTML5, CSS3, JavaScript (ES2015+) e Bootstrap 5.3**, seguindo a *Apostila de Desenvolvimento Web I* (Faculdade Senac AM – FATESE).

> Produtos, preços e contatos são fictícios.

## Sobre o desafio

O desafio era reestruturar o site da loja aplicando boas práticas de desenvolvimento web: HTML semântico, separação de responsabilidades, acessibilidade, usabilidade, desempenho e segurança. O resultado é uma página única dividida em quatro seções:

| Seção | O que tem |
| --- | --- |
| **A empresa** | Apresentação, linhas de produto, forma de trabalho e horários de atendimento |
| **Produtos** | Catálogo com filtro por linha, busca e montagem do pedido |
| **Contato** | Formulário com validação que gera uma mensagem pronta para WhatsApp ou e-mail |
| **Perguntas frequentes** | Respostas sobre pedido, pagamento, entrega, garantia e trocas |

## Funcionalidades

- **Catálogo** com 12 produtos em três linhas: computadores e notebooks, redes e conectividade, armazenamento e proteção.
- **Busca que ignora acentos**: "protecao" encontra "proteção". A página também mostra quantos produtos foram encontrados.
- **Pedido** com quantidades, subtotal e total. Ele fica salvo no navegador (`localStorage`) e é sincronizado entre abas.
- **Solicitar pedido** leva ao formulário de contato com a lista de produtos já na mensagem.
- **Formulário de contato** valida nome, e-mail, telefone com DDD e mensagem, e gera o texto para enviar por WhatsApp, por e-mail ou para copiar.
- **Tema claro e escuro**, conforme a preferência do sistema.

## Tecnologias

- HTML5 semântico, com `<template>` para os itens criados dinamicamente
- CSS3 com variáveis (tokens) e tema escuro via `prefers-color-scheme`
- JavaScript puro, sem frameworks nem build
- [Bootstrap 5.3.3](https://getbootstrap.com/), somente o CSS, carregado por CDN com SRI
- Fontes do Google Fonts: Chakra Petch, IBM Plex Sans e IBM Plex Mono

## Como executar

Não há build nem dependências para instalar.

1. Clone o repositório:
   ```bash
   git clone https://github.com/JotaMarcos/Desafio-da-Loja-Nodo-Inform-tica.git
   ```
2. Abra a pasta no VS Code.
3. Clique com o botão direito em `index.html` e escolha **Open with Live Server**.

Abrir o `index.html` com dois cliques também funciona. A única diferença está nos botões **Copiar**: sem servidor (`file://`), o navegador bloqueia a área de transferência, então o texto fica selecionado para você copiar com `Ctrl+C`.

## Estrutura

```
├── index.html            # Estrutura e conteúdo (HTML5 semântico)
├── assets/
│   ├── css/style.css     # Aparência: tokens, tema escuro e personalização do Bootstrap
│   ├── js/dados.js       # Dados: linhas, produtos e contatos
│   ├── js/icones.js      # Ícones SVG dos produtos
│   ├── js/app.js         # Comportamento: navegação, catálogo, pedido e formulário
│   └── img/favicon.svg
└── README.md
```

Cada camada tem uma responsabilidade (Unidade 1.2). O HTML guarda a marcação, inclusive a dos itens dinâmicos. O CSS cuida da aparência. O JavaScript só troca atributos e classes. Para mudar um produto ou um preço, basta editar `dados.js`.

## Boas práticas aplicadas

### Acessibilidade (Unidade 5)
- `lang="pt-BR"`, link **Pular para o conteúdo** e títulos em hierarquia correta (`h1` → `h4`).
- Navegação com `<nav>` e `aria-current="page"`. Ao trocar de seção, o foco vai para o título dela e o `<title>` da aba muda.
- O foco não se perde ao usar os filtros ou os botões + e − do pedido.
- Uma região `aria-live` anuncia produto adicionado, quantidades, cópia e erros.
- Os botões "Adicionar ao pedido" dizem qual é o produto, e o nome acessível começa pelo texto visível (WCAG 2.5.3).
- No formulário: `required`, `autocomplete`, `inputmode`, erros ligados ao campo por `aria-describedby` e foco no primeiro campo com erro.
- Foco sempre visível, alvos de toque de 40 a 44 px, contraste AA nos dois temas e respeito a `prefers-reduced-motion`.
- As perguntas frequentes usam `<details>` nativo, que funciona sem JavaScript e sem ARIA extra.

### Desempenho (Unidades 6.4 e 6.7)
- O catálogo é montado **uma única vez** com `DocumentFragment`. Filtrar só liga e desliga o atributo `hidden`.
- A busca tem *debounce* de 200 ms.
- Scripts com `defer`, `preconnect` para as CDNs e `font-display: swap`.
- Um único ouvinte de clique para a página toda (delegação de eventos).
- O `bootstrap.bundle.js` não é carregado. O toast é exibido com poucas linhas próprias.

### Segurança (Unidade 11.4)
- Os dados entram no DOM por `textContent`, nunca por `innerHTML`. A única exceção são os ícones SVG estáticos de `icones.js`.
- `rel="noopener"` nos links que abrem nova aba e SRI no Bootstrap.

### Progressive enhancement (Unidade 1.2)
Sem JavaScript, todas as seções aparecem em sequência e os links do menu rolam até elas. A busca e os filtros só aparecem quando podem funcionar.

## Testes realizados

- Testes automatizados no Microsoft Edge (headless), com 33 verificações: navegação e foco, filtros, busca, pedido (total, foco e persistência), validação do formulário, link de pular conteúdo, ausência de rolagem horizontal em 375 px e console sem erros.
- Inspeção visual no desktop (tema claro) e no celular (tema escuro).

Para complementar, vale rodar o Lighthouse e o axe DevTools, navegar só com o teclado e testar com o leitor de tela NVDA (Unidade 5.6).

## Autor

**João Marcos Duarte** ([@JotaMarcos](https://github.com/JotaMarcos))
