# The Next.js Handbook

## Index

1. [Introduction](#introduction)

## Introduction

Working on a modern JavaScript application powered by React is awesome until you realize that there are a couple problems related to rendering all the content on the client-side.

First, the page takes longer to the become visible to the user, because before the content loads, all the JavaScript must load, and your application needs to run to determine what to show on the page.

Second, if you are building a publicly available website, you have a content SEO issue. Search engines are getting better%20at%20running and indexing JavaScript apps, but it's much better if we can send them content instead of letting them figure it out.

The solution to both of those problems is **server rendering**, also called **static pre-rendering**.

Next.js is one React framework to do all of this in a very simple way, but it's not limited to this. It's advertised by its creators as a **zero-configuration, single-command toolchain for React apps**.

It provides a common structure that allows you to easily build a frontend React application, and transparently handle server-side rendering for you.

## The main features provided by Next.js

Here is a non-exhaustive list of the main Next.js features:

### Hot Code Reloading

Next.js reloads the page when it detects any change saved to disk.

### Automatic Routing

Any URL is mapped to the filesystem, to files put in the `pages` folder, and you don't need any configuration (you have customization options of course).

### Single File Components

Using `styled-jsx`, completely integrated as built by the same team, it's trivial to add styles scoped to the component.

### Server Rendering

You can render React components on the server side, before sending the HTML to the client.

### Ecosystem Compatibility

Next.js plays well with the rest of the JavaScript, Node and React ecosystem.

### Automatic Code Splitting

Pages are rendered with just the libraries and JavaScript that they need, no more. Instead of generating one single JavaScript file containing all the app code, the app is broken up automatically by Next.js in several different resources.

Loading a page only loads the JavaScript necessary for that particular page.

Next.js does that by analyzing the resources imported.

If only one of your pages imports the Axios library, for example, that specific page will include the library in its bundle.

This ensures your first page load is as fast as it can be, and only future page loads (if they will ever be triggered) will send the JavaScript needed to the client.

There is one notable exception. Frequently used imports are moved into the main JavaScript bundle if they are used in%20at%20least half of the site pages.

### Prefetching

The `Link` component, used to link together different pages, supports a `prefetch` prop which automatically prefetches page resources (including code missing due to code splitting) in the background.

### Dynamic Components

You can import JavaScript modules and React Components dynamically.

### Static Exports

Using the `next export` command, Next.js allows you to export a fully static site from your app.

### TypeScript support

Next.js is written in TypeScript and as such comes with an excellent TypeScript support.

## Next.js vs Gatsby vs `create-react-app`

Next.js, [Gatsby](https://flaviocopes.com/gatsby/) and [`create-react-app`](https://flaviocopes.com/react-create-react-app/) are amazing tools we can use to power our applications.

Let's first say what they have in common. They all have React under the hood, powering the entire development experience. They also abstract [webpack](https://flaviocopes.com/webpack/) and all those low level things that we used to configure manually in the good old days.

`create-react-app` does not help you generate a server-side-rendered app easily. Anything that comes with it (SEO, speed...) is only provided by tools like Next.js and Gatsby.

**When is Next.js better than Gatsby?**

They can both help with **server-side rendering**, but in 2 different ways.

The end result using Gatsby is a static site generator, without a server. You build the site, and then you deploy the result of the build process statically on Netlify or another static hosting site.

Next.js provides a backend that can server side render a response to request, allowing you to create a dynamic website, which means you will deploy it on a platform that can run Node.js.

Next.js _can_ generate a static site too, but I would not say it's its main use case.

If my goal was to build a static site, I'd have a hard time choosing and perhaps Gatsby has a better ecosystem of plugins, including many for blogging in particular.

Gatsby is also heavily based on [GraphQL](https://flaviocopes.com/graphql/), something you might really like or dislike depending on your opinions and needs.

## How to install Next.js

To install Next.js, you need to have Node.js installed. 

Make sure that you have the latest version of Node. Check with running `node -v` in your terminal, and compare it to the latest LTS version listed on https://nodejs.org/.

After you install Node.js, you will have the `npm` command available into your command line.

If you have any trouble%20at%20this stage, I recommend the following tutorials I wrote for you:

- [how to install Node.js](https://flaviocopes.com/node-installation/) 
- [how to update Node.js](https://flaviocopes.com/how-to-update-node/) 
- [An introduction to the npm package manager](https://flaviocopes.com/npm/)
- [Unix Shells Tutorial](https://flaviocopes.com/shells/)
- [How to use the macOS terminal](https://flaviocopes.com/macos-terminal/) 
- [The Bash Shell](https://flaviocopes.com/bash/)

Now that you have Node updated to the latest version and `npm`, we're set!

We can choose 2 routes now: using `create-next-app` or the classic approach which involves installing and setting up a Next app manually.

### Using create-next-app

If you're familiar with [`create-react-app`](https://flaviocopes.com/react-create-react-app/), `create-next-app` is the same thing - except it creates a Next app instead of a React app, as the name implies.

I assume you installed Node.js already, which from version 5.2 (2+ years ago%20at%20the time of writing) comes with the [`npx` command](https://flaviocopes.com/npx/) bundled. This handy tool lets us download and execute a JavaScript command, and we'll use it like this:

```bash
npx create-next-app
```

The command asks the application name (and creates a new folder for you with that name), then downloads all the packages it needs (`react`, `react-dom`, `next`), sets the `package.json` to:

![](./Screen%20Shot%202019-11-14%20at%2016.46.47.png)

and you can immediately run the sample app by running `npm run dev`:

![](Screen%20Shot%202019-11-14%20at%2016.46.32.png)

And here's the result on http://localhost:3000:

![](Screen%20Shot%202019-11-14%20at%2016.47.17.png)

This is the recommended way to start a Next.js application, as it gives you structure and sample code to play with. And there's more than just that default sample application: you can use any of the examples stored%20at%20<https://github.com/zeit/next.js/tree/canary/examples> using the `--example` option, for example try:

```bash
npx create-next-app --example blog-starter
```

Which gives you an immediately usable blog instance with syntax highlighting too:

![](Screen%20Shot%202019-11-14%20at%2017.13.29.png)

### Manually create a Next.js app

You can avoid `create-next-app` if you feel like creating a Next app from scratch. Here's how: create an empty folder anywhere you like, for example in your home folder, and go into it:

```sh
mkdir nextjs
cd nextjs
```

and create your first Next project

```sh
mkdir firstproject
cd firstproject
```

Now use the `npm` command to initialize it as a Node project:

```sh
npm init -y
```

The `-y` option tells `npm` to use the default settings for a project, populating a sample `package.json` file.

![](Screen%20Shot%202019-11-04%20at%2016.59.21.png)

Now install Next and React:

```sh
npm install next react react-dom
```

Your project folder should now have 2 files:

- `package.json` ([see my tutorial on it](https://flaviocopes.com/package-json/))
- `package-lock.json` ([see my tutorial on package-lock](https://flaviocopes.com/package-lock-json/))

and the `node_modules` folder.

Open the project folder using your favorite editor. My favorite editor is [VS Code](https://flaviocopes.com/vscode/). If you have that installed, you can run `code .` in your terminal to open the current folder in the editor (if the command does not work for you, see [this](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line))

Open `package.json`, which now has this content:

```json
{
  "name": "firstproject",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies":  {
    "next": "^9.1.2",
    "react": "^16.11.0",
    "react-dom": "^16.11.0"
  }
}
```

and replace the `scripts` section with:

```json
"scripts": {
  "dev": "next",
  "build": "next build",
  "start": "next start"
}
```

to add the Next.js build commands, which we're going to use soon.

> Tip: use `"dev": "next -p 3001",` to change the port and run, in this example, on port 3001 

![](Screen%20Shot%202019-11-04%20at%2017.01.03.png)

Now create a `pages` folder, and add an `index.js` file.

In this file, let's create our first React component.

We're going to use it as the default export:

```js
const Index = () => (
  <div>
    <h1>Home page</h1>
  </div>
)

export default Index
```

Now using the terminal, run `npm run dev` to start the Next development server.

This will make the app available on port 3000, on localhost.

![](Screen%20Shot%202019-11-04%20at%2011.24.02.png)

Open <http://localhost:3000> in your browser to see it.

![](Screen%20Shot%202019-11-04%20at%2011.24.23.png)

## View source to confirm SSR is working

Let's now check the application is working as we expect it to work. It's a Next.js app, so it should be **server side rendered**.

It's one of the main selling points of Next.js: if we create a site using Next.js, the site pages are rendered on the server, which delivers HTML to the browser.

This has 3 major benefits:

- The client does not need to instantiate React to render, which makes the site faster to your users.
- Search engines will index the pages without needing to run the client-side JavaScript. Something Google started doing, but openly admitted to be a slower process (and you should help Google as much as possible, if you want to rank well.
- You can have social media meta tags, useful to add preview images, customize title and description for any of your pages shared on Facebook, Twitter and so on.

Let's view the source of the app.
Using Chrome you can right-click anywhere in the page, and press **View Page Source**.

![](Screen%20Shot%202019-11-04%20at%2011.33.10.png)

If you view the source of the page, you'll see the `<div><h1>Airbnb clone</h1></div>` snippet in the HTML `body`, along with a bunch of JavaScript files - the app bundles.

We don't need to set up anything, SSR (server-side rendering) is already working for us.

The React app will be launched on the client, and will be the one powering interactions like clicking a link, using client-side rendering. But reloading a page will re-load it from the server. And using Next.js there should be no difference in the result inside the browser - a server-rendered page should look exactly like a client-rendered page.
