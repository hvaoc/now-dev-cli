## Now Dev CLI

[![npm version](https://d25lcipzij17d.cloudfront.net/badge.svg?id=js&type=6&v=1.1.2&x2=0)](https://www.npmjs.com/package/now-dev-cli)

A development server for Now V2 (for NextJS applications)

## Installation

```
npm i -g now-dev-cli
```

## Usage

Step 1: Create your own `now.dev.json`:

```js
{
  "patterns": {
    "first": "(?<first>.*)",
    "uuid": "(?<uuid>[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}){1}",
    "slug":"(?<slug>[^/]*)",
    "year":"(?<year>[0-9]{4})",
    "month":"(?<month>[0-9]{2})",
    "day":"(?<day>[0-9]{2})"
  },
  "builds": [
    {
      "src": "next.config.js", "use": "@now/next"
    },
    {
      "src": "static", "use": "@now/static"
    }
  ],
  "routes": [
    {
      "src": "/favicon.ico",
      "dest": "static/favicon.ico"
    },
    { 
      "src": "/w/${first}", 
      "dest": "/work?slug=${first}" 
    },
    { 
      "src": "/resource/${uuid}", 
      "dest": "/complex?id=${uuid}" 
    },
    { 
      "src": "/t/${slug}/${year}-${month}-${day}", 
      "dest": "/more_complex?day=${day}&month=${month}&year=${year}&slug=${slug}" 
    },
    { "src": "/", "dest": "/index" }
  ]
}

```

Step 2: Run `now-dev` to serve your NextJS application

Compiled JSON file:

```js

{
  "builds": [
    {
      "src": "next.config.js",
      "use": "@now/next"
    },
    {
      "src": "static",
      "use": "@now/static"
    }
  ],
  "routes": [
    {
      "src": "/favicon.ico",
      "dest": "static/favicon.ico",
      "methods": [
        "GET"
      ]
    },
    {
      "src": "/w/(?<first>.*)",
      "dest": "/work?slug=$first",
      "methods": [
        "GET"
      ]
    },
    {
      "src": "/resource/(?<uuid>[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}){1}",
      "dest": "/complex?id=$uuid",
      "methods": [
        "GET"
      ]
    },
    {
      "src": "/t/(?<slug>[^/]*)/(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})",
      "dest": "/more_complex?day=$day&month=$month&year=$year&slug=$slug",
      "methods": [
        "GET"
      ]
    },
    {
      "src": "/",
      "dest": "/index",
      "methods": [
        "GET"
      ]
    }
  ]
}

```

