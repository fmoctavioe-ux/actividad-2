<script lang="ts">
    import { goto } from '$app/navigation';
    import { page } from '$app/stores';
    import { CharacterBrowser } from '$lib/features/character-browser';
    import type { PageData } from './$types';

    export let data: PageData;

    async function updateQuery(value: string) {
        const trimmed = value.trim();
        const url = new URL($page.url);

        if (trimmed) {
            url.searchParams.set('q', trimmed);
        } else {
            url.searchParams.delete('q');
        }

        // Actualizamos la URL
        await goto(url.pathname + url.search, { 
            replaceState: true, 
            keepFocus: true, 
            noScroll: true 
        });
    }
</script>

{#key data}
    <CharacterBrowser data={data} onQueryChange={updateQuery} />
{/key}