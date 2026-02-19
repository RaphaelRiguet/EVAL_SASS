# EVAL_SASS

```bash
npm install # Initialise un nouveau projet Node.js avec les paramètres par défaut
```

```bash
"watch": "sass --watch assets/scss/style.scss:assets/css/style.css" # Surveille les fichiers Sass pour les modifications et recompile automatiquement en temps réel
````


> Ce dépôt contient un petit projet SASS pour apprendre à structurer des styles et réutiliser des composants.

## Réutilisation des boutons

Les boutons sont des composants courants dans les interfaces web. Une bonne organisation CSS/Sass permet de les réutiliser facilement avec des variantes (couleurs, tailles, états) et sans duplication de code.



### 1 Exemple adapté à votre code

Votre fichier `modules/button.scss` utilise une imbrication autour de `button` et applique des modificateurs avec la syntaxe BEM (ex. `.button--primary`, `.button--primary--rounded`, etc.). Voici un passage commenté et un moyen de conserver cette organisation tout en généralisant les styles:

```scss
// assets/scss/modules/button.scss
button {
  &.button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    color: #ffffff;

    &--primary {
      background-color: #241edb;
      &--rounded {
        border-radius: 50px;
        background-color: #241edb;
      }
      &--output {
        background-color: #ffffff;
        color: #17a2b8;
        border: 2px solid #17a2b8;
      }
    }
    // autres variantes...
  }
}
```

Pour réduire la duplication et faciliter la création de nouvelles variantes:

* Déplacer les valeurs de couleur/espacement vers des variables.
* Transformer le bloc de base en un mixin ou un placeholder (`%button-base`).
* Utiliser le mixin pour implémenter chaque modificateur BEM.

```scss
// mixins.scss
@mixin button-base($bg, $color: #fff) {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  color: $color;
  background-color: $bg;
  cursor: pointer;

  &:hover { opacity: 0.9; }
}
```

Cette approche conserve votre nomenclature existante tout en rendant chaque variante facile à maintenir ou étendre.

---

### 2. Exemples d'utilisation HTML

```html
<a href="#" class="btn btn--primary">Principal</a>
<button class="btn btn--secondary">Secondaire</button>
``` 

Grâce aux mixins et placeholders, vous pouvez ajouter d'autres variantes sans répéter le code.

### 3. Bonnes pratiques

1. Gardez les styles génériques dans des modules indépendants.
2. Nommez les classes selon la méthodologie BEM (`.btn--large`, `.btn--danger`).
3. Utilisez des variables pour les thèmes et facilitez l'overload.
4. Testez les états (hover, focus, disabled) dans `states.scss`.

### 5. Compilation

Configurez votre workflow (gulp, webpack, etc.) pour compiler `style.scss` qui importe les différents fichiers:

```scss
// style.scss
@import "variables";
@import "mixins";
@import "states";
@import "modules/button";
```


# Les cards possèdent un modèle de base et des variantes plus petites pour la galerie de cards et pour la card sans image



# exemple de grille a une collone:
```scss
&__col-12{
            width: 100%;
            background-color: blue;
            height: 50px;
            border-radius: 10px;
            color: white;
            margin-top: 10px;

        }

on utilise width: 100% pour que la colonne prenne toute la largeur de la grille.



# les grilles responsives

on peut faire des grilles responsives en utilisant les mixins, par exemple:

@mixin telephone{
    @media (max-width: templates.$telephone){
        @content;
    }
}

.container{

    &__grilleresponsive{
        @include telephone{
            display: flex !important;
            flex-direction: column !important;
            justify-content: center;
            align-items: center;
            gap: 10px;


            &-bleu{
                width: 40%;
                background-color: blue;
                height: 50px;
                border-radius: 10px;
                color: white;
                margin-top: 10px;
            }
            &-gris{
                width: 40%;
                background-color: gray;
                height: 50px;
                border-radius: 10px;
                color: white;
                margin-top: 10px;
            }
        }
    }
}



---