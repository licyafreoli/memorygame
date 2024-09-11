# Jogo da Memória

## Descrição

O Jogo da Memória é um jogo interativo de memória baseado em cartas. O objetivo é encontrar pares de cartas idênticas em um tabuleiro embaralhado. Este projeto foi desenvolvido utilizando Vue.js para a construção da interface e Eleven (11ty) para o gerenciamento do conteúdo do blog associado ao projeto.

## Funcionalidades

- **Níveis de Dificuldade**: Três níveis de dificuldade (Fácil, Médio e Difícil) com diferentes conjuntos de imagens.
- **Responsividade**: O layout é adaptativo e funciona bem em diferentes tamanhos de tela.
- **Temporizador**: Um temporizador para acompanhar o tempo gasto no jogo.
- **Pontuação**: Sistema de pontuação para avaliar o desempenho do jogador.

## Tecnologias Utilizadas

- **Vue.js**: Framework JavaScript para a construção da interface.
- **Eleven (11ty)**: Gerador de site estático para o blog associado.
- **HTML5** e **CSS3**: Tecnologias fundamentais para a estrutura e estilo do jogo.
- **Unsplash API**: Fonte para as imagens utilizadas no jogo.

## Instruções para Desenvolvimento

1. **Clone o Repositório**

   ```bash
   git clone https://github.com/usuario/repo.git
   cd repo


# This repo is no longer maintained. Consider using `npm init vite` and selecting the `svelte` option or — if you want a full-fledged app framework — use [SvelteKit](https://kit.svelte.dev), the official application framework for Svelte.

---

# svelte app

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:8080](http://localhost:8080). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for *any* path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Using TypeScript

This template comes with a script to set up a TypeScript development environment, you can run it immediately after cloning the template with:

```bash
node scripts/setupTypeScript.js
```

Or remove the script via:

```bash
rm scripts/setupTypeScript.js
```

If you want to use `baseUrl` or `path` aliases within your `tsconfig`, you need to set up `@rollup/plugin-alias` to tell Rollup to resolve the aliases. For more info, see [this StackOverflow question](https://stackoverflow.com/questions/63427935/setup-tsconfig-path-in-svelte).

## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build

