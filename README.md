# Postgres Error Codes

![actions-badge](https://github.com/drdgvhbh/postgres-error-codes/workflows/CI/badge.svg)

Postgres error codes mapping for NodeJS.

## Install
```
npm i @drdgvhbh/postgres-error-codes
```

## Usage

Each condition from the [PG documentation](https://www.postgresql.org/docs/9.2/errcodes-appendix.html) is available in the module. In order to obtain the status code use the prefixed uppercase condition name:

`unique_violation` => `PG_UNIQUE_VIOLATION`

`not_null_violation` => `PG_NOT_NULL_VIOLATION`

```javascript
const { PG_UNIQUE_VIOLATION, PG_NOT_NULL_VIOLATION } = require('@drdgvhbh/postgres-error-codes')

async function createUserMethod(req, res, next) {
    try {
        // Run insert user SQL
    } catch (err) {
        // If user with same email already exists
        if (err.code === PG_UNIQUE_VIOLATION) {
            return next('Email already exists!')
        }

        // Param should not be null
        if (err.code === PG_NOT_NULL_VIOLATION) {
            return next('Email required!')
        }

        next(err)
    }
}
```

## Related
- [PostgreSQL Error Codes Documentation](https://www.postgresql.org/docs/9.2/errcodes-appendix.html)
