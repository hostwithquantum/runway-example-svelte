

# Runway Example svelte App

This is an example app demonstrating how to deploy a svelte app
to [runway](https://runway.planetary-quantum.com/).

* clone this repo, and navigate into that directory
* `runway app create`
* `runway app deploy`
* `runway open`

You can then deploy changes by `git commit`ing them, and running `runway app
deploy` again.

This is a todo app (aka a demo app) for SvelteKit (via `npm create svelte@latest`).

Follow these steps to prepare the application for deployment on runway:

## Step 1

In order to demonstrate that the actual nodejs runtime works, we added the node adapter to Svelte after the installation: `npm i -D @sveltejs/adapter-node`

```diff
❯ git diff
diff --git a/content/svelte/package.json b/content/svelte/package.json
index ca33aa5..74eef09 100644
--- a/content/svelte/package.json
+++ b/content/svelte/package.json
@@ -11,6 +11,7 @@
        },
        "devDependencies": {
                "@sveltejs/adapter-auto": "next",
+               "@sveltejs/adapter-node": "^1.0.0-next.86",
                "@sveltejs/kit": "next",
                "@types/cookie": "^0.5.1",
                "svelte": "^3.46.0",
diff --git a/content/svelte/svelte.config.js b/content/svelte/svelte.config.js
index 48e3f1e..52851ff 100644
--- a/content/svelte/svelte.config.js
+++ b/content/svelte/svelte.config.js
@@ -1,4 +1,4 @@
-import adapter from '@sveltejs/adapter-auto';
+import adapter from '@sveltejs/adapter-node';
 
 /** @type {import('@sveltejs/kit').Config} */
 const config = {
```

## Step 2

Since Sveltekit currently doesn't include a `start` command, we will add that:

```diff
diff --git a/package.json b/package.json
index 3803c14..f4d490f 100644
--- a/package.json
+++ b/package.json
@@ -7,7 +7,8 @@
                "package": "svelte-kit package",
                "preview": "vite preview",
                "check": "svelte-check --tsconfig ./jsconfig.json",
-               "check:watch": "svelte-check --tsconfig ./jsconfig.json --watch"
+               "check:watch": "svelte-check --tsconfig ./jsconfig.json --watch",
+               "start": "node build/index.js"
        },
        "devDependencies": {
                "@sveltejs/adapter-auto": "next",
@@ -19,6 +20,9 @@
                "typescript": "^4.7.4",
                "vite": "^3.0.0"
        },
```

## Step 3 (deployment)

Commit everything, `git commit -a -m 'My first release` and deploy the code with `runway app deploy`. Done!

