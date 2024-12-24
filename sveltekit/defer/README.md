# SvelteKit Defer

TL;DR: How to only load content that you need for the first paint of the page, then load the rest of the elements.

The following code was from 
[New SvelteKit Feature - Defer: Huntabyte](https://youtu.be/wTF9uunxSvA?si=xgz822qtf1_kheT2).

+page.server.ts
```ts
import { db } from "$lib/server/db";
import type { PageServerLoad } from './types';

export const load: PageServerLoad = async() => {
    return {
        posts: db.getBlogPostList(10),
        lazy: {
            posts.db.getBlogPostList(90, 10, 3000), // Get 90 more and ignore the first 10 since you already got it.
        }
    }
}
```

+page.svelte
```js
<script lang="ts">
    import PostCard from '$lib/components/PostCard.svelte';
    import type { PageData } from './$types';

    export let data: PageData
</script>

<div class="post-list">
    <h1 class="text-3xl font-bold underline">Featured</h1>
    {#each data.posts as post}
        <PostCard {post} />
    {/each}
    {#await data.lazy.posts}
        <p>Loading more posts...</p>
    {:then posts}
        {#each posts as post}
            <PostCard {post} />
        {/each}
    {:catch}
        <p>Error loading posts...</p>
    {/await}
</div>
```