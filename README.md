# GVG & ARTEFAL — PWA (shell de instalação)

Este diretório é o shell instalável que abre o sistema já existente em Google Apps Script.
O backend, Google Sheets, permissões e o dashboard atual **não foram reescritos**.

## Arquitetura

```
GitHub Pages (PWA shell: manifest + service worker + ícones)
        └── iframe → Google Apps Script /exec (sistema real)
```

O Apps Script foi configurado com `XFrameOptionsMode.ALLOWALL` para permitir a incorporação.
O service worker faz cache apenas do shell (HTML, manifest, ícones). O sistema dentro do iframe
continua exigindo internet e conta Google autorizada.

## Arquivos

- `index.html` — shell PWA + botão de instalação + instruções iOS/Android.
- `manifest.webmanifest` — nome, ícones, cores, `standalone`, `start_url` e `scope`.
- `sw.js` — service worker com versionamento de cache.
- `icons/` — favicon, ícones 192/512, maskable e Apple Touch Icon.
- `.nojekyll` — necessário para GitHub Pages.

## Publicar no GitHub Pages

Este é um repositório dedicado somente ao app de Fornecedores:

- Repositório: `higoragenteia/gvg-fornecedores`
- URL: `https://higoragenteia.github.io/gvg-fornecedores/`

Em **Settings → Pages**, use a branch `main` e a pasta `/ (root)`.

> Repositório privado no GitHub Pages exige plano GitHub Pro/Team/Enterprise.
> Este repositório está público para usar o Pages gratuito.

## Instalação

### Android

Abra a URL do GitHub Pages no Chrome e use **📲 Instalar** na barra superior do shell. O Chrome exige HTTPS, manifest válido e service worker — todos presentes.

### iPhone

No Safari, abra a URL do GitHub Pages e use **Compartilhar → Adicionar à Tela de Início**.
Também é possível adicionar diretamente a URL `/exec` do Apps Script à Tela de Início.

## Atualizações

O service worker usa `CACHE = 'gvg-artefal-pwa-v2'`. Ao publicar uma nova versão do shell,
incremente esse valor para invalidar o cache antigo. O conteúdo do Apps Script é atualizado
pelo próprio Apps Script; os funcionários não precisam reinstalar o PWA.

## Ícone oficial

Os ícones foram gerados a partir da arte oficial:

`Parceria GVG & Artefal em Ouro.png`

Arquivos gerados:

- `icons/icon-192.png`
- `icons/icon-512.png`
- `icons/icon-maskable-512.png`
- `icons/apple-touch-icon.png`
- `icons/favicon-32.png`
- `icons/favicon.ico`

O maskable foi criado com margem de segurança de 10% em fundo escuro.
