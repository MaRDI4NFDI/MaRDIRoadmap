# Access Control for `Special:ImportFromPid`

## Finding

The [`Special:ImportFromPid`](https://portal.mardi4nfdi.de/wiki/Special:ImportFromPid) page is
implemented by `SpecialImport` in the
[MathSearch extension](https://github.com/wikimedia/mediawiki-extensions-MathSearch).

In `includes/Specials/SpecialImport.php`, the page constructor sets the required right to
`'import'`:

```php
parent::__construct( 'ImportFromPid', 'import' );
```

The MediaWiki `import` right is only granted to the `sysop` group by default, so **only admins
can access this page**.

## Recommended Fix

Change the required right from `'import'` to a dedicated right (e.g. `'mardimport'`) and grant
that right to the `user` group so that all registered users can access the page.

### 1. `includes/Specials/SpecialImport.php`

```php
// Before
parent::__construct( 'ImportFromPid', 'import' );

// After
parent::__construct( 'ImportFromPid', 'mardimport' );
```

### 2. `extension.json`

Add the new right to `AvailableRights` and grant it to `user`:

```json
"AvailableRights": [
    "mathwmcsubmit",
    "mardimport"
],
"GroupPermissions": {
    "sysop": {
        "mathwmcsubmit": true
    },
    "user": {
        "mardimport": true
    }
}
```

These changes need to be made in the
[`wikimedia/mediawiki-extensions-MathSearch`](https://github.com/wikimedia/mediawiki-extensions-MathSearch)
repository and then picked up by the MaRDI portal deployment.
