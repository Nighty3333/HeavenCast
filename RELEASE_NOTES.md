# Heaven Cast 1.0.1

A fix for installs Heaven Cast could not find.

## Fixed

- **Game data was not detected.** The folder Umamusume keeps its data in was assumed to sit
  directly under your user profile, which is wrong whenever Windows keeps AppData somewhere else.
  Setup then failed with a "Game manifest not found" error and the game card stayed red. The
  folder is now detected properly, and can be pointed somewhere else if your install is unusual.

- **Skills showed as numbers instead of names.** The same missing folder left the overlay without
  the game's text database, so every skill fell back to its raw id — and nothing said why. The
  database is now found along with the rest of the game data, and if it ever cannot be opened
  Heaven Cast says so instead of failing quietly.

Everything else is unchanged from 1.0.0. Your settings and profiles carry over.

## Known release condition

The executables are not code-signed. Windows SmartScreen may display an unknown-publisher warning.
Verify the SHA-256 hash supplied with the release before running the file.
