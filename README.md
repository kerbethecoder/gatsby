![image](./src/images/snap.png)

![Static Badge](https://img.shields.io/badge/gatsby-v5%2e13%2e5-663399) ![Static Badge](https://img.shields.io/badge/tailwindcss-v3%2e4%2e7-38bdf8)

"[Gatsby](https://www.gatsbyjs.com/) is a React-based open source framework for creating websites. Whether your site has 100 pages or 100,000 pages — if you care deeply about performance, scalability, and built-in security — you'll love building with us. Start pulling data from your favorite headless CMS easily!"

This guide provides a first-hand experience on building a Gatsby project using [gatsby-cli](https://www.gatsbyjs.com/docs/tutorial/getting-started/part-0/#gatsby-cli) + [Tailwind CSS](https://tailwindcss.com/docs/guides/gatsby) and deploying it on [GitHub Pages](https://pages.github.com/).

## 🛠️ Installation

**1. Install `gatsby-cli`.**

```bash
# terminal
npm install -g gatsby-cli
```

To check version or if gatsby-cli is installed.

```bash
gatsby -v
```

**2. Create a new project using a starter site.**

```bash
# terminal
gatsby new project_name https://github.com/gatsbyjs/gatsby-starter-default
cd project_name
```

> [!NOTE]
>
> If you want to check some more [starters](https://www.gatsbyjs.com/starters/?v=2).

**3. Install Tailwind CSS.**

```bash
# terminal
npm install -D tailwindcss postcss autoprefixer gatsby-plugin-postcss
npx tailwindcss init -p
```

**4. Enable the Gatsby PostCSS plugin.**

```js
// gatsby-config.js
module.exports = {
  plugins: [
    "gatsby-plugin-postcss",
    // ...
  ],
}
```

**5. Configure your template paths.**

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/pages/**/*.{js,jsx,ts,tsx}",
    "./src/components/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

**6. Add the Tailwind directives to your CSS.**

```css
/* create file ./src/styles/global.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

**7. Import the CSS file.**

```js
// gatsby-browser.js
import "./src/styles/global.css"
```

**8. Start your build process.**

```bash
gatsby develop
```

**9. Start using Tailwind in your project.**

```js
// index.js
export default function IndexPage() {
  return (
    <Layout>
      <h1 className="text-3xl font-bold underline">Hello world!</h1>
    </Layout>
  )
}
```

## 🗂️ File Structure

A quick look at the top-level files and directories you'll see in a typical Gatsby project. <small>[reference here](https://github.com/gatsbyjs/gatsby-starter-default?tab=readme-ov-file#-whats-inside)</small>

    .
    ├── node_modules
    ├── src
    ├── .gitignore
    ├── gatsby-browser.js
    ├── gatsby-config.js
    ├── gatsby-node.js
    ├── gatsby-ssr.js
    ├── LICENSE
    ├── package.json
    └── README.md

1.  **`/node_modules`**: This directory contains all of the modules of code that your project depends on (npm packages) are automatically installed.

2.  **`/src`**: This directory will contain all of the code related to what you will see on the front-end of your site (what you see in the browser) such as your site header or a page template. `src` is a convention for “source code”.

3.  **`.gitignore`**: This file tells git which files it should not track / not maintain a version history for.

4.  **`gatsby-browser.js`**: This file is where Gatsby expects to find any usage of the [Gatsby browser APIs](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-browser/) (if any). These allow customization/extension of default Gatsby settings affecting the browser.

5.  **`gatsby-config.js`**: This is the main configuration file for a Gatsby site. This is where you can specify information about your site (metadata) like the site title and description, which Gatsby plugins you’d like to include, etc. (Check out the [config docs](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-config/) for more detail).

6.  **`gatsby-node.js`**: This file is where Gatsby expects to find any usage of the [Gatsby Node APIs](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-node/) (if any). These allow customization/extension of default Gatsby settings affecting pieces of the site build process.

7.  **`gatsby-ssr.js`**: This file is where Gatsby expects to find any usage of the [Gatsby server-side rendering APIs](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-ssr/) (if any). These allow customization of default Gatsby settings affecting server-side rendering.

8.  **`LICENSE`**: This Gatsby starter is licensed under the 0BSD license. This means that you can see this file as a placeholder and replace it with your own license.

9.  **`package.json`**: A manifest file for Node.js projects, which includes things like metadata (the project’s name, author, etc). This manifest is how npm knows which packages to install for your project.

10. **`README.md`**: A text file containing useful reference information about your project.

## 🛫 How to deploy to GitHub Pages

Deploying to github pages is totally up to you, be it through **[GitHub Actions](https://docs.github.com/en/actions/deployment/about-deployments/deploying-with-github-actions)**, or via **[gh-pages](https://www.npmjs.com/package/gh-pages)** package, or manually.

> [!NOTE]
>
> Remember that [GitHub Pages](https://pages.github.com/) have limitations, so for this project, I removed the page with server side rendering.

### ❗ via package ❗

**1. Install `gh-pages` package.**

```bash
# terminal
npm install gh-pages --save-dev
```

**2. Configure paths.** <small>[reference here](https://www.gatsbyjs.com/docs/how-to/previews-deploys-hosting/path-prefix/)</small>

```js
// gatsby.config.js
module.exports = {
  pathPrefix: `/blog`,
}
```

**3. Modify your _scripts_ in `package.json`.**

```json
{
  "scripts": {
    "build": "gatsby build --prefix-paths",
    "deploy": "npm run build && gh-pages -d public"
  }
}
```

**4. Create and configure a new branch for `gh-pages`.**

> [!IMPORTANT]
>
> Make sure that you have committed your changes before doing this. All untracked and staged files may be deleted.
>
> I like to do this manually. If there is some automated way, feel free to let me know by any means.

```bash
git checkout --orphan gh-pages
git reset --hard
git commit --allow-empty -m 'commit_message'
git push origin gh-pages
```

**5. Publish the production build.**

```bash
npm run deploy
```

### ❗ via manually configuring github pages settings ❗

**1. Create your project.**
Start coding your project, either use a framework like React, Vue, or not.

**2. Publish production build to GitHub.**
Push your _production build_ to your github repo. After that, check if your `index.html` file is uploaded, since it is one of the core files needed for your website to work.

**3. Configure your GitHub Pages on repo Settings.**
Navigate to `Settings > Pages > Build and deployment`. Make sure the **Source** says 'Deploy from a branch', and then configure the **Branch** settings and change it to your branch with the files.

## 💡 Learn More

Learn more with the official [docs](https://www.gatsbyjs.com/docs). If you're new to `gatsbyjs`, you might as well try the [tutorial](https://www.gatsbyjs.com/docs/tutorial/getting-started/) provided by Gatsby.

---

🌎 [kerbethecoder](https://kerbethecoder.com/)  
📫 krby.cnts@gmail.com  
📌 July 29, 2024
