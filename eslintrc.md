
# Configuration ESLint pour Angular/TypeScript avec Prettier

## 1. Fichier `.eslintrc.json` 

```
{
  "root": true,
  "ignorePatterns": ["projects/**/*"],
  "overrides": [
    {
      "files": ["*.ts"],
      "extends": [
        "eslint:recommended",
        "plugin:@typescript-eslint/recommended",
        "plugin:@typescript-eslint/recommended-requiring-type-checking",
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/template/process-inline-templates",
        "plugin:prettier/recommended"
      ],
      "parserOptions": {
        "project": ["tsconfig.json", "tsconfig.app.json", "tsconfig.spec.json"],
        "createDefaultProgram": true,
        "ecmaVersion": "latest"
      },
      "plugins": ["prettier", "import", "@typescript-eslint"],
      "rules": {
        "@angular-eslint/prefer-output-readonly": "error",
        "@angular-eslint/no-host-metadata-property": "error",
        "@angular-eslint/no-lifecycle-call": "error",
        "@angular-eslint/directive-selector": [
          "error",
          {
            "type": "attribute",
            "prefix": "app",
            "style": "camelCase"
          }
        ],
        "@angular-eslint/component-selector": [
          "error",
          {
            "type": "element",
            "prefix": "app",
            "style": "kebab-case"
          }
        ],
        "@typescript-eslint/strict-boolean-expressions": "error",
        "@typescript-eslint/explicit-member-accessibility": [
          "error",
          {
            "accessibility": "explicit",
            "overrides": {
              "constructors": "no-public",
              "accessors": "explicit",
              "methods": "explicit",
              "properties": "explicit",
              "parameterProperties": "explicit"
            }
          }
        ],
        "@typescript-eslint/member-ordering": [
          "error",
          {
            "default": [
              "public-static-field",
              "protected-static-field",
              "private-static-field",
              "public-instance-field",
              "protected-instance-field",
              "private-instance-field",
              "constructor",
              "public-instance-method",
              "protected-instance-method",
              "private-instance-method"
            ]
          }
        ],
        "@typescript-eslint/unbound-method": [
          "error",
          {
            "ignoreStatic": true
          }
        ],
        "import/order": [
          "error",
          {
            "groups": [
              ["builtin", "external"],
              "internal",
              ["parent", "sibling", "index"]
            ],
            "pathGroups": [
              {
                "pattern": "@angular/**",
                "group": "external",
                "position": "before"
              },
              {
                "pattern": "@core/**",
                "group": "internal",
                "position": "before"
              },
              {
                "pattern": "@utils/**",
                "group": "internal",
                "position": "after"
              },
              {
                "pattern": "@ui-shared/**",
                "group": "internal",
                "position": "after"
              }
            ],
            "pathGroupsExcludedImportTypes": ["@angular/**"],
            "newlines-between": "always",
            "alphabetize": {
              "order": "asc",
              "caseInsensitive": true
            }
          }
        ],
        "import/no-duplicates": "error",
        "no-console": ["warn", { "allow": ["warn", "error"] }],
        "no-debugger": "error",
        "no-unused-vars": "off",
        "@typescript-eslint/no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
        "no-multiple-empty-lines": ["error", { "max": 1 }],
        "prefer-const": "error",
        "no-var": "error",
        "prettier/prettier": ["error"]
      }
    },
    {
      "files": ["*.html"],
      "extends": [
        "plugin:@angular-eslint/template/recommended",
        "plugin:@angular-eslint/template/accessibility"
      ],
      "rules": {
        "@angular-eslint/template/prefer-self-closing-tags": "error",
        "@angular-eslint/template/prefer-ngsrc": "error",
        "@angular-eslint/template/prefer-control-flow": "error",
        "@angular-eslint/template/no-negated-async": "error",
        "@angular-eslint/template/accessibility-valid-aria": "error",
        "@angular-eslint/template/click-events-have-key-events": "error",
        "@angular-eslint/template/no-autofocus": "error",
        "@angular-eslint/template/no-positive-tabindex": "error"
      }
    }
  ]
}

```



## 2. Explications détaillées

### Racine et motifs ignorés

-   **`"root": true"`**  
    Indique à ESLint que ce fichier est la configuration racine. ESLint ne recherchera donc pas d’autres fichiers de configuration dans les répertoires supérieurs.
    
-   **`"ignorePatterns": ["projects/**/*"]`**  
    Tous les fichiers et sous-dossiers situés sous `projects/` sont ignorés. Cela peut être pratique si ce répertoire est géré séparément ou s’il n’a pas besoin d’être analysé.
    

### Overrides

La clé `overrides` permet d’appliquer des configurations ciblées en fonction d’un pattern de fichiers (ici, `*.ts` et `*.html`).

#### Bloc TypeScript

1.  **`files: ["*.ts"]`**  
    S’applique à tous les fichiers `.ts`.
    
2.  **`extends`**
    -   **`eslint:recommended`** : active les règles de base recommandées par ESLint.
    -   **`plugin:@typescript-eslint/recommended`** : active les règles de base pour TypeScript.
    -   **`plugin:@typescript-eslint/recommended-requiring-type-checking`** : active les règles nécessitant la vérification de types (type-checking).
    -   **`plugin:@angular-eslint/recommended`** : active les règles recommandées pour Angular.
    -   **`plugin:@angular-eslint/template/process-inline-templates`** : analyse et applique des règles sur les templates inline définis dans les fichiers TypeScript.
    -   **`plugin:prettier/recommended`** : active les règles liées à Prettier et s’assure qu’il n’y ait pas de conflit entre Prettier et ESLint.
      
