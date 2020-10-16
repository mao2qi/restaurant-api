<p align="center">
  <img alt="Web client demo" src="./demos/client.png?v=3">
</p>

# PandoraAI

PandoraAI is a web chat client powered by [node-chatgpt-api](https://github.com/waylaidwanderer/node-chatgpt-api), allowing users to easily chat with multiple AI systems while also offering support for custom presets. With its seamless and convenient design, PandoraAI provides an engaging conversational AI experience.

Built using [Nuxt 3](https://v3.nuxtjs.org/), a Vue 3 framework.  
You may also use PandoraAI with other API server implementations as long as the endpoints are compatible.

## Features

- Chat with all the AI that `node-chatgpt-api` supports, including `gpt-3.5-turbo`, `text-davinci-003`, ChatGPT, and Bing.
- Supports creating multiple presets for each client.  
![Client Settings](demos/client-settings.png) 
- Choose between different clients or custom presets.  
![Client Dropdown](demos/client-dropdown.png)
- Everything is stored in local storage, so you can use this client without an account, and it can be imported or exported to other devices.

<details>
<summary><strong>Nuxt 3 Setup</strong></summary>

Look at the [Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

Make sure to install the dependencies:

```bash
# yarn
yarn ins