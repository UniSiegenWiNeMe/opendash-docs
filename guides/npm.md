# npm Cheatsheet für open.DASH

Es wird davon ausgegangen, dass npm Version `^5.2.0` installiert ist.

[Hier kommt ihr zur Dokumentation von npm.](https://docs.npmjs.com/index)

## npm Updaten

``` bash
npm install -g npm
```

## Projekt starten

Mit dem init Befehl erstellt man eine neue package.json Datei, mit den nötigsten Informationen.

``` bash
npm init
```

Wenn man möglichst schnell loslegen will, dann kann man die `y` Flag benutzen, um alle Fragen mit yes zu bestätigen, die normalerweise bei der initialisierung gestellt werden.

``` bash
npm init -y
```

## Pakete installieren

Wenn ein Projekt vorhanden ist, dann kann man Pakete als Dependency hinzufügen, indem man den `install` Befehl benutzt, damit die Dependency in der `package.json` gespeichert wird, wird die `save` Flag benutzt.

``` bash
npm install <module-name> --save
```

Um ein paar Tastenanschläge zu sparen, kann man den Befehl wie folgt abkürzen:

``` bash
npm i -S <module-name>
```

Hat man eine Dependency, die nur während der Entwicklung benötigt wird, benutzt man statt der `save` Flag die `save-dev` Flag.

``` bash
npm install --save-dev <module-name>

# ..oder in kurz:

npm i -D <module-name>
```