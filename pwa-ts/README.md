
#### Parcerias Digitais

### Install
yarn create next-app --typescript



### TailwindCSS
https://www.kyrelldixon.com/blog/setup-nextjs-with-tailwindcss-and-typescript


> npm i -D postcss-preset-env tailwindcss

> npx tailwind init

> touch postcss.config.js


next.config.js
```js
// PWA E TAMBEM O TAILWIND


const withPWA = require("next-pwa");

module.exports = withPWA({
  pwa: {
    dest: "public",
    register: true,
    skipWaiting: true,
    disable: process.env.NODE_ENV === 'development'
  },
  plugins: [
    'tailwindcss',
    'postcss-preset-env',
  ],
});

```



styles/index.css
```css
/* purgecss start ignore */
@tailwind base;
@tailwind components;
/* purgecss end ignore */
@tailwind utilities;


```

_app.tsx
```js

import '../styles/index.css'

```

> npm i -D @fullhuman/postcss-purgecss



postcss.config.js
```js

  module.exports = {
    plugins: [
      'tailwindcss',
      process.env.NODE_ENV === 'production'
        ? [
            '@fullhuman/postcss-purgecss',
            {
              content: [
                './pages/**/*.{js,jsx,ts,tsx}',
                './components/**/*.{js,jsx,ts,tsx}',
              ],
              defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || [],
            },
          ]
        : undefined,
      'postcss-preset-env',
    ],
  }


```




tailwind.config.js
```js
module.exports = {
	content: [
		'./pages/**/*.{js,ts,jsx,tsx}',
		'./components/**/*.{js,ts,jsx,tsx}',
	],
	darkMode: 'class',
	plugins: [require('tailwindcss-safe-area')],
}

// obs: tive que instalar > npm i tailwindcss-safe-area

```




> rm -rf ./next

> npm run build

> npm run start




### PWA


esse funciona
https://dev.to/byteslash/how-to-create-a-pwa-with-next-js-4dbm
https://www.youtube.com/watch?v=ARNN_zmrwcw


> npm i next-pwa


#### generate manifest.json
https://www.simicart.com/manifest-generator.html/

obs: arquivo download vem manifest.webmanifest mude pra manifest.json somente


public/manifest.json
```js
{
    "theme_color": "#f69435",
    "background_color": "#F2F2F2",
    "display": "standalone",
    "scope": "/",
    "start_url": "/",
    "name": "Parcerias Digitais",
    "short_name": "Parcerias Digitais",
    "description": "Parcerias Digitais",
    "icons": [
        {
            "src": "/icon-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/icon-256x256.png",
            "sizes": "256x256",
            "type": "image/png"
        },
        {
            "src": "/icon-384x384.png",
            "sizes": "384x384",
            "type": "image/png"
        },
        {
            "src": "/icon-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ]
}


// lembre-se das imagens

```


pages/_document.tsx
```js
import Document, { Html, Head, Main, NextScript } from "next/document";

class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>
          <link rel="manifest" href="/manifest.json" />
          <link rel="apple-touch-icon" href="/icon.png"></link>
          <meta name="theme-color" content="#fff" />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}

export default MyDocument;

```


.gitignore
```js
# PWA files
**/public/sw.js
**/public/workbox-*.js
**/public/worker-*.js
**/public/sw.js.map
**/public/workbox-*.js.map
**/public/worker-*.js.map

```

> npm run build
> npm run start


#### Docker

Dockerfile
```js
FROM node:14.15.4-alpine3.12

USER node

WORKDIR /home/node/app

```


docker.compose.yaml
```yaml
version: '3'

services:

  app:
    build: .
    entrypoint: sh -c "npm install && npm run dev"
    ports:
      - 3000:3000
    volumes:
      - .:/home/node/app

```
