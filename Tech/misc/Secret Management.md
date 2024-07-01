## Checking/fixing/comparing `.env`files with [dotenv-linter](https://dotenv-linter.github.io/)

Very useful tool! Can be used for verifying your `.env.example` files match the actual `.env`
```bash
dotenv-linter compare .env.example .env
```

This will print things like
```
.env.example is missing keys: DB_URL
```