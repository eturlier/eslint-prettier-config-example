
# Configuration Prettier

## 1. Fichier `prettier.config.json` (sans commentaires)


```
{
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "quoteProps": "as-needed",
  "arrowParens": "always",
  "bracketSpacing": true,
  "htmlWhitespaceSensitivity": "css",
  "singleAttributePerLine": false,
  "bracketSameLine": false,
  "endOfLine": "lf",
  "proseWrap": "preserve",
  "plugins": ["@trivago/prettier-plugin-sort-imports"],
  "importOrder": [
    "^@angular/(.*)$",
    "^@core/(.*)$",
    "^@utils/(.*)$",
    "^@shared/(.*)$",
    "^[./]"
  ],
  "importOrderSeparation": true,
  "importOrderSortSpecifiers": true,
  "importOrderParserPlugins": ["typescript", "decorators-legacy"],
  "overrides": [
    {
      "files": "*.component.html",
      "options": {
        "parser": "angular"
      }
    },
    {
      "files": "*.scss",
      "options": {
        "singleQuote": false
      }
    }
  ]
}


```



## 2. Explications détaillées

### Paramètres généraux

-   **`printWidth`: 100**  
    Définit la largeur de ligne maximale avant que Prettier ne fasse un retour à la ligne. Ici, 100 caractères.
    
-   **`tabWidth`: 2**  
    Utilise 2 espaces pour chaque niveau d’indentation.
    
-   **`useTabs`: false**  
    Indique qu’on n’utilise pas d’onglets (\t) pour l’indentation, mais des espaces.
    
-   **`semi`: true**  
    Force l’ajout d’un point-virgule (`;`) en fin d’instruction.
    
-   **`singleQuote`: true**  
    Utilise des guillemets simples au lieu de guillemets doubles pour les chaînes de caractères dans le code JavaScript/TypeScript.
    
-   **`trailingComma`: "all"**  
    Ajoute une virgule finale (trailing comma) après le dernier élément d’un objet, d’un tableau, ou dans les paramètres de fonctions. Cela facilite les diffs plus propres (quand on ajoute un élément, il n’y a pas de modification sur la ligne précédente).
    
-   **`quoteProps`: "as-needed"**  
    N’ajoute des guillemets autour des noms de propriétés d’objets que si nécessaire (par ex. en cas d’espaces ou de caractères spéciaux).
    
-   **`arrowParens`: "always"**  
    Force l’utilisation de parenthèses autour des paramètres de fonctions fléchées, même s’il n’y en a qu’un seul.  
    Exemple : `(x) => x * 2`.
    
-   **`bracketSpacing`: true**  
    Ajoute un espace entre les accolades et le contenu, par exemple `{ foo: bar }` plutôt que `{foo: bar}`.
    
-   **`htmlWhitespaceSensitivity`: "css"**  
    Détermine comment Prettier gère les espaces dans le HTML. Avec la valeur `"css"`, il respecte les règles de mise en page définies par le CSS.
    
-   **`singleAttributePerLine`: false**  
    Quand `true`, oblige chaque attribut HTML à être sur sa propre ligne. Ici, `false` pour autoriser plusieurs attributs sur la même ligne.
    
-   **`bracketSameLine`: false**  
    Contrôle la position de la chevron fermante (`>`) dans les balises JSX/HTML quand elles sont sur plusieurs lignes.
    
    -   `false` => le `>` passe à la ligne suivante.
-   **`endOfLine`: "lf"**  
    Force l’utilisation du caractère de fin de ligne `LF` (line feed), standard sur Linux et Mac. Évite les différences de fin de ligne entre systèmes d’exploitation (Windows vs Linux).
    
-   **`proseWrap`: "preserve"**  
    Dans les fichiers Markdown ou texte, garde le retour à la ligne tel quel (`preserve`) sans reformater automatiquement les paragraphes.
    





### Plugins et tri des imports

-   **`plugins`: ["@trivago/prettier-plugin-sort-imports"]**  
    Liste les plugins chargés par Prettier, ici le plugin `@trivago/prettier-plugin-sort-imports` pour trier automatiquement les imports.
    
-   **`importOrder`: [...]**  
    Définit l’ordre de tri des imports. Les chaînes Regex sont testées dans cet ordre :
    
    1.  `^@angular/(.*)$` (tout ce qui commence par `@angular/`)
    2.  `^@core/(.*)$`
    3.  `^@utils/(.*)$`
    4.  `^@shared/(.*)$`
    5.  `^[./]` (tous les imports relatifs restants : `./` ou `../`)
-   **`importOrderSeparation`: true**  
    Ajoute une ligne vide entre les différents groupes d’imports.
    
-   **`importOrderSortSpecifiers`: true**  
    Trie aussi les spécificateurs d’import en ordre alphabétique.  
    Exemple :
    
    ```
    
    `- import { B, A } from "./something";
    + import { A, B } from "./something";`

    ```
    
-   **`importOrderParserPlugins`: ["typescript", "decorators-legacy"]**  
    Indique à `sort-imports` quels parseurs utiliser pour comprendre la syntaxe TypeScript et les décorateurs (legacy) — par exemple ceux utilisés par Angular.
    





### Overrides (règles spécifiques à certains fichiers)

-   **`"overrides"`**  
    Permet de surcharger les paramètres globaux pour certains fichiers.

1.  **`files: "*.component.html"`**
    
    -   **`options: { "parser": "angular" }`**  
        Utilise le parser `"angular"` pour les fichiers se terminant par `.component.html`, ce qui optimise la mise en forme de templates Angular (HTML).
2.  **`files: "*.scss"`**
    
    -   **`options: { "singleQuote": false }`**  
        Force l’utilisation de guillemets doubles (`"..."`) plutôt que simples (`'...'`) dans les fichiers `.scss` (car en CSS/SCSS, on a souvent pour habitude d’utiliser les guillemets doubles).
