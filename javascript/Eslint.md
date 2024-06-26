# Eslint란?

EsLint는 Es와 Lint를 합친 용어이다.

- ES: 표준 Javascript를 의미한다.
- Lint: 에러가 있는 코드에 표시를 달아놓는 것을 의미한다.

그렇기에 ESLint는 자바스크립트 문법에서 에러를 표시해주는 도구이다.

### Eslint 예시

```tsx
{
 "env": {
   "browser": true,
   "es6": true,
   "node": true
 },
 "parser": "@typescript-eslint/parser",
 "plugins": ["@typescript-eslint", "import"],
 "extends": [
   "airbnb",
   "airbnb/hooks",
   "plugin:@typescript-eslint/recommended",
   "plugin:prettier/recommended",
   "plugin:import/errors",
   "plugin:import/warnings"
 ],
 "parserOptions": {
   "ecmaVersion": 2020,
   "sourceType": "module",
   "ecmaFeatures": {
     "jsx": true
   }
 },
 "rules": {
   "linebreak-style": 0,
   "import/no-dynamic-require": 0,
   "import/no-unresolved": 0,
   "import/prefer-default-export": 0,
   "global-require": 0,
   "import/no-extraneous-dependencies": 0,
   "jsx-quotes": ["error", "prefer-single"],
   "react/jsx-props-no-spreading": 0,
   "react/forbid-prop-types": 0,
   "react/jsx-filename-extension": [
     2,
     { "extensions": [".js", ".jsx", ".ts", ".tsx"] }
   ],
   "import/extensions": 0,
   "no-use-before-define": 0,
   "@typescript-eslint/no-empty-interface": 0,
   "@typescript-eslint/no-explicit-any": 0,
   "@typescript-eslint/no-var-requires": 0,
   "no-shadow": "off",
   "react/prop-types": 0,
   "no-empty-pattern": 0,
   "no-alert": 0,
   "react-hooks/exhaustive-deps": 0
 },
 "settings": {
   "import/parsers": {
     "@typescript-eslint/parser": [".ts", ".tsx"]
   },
   "import/resolver": {
     "typescript": "./tsconfig.json"
   }
 }
}
```
