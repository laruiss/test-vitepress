# Commencer avec VueDsfr

Ceci est le guide d̛’utilisation de la bibliothèque. Si vous cherchez à contribuer, se référer au
[Guide du développeur](/guide-developpeur).

## Utiliser create-vue-dsfr (fortement recommandé)

La façon la plus simple de commencer un projet est d’utiliser le package `create-vue-dsfr`, qui permet de créer un projet
NPM avec tout le nécessaire pour développer un projet utilisant VueDsfr, que ce soit pour Vite (Vue3) ou pour Nuxt 3 (Nuxt3),
avec ou sans TypeScript.

Avec npm :

```shell
npm init vue-dsfr
```

Avec pnpm :

```shell
pnpm create vue-dsfr
```

Avec yarn :

```shell
yarn create vue-dsfr
```

Et suivez les indications de l’assistant.

## Ajouter la bibliothèque à un projet existant

### Utiliser la bibliothèque en tant que plugin

| Notes :              |
|:---------------------------|
| Pour utiliser cette bibliothèque, il vous faudra **[Vue 3](https://v3.vuejs.org/)** (et **[Vue-Router 4](https://next.router.vuejs.org/)**). Par conséquent, si vous utilisez Nuxt, il vous faut **[Nuxt 3](https://v3.nuxtjs.org/)** (plus de détails plus loin). |

#### Installer la bibliothèque en tant que dépendance du projet

Afin d'installer la bibliothèque, taper ces commandes dans votre console au sein du répertoire du projet :

```shell
npm install @gouvfr/dsfr @gouvminint/vue-dsfr
```

::: info

`@gouvminint/vue-dsfr` utilise le CSS de `@gouvfr/dsfr`, c’est pourquoi il faut l’installer aussi.

:::

#### Ajouter le plugin

##### Dans une application Vite (recommandé) ou Vue-CLI

À partir d'un fichier `main.js` simple comme celui-ci :

```js
import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)
  .mount('#app')
```

ajouter les lignes suivantes :

```typescript{2-4,9}
import { createApp } from 'vue'
import '@gouvfr/dsfr/dist/dsfr.min.css'      // Import des styles du DSFR //
import '@gouvminint/vue-dsfr/styles'         // Import des styles globaux propre à VueDSFR //
import VueDsfr from '@gouvminint/vue-dsfr'   // Import (par défaut) de la bibliothèque //

import App from './App.vue'

const app = createApp(App)
  .use(VueDsfr)                              // Enregistrement de la bibliothèque en tant que plugin //
  .mount('#app')
```

##### Dans nuxt 3

La bibliothèque **`VueDsfr`** fournit bien plusieurs builds (`esm` et `umd`) et Nuxt3 sait lequel choisir.

Ensuite, il faut ajouter le plugin en créant le dossier `/plugins` s’il n’existe pas et en créant dedans un fichier `vue-dsfr.js`
avec le contenu suivant :

```typescript
// /plugins/vue-dsfr.js

import { defineNuxtPlugin } from '#app'
import VueDsfr from '@gouvminint/vue-dsfr'

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(VueDsfr)
})
```

Enfin, il faudra ajouter les feuilles CSS, pour ce faire, ajouter ceci dans `nuxt.config.js` :

```typescript{4-7}
import { defineNuxtConfig } from 'nuxt3';
// https://v3.nuxtjs.org/docs/directory-structure/nuxt.config
export default defineNuxtConfig({
 css: [
   '@gouvfr/dsfr/dist/dsfr.min.css',
   '@gouvminint/vue-dsfr/styles',
 ],
})
```

Vous pouvez voir une implémentation **[sur Codesandbox ici](https://codesandbox.io/p/github/laruiss/nuxt-dsfr/nuxt-dsfr)**.

## Utiliser la bibliothèque de composants sans plugin

Pour les petits projets, il est possible de ne pas importer tous les composants, et de sélectionner
les composants utilisés :

```js{2,16}=
import { createApp } from 'vue'
import { OhVueIcon } from 'oh-vue-icons'        // Import du composant OhVueIcon du pkg oh-vue-icons

import App from './App.vue'
import {
  DsfrHeader,
  DsfrButton,
  DsfrBreadcrumb,
  DsfrCard,
} from '@gouvminint/vue-dsfr'                   // Imports nommés de la bibliothèque

import '@gouvfr/dsfr/dist/dsfr.min.css'         // Import des styles du DSFR
import '@gouvminint/vue-dsfr/styles'            // Import des styles propres à la bibliothèque VueDSFR

const app = createApp(App)
  .component('VIcon', OhVueIcon)                // Enregistrement global du composant OhVueIcon
  .component('DsfrHeader', DsfrHeader)          // Enregistrement global du composant DsfrHeader
  .component('DsfrButton', DsfrButton)          // Enregistrement global du composant DsfrButton
  .component('DsfrBreadcrumb', DsfrBreadcrumb)  // Enregistrement global du composant DsfrBreadcrumb
  .component('DsfrCard', DsfrCard)              // Enregistrement global du composant DsfrCard
  .mount('#app')
```

:::info
N.B. : il faut bien en plus enregistrer globalement le composant **VIcon** car il est utilisé en interne dans VueDsfr.
:::

## Utiliser les icônes officielles

Pour utiliser les icônes officielles avec les classes CSS du DSFR, il n’y a pas d’actions en plus à faire,
puisque c’est le CSS officiel du DSFR qui est utilisé.

## Ajouter des icônes

Pour ajouter des icônes qui ne sont pas importées dans la bibliothèque, veuillez consulter
[la page dédiée](/icones-personnalisees).

## Avoir un bundle minimal

Il est possible d’intégrer moins de CSS pour les petits projets.

### Vue3

Dans le point d’entrée de votre application Vue (souvent `main.js` ou `main.ts`) :

```typescript
import '@gouvfr/dsfr/dist/core/core.main.min.css'            // Le CSS minimal du DSFR
import '@gouvfr/dsfr/dist/component/component.main.min.css'  // Styles de tous les composants du DSFR
import '@gouvfr/dsfr/dist/utility/utility.main.min.css'      // Classes utilitaires : les composants de VueDsfr en ont besoin
import '@gouvminint/vue-dsfr/styles'                         // Les styles propres aux composants de VueDsfr

import '@gouvfr/dsfr/dist/scheme/scheme.min.css'             // Facultatif : Si les thèmes sont utilisés (thème sombre, thème clair)
import '@gouvfr/dsfr/dist/utility/icons/icons.min.css'       // Facultatif : Si des icônes sont utilisées avec les classes "fr-icon-..."
```

### Nuxt3

Dans `nuxt.config.js` :

```typescript
export default defineNuxtConfig({
  css: [
    '@gouvfr/dsfr/dist/core/core.main.min.css',           // Le CSS du DSFR
    '@gouvfr/dsfr/dist/component/component.main.min.css'  // Styles de tous les composants du DSFR
    '@gouvfr/dsfr/dist/utility/utility.main.min.css'      // Classes utilitaires : les composants de VueDsfr en ont besoin
    '@gouvminint/vue-dsfr/styles',                        // Les styles propres aux composants de VueDsfr

    '@gouvfr/dsfr/dist/scheme/scheme.min.css'             // Facultatif : Si les thèmes sont utilisés (thème sombre, thème en bernes)
    '@gouvfr/dsfr/dist/utility/icons/icons.min.css',      // Facultatif : Si des icônes sont utilisées avec les classes "fr-icon-..."
  ],
  ignore: [
    '**/*.test.*',
    '**/*.spec.*',
    '**/*.cy.*',
  ],
})
```
