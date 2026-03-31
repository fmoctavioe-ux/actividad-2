<script lang="ts">
    import { goto, invalidateAll } from '$app/navigation';
    import { page } from '$app/stores';
    import { CharacterBrowser } from '$lib/features/character-browser';
    import type { PageData } from './$types';

    export let data: PageData;

    async function updateQuery(value: string) {
        const trimmed = value.trim();
        
        // Usamos el sistema interno de rutas de SvelteKit ($page.url)
        const url = new URL($page.url);

        if (trimmed) {
            url.searchParams.set('q', trimmed);
        } else {
            url.searchParams.delete('q');
        }

        // 1. Actualizamos la URL sin salir de tu proyecto (/actividad-2/)
        await goto(url.pathname + url.search, { 
            replaceState: true, 
            keepFocus: true, 
            noScroll: true 
        });

        // 2. ¡El toque mágico! Forzamos a que la página vuelva a cargar los personajes
        await invalidateAll();
    }
</script>

<CharacterBrowser data={data} onQueryChange={updateQuery} />