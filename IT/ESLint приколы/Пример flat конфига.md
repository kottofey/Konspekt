В версии ESLint 9+ применяется flat конфиг. Пример:
```js title=eslint.config.js
import babelParser from '@babel/eslint-parser';
import js from '@eslint/js';
import globals from 'globals';

export default [
  {
    ignores: ['dist/**/*'],
  },
  js.configs.recommended,
  {
    files: ['src/**/*.{js,ts,jsx,tsx,vue}'],
    languageOptions: {
      sourceType: 'module',
      ecmaVersion: 'latest',
      parser: babelParser,
      parserOptions: {
        babelrc: false,
        requireConfigFile: false,
        presets: ['@babel/preset-env'],
      },
      globals: {
        ...globals.browser,
        ...globals.node,
      },
    },
    rules: {
      'indent': ['error', 2],
      'linebreak-style': [0, 'windows'],
      'quotes': ['error', 'single'],
      'semi': 'warn',
      'no-unused-vars': 'off',
      'no-undef': 'off',
    },
    plugins: {},
  },
];

```
