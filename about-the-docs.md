# About the documentation

The documentation of open.DASH uses [gitbook](https://github.com/GitbookIO/gitbook) and [markdown](#) files.

## Contributing

If you want to contribute to the documentation, by adding or improving content, you can do so by following the *"Improve this page"* button on the top left of each page. It will redirect you to Github, where you can edit the content directly.

You can also fork `https://github.com/UniSiegenWiNeMe/opendash-docs` and create a pull request on the `master` branch. 

The `live` branch is the published version.

### Running gitbook locally

```
> git clone https://github.com/UniSiegenWiNeMe/opendash-docs.git
...
> cd opendash-docs
> npm install
...
> npm run build // The build will be in ./_book
> npm run serve // A webserver starts and serves the current version
```

There is a [bug when running the serve command on Windows](https://github.com/GitbookIO/gitbook/issues/1379). The workaround looks like this:
> 1. gitbook serve
> 2. delete _book folder once
> 3. now each time you change the md file, the server will stop and start over again and again