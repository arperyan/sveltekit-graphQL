<script>
	import { globalStyles } from "$lib/styles/global";
	import Header from "$components/Header.svelte";
	// import "../global.css";
	import { endpoint, prodEndpoint } from "../../config";
	import { createClient, setClient } from "@urql/svelte";
	import { multipartFetchExchange } from "@urql/exchange-multipart-fetch";
	import { dedupExchange, cacheExchange } from "@urql/svelte";
	import { onMount } from "svelte";
	import { seoData } from "$lib/SEO";
	import SvelteSeo from "svelte-seo";

	onMount(() => globalStyles());

	const client = createClient({
		url: prodEndpoint,
		exchanges: [dedupExchange, cacheExchange, multipartFetchExchange]
	});

	setClient(client);
</script>

<SvelteSeo {...seoData({})} />
<main>
	<Header />
	<div class="container">
		<slot />
		<!-- <button class={buttons({ size: "large" })}>Hello Worls</button> -->
	</div>
</main>

<style>
	.container {
		max-width: var(--sizes-maxWidth);
		margin: 0 auto;
		padding: 2rem;
	}
</style>
