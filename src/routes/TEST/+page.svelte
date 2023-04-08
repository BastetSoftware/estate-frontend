<script>
    import { SendAPICall } from "$lib/API.svelte";
    
    import { Button } from "flowbite-svelte";
    
    async function Ping() {
        alert(await SendAPICall("ping", {}))
    }
    
    const pingBtn = () => {
        Ping();
    }
</script>

<Button on:click={pingBtn}>Пинг!</Button>