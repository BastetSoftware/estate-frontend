<script>
    import { SendAPICall } from "$lib/API.svelte";
    
    import { Button } from "flowbite-svelte";
    
    async function Ping() {
        var data = await SendAPICall("ping", {});
        alert(data)
    }
    
    const pingBtn = async () => {
        await Ping();
    }
</script>

<Button on:click={pingBtn}>Пинг!</Button>