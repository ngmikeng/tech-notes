Node debug in vs code
===
- VS Code version 1.26.1.
- Node version >= 6.9.
- Using 'Inspector' Protocol.
- Add config launch via npm in `.vscode/launch.json`.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Launch via NPM",
      "runtimeExecutable": "npm",
      "runtimeArgs": [
        "run-script",
        "debug"
      ],
      "port": 9230
    }
  ]
}
```

- Add debug script in file `package.json`.

```json
  "scripts": {
    "debug": "node --inspect=9230 server.js"
  },
```
