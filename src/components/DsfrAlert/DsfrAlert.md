# DsfrAlert

Les alertes permettent d’attirer l’attention de l’utilisateur sur une information sans interrompre sa tâche en cours.

L’alerte est disponible en deux tailles :

- taille médium (MD, par défaut, si la prop `small` est absente ou à `false`) et
- petite taille ‘SM’ si la prop `small` est à `true`.

La documentation sur l’alerte sur le [DSFR](https://www.systeme-de-design.gouv.fr/elements-d-interface/composants/alerte)

La story sur l’alerte sur le storybook de [VueDsfr](https://vue-dsfr.netlify.app/?path=/docs/composants-dsfralert--docs)

## Structure

L’alerte est composée des éléments suivants :

- un titre (prop `title`, de type `string`) :
  - obligatoire sur la version MD (si la prop `small` est absente ou à `false`),
  - optionnel sur la version SM (si la prop `small` est à `true`).
- un pictogramme et une couleur déterminés par la prop `type` qui peut valoir une des chaînes suivantes :
  - `'info'` (valeur par défaut si la prop `type` est absente)
  - `'success'`
  - `'warning'`
  - `'error'`
- un texte de description (avec la prop `description`, de type `string`) :
  - optionnel sur la version MD
  - obligatoire sur la version SM
- une croix de fermeture si la prop `closeable` est à `true`

Autres props :

- `closed` sert à indiquer si l’alerte doit être présente (`false`) ou non (`true`) dans le DOM.
- `titleTag` permet d’indiquer la balise à utiliser pour le `title` : il s’agit de `h3` par défaut, cependant, pour passer les tests RGAA, il faut que les niveaux de titres se suivent et soient cohérents (par exemple, si sur la page il n’y a pas de h2, il faut que le titre de la modal soit un `h2`).

## Toutes les variantes d’Alertes

::: code-group

<Story data-title="Preview" min-h="1600px" dark>
  <DsfrAlertDemo />
</Story>

<<< docs-demo/DsfrAlertDemo.vue [Code de la démo]

<<< DsfrAlert.vue
:::

<script setup lang="ts">
import DsfrAlertDemo from './docs-demo/DsfrAlertDemo.vue'
</script>
