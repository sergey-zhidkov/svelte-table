# Svelte Table

This project is build with a template for [Svelte](https://svelte.dev) apps.

I've decided to use _Svelte.js_ for this small app. Since it's my first time using it, it took me longer than 4 hours. I used this assignment task as an opportunity to try this new framework.

In the app I used `css-grid` instead of a standard table as an attempt to implement a responsive table component. Most likely, in a production app I would select a normal html table.

Because I selected `css-grid` approach instead of the `table` element my solution has many disadvantages, such as lack of accessibility support, width of the header and body cells may vary, etc. These things would require additional dev time.

Although the solution is not ideal it was worth trying implementing a simple table with `css-grid` to see the limitations of the selected approach.

I have not had enough time to add unit tests to the projects. Seems like it's not a trivial task for _Svelte.js_ with Typescript enabled.

Video:

![example](https://github.com/sergey-zhidkov/svelte-table/blob/main/animation.gif)

## Get started

Install the dependencies...

```bash
cd svelte-table
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:8080](http://localhost:8080). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```
