# Day 5 Data Sources

This directory holds one file, which is a copy of a published sample database.
Nothing here was generated, and nothing was collected for this workshop.

## The Source Database

- **Title:** Sakila, the sample database of a fictional film rental business.
- **Original author:** Mike Hillyer, of the MySQL AB documentation team.
- **Publisher of the original:** Oracle, at
  `https://dev.mysql.com/doc/sakila/en/`.
- **Licence of the original:** the New BSD licence covers the contents of the
  `sakila-schema.sql` and `sakila-data.sql` files, as stated at
  `https://dev.mysql.com/doc/sakila/en/sakila-license.html`. The documentation
  that accompanies the MySQL distribution is under separate terms and is not
  reproduced here.

Sakila is written for MySQL, and this directory holds a port of it to SQLite.
The port was made by DB Software Laboratory, and its SQL scripts carry the
following notice, which is reproduced here because the BSD licence requires a
redistribution to retain it and a binary database file has nowhere to keep it.

> Sakila for SQLite is a port of the Sakila example database available for
> MySQL, which was originally developed by Mike Hillyer of the MySQL AB
> documentation team. This project is designed to help database administrators
> to decide which database to use for development of new products. The user can
> run the same SQL against different kind of databases and compare the
> performance.
>
> License: BSD
> Copyright DB Software Laboratory
> http://www.etl-tools.com

Copies of that port circulate under several names and through several
redistributors, and the binary file records none of them, so the immediate
source of this particular copy cannot be established from the file itself. What
can be established is the lineage, and it was checked rather than assumed. The
table definitions in this file carry the port's distinctive style, declaring
`description` as `BLOB SUB_TYPE TEXT` and writing each primary key as a
separate clause, which the MySQL original does not and which the other SQLite
ports in circulation do not either, since those declare their keys as
`INTEGER PRIMARY KEY AUTOINCREMENT`. The licence is the same throughout the
lineage in any case, being BSD at the port and New BSD upstream, so both permit
redistribution on the condition that the notice above travels with the data.

The rows themselves carry the moment this copy was built. Every table has a
`last_update` column, and an insert trigger sets it to the time of the insert,
so the values record the load rather than any event in the fictional business.
They run from `2021-03-06 15:51:59` to `2021-03-06 15:55:57`.

## What This Directory Contains

`sqlite-sakila.db`, a single SQLite file of 5828608 bytes. Its MD5 checksum is
`e5b01e0c1711ba60bd50e3bde854e755` and its SHA-256 checksum is
`dbca3837b9965d75fbc2b4af1b2daec57d841f95942e656cea44db997e05da88`.

It holds 16 tables, 5 views, 40 indexes, and 30 triggers. The tables and their
row counts are the following.

| Table | Rows |
| --- | --- |
| `actor` | 200 |
| `address` | 603 |
| `category` | 16 |
| `city` | 600 |
| `country` | 109 |
| `customer` | 599 |
| `film` | 1000 |
| `film_actor` | 5462 |
| `film_category` | 1000 |
| `film_text` | 0 |
| `inventory` | 4581 |
| `language` | 6 |
| `payment` | 16049 |
| `rental` | 16044 |
| `staff` | 2 |
| `store` | 2 |

The `film_text` row count is not a mistake in this table. MySQL populates that
table from `film` through triggers, in order to give it a full text index, and
the SQLite port creates the table without those triggers and without the rows.
None of the 30 triggers in this file mentions `film_text`, so it is empty and
stays empty. The film descriptions live in the `description` column of `film`,
where all 1000 are present and none is null.

## How This File Was Prepared

It was not. The file is committed exactly as it was obtained, byte for byte,
and the checksums above are of the file in this directory. No row was added,
removed, corrected, or reordered, and no table, view, index, or trigger was
touched.

## Network Access

The notebooks in this day read the database from this directory, so no data
arrives over the network. They do reach the network for something else, which
is the language model they send questions to. The day's `README.md` records
which model, through which endpoint, and how many calls a session makes.

## Files The Notebooks Write

Neither notebook writes a file. The conversation between the model and the
database lives in memory until the kernel stops, and no transcript, cached
response, or checkpoint is stored in this repository.
