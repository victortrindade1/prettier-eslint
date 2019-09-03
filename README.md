# Prettier + ESLint

Fonte: https://medium.com/dubizzletechblog/setting-up-prettier-and-eslint-for-js-and-react-apps-bbc779d29062

## Instale as libs

Com npm:
`npm install --save-dev babel-eslint eslint eslint-config-airbnb eslint-config-prettier eslint-plugin-react eslint-plugin-import prettier pretty-quick`

Com yarn:
`yarn add -D babel-eslint eslint eslint-config-airbnb eslint-config-prettier eslint-plugin-react eslint-plugin-import prettier pretty-quick`

## .prettierrc

Adicione o arquivo .prettierrc no root do app

```
{
 "printWidth": 100,
 "trailingComma": "all",
 "tabWidth": 2,
 "semi": true,
 "singleQuote": true
}
```

## .eslintrc

Adicione o arquivo .eslintrc no root do app

```
{
    "parser": "babel-eslint",
    "parserOptions": {
    "sourceType": "module",
    "allowImportExportEverywhere": false,
    "codeFrame": false
},
"extends": ["airbnb", "prettier"],
"env": {
    "browser": true,
    "jest": true
},
"rules": {
    "max-len": ["error", {"code": 100}],
    "prefer-promise-reject-errors": ["off"],
    "react/jsx-filename-extension": ["off"],
    "react/prop-types": ["warn"],
    "no-return-assign": ["off"]
  }
}
```

## .eslintignore

Adicione o arquivo .eslintignore no root do app

```
src/serviceWorker.js
node_modules/*
public/*
build/*
config/*
```

## Configurando o VSCode

### .editorconfig

No VSCode, dê um Ctrl + P: `ext install EditorConfig.EditorConfig` (só é necessário na primeira vez)

Adicione o arquivo .editorconfig no root do app

```
# http://editorconfig.org
root = true
[*]
charset = utf-8
end_of_line = lf
indent_size = 2
indent_style = space
insert_final_newline = true
max_line_length = 100
trim_trailing_whitespace = true
[*.md]
max_line_length = 0
trim_trailing_whitespace = false
[{Makefile,**.mk}]
# Use tabs for indentation (Makefiles require tabs)
indent_style = tab
[*.scss]
indent_size = 2
indent_style = space
```

### Extensão do Prettier no VSCode

No VSCode, dê um Ctrl + P: `ext install esbenp.prettier-vscode` (só é necessário na primeira vez)

### Nas configurações do VSCode

Code > Preferences > settings

```
"editor.formatOnSave": true,
"eslint.autoFixOnSave": true
```

Aqui no novo VSCode é um pouco diferente. Basta procurar na barra de buscadentro do settings pelo nome editor.formatOnSave q acha.

## Formatando o pré-commit

`npm install --save-dev lint-staged husky`

### No package.json

```
"husky": {
    "hooks": {
        "pre-commit": "lint-staged"
    }
},
"lint-staged": {
    "src/**/*.{js,jsx}": ["eslint", "pretty-quick — staged", "git add"]
},
```
