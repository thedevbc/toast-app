<script lang="ts">
    import { getToastStore, initializeStores, Toast } from '@skeletonlabs/skeleton';
    // import type { ToastSettings, ToastStore } from '@skeletonlabs/skeleton';
	import '../app.postcss';

    initializeStores();
    const toastStore = getToastStore();
</script>
<Toast />
<slot></slot>

<style></style>
