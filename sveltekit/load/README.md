# SvelteKit 

TL;DR: How to "stream" a load on the *+page.svelte*

The following code was from 
[5 Things I Wish I Knew When I Started Using SvelteKit - Ben Davis](https://youtu.be/eJpPNg-v0Fo?si=AHLD_Khs5InlgWWF).

+page.server.ts
```ts
export const load = async () => {
    const streamed = fakeFetch();

    const normal = {message: 'this was fast!' };

    return {
        normal,
        streamed
    };
}

async function fakeFetch() {
    await delay(3000);
    return {
        message: 'this was slow!'
    }
}

function delay(ms: number): Promise<void> {
    return new Promise((resolve) => setTimeout(resolve, ms));
}
```

+page.svelte

```ts
<script lang="ts">
    const { data } = $props();
</script>

<h2> MY NORMAL MESSAGE: {data.normal.message}</h2>

{#await data.streamed}
    <h2>LOADING MY STREAMD RESPONSE</h2>
{:then streamedData}
    <h2> MY STREAMED RESPONSE: {streamedData.message}</h2>
{/await}
```