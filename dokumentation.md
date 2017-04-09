# Dokumentation

Die open.DASH Dokumentation wird mit [gitbook](https://github.com/GitbookIO/gitbook) erstellt. Man benötigt also nur Nodejs und npm um sich an der Dokumentation zu beteiligen.

## Dokumentation bearbeiten

Wenn man zu der Dokumentation beitragen will, kann man einzelene Seiten bearbeiten, indem man oben links auf jeder Seite der Dokumentation einem Link *"Seite bearbeiten"* folgt, über den man auf die entsprechende Seite auf Github weitergeleitet wird. Alternativ kann man direkt einen Fork von `https://github.com/UniSiegenWiNeMe/opendash-docs` erstellen.

Im Falle eines Forks, wird dann ein Pull- Request auf die `master` Branch erstellt, der kontrolliert wird und ggf. in die `live` Branch migriert wird.

### Lokal die Dokumentation hosten

```
$ git clone https://github.com/UniSiegenWiNeMe/opendash-docs.git
...
$ cd opendash-docs
$ npm install
...
$ npm run build // Die fertige Seite wird in ./_book generiert
$ npm run serve // Es wird ein Webserver gestartet, der auf Änderungen im "code" wartet
```