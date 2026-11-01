# GVG & ARTEFAL — PWA (shell de instalação)

Este diretório é o shell instalável que abre o sistema já existente em Google Apps Script dentro do próprio app.
O backend, Google Sheets, permissões e o dashboard atual **não foram reescritos**.

## Arquitetura

```
GitHub Pages (PWA: shell + manifest + service worker + ícones)
        └── iframe em tela cheia → Google Apps Script /exec (sistema real)
```

O `index.html` carrega o `/exec` em um iframe que ocupa a tela inteira. Nessa forma de
incorporação o aviso azul do Google ("Este aplicativo foi criado por um usuário do Google
Apps Script") **não é exibido**, e o usuário permanece na URL do GitHub Pages, sem ser
redirecionado para `script.google.com`.

O service worker faz cache apenas do shell, manifest e ícones. O sistema continua no Google
Apps Script e exige internet e conta Google autorizada.

## Arquivos

- `index.html` — shell em tela cheia + iframe do app + instalação + instruções iOS/Android.
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

Abra a URL do GitHub Pages no Chrome e use **📲 Instalar** no canto inferior direito.

### iPhone

No Safari, abra a URL do GitHub Pages e use **Compartilhar → Adicionar à Tela de Início**.
O atalho permanece no GitHub Pages e abre o Apps Script no iframe, sem a faixa azul do Google.
Não há redirecionamento automático para `script.google.com`.

Se o atalho antigo ainda mostrar o ícone anterior, apague-o da Tela de Início e adicione de novo,
pois o iOS mantém o ícone em cache. Os arquivos `*-v3.png` foram versionados para forçar a troca.

> No iOS, o Safari pode bloquear cookies de terceiros dentro do iframe. Se o login não
> funcionar, use o link **Problemas para abrir? Toque aqui**, que só aparece após 15 segundos
> sem carregamento.

## Atualizações

O service worker usa `CACHE = 'gvg-artefal-pwa-v11'`. Ao publicar uma nova versão do shell,
incremente esse valor para invalidar o cache antigo. O conteúdo do Apps Script é atualizado
pelo próprio Apps Script; os funcionários não precisam reinstalar o PWA.

A navegação do shell é *network-first*: alterações no `index.html` aparecem no próximo
carregamento, mesmo sem trocar a versão do cache.

## Ícone oficial

Os ícones foram gerados a partir da arte oficial `Emblema Metálico GVG&ARTEFAL.png`:

- `icons/icon-192-v3.png`
- `icons/icon-512-v3.png`
- `icons/icon-maskable-512-v3.png`
- `icons/apple-touch-icon-v3.png`
- `icons/favicon-32-v3.png`
- `icons/favicon-v3.ico`

Os nomes terminam em `-v3` para forçar a atualização do ícone em navegadores que já
tinham o PWA instalado. O maskable foi criado com margem de segurança sobre fundo escuro.
