<!-- img snap -->

<!-- badges -->

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
    'gatsby-plugin-postcss',
    // ...
  ],
};
```

**5. Configure your template paths.**

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './src/pages/**/*.{js,jsx,ts,tsx}',
    './src/components/**/*.{js,jsx,ts,tsx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
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
import './src/styles/global.css';
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
  );
}
```
