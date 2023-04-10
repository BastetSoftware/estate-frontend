<script context="module">
    import { unpack, pack } from 'msgpackr';
    
    export async function SendAPICall(method, args, address=`http://localhost:8080/`) {
        var query = pack(args);
        
        address += "api/" + method;
        
        let response = await fetch(address, {
            method: 'POST',
            body: query,
            headers: {
                "Access-Control-Request-Headers": "Content-Type, x-requested-with",
                "Access-Control-Request-Method": "POST"
            }
        });
        
        if (response.ok) {
            let resp = await response.arrayBuffer();
            let resp_data = new Uint8Array(resp);
            
            var result = unpack(resp_data);
            return result
        } else {
            return {error: "Can\'t connect to backend"}
        }
    }
</script>