# kpMigrator · CI4 Migration Studio

Generador visual de **migracions** (mètodes `up()` i `down()`) i **seeders** per a **CodeIgniter 4.7+** (PHP 8.2+).
És un sol fitxer `index.html` sense build ni servidor: tot es genera al navegador.

## Funcionalitats

- **Migracions de creació**: columnes, tipus, longitud, `UNSIGNED`, `NULL`, `AUTO_INCREMENT`, valor per defecte
  (incloent-hi `CURRENT_TIMESTAMP` amb `RawSql`), comentaris, clau primària (simple o composta), únics, índexs,
  índexs compostos, claus foranes, motor i comentari de taula.
- **Migracions de modificació**: afegir, eliminar, modificar o renombrar columnes; afegir o eliminar índexs i
  claus foranes; renombrar la taula; SQL personalitzat. El `down()` es genera automàticament **en ordre invers**,
  perquè `php spark migrate:rollback` funcioni.
- **Seeder** proposat segons l'estructura de la taula:
  - *Faker* (`fakerphp/faker`, ja inclòs a `require-dev` de l'appstarter): detecta el generador adequat pel
    nom i el tipus de la columna (email, nom, telèfon, slug, preu, ENUM…), respecta la longitud, els camps
    únics i els nullable, i agafa IDs reals de les taules relacionades per a les claus foranes.
  - *Dades fixes*: genera un array PHP amb dades aleatòries, sense cap dependència.
  - Pots canviar el generador de cada columna o escriure-hi una expressió PHP pròpia.
- Validació en temps real (FK `SET NULL` sobre una columna NOT NULL, `ENUM` sense valors, `VARCHAR` sense longitud…).
- Plantilles, desat automàtic al navegador, exportar/importar JSON (també el format de l'eina antiga)
  i **enllaç per compartir** amb tot l'esquema dins la URL.
- Tema clar/fosc i disseny adaptat a mòbil.

## Ús

1. Obre l'aplicació (vegeu la secció següent).
2. Tria **Crear taula** o **Modificar taula** i defineix l'estructura.
3. Descarrega el fitxer i desa'l a `app/Database/Migrations/` (o `app/Database/Seeds/` per al seeder).
4. Executa:

```bash
php spark migrate
```

```bash
php spark db:seed UsersSeeder
```

## Publicar-la a GitHub Pages

1. Al repositori: **Settings → Pages**.
2. A *Build and deployment*, tria **Deploy from a branch**, branca `main` i carpeta `/ (root)`.
3. Al cap d'un minut estarà disponible a `https://<usuari-o-organització>.github.io/kpMigrator/`.

> Si el repositori és privat, GitHub Pages necessita un pla de pagament (Pro, Team o Enterprise).
> Si no en tens, fes el repositori públic o obre `index.html` directament al navegador.

## Notes

- El codi generat està pensat per a MySQL/MariaDB (`after`, `first`, `ENGINE` i `COMMENT` només hi tenen efecte).
- Per eliminar una clau forana creada amb `createTable()` quan uses `DBPrefix`, indica el prefix a
  *Opcions avançades*: el nom per defecte de CI4 l'inclou.
