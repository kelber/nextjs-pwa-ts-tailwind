
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


```




### PWA


esse funciona
https://dev.to/byteslash/how-to-create-a-pwa-with-next-js-4dbm
https://www.youtube.com/watch?v=ARNN_zmrwcw



> npm run build
> npm run start