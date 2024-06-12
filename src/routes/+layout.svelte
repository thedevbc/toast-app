<script lang="ts">
	import { getToastStore, initializeStores, Toast } from '@skeletonlabs/skeleton';
	// import type { ToastSettings, ToastStore } from '@skeletonlabs/skeleton';
	import '../app.postcss';
	import { browser } from '$app/environment';
	import { onMount, tick } from 'svelte';


		setTimeout(() => {
            throw new ErrorEvent('This is an error.');
        }, 1000);


	initializeStores();
	const toastStore = getToastStore();

	async function handleError(e: string | Event) {
		let message = 'Unknown error';
		if (typeof e === 'string') {
			message = e;
		} else {
			const typedError = e as Event & { currentTarget: EventTarget & HTMLElement } & {
				reason?: { message: string; stack: string };
			};
			message = typedError.reason
				? `${typedError.reason.message}\r\n\r\n${typedError.reason.stack}`
				: typedError.toString();
		}

		const hookClassForToastErrorMessage = 'hook-for-toast-error-message';
		toastStore.trigger({
			message,
			classes: `${hookClassForToastErrorMessage} bg-red-500 text-white break-all text-wrap`,
			autohide: false,
			action: {
				label: 'To Clipboard',
				response: () => navigator.clipboard.writeText(message)
			}
		});
		await tick();
		const checkForToast = document.querySelector(`.${hookClassForToastErrorMessage}`);

		if (!checkForToast) {
			console.error('Standard error message may have failed; showing backup error message');
			alert(`${message}`);
		}
	}
	if (browser) {
		// Cannot use <svelte:window> since they seem to get initalized after
		// other javascript code has run; which is too late if an error is thrown
		// during the initial client side execution of code
		window.onerror = handleError;
		window.onunhandledrejection = handleError;
	}
</script>

<Toast />
<slot></slot>

<style></style>
