# Wappalyzer



Files pulled from
https://github.com/hunter-io/wappalyzer/tree/fix

Based off [Wappalyzer](https://github.com/wappalyzer/wappalyzer)

## Goal of Repo

To set up a docker api of wappalyzer

### Tasks / To-Dos

- [ ] Pull all technologies from [wappalyzer/technologies](https://github.com/wappalyzer/wappalyzer/tree/master/src/technologies)
- [ ] Drop techs into /apps.json
- [ ] Deploy to Dockerhub
- [ ] Fix this ReadMe
- [ ] Branding and such
- [ ] Docs
- [ ] Issue Templates

























[Wappalyzer](https://www.wappalyzer.com/) is a
[cross-platform](https://www.wappalyzer.com/nodejs) utility that uncovers the
technologies used on websites. It detects
[content management systems](https://www.wappalyzer.com/technologies/cms), [ecommerce platforms](https://www.wappalyzer.com/technologies/ecommerce), [web servers](https://www.wappalyzer.com/technologies/web-servers), [JavaScript frameworks](https://www.wappalyzer.com/technologies/javascript-frameworks),
[analytics tools](https://www.wappalyzer.com/technologies/analytics) and
[many more](https://www.wappalyzer.com/technologies).


## Installation

```shell
$ npm i -g wappalyzer      # Globally
$ npm i wappalyzer --save  # As a dependency
```

To use Puppeteer (headless Chrome browser), you must install the NPM package manually:

```shell
$ npm i puppeteer@^2.0.0
```


## Run from the command line

```
wappalyzer <url> [options]
```

### Options

```
-b, --browser=...        Specify which headless browser to use (zombie or puppeteer)
-c, --chunk-size=...     Process links in chunks
-d, --debug              Output debug messages
-t, --delay=ms           Wait for ms milliseconds between requests
-h, --help               This text
--html-max-cols=...      Limit the number of HTML characters per line processed
--html-max-rows=...      Limit the number of HTML lines processed
-D, --max-depth=...      Don't analyse pages more than num levels deep
-m, --max-urls=...       Exit when num URLs have been analysed
-w, --max-wait=...       Wait no more than ms milliseconds for page resources to load
-p, --password=...       Password to be used for basic HTTP authentication (zombie only)
-P, --pretty             Pretty-print JSON output
--proxy=...              Proxy URL, e.g. 'http://user:pass@proxy:8080' (zombie only)
-r, --recursive          Follow links on pages (crawler)
-a, --user-agent=...     Set the user agent string
-u, --username=...       Username to be used for basic HTTP authentication (zombie only)
```


## Run from a script

```javascript
const Wappalyzer = require('wappalyzer');

const url = 'https://www.wappalyzer.com';

const options = {
  // browser: 'puppeteer',
  debug: false,
  delay: 500,
  maxDepth: 3,
  maxUrls: 10,
  maxWait: 5000,
  recursive: true,
  userAgent: 'Wappalyzer',
  htmlMaxCols: 2000,
  htmlMaxRows: 2000,
};

const wappalyzer = new Wappalyzer(url, options);

// Optional: capture log output
// wappalyzer.on('log', params => {
//   const { message, source, type } = params;
// });

// Optional: do something on page visit
// wappalyzer.on('visit', params => {
//   const { browser, pageUrl } = params;
// });

wappalyzer.analyze()
  .then((json) => {
    process.stdout.write(`${JSON.stringify(json, null, 2)}\n`);

    process.exit(0);
  })
  .catch((error) => {
    process.stderr.write(`${error}\n`);

    process.exit(1);
  });
```
