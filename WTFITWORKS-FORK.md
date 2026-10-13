# WTFitworks-Fork von GRDB.swift (SQLCipher)

Dieser Fork existiert nur, um GRDB über SPM mit **SQLCipher statt System-SQLite** zu linken
(benötigt von `WTFitworks/logbuch`). Upstream: https://github.com/groue/GRDB.swift

## Patch
Ausschließlich `Package.swift`, exakt nach den Kommentaren `GRDB+SQLCipher` im Upstream:
- `SQLCipher.swift` als Dependency (exakt gepinnt), `SQLITE_HAS_CODEC` + `SQLCipher` definiert
- Library und Target `GRDBSQLite` entfernt, Target `GRDBSQLCipher` aktiviert

Keine Änderungen am GRDB-Quellcode.

## Branches und Tags
- Branch `sqlcipher/vX.Y.Z` = Upstream-Tag `vX.Y.Z` + Patch
- Tag `X.Y.Z-sqlcipher.N` (N zählt bei Patch-Änderungen hoch); Logbuch pinnt dieses Tag exakt

## Update auf neue Upstream-Version
```bash
git fetch https://github.com/groue/GRDB.swift.git 'refs/tags/vX.Y.Z:refs/tags/vX.Y.Z'
git checkout -b sqlcipher/vX.Y.Z vX.Y.Z
# Patch nach den GRDB+SQLCipher-Kommentaren erneut anwenden, SQLCipher-Version prüfen
swift test --filter "Cipher|Encryp"   # muss grün sein
git tag X.Y.Z-sqlcipher.1 && git push origin sqlcipher/vX.Y.Z X.Y.Z-sqlcipher.1
```

| Tag | Upstream | SQLCipher.swift | Cipher-Tests |
|---|---|---|---|
| 7.11.1-sqlcipher.1 | v7.11.1 | 4.19.0 (exakt) | 29/29 grün (2026-10-13) |
