# Prettier

## When does prettier ignore the rules (such as 'single-quote') in .eslintrc.js?

When you refer to a plugin that it can't find. e.g. In

```
    module.exports = {
      env: {
        browser: true,
        commonjs: true,
        es6: true
      },
      extends: "eslint:recommended",
      rules: {
        indent: ["error", 2],
        "linebreak-style": ["error", "unix"],
        quotes: ["error", "single", { avoidEscape: true }],
        semi: ["error", "always"],
        "no-console": "off",
        "prefer-spread": "off"
      },
      parserOptions: {
        sourceType: "module"
      },
      overrides: [
        {
          files: ["**/*.ts"],
          plugins: ["@typescript-eslint/eslint-plugin"],
          parser: "@typescript-eslint/parser",
          parserOptions: {
            project: "./tsconfig.json"
          },
          extends: ["plugin:@typescript-eslint/recommended", "eslint:recommended"],
          rules: {
            "no-var": "off",
            "@typescript-eslint/no-var-requires": "off",
            "@typescript-eslint/no-use-before-define": "off",
            "@typescript-eslint/explicit-function-return-type": "off",
            "prefer-const": "off",
            "@typescript-eslint/camelcase": "off",
            "prefer-spread": "off",
            "@typescript-eslint/no-empty-function": "off"
          }
        }
      ]
    };
```

if `@typescript-eslint/recommended` isn't installed in node_modules, the rules will be ignored.
