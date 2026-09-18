# Changelog

## v0.1.0
- `GET /api/v1/me`: the current reader.

## v0.2.0
- `GET /api/v1/isbn/{isbn}`: what the public sources know about an ISBN; nothing is stored.

## v0.3.0
- `GET /api/v1/isbn/{isbn}` takes the ISBN-13 as thirteen digits; schemas `Isbn`, `IsbnAuthor`, `IsbnSeries`; problems carry no `detail`, validation errors carry `{field, code}`; a problem body marks an answer from Libris itself. Supersedes v0.2.0, which nothing pins.

## v0.4.0
- `Isbn` no longer carries `sources`: the answer says what is known, not who knew it.

## v0.5.0
- `Isbn` becomes `IsbnLookup` and carries `kind` (`BOOK`, `BD`, `MANGA`); `IsbnAuthor` and `IsbnSeries` become `Author` and `Series`; `ValidationProblem` folds into `Problem`, whose `errors` is optional. No byte of an answer changes but the new field.

## v0.6.0
- `POST /api/v1/bookshelves/{id}/books`: a copy of the book on the bookshelf, the body a `NewBook`, the book as the reader submits it, with or without an ISBN; `IsbnLookup` carries `copies`, the copies on the reader's bookshelves; `CurrentReader` carries `defaultBookshelf`; schemas `Copy` and `Bookshelf`; the body examples live under `components/examples`.