3.  **`parserOptions`**
    -   **`project`** : liste de fichiers `tsconfig` (par ex. `tsconfig.json`, `tsconfig.app.json`, `tsconfig.spec.json`) servant de base pour la compilation et la vérification de types.
    -   **`createDefaultProgram`** : permet à ESLint de créer un programme TypeScript par défaut si aucune configuration n’est trouvée.
    -   **`ecmaVersion`** : version d’ECMAScript à supporter pour l’analyse (ici, `latest`).
      
4.  **`plugins`**
    -   **`prettier`** : gère la mise en forme du code via Prettier et évite les conflits.
    -   **`import`** : propose des règles pour l’organisation et la validation des imports.
    -   **`@typescript-eslint`** : apporte des règles spécifiques à TypeScript (analyses de types, conventions, etc.).
      
5.  **`rules`** : personnalisation des règles
    -   **`@angular-eslint/prefer-output-readonly`** : impose `readonly` pour les propriétés marquées comme `@Output`.
    -   **`@angular-eslint/no-host-metadata-property`** : interdit l’utilisation de `host` dans les décorateurs Angular. On recommande plutôt `@HostBinding` et `@HostListener`.
    -   **`@angular-eslint/no-lifecycle-call`** : empêche d’appeler directement les méthodes du cycle de vie Angular (`ngOnInit`, etc.), gérées automatiquement par le framework.
    -   **`@angular-eslint/directive-selector`** : impose l’utilisation du type `attribute`, du préfixe `app` et du style `camelCase` pour les directives.
    -   **`@angular-eslint/component-selector`** : impose un type `element`, le préfixe `app` et le style `kebab-case` pour les composants Angular.
    -   **`@typescript-eslint/strict-boolean-expressions`** : exige un usage explicite des booléens dans les conditions.
    -   **`@typescript-eslint/explicit-member-accessibility`** : nécessite de déclarer explicitement la visibilité (public, private, etc.) des membres de classe.
    -   **`@typescript-eslint/member-ordering`** : impose un ordre spécifique pour les propriétés, le constructeur et les méthodes dans une classe.
    -   **`@typescript-eslint/unbound-method`** : interdit d’utiliser une méthode d’instance comme callback sans la binder (`this`).
    -   **`import/order`** : force un ordre logique pour les imports, avec des groupes (builtin, external, internal, etc.), un tri alphabétique, et une ligne vide entre chaque groupe.
    -   **`import/no-duplicates`** : empêche l’import multiple d’un même module dans un même fichier.
    -   **`no-console`** : avertit (`warn`) en cas d’utilisation de `console.log` ou `console.info`, tout en autorisant `console.warn` et `console.error`.
    -   **`no-debugger`** : interdit l’utilisation du mot-clé `debugger`.
    -   **`no-unused-vars`** (de base ESLint) est désactivée au profit de **`@typescript-eslint/no-unused-vars`**, qui autorise les noms commençant par `_`.
    -   **`no-multiple-empty-lines`** : interdit plusieurs lignes vides consécutives (max. 1).
    -   **`prefer-const`** : encourage l’utilisation de `const` lorsqu’une variable n’est pas réaffectée.
    -   **`no-var`** : interdit le mot-clé `var`, au profit de `let` ou `const`.
    -   **`prettier/prettier`** : génère une erreur si le code enfreint les règles de formatage Prettier.

#### Bloc HTML

1.  **`files: ["*.html"]`**  
    S’applique aux fichiers de type `.html` (templates Angular).
    
2.  **`extends`**
    -   **`plugin:@angular-eslint/template/recommended`** : active les règles recommandées pour les templates Angular (HTML).
    -   **`plugin:@angular-eslint/template/accessibility`** : inclut des règles relatives à l’accessibilité dans les templates.
      
3.  **`rules`** :
    -   **`@angular-eslint/template/prefer-self-closing-tags`** : balises autofermantes si elles n’ont pas d’enfant (ex : `<img />`).
    -   **`@angular-eslint/template/prefer-ngsrc`** : encourage l’utilisation de `[ngSrc]` au lieu de `[src]`.
    -   **`@angular-eslint/template/prefer-control-flow`** : invite à privilégier les constructions de flux Angular (`*ngIf`, `*ngFor`, etc.) plutôt que du code complexe.
    -   **`@angular-eslint/template/no-negated-async`** : interdit l’opérateur de négation `!` avant un pipe `async` (`!observable | async`).
    -   **`@angular-eslint/template/accessibility-valid-aria`** : vérifie la validité des attributs ARIA.
    -   **`@angular-eslint/template/click-events-have-key-events`** : demande à inclure des événements clavier si on ajoute des événements de clic.
    -   **`@angular-eslint/template/no-autofocus`** : interdit l’attribut `autofocus`, jugé incompatible avec certaines règles d’accessibilité.
    -   **`@angular-eslint/template/no-positive-tabindex`** : interdit l’utilisation de `tabindex` supérieur à 0, qui nuit à l’ordre de tabulation naturel.
