---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---

# Présentation de la stack et architecture front



---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---


### Partie 1 : 

<v-clicks>
<h1 style="padding: 2rem 0 0.5rem 0">La stack :</h1>
<h1 style="font-size: 2rem; line-height: 1.75rem">- projet</h1>
<h1 style="font-size: 2rem; line-height: 1.75rem">- applications</h1>

</v-clicks>

---

# Projet 
...

<v-clicks>

*Nb: projet = ensemble des applications front*

Stack :
- Lerna

</v-clicks>

---

# Lerna
...

<v-clicks>

**Définition :** outils de gestion de projets JavaScript

**Pourquoi ?**

Les applications (indépendantes mais de même stack) partagent : 
- dépendances: Vue, TypeScript, Jest, eslint...
- commandes : dev, build, tests...

=> peu maintenable (ex: montée de version)

=> L'outil de gestion de packages : centraliser les dépendances et commandes commune à la racine du projet

</v-clicks>

---

# Pourquoi Lerna ?
...

<v-clicks>

*Autres solutions : Nx, Yarn worskpaces, Bit, Bazel...*

- spécialisé projets JavaScript
- framework agnostique (Nx: très couplé à Angular)

</v-clicks>

---

# Applications

<div style="margin-bottom: 10px">
<v-clicks>

Stack :
- Vue 3
- TypeScript
- Quasar

</v-clicks>
</div>

<v-clicks>

Librairies :
- State management: Pinia (paradigme : API composition - cf après)
- Tests : Jest, Cypress / Storybook

</v-clicks>

---

# Vue
...

<v-clicks>

- Version 3 (octobre 2020) :
  - API de composition (cf partie 3)
  - réécriture en TypeScript

</v-clicks>

---

# TypeScript
...

<v-clicks>

- Typage
- Support natif Vue 3
- Continuité avec Angular 

</v-clicks>

---

# Quasar
...

<v-clicks>

**Définition :** meta-framework basé sur Vue

*Nb: meta-framework = framework de haut niveau écrit sur un autre framework*

</v-clicks>

---

# Pourquoi des meta-frameworks ?
...

<v-clicks>

- Vue : "Le Framework JavaScript Évolutif" *=> UI runtime + routing et state management non imposés*
- Angular : "The modern web developer's platform" *=> langage, directory structure, UI runtime, routing, formulaires, client HTTP, tests...*
- React : "Une bibliothèque JavaScript pour créer des interfaces utilisateurs" *=> UI runtime*

</v-clicks>

<v-clicks>

=> React et Vue : grand flexibilité, mais
- peu de 'cadre' (arborescence, conventions)
- bootstrap plus long (router, tests, linters, ...)
- certaines fonctionalités difficiles à implémenter (SSR)

=> Meta-frameworks vont s'en charger

</v-clicks>

---

# Pourquoi des meta-frameworks ?
...

<v-clicks>

- Vue : Nuxt, Quasar, Gridsome
- React : Next, Gatsby

~~

>"To me, that sounds like React is a kernel. Webpack/Create React App are bootloaders. Next.js and Gatsby are the closest things we've got to distros."
>
>James K Nelson

</v-clicks>


---

# Quasar
...

**Définition :** meta-framework basé sur Vue

*Nb: meta-framework = framework de haut niveau écrit sur un autre framework*

<v-clicks>

**Pourquoi un meta-framework ?**
- bootstrap 
- convensions fortes 
=> unité entre les applications, continuité avec Angular

**Pourquoi Quasar ?**
- support Vue 3
- librairie de style très complète basée sur Material

</v-clicks>

---

# State management : Pinia
...

<v-clicks>

**Définition :** librairie de state management basée sur l'API de composition
- apparue avec Vue 3
- développée par des membres de la core team Vue

**Pourquoi pas Vuex 4 ?** 
- ancien paradigme ('pluggé' sur le système de reactivité) : plus verbeux, moins flexible mais plus 'cadré'
- mutation : RFC Vuex 5 plus proche de Pinia que de Vuex 4

</v-clicks>

---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---

### Partie 2 : 

<v-clicks>
<h1 style="padding: 2rem 0 0.5rem 0">L'architecture :</h1>
<h1 style="font-size: 2rem; line-height: 1.75rem">- projet</h1>
<h1 style="font-size: 2rem; line-height: 1.75rem">- applications</h1>

</v-clicks>

---

# Projet
...

<v-clicks>

Existant composé de SPA indépendantes.

Plusieurs options :
- Web components => peu optimisé
- Webpack module federation => trop jeune

=> SPA indépendantes, mais avec un découpage adapté

</v-clicks>

---

# Applications
...

- modules "domaines"

---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---

### Partie 3 : 

<v-clicks>

<h1 style="padding: 2rem 0 0.5rem 0">L'API de composition</h1>

</v-clicks>

---

# L'API de composition
...

<v-clicks>

**Définition** : Exposition de la configuration des composants sous forme d'API

Permet : 
- d'organiser le code par **'concern'** (et non par options) => intéressant en particulier pour les composants ayant plusieurs responsabilités.
- de **mutualiser** le code (beaucoup mieux qu'avec les mixins par exemple)

</v-clicks>

---

<div grid="~ cols-2 gap-4">
<div>

# Exemple

```html
<Counter name="Mon compteur" />
```
<div style="margin-top: 20px">
<Counter1 name="Mon compteur" />
</div>
</div>
<div style="margin-top: -30px">

```html
<script>
export default {
    props: {
        name: { type: String, required: true}
    },
    data() {
        return { counter: 0 }
    },
    computed: {
        doubleCounter() { return this.counter * 2 }
    },
    methods: {
        reinitializeCounter() { this.counter = 0 }
    }
}
</script>
<template>
  <h3>{{name}}</h3>
  <div>
    <div flex="~" w="min" border="~ gray-400 opacity-50 rounded-md">
      <Button @click="counter -= 1">-</Button>
      <span m="auto" p="2" border="r l gray-400 opacity-50">{{ counter }}</span>
      <Button @click="counter += 1">+</Button>
    </div>
    <div>Double compteur : {{doubleCounter}}</div>
    <Button @click="reinitializeCounter">Réinitialiser</Button>
  </div>
</template>
```

</div>
</div>

---

# Option API vs Composition API

<div grid="~ cols-2 gap-4">
<div>

```ts
export default {
    props: {
        name: { type: String, required: true}
    },
    data() {
        return { counter: 0 }
    },
    computed: {
        doubleCounter() { return this.counter * 2 }
    },
    methods: {
        reinitializeCounter() { this.counter = 0 }
    }
}
```

</div>

<div>

```ts {all|4-7|8|9|10|all}
import Button from './Button.vue'
import { ref, computed } from 'vue'

const props = defineProps({
  name: { type: String, required: true },
})
const name = props.name
const counter = ref(0)
const doubleCounter = computed(() => counter.value * 2)
const reinitializeCounter = () => counter.value = 0
```

</div>
</div>




---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---
# Fin

