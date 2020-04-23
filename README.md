# GitLab CI Puppeteer Headful
GitLab CI compatible adaption of [Puppeteer Headful for GitHub Actions](https://github.com/mujo-code/puppeteer-headful).

## Purpose
Makes it possible to run Puppeteer in headful mode in GitLab CI using Docker executor.

## Usage
This installs Puppeteer ontop of a [NodeJS](https://nodejs.org) container so you have access to run [npm](https://www.npmjs.com) scripts. The container comes with [Xvfb](https://www.x.org/releases/X11R7.6/doc/man/man1/Xvfb.1.xhtml) which you need to start manually before your Puppeteer scripts run.

```yaml
variables:
  CI: "true"

stages:
  - test

test:
  stage: test
  image: gitlab-ci-puppeteer-headful:latest
  script:
    - Xvfb -ac :99 -screen 0 1280x1024x16 > /dev/null 2>&1 & # Start virtual display
    - npm test # Your test command(s)
```

You will also need to make sure Puppeteer is launched in headless mode.

```javascript
browser = await puppeteer.launch({
  headless: false,
  ...
});
```
