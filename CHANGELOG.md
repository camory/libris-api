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

## v0.6.1
- `POST /api/v1/bookshelves/{id}/books`: `id` is typed as a string with a uuid pattern instead of `format: uuid`, until Contracteer 4.1.0. No byte of a request or an answer changes.

## v0.6.2
- `NewBook.title`, `Author.name` and `Series.name` refuse a blank value with a `pattern` beside their `minLength: 1`. No byte of a request or an answer changes.

## v0.7.0
- `GET /api/v1/books`: the reader's catalogue, the house's books with a copy on a bookshelf they belong to, fifty at a time as a shelf reads; `after` the id of the last book received; the answer a `BookPage`, `books` and `next`, the `after` of the next page, null on the last, verified on its shape, no example; schema `Edition`, the thirteen fields of a published version of a work, `isbn13` nullable, the blank title refused; `NewBook`, `IsbnLookup` and `Book` compose over it with `allOf`, `IsbnLookup` its `isbn13` never null and `copies`, `Book` the stored edition addressed by `id` with `copies`; these three no longer say `additionalProperties: false`. No byte of an existing answer changes.

## v0.8.0
- `GET /api/v1/covers/{name}`: a stored cover by the name of its picture, the hash of its bytes, an `image/*` body, JPEG or WebP as stored, `Cache-Control: public, max-age=31536000, immutable`; `404` when no cover bears the name. `Edition` loses `coverUrl`; `CoverCandidate` `{source, url}`, `source` the name Libris knows the source by; `IsbnLookup` gains `id`, the house's edition when it holds the ISBN, null when it does not, and `covers`, the candidates in the order to try them, the house's own alone when it holds the edition, and keeps `coverUrl` deprecated as the first candidate's url or null; `NewBook` gains `coverSource`, nullable, the name of the source of the cover the reader chose; `Book` gains `coverUrl`, the relative address of the stored cover or null. `ONE_PIECE_1` answers three candidates, `ONE_PIECE_2_OWNED` the house's own. `coverUrl` on the lookup now names the first candidate's picture, inventaire.io's where it was Open Library's; every other byte of an existing answer stays. The `201` of the add and every error response lose their example bodies, verified on their schema; `ADD_ONE_PIECE_1` leaves with them, the `201` case generated.

## v0.8.1
- `POST /api/v1/bookshelves/{id}/books`: the `201` is keyed again, `201_ADD_ONE_PIECE_1` on the bookshelf id and on the body `NewOnePiece1`, so the case sends an ISBN whose check digit holds; its answer stays verified on its schema, with no example. No byte of a request or an answer changes.
