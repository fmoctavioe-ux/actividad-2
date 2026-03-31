<script lang="ts">
    import { goto } from '$app/navigation';
    import { CharacterBrowser } from '$lib/features/character-browser';
    import type { PageData } from './$types';

    export let data: PageData;

    function updateQuery(value: string) {
        const trimmed = value.trim();
        // Usamos la URL actual del navegador
        const params = new URLSearchParams(window.location.search);

        if (trimmed) {
            params.set('q', trimmed);
        } else {
            params.delete('q');
        }

        // Construimos la nueva ruta
        const query = params.toString() ? `?${params.toString()}` : '';
        
        // window.location.pathname asegura que nos quedemos en /actividad-2/
        // keepFocus y replaceState evitan que se pierda el cursor o se llene el historial
        goto(`${window.location.pathname}${query}`, { 
            replaceState: true, 
            keepFocus: true, 
            noScroll: true 
        });
    }
</script>

<CharacterBrowser data={data} onQueryChange={updateQuery} />