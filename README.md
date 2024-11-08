# Workshop - Databasemigraties met Laravel

Applicatie starten
`php artisan serve`

## Algemene informatie
- Error log bestanden staan in logs/laravel.log
- Je krijgt een Server Error 500 wanneer je geen .env bestand hebt.
- sqlite databaseviewer in VSCode moet ververst worden na het uitvoeren van een migratie om de wijzigingen te laten zien.

Nadat je geen bekende foutmeldingen meer krijgt kan je `php artisan migrate` uitvoeren om de eerste tabelopstelling te genereren.

===
## Foutmeldingen + fixes
-  MissingAppKeyException: (komt omdat APP_KEY in .env niet is gezet.)
    `php artisan key:generate` kan uitgevoerd worden om de APP_KEY value in de .env automatisch te vullen met een gegenereerde sleutel

- QueryException -> [XXXXXX.sqlite] does not exit.
    Bestand aanmaken: database/database.sqlite

- QueryException -> could not find driver (Connection: sqlite, SQL: PRAGMA foreign_keys = ON;)
    `php.ini` aanpassen: Volgende drivers uncommenten:
        - extension=pdo_sqlite
        - extension=sqlite3

===
## Handige commando's
- `php.ini`-locatie vinden:
    `php --ini`

===
## Migratie informatie
Tabel hernoemen: (`hasTable` nodig voor wanneer `down()` aangeroepen wordt)
```php
if (Schema::hasTable('visitors')) {
    Schema::rename('visitors', 'users');
}
```

## Migratie maken
`php artisan make:migration <action_<tablename>_table` maakt een scaffolding bestand aan.
Inhoud de migratie (dus wat de migratie moet doen) moet nog geschreven worden.

## Alle migraties opnieuw uitvoeren
`php artisan migrate:refresh`

## Alle migraties die nog niet zijn uitgevoerd uitvoeren
`php artisan migrate`

## Migratiestatus inzien
`php artisan migrate:status`

## ALLE migraties terugrollen
`php artisan migrate:rollback`

## Specifiek aantal migraties terugrollen
`php artisan migrate:rollback --step=2`

## Migraties 'pretenden' en SQL query ervan inzien
`php artisan migrate --pretend`
