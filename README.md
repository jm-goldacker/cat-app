# CatApp

This app shows you a funny cat meme from GIPHY and a random cat fact from [catfact.ninja](https://catfact.ninja).

## Project Setup

Enter the `.env` file in the root directory and replace the value of `VUE_APP_GIPHY_API_KEY` with a valid [GIPHY API](https://developers.giphy.com/docs/api/#quick-start-guide) Key.

```sh
npm install
```

### Compile and Hot-Reload for Development

#### Browser

```sh
npm run dev
```

#### Electron app

```sh
npm run electron:serve
```

### Compile and Minify for Production

#### Browser

```sh
npm run build
```

#### Electron app

```sh
npm run electron:build
```