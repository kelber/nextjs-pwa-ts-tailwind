
#### Parcerias Digitais

### Install
yarn create next-app --typescript



### TailwindCSS
https://www.kyrelldixon.com/blog/setup-nextjs-with-tailwindcss-and-typescript

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

postcss.config.js
```js
// module.exports = {
// 	plugins: {
// 		tailwindcss: {},
// 		autoprefixer: {},
// 	},
// }


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




### PWA


esse funciona
https://dev.to/byteslash/how-to-create-a-pwa-with-next-js-4dbm
https://www.youtube.com/watch?v=ARNN_zmrwcw



> npm run build
> npm run start