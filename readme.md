# Cloudflare 1020 Bypass Examples (Python & Node.js)

This repo contains working examples of bypassing **Cloudflare 1020** errors using **Playwright + Stealth** with **residential proxies**, **rotating headers**, and **basic anti-bot evasion tricks**. Works in **Node.js** and **Python**.

## Table of Contents

1. [Requirements](#requirements)
2. [Project Structure](#project-structure)
3. [Bypass Examples](#bypass-examples)
   * [Playwright Basic](#playwright-basic)
   * [Playwright + Stealth](#playwright--stealth)
   * [Residential Proxy Rotation](#residential-proxy-rotation)
   * [User-Agent + Header Spoofing](#user-agent--header-spoofing)
   * [Human-like Behavior](#human-like-behavior)
   * [Full Flow Example](#full-flow-example)

## Requirements

**Python 3.10+** or **Node.js 18+**

### Python Setup

Required packages:

- `requests`
- `playwright`
- `playwright-stealth`

Install:

```bash
pip install playwright
playwright install
pip install playwright-stealth
```

### Node.js Setup

Required packages:

- `playwright`
- `playwright-extra`
- `playwright-extra-plugin-stealth`

Install:

```bash
npm install playwright playwright-extra playwright-extra-plugin-stealth
```

## Project Structure

```
cf1020-bypass-examples/
│
├── python/
│   ├── basic_playwright.py
│   ├── stealth_playwright.py
│   ├── proxy_rotation.py
│   ├── header_rotation.py
│   ├── human_behavior.py
│   ├── full_flow_example.py
│
├── nodejs/
│   ├── basic_playwright.js
│   ├── stealth_playwright.js
│   ├── proxy_rotation.js
│   ├── header_rotation.js
│   ├── human_behavior.js
│   ├── full_flow_example.js
│
└── README.md
```

Each script shows a different tactic for avoiding Cloudflare 1020. No frameworks, no noise — just straight working examples.

## Bypass Examples


### Playwright Basic

Basic page load using vanilla Playwright (likely to trigger CAPTCHA or 1020).
| Parameter     | Description            | Example                 |
| ------------- | ---------------------- | ----------------------- |
| `url`         | Target URL to load     | `'https://example.com'` |
| `timeout`     | Maximum wait time (ms) | `60000`                 |
| `output_file` | File to save page HTML | `'page.html'`           |


### Playwright + Stealth

Hide `webdriver` flag, spoof plugins, patch headless indicators.

| Parameter    | Description                  | Example                 |
| ------------ | ---------------------------- | ----------------------- |
| `target_url` | URL to visit and scrape      | `'https://example.com'` |
| `headless`   | Run browser in headless mode | `True`                  |
| `timeout`    | Maximum wait time (ms)       | `60000`                 |


### Residential Proxy Rotation

Add a pool of rotating residential proxies for better IP reputation.

| Parameter       | Description                                   | Example                                 |
| --------------- | --------------------------------------------- | --------------------------------------- |
| `target_url`    | URL to visit with rotating headers            | `'https://example.com'`                 |
| `user_agents`   | List of User-Agent strings to rotate          | `['Mozilla/5.0...', 'Chrome/91.0...']`  |
| `extra_headers` | Additional HTTP headers to include (optional) | `{'Accept-Language': 'en-US,en;q=0.9'}` |
| `rotate_every`  | Number of requests before changing header     | `1` (rotate every request)              |


### User-Agent + Header Spoofing

Randomized headers and modern user agents for each session.
| Parameter     | Description                              | Example                                 |
| ------------- | ---------------------------------------- | --------------------------------------- |
| `target_url`  | URL to visit with rotated headers        | `'https://example.com'`                 |
| `user_agents` | List of User-Agent strings to rotate     | `["Mozilla/5.0...", "Safari/537.36"]`   |
| `headers`     | Additional HTTP headers to include       | `{"Accept-Language": "en-US,en;q=0.9"}` |
| `proxy`       | Proxy server address (optional)          | `'http://user:pass@proxy.com:8080'`     |
| `timeout`     | Max time to wait for page load (seconds) | `30`                                    |


### Human-like Behavior

Add mouse movement, scrolling, and timed delays.
| Parameter                     | Description                 | Example                                      |
| ----------------------------- | --------------------------- | -------------------------------------------- |
| `page`                        | Playwright page object      | `page.goto('https://example.com')`           |
| `sleep`                       | Pause execution for realism | `time.sleep(1.5)` / `await sleep(1500)` (ms) |
| `mouse.move(x, y)`            | Move mouse cursor to (x, y) | `page.mouse.move(100, 100)`                  |
| `mouse.click(x, y)`           | Click at coordinates (x, y) | `page.mouse.click(200, 300)`                 |
| `keyboard.press(key)`         | Simulate keyboard key press | `page.keyboard.press('PageDown')`            |
| `mouse.wheel(deltaX, deltaY)` | Scroll page by delta        | `page.mouse.wheel(0, 400)`                   |


### Full Flow Example

All combined: stealth, headers, proxies, behavior — in one script.

| Parameter     | Description                                       | Example                                          |
| ------------- | ------------------------------------------------- | ------------------------------------------------ |
| `proxy`       | Proxy server URL with auth                        | `'http://user:pass@proxy.example:8000'`          |
| `user_agent`  | Browser user agent string                         | `'Mozilla/5.0 (Windows NT 10.0; Win64; x64)...'` |
| `target_url`  | URL to navigate and scrape                        | `'https://example.com'`                          |
| `headless`    | Whether to run browser in headless mode           | `True` (Python) / `true` (Node.js)               |
| `delay_range` | Range (seconds) for random delays between actions | `0.5 to 2 seconds`                               |


## Disclaimer

These examples are for **educational purposes** only. Learn more about [the legality of web scraping](https://hasdata.com/blog/is-web-scraping-legal).



## 📎 More Resources

* [How to Bypass Cloudflare 1020](https://hasdata.com/blog/bypass-cloudflare-1020)
* [Join the community on Discord](https://email.hasdata.com/e/c/eyJlbWFpbF9pZCI6ImRnU2RrUWdEQVBENUF1XzVBZ0dXcXhUNGdSTk12RXZEb0pPM3UxUT0iLCJocmVmIjoiaHR0cHM6Ly9oYXNkYXRhLmNvbS9qb2luLWRpc2NvcmQiLCJpbnRlcm5hbCI6IjlkOTEwODAxYmY4ZjAxZjBmOTAyIiwibGlua19pZCI6MjMzfQ/7b95f85846853ee473b2d955c1e158190975e23eb18b11156d6df08e1f544488)
* [Star this repo if helpful ⭐](#)

### NodeJS/basic_playwright.js:
```bash
const { chromium } = require('playwright-extra');
const stealth = require('playwright-extra-plugin-stealth');

chromium.use(stealth());

const PROXIES = [
  'http://username:password@proxy1.example.com:8000',
  'http://username:password@proxy2.example.com:8000',
];

const USER_AGENTS = [
  'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36',
  'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.1 Safari/605.1.15',
];

function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function humanLikeInteraction(page) {
  await page.mouse.move(100, 100);
  await sleep(Math.random() * 1000 + 500);
  await page.mouse.move(200, 300);
  await sleep(Math.random() * 1000 + 500);
  await page.evaluate(() => window.scrollBy(0, window.innerHeight / 2));
  await sleep(Math.random() * 1000 + 1000);
}

(async () => {
  const proxy = PROXIES[Math.floor(Math.random() * PROXIES.length)];
  const userAgent = USER_AGENTS[Math.floor(Math.random() * USER_AGENTS.length)];

  const browser = await chromium.launch({
    proxy: { server: proxy },
    headless: true,
  });

  const context = await browser.newContext({
    userAgent,
  });

  const page = await context.newPage();

  await page.goto('https://example.com');
  await humanLikeInteraction(page);

  const content = await page.content();
  console.log(content.slice(0, 500)); // print first 500 chars

  await browser.close();
})();
```

### NodeJS/header_rotation.js
```bash
const { chromium } = require('playwright');
const headersList = [
  {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)',
    'Accept-Language': 'en-US,en;q=0.9',
    'Accept-Encoding': 'gzip, deflate, br',
  },
  {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)',
    'Accept-Language': 'en-GB,en;q=0.8',
    'Accept-Encoding': 'gzip, deflate',
  }
];

(async () => {
  const browser = await chromium.launch({ headless: true });
  const context = await browser.newContext({
    extraHTTPHeaders: headersList[Math.floor(Math.random() * headersList.length)]
  });
  const page = await context.newPage();
  await page.goto('https://httpbin.org/headers');
  const content = await page.textContent('pre');
  console.log(content);
  await browser.close();
})();
```

### NodeJS/human_behavior.js
```bash
const { chromium } = require('playwright-extra');
const Stealth = require('playwright-extra-plugin-stealth');
chromium.use(Stealth());

function sleep(ms) {
  return new Promise(r => setTimeout(r, ms));
}

async function humanBehavior(page) {
  // random mouse moves
  for (let i = 0; i < 5; i++) {
    const x = Math.floor(Math.random() * 700) + 100;
    const y = Math.floor(Math.random() * 500) + 100;
    await page.mouse.move(x, y, { steps: Math.floor(Math.random() * 20) + 5 });
    await sleep(Math.random() * 400 + 200);
  }

  // scroll down in chunks
  for (let i = 0; i < 3; i++) {
    await page.evaluate(() => {
      window.scrollBy(0, window.innerHeight * 0.8);
    });
    await sleep(Math.random() * 700 + 500);
  }

  // pause and scroll up
  await sleep(Math.random() * 500 + 500);
  await page.evaluate(() => {
    window.scrollBy(0, -window.innerHeight * 0.5);
  });
  await sleep(Math.random() * 500 + 300);

  // random click
  const bx = Math.floor(Math.random() * 700) + 50;
  const by = Math.floor(Math.random() * 500) + 50;
  await page.mouse.click(bx, by);
  await sleep(Math.random() * 1000 + 1000);
}

(async () => {
  const browser = await chromium.launch({ headless: true });
  const context = await browser.newContext();
  const page = await context.newPage();

  await page.goto('https://example.com');
  await humanBehavior(page);
  // continue with your scraping...
  await browser.close();
})();
```

### NodeJS/proxy_rotation.js
```bash
const { chromium } = require('playwright');

const proxies = [
  'http://user:pass@proxy1.example.com:8000',
  'http://user:pass@proxy2.example.com:8000',
  'http://user:pass@proxy3.example.com:8000'
];

const proxy = proxies[Math.floor(Math.random() * proxies.length)];

(async () => {
  const browser = await chromium.launch({
    proxy: { server: proxy }
  });

  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('https://httpbin.org/ip');
  const content = await page.textContent('body');
  console.log(content);
  await browser.close();
})();
```
