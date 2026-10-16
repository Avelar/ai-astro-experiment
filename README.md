# Atlas Sonoro — A História da Música no Mundo

Projeto experimental para validar um fluxo simples de publicação editorial: **Codex → Astro → GitHub → Vercel → Pages CMS**. O site é estático; os textos ficam em JSON e Markdown no repositório, separados da apresentação.

## Tecnologias

- Astro 7 com saída estática (SSG)
- Tailwind CSS 4 com o plugin oficial do Vite
- JSON para página inicial, linha do tempo e movimentos
- Markdown com frontmatter YAML para artigos
- Vercel para deploy e Pages CMS para edição Git-based

O projeto usa Node.js 24, npm e não inclui React, backend, SSR ou integrações pagas.

## Instalação e desenvolvimento

Requisitos: Node.js 24 e npm.

```sh
npm install
npm run dev
```

Abra o endereço local informado pelo Astro (normalmente `http://localhost:4321`). Para gerar e conferir o site de produção:

```sh
npm run build
npm run preview
```

O build estático é gerado em `dist/`.

## Estrutura

```text
.
├── .pages.yml                 # coleções e campos do Pages CMS
├── public/images/             # ilustrações SVG próprias e uploads do CMS
├── src/
│   ├── components/            # seções e elementos reutilizáveis
│   ├── content/
│   │   ├── home.json          # textos da página inicial e rodapé
│   │   ├── timeline.json      # eventos da linha do tempo
│   │   ├── movements.json     # movimentos musicais
│   │   ├── blog/*.md          # artigos em Markdown
│   │   └── pages/*.md         # páginas independentes em Markdown
│   ├── layouts/               # estrutura compartilhada
│   ├── pages/                 # rotas estáticas, incluindo /blog/[slug]/
│   └── styles/                # CSS global e Tailwind
├── astro.config.mjs
└── package.json
```

## Conteúdo

Edite `src/content/home.json` para alterar o título, subtítulo, imagem e botão do destaque, introdução, chamada do blog e informações do rodapé. Os campos `image` e `coverImage` usam caminhos públicos, como `/images/hero.svg`.

Edite `src/content/timeline.json` e `src/content/movements.json` para incluir, modificar ou remover itens. Cada arquivo contém uma lista JSON. Preserve a estrutura dos itens e seus números de ordem; os cartões de movimentos também usam `color` com um dos valores `ochre`, `plum`, `coral`, `green` ou `blue`.

Para adicionar um artigo, crie um arquivo `.md` em `src/content/blog/`, usando um nome curto em minúsculas separado por hífens, por exemplo `minha-nova-escuta.md`. Inclua estes metadados no início:

```yaml
---
title: "Título do artigo"
date: 2026-10-15
category: "Categoria"
excerpt: "Um resumo breve que aparece na página inicial."
coverImage: "/images/minha-capa.svg"
coverAlt: "Descrição acessível da imagem"
---

O conteúdo do artigo em Markdown.
```

O nome do arquivo vira o endereço `/blog/minha-nova-escuta/`. Adicione imagens próprias em `public/images/` e use `/images/nome-do-arquivo.ext`.

Para criar uma página independente no Pages CMS, abra **Páginas do site → Add an entry**, preencha o título, resumo e conteúdo. A página é criada a partir do título, publicada em `/<slug>/` e aparece automaticamente no menu **Páginas** do site. Há uma página demonstrativa chamada “Sobre o Atlas Sonoro” que pode ser editada ou removida.

## Publicar na Vercel

1. Envie o repositório para o GitHub e importe-o na Vercel.
2. Se a Vercel pedir os comandos, use **Build Command** `npm run build` e **Output Directory** `dist`.
3. Mantenha o deploy como estático e use a versão de Node indicada pelo projeto (24).
4. A Vercel cria deploys para commits no GitHub. Não é necessário domínio próprio.

## Conectar ao Pages CMS

1. Acesse [Pages CMS](https://app.pagescms.org/) e entre com GitHub.
2. Instale/autorize o aplicativo GitHub para o proprietário do repositório `Avelar/ai-astro-experiment`.
3. Selecione o repositório e a branch principal. O arquivo `.pages.yml` na raiz informa onde editar cada conteúdo.
4. Abra **Página inicial**, **Linha do tempo**, **Movimentos musicais**, **Páginas do site** ou **Artigos do blog**. Salvar alterações cria commits no GitHub; o deploy da Vercel é acionado pelo commit.
5. Imagens enviadas pelos campos do CMS vão para `public/images/` e são referenciadas no site por `/images/...`.

Não há credenciais do CMS nem configuração do CloudCannon neste repositório. A organização de conteúdo e componentes permanece independente do CMS para permitir o teste futuro com CloudCannon.
