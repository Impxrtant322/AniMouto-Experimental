# AniMouto Experimental [![GitHub package.json version](https://img.shields.io/github/package-json/v/Impxrtant322/AniMouto-Experimental?style=flat-square)](https://github.com/Impxrtant322/AniMouto-Experimental/releases/latest) [![GitHub](https://img.shields.io/github/license/Impxrtant322/AniMouto-Experimental?style=flat-square)](https://en.wikipedia.org/wiki/MIT_License) [![Discord](https://img.shields.io/discord/1311848924239106098?logo=discord&logoColor=white&label=Discord&style=flat-square)](https://discord.gg/bpEGPyH55Q)

<a><img align="right" src="https://animouto.moe/logo_128px_bg.png"></a>

### Experimental version of AniMouto with new features and bug fixes. NOT THE ORIGINAL, DEVELOPED SEPERATELY. If you have questions, pop into my [discord server](https://discord.gg/bpEGPyH55Q) and @ Genesis.

As the original developer of this application has said that they are focusing on other projects and not this,
I have decided to take on the challenge of maintaining this project for years to come.

#### Click below to get your respective extension:

[Firefox](https://github.com/Impxrtant322/AniMouto-Experimental/releases/latest) will automatically check for updates after downloading the extension.

- Working on getting firefox listed on the AMO so I don't have to keep updates.json updated.

[Chromium](https://chromewebstore.google.com/detail/animouto-experimental/cbhiciobopkafdkekindhidajdhkioef) is officially on the web store (unlisted)! Download the extension from there for automatic updates!

### The original owner reserves all rights to this application and may request for this repository to be privated.

### AniMouto original description:

AniMouto is an unofficial AniList extension which allows quick access to many features of AniList including your current Airing, Anime, and Manga lists, notifications, and search.

AniMouto is designed to feel like a true extension to AniList by providing a very similar look and feel.

## Images

<img src="https://animouto.moe/preview/list.png" width="280"> <img src="https://animouto.moe/preview/search.png" width="280"> <img src="https://animouto.moe/preview/details.png" width="280"> <img src="https://animouto.moe/preview/notifications.png" width="280">

## Contributing

Make sure you have [Node.js](https://nodejs.org/) installed.

Run these commands to get the project locally:

```sh
git clone https://github.com/Impxrtant322/AniMouto-Experimental.git # or clone your own fork
cd AniMouto
npm install
npm run codegen:graphql
```

The dependencies should now all be installed. Next, run the `watch:*` script. This will watch for file changes and rebuild the extension for each supported browser environment. You can either install the built directories as temporary extensions, or run the relevant `serve` command to launch temporary browser environments with the extension pre-installed.

### Packaging

#### `npm run build:*`

Builds the project for all supported browser environments and places them into `/dist/`.
