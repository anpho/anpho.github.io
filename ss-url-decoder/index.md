# Shadowsocks URL Decoder

Paste Shadowsocks URL here:

<input id="ssurl"><button onclick="javascript:decodess()">Decode</button>

<div id='result' style="display:none">
    <ul>
        <li><b>Encryption Method:</b>
        <li id='enc'>
        <li><b>Password:</b>
        <li id='pwd'>
        <li><b>Server:</b>
        <li id='srv'>
        <li><b>Port:</b>
        <li id='prt'>
</div>
<div id='err' style='display:none'>
</div>

<script>
  function decodess(){
    var url=$("ssurl").value;
    try{
        var w = url.split("//");
        var el = w.split(/:|@/);
        $('enc').innerHTML=el[0];
        $('pwd').innerHTML=el[1];
        $('srv').innerHTML=el[2];
        $('prt').innerHTML=el[3];
        $('err').style.display="none";
        $('result').style.display='block';
    }catch(e){
        $('result').style.display='none';
        $('err').innerHTML=e;
        $('err').style.display="block";
    }
  }
    function $(id){
        return document.getElementById(id);
    }
</script>