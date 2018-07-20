# Shadowsocks URL Decoder

Paste Shadowsocks URL here:
<input id="ssurl"></input> <button onclick="javascript:decodess()">Decode</button>

<script>
    function decodess(){
        var url=document.getElementById('ssurl').value;
        var w = url.split("//");
        document.write(atob(w[1]))
    }
</script>