# OpenIntegration GitHub Sample

This repository contains a minimal OpenIntegration example for [paperlesspaper](https://paperlesspaper.de).

The current UI layer is a simple GitHub username widget:

- [render.html](/Users/utzel/htdocs/openintegration-github/render.html) displays the configured GitHub username.
- [settings.html](/Users/utzel/htdocs/openintegration-github/settings.html) lets the host app edit the `githubUsername` setting through `postMessage`.

If you want a fully consistent GitHub integration, those two files should be updated next.

## How it works

The integration is split into two pages:

1. [render.html](/Users/utzel/htdocs/openintegration-github/render.html) receives integration data from the host app and renders the configured GitHub username.
2. [settings.html](/Users/utzel/htdocs/openintegration-github/settings.html) receives initial settings from the host app, lets the user edit them, and posts `UPDATE_SETTINGS` and `SET_HEIGHT` messages back.

The settings page follows the expected `paperlesspaper` message flow:

- listen for `INIT`
- apply incoming settings
- post `UPDATE_SETTINGS` when the input changes
- post `SET_HEIGHT` so the host can size the settings iframe correctly

## Key files

- [render.html](/Users/utzel/htdocs/openintegration-github/render.html): Render page shown inside the integration.
- [settings.html](/Users/utzel/htdocs/openintegration-github/settings.html): Settings UI for editing the GitHub username.
- [config.json](/Users/utzel/htdocs/openintegration-github/config.json): Integration manifest currently still using the older XKCD name and defaults.
- [api/xkcd.js](/Users/utzel/htdocs/openintegration-github/api/xkcd.js): Legacy serverless XKCD proxy kept from the earlier sample.
- [INSTRUCTIONS.md](/Users/utzel/htdocs/openintegration-github/INSTRUCTIONS.md): Prompt-style implementation notes for generating simple OpenIntegrations.
- [vercel.json](/Users/utzel/htdocs/openintegration-github/vercel.json): Vercel routing and deployment configuration.

## Local development

Run the project locally with Vercel:

1. Install the Vercel CLI: `npm i -g vercel`
2. Start the dev server: `vercel dev`

The project will usually be available at `http://localhost:3000`.

Useful local URLs:

- `/render.html` for the render preview
- `/settings.html` for the settings preview
- `/config.json` for the integration manifest

## Usage in paperlesspaper

Deploy the repository and use the deployed `config.json` URL as the custom integration URL inside paperlesspaper.

Example:

`https://your-deployment.example/config.json`

Because the manifest still contains XKCD metadata, the integration may appear under that older name until [config.json](/Users/utzel/htdocs/openintegration-github/config.json) is updated.

## Deployment

This project is set up for Vercel hosting with static pages plus serverless API routes.

Deploy with Vercel and make sure these files remain publicly available:

- [render.html](/Users/utzel/htdocs/openintegration-github/render.html)
- [settings.html](/Users/utzel/htdocs/openintegration-github/settings.html)
- [config.json](/Users/utzel/htdocs/openintegration-github/config.json)

## Notes

If you are building a new integration from this repo, use the GitHub-related UI files as the reference for host communication and update the manifest and API layer to match the final integration behavior.
