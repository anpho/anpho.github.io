# Shadowsocks URL Decoder

Paste Shadowsocks URL here:

<input id="ssurl"><button onclick="javascript:decodess()">Decode</button>


Protocol | Encryption Method | Password | Server | Port
---------|-------------------|----------|--------|----------
<span id="pr"></span> | <span id="enc"></span> | <span id="pwd"></span> | <span id="srv"></span> | <span id="prt"></span>

<div id="err" style="display:none">
	<span id="msg"></span>
</div>

[Home](https://anpho.github.io)

<script>
  function decodess(){
    var url=$("ssurl").value;
    try{
        var w = url.split("//");
        $("pr").innerHTML=w[0];
        var el = atob(w[1]).split(/:|@/);
        $("enc").innerHTML=el[0];
        $("pwd").innerHTML=el[1];
        $("srv").innerHTML=el[2];
        $("prt").innerHTML=el[3];
        $("err").style.display="none";

    }catch(e){
        $("enc").innerHTML="";
        $("pwd").innerHTML="";
        $("srv").innerHTML="";
        $("prt").innerHTML="";
        $("msg").innerHTML=e;
        $("err").style.display="block";
    }
  }
    function $(id){
        return document.getElementById(id);
    }
</script>
