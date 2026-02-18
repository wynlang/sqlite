# sqlite — Embedded Database for Wyn

SQLite 3.47.2 embedded database. No system install needed.

## Install

```bash
wyn pkg install github.com/wynlang/sqlite
```

## Usage

The `Db.*` API is built into Wyn. This package provides the SQLite C library that it links against.

```wyn
var db = Db.open("myapp.db")
Db.exec(db, "CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)")
Db.exec_p(db, "INSERT INTO users (name) VALUES (?)", ["Alice"])
var name = Db.query(db, "SELECT name FROM users WHERE id = 1")
println(name)  // Alice
Db.close(db)
```

## How it works

This package contains `sqlite3.c` and `sqlite3.h` (the SQLite amalgamation). When you `wyn pkg install` it, these files go into your project's `packages/sqlite/src/`. The Wyn compiler detects them and compiles SQLite into your binary automatically.

No `.wyn` wrapper file is needed — the `Db.*` API is part of the Wyn standard library. This package just provides the C implementation behind it.

## API

| Function | Description |
|----------|-------------|
| `Db.open(path)` | Open/create database, returns handle |
| `Db.exec(db, sql)` | Execute SQL statement |
| `Db.exec_p(db, sql, params)` | Execute with parameterized values (SQL injection safe) |
| `Db.query(db, sql)` | Query, returns first result as string |
| `Db.query_p(db, sql, params)` | Query with parameters |
| `Db.close(db)` | Close database |
