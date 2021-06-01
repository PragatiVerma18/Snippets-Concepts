# Installation and building Tailwind for production in React

- [Using Tailwind in Production](https://blog.logrocket.com/using-tailwind-css-in-production/)
- [Purge CSS options](https://tailwindcss.com/docs/optimizing-for-production#purge-css-options)
- [Purge Tailwind in CRA](https://dev.to/jmhungdev/purging-tailwindcss-without-ejecting-create-react-app-4mef)
- [Example scritps](https://github.com/StandNote/StandNote.tech)

### Purging CSS
- remove unused CSS. It can be part of your development workflow.
When you are building a website, you might decide to use a CSS framework like TailwindCSS, Bootstrap, MaterializeCSS, Foundation, etc... But you will only use a small set of the framework, and a lot of unused CSS styles will be included.
- analyzes your content and your CSS files. Then it matches the selectors used in your files with the one in your content files. It removes unused selectors from your CSS, resulting in smaller CSS files.
