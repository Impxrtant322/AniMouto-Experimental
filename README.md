# AniMouto Experimental ![GitHub package.json version](https://img.shields.io/github/package-json/v/Impxrtant322/AniMouto-Experimental) ![GitHub](https://img.shields.io/github/license/Impxrtant322/AniMouto-Experimental) ![Discord](https://img.shields.io/discord/1311848924239106098?logo=discord&logoColor=white&label=Discord)

<a><img align="right" src="https://animouto.moe/logo_128px_bg.png"></a>

### Experimental version of AniMouto with bug fixes. NOT THE ORIGINAL, DEVELOPED SEPERATELY.

As the original developer of this application has said that they are focusing on other projects and not this,
I have decided to take on the challenge of maintaining this project for years to come.

Click [here](https://github.com/Impxrtant322/AniMouto-Experimental/releases/latest) and download the correct experimental file for your browser.

[firefox](https://github.com/Impxrtant322/AniMouto-Experimental/releases/latest) is automatically installed onto your browser and will automatically check for updates.

[Chromium](https://github.com/Impxrtant322/AniMouto-Experimental/releases/latest) does not yet have a extension link. You will have to manually download the zip file and manually add it as an extension in the chrome extensions tab.
1. Click the above Chromium link, which will direct you to the latest release. Download the chromium zip file.
2. Unzip the chromium zip file.
3. Manage your extensions, click "Developer Mode" at the top right, and click "Load Unpacked"
4. Browse to your chromium folder and load the folder contents into chrome.

If you have questions, pop into my [discord server](https://discord.gg/bpEGPyH55Q) and @ Genesis.

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
