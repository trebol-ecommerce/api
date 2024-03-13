# Trébol eCommerce API

[![GitHub Super-Linter](https://github.com/trebol-ecommerce/api/actions/workflows/linter.yaml/badge.svg)](https://github.com/marketplace/actions/super-linter)

The contract that Trébol as a whole must comply with.

## Documentation

Run this command in your terminal at the project root directory:

```bash
mkdir docs/ && npx @redocly/cli build-docs src/trebol-api.json --output=docs/index.html
```

Then browse the generated `docs/index.html` file. [Read more about Redoc here](https://github.com/Redocly/redoc).
