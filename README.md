# test `npx` and `node`

[![WTFPL](http://www.wtfpl.net/wp-content/uploads/2012/12/wtfpl-badge-4.png)](http://wtfpl.net)

Testing how to run a node script with a defined Node.js version with `npx` or by adding `node` as a regular `npm` dependency.

See medium zkat blog (20170711) : [Introducing npx: an npm package runner](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b)

**requirements**

`npm@5.2.0` is mandatory to use npx.

`npm@5.3.0` contains a lot of npx fixes.

`npm@5.4.0` contains a lot of windows npx fixes.

**packages links**

- [npx package](https://www.npmjs.com/package/npx)
- [node package](https://www.npmjs.com/package/node)

**others resources**

- [awesome-npx](https://github.com/suarasaur/awesome-npx)

## npx goals

- using npm binaries without the need to install them globally or to point manually to a local install (through `node_modules/.bin/<binary>`)
- ease the quick test of a new binary (npx will download at execution the wanted package version to `$HOME/.npm/_npx/`)

## concrete usages

### running node as a dependency with npx

Node.js has been packaged in npm in the [node package](https://www.npmjs.com/package/node).

Used with npx it means we can now install [node as a dependency](https://registry.npmjs.org/node/) and run a project with this bin instead of the platform bin.

Just add node in the desired version :

```javascript
// package.json file

// ...

  "dependencies": {
    "node": "10.0.0"
  },

// ...

  "scripts": {
    "start": "npx node index"
  },

// ...

```

The `start` command will run you node project with the node bin in version 10.0.0 installed as a dependency.
 
### running node with npx

Just add node in the desired version :

```javascript
// package.json file

// ...

  "scripts": {
    "start": "npx -p node@10.5.0 -- node index"
  },

// ...

```

The `start` command will run you node project with the node bin in version 10.5.0.

`npx` will download and install the package defined with the `-p <package@version>` option in `$HOME/.npm/_npx/`.

This one is super useful to run tests against a specific node version without modifying anything to deps or without the need of external tools like `nvm`.

### running gist

You can run a github gist with npx, the gist just need a package.json file and an index.js file.

Example : https://gist.github.com/zkat/4bc19503fe9e9309e2bfaa2c58074d32

```javascript
// package.json file

// ...

  "scripts": {
    "start": "npx https://gist.github.com/zkat/4bc19503fe9e9309e2bfaa2c58074d32"
  },

// ...

```

