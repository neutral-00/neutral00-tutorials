# Website

This website is built using [Docusaurus](https://docusaurus.io/), a modern static website generator.

### Installation

```
$ yarn
```

### Local Development

```
$ yarn start
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

### Build

```
$ yarn build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

### Deployment

Using SSH:

```
$ USE_SSH=true yarn deploy
```

Not using SSH:

```
$ GIT_USER=<Your GitHub username> yarn deploy
```

If you are using GitHub pages for hosting, this command is a convenient way to build the website and push to the `gh-pages` branch.

## let mdx parse only .mdx files.

To make MDX parse only `.mdx` files and exclude `.md` files in Docusaurus, you'll need to modify the configuration to ensure that regular Markdown files are not processed by MDX.

### **Steps to Achieve This:**
1. **Configure Docusaurus to Handle MDX Separately**
   In `docusaurus.config.js`, update the presets so that MDX processing is restricted to `.mdx` files:
   ```js
   module.exports = {
     presets: [
       [
         '@docusaurus/preset-classic',
         {
           docs: {
             path: 'docs',
             routeBasePath: 'docs',
             extensions: ['mdx'], // Restricts MDX processing to .mdx files
           },
         },
       ],
     ],
   };
   ```

2. **Ensure Markdown Files Are Not Processed as MDX**
   In some cases, `.md` files might still get parsed. If you're using custom webpack settings, ensure that you explicitly exclude `.md` files from MDX processing:
   ```js
   module.exports = {
     webpack: {
       configure: (config) => {
         config.module.rules.push({
           test: /\.md$/,
           use: 'raw-loader', // Treat .md files as plain text
         });
         return config;
       },
     },
   };
   ```

3. **Verify Your File Structure**
   - Place `.mdx` files inside the `docs/` or `blog/` folder.
   - Ensure `.md` files are outside folders that use MDX processing or are loaded manually as plain Markdown.

---

### **Result:**
With this setup:
✅ `.mdx` files will be parsed by MDX.  
❌ `.md` files will remain as plain Markdown or be handled separately.

Let me know if you need any tweaks or debugging assistance! 🚀😊

