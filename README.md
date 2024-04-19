# Annoying svelte-adapter-bun problem.

No response from http requests, browser waits for ever. However, /healthcheck works.

Use the bun package manager

Steps required to get here:

- Installed the `svelte-adapter-bun` and `express` dependencies. (Already added via packages.json, you can skip this step.)
- Switch the adapter to `svelte-adapter-bun` in svelte.config.js
- Referenced the SvelteKit docs to create a my-server.js custom server script, that will load SvelteKit using Epxress server.
- Install project dependencies using `bun i`

Custom server docs can be found at: https://kit.svelte.dev/docs/adapter-node#custom-server

Okay, now start build the project with `bun run build`. Upon completion, the compiled application will be available in the ./build directory.

Now let's fire up the custom server script.

Run `bun my-server.js`.

-------------

First issue, there is no exported handler named "handler". So, I found it as "handler_default". I updated the script accordingly. Seems to not error anymore.

The issue here is that the web server will never serve a page, but the /healthcheck endpoint works.

------------

If I switch back to node-adapter and reset the handler_default back to handler, the web server works perfectly fine.

Once this issue is resolved, I can define my startup tasks in this intermediary script that in turn, calls up the SvelteKit compiled app.

----

UPATE: The custom server script updated, thanks to a suggestion by Paolo Ricciuti. Basically a modified version of the index.js found in the svelte-adapter-bun package.

Next up, figuring out how to get context of the application.