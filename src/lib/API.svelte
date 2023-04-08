<script context="module">
    import { unpack, pack } from 'msgpackr';
    
    import { onMount } from 'svelte';
    
    export async function SendAPICall(method, args, address="http://localhost:8080/") {
        var query = pack({
            "Func": APIMethod[method],
            "Args": args
        });
        
        let response = await fetch(address, {
            method: 'POST',
            body: query.toString()
        });
        
        if (response.ok) {
            return unpack(await response.text());
        } else {
            return {"error": "Can't connect to backend"}
        }
    }
    
    export const APIMethod = {
        "ping": 0,
        "createUser": 1,
        "login": 2,
        "logout": 3,
        "getUserInfo": 4,
        "editUserInfo": 5
    };
</script>