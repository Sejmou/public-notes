## Lifecycle
Any service worker passes multiple stages during its 'lifecycle'

1. Registration: The browser downloads and parses the service worker file. If everything's fine we proceed with
2. Installation: The service worker's `install` event fires. By attaching a listener for that `install` event, we can make sure that any setup logic for the service worker is executed (most notably caching files/assets) 
3. Activation: A service worker can only start managing a page that registered it _after_ you navigate to that page again by reloading or reopening the PWA

## Listening for events
we can reference the service worker via the `self` keyword (in SvelteKit, we can reassign `self` to `sw` for [typesafety purposes](https://kit.svelte.dev/docs/service-workers#type-safety))

[`waitUntil`](https://developer.mozilla.org/en-US/docs/Web/API/ExtendableEvent/waitUntil) is a very useful additional property available on the service worker events that allows us to make sure any logic completed successfully. This is especially useful for the `install` event, where we need to make sure that the `activate` event doesn't fire before the service worker setup is done:
```ts
self.addEventListener('install', (event) => {
	// Create a new cache and add all files to it
	async function addFilesToCache() {
		const cache = await caches.open(CACHE);
		await cache.addAll(ASSETS);
	}

    // IIUC, waitUntil will essentially block the 'service worker setup logic' which triggers the activate event until addFilesToCache has been resolved successfully
	event.waitUntil(addFilesToCache());
});
```