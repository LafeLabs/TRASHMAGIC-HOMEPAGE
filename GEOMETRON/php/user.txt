<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">

    <!--

        EVERYTHING IS PHYSICAL 
        EVERYTHING IS FRACTAL
        EVERYTHING IS RECURSIVEm
        NO MONEY 
        MO MINING 
        NO PROPERTY
        LOOK AT THE INSECTS
        LOOK AT THE FUNGI
        LANGUAGE IS HOW THE MIND PARSES REALITY 

    -->
    <link href="data:image/x-icon;base64,AAABAAEAEBAQAAEABAAoAQAAFgAAACgAAAAQAAAAIAAAAAEABAAAAAAAgAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAP//AP///wANAP8A5Dz6ABueRwAAt/8A6BonABo86AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAREREREREREREREAAAEREREREQCIgREREd3dwAAB3d3d3d3d3d3d3d3d3d3d3d3d3VVVVVVVQAFVVAAVVVQIiBRAiIBEQIAIBECAAERAgAgFgIABmYCIiBmAiIGZgIiIGYCIgZmYCIAaIAAMzMzAAiIiIiIiIiIiIiIiIiIiIiIgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA" rel="icon" type="image/x-icon" />

    <!--Stop Google:-->
    <META NAME="robots" CONTENT="noindex,nofollow">

    <script src="jscode/mapfactory.js"></script>


<!--       un comment to use math

        <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
        <script>
            MathJax.Hub.Config({
                tex2jax: {
                inlineMath: [['$','$'], ['\\(','\\)']],
                processEscapes: true,
                processClass: "mathjax",
                ignoreClass: "no-mathjax"
                }
            });//			MathJax.Hub.Typeset();//tell Mathjax to update the math
        </script>
    -->

    
</head>
<body>    
<div id = "mainmap"></div>
<div id = "modebutton" class = "button">LIGHT<br>DARK</div>
<div id = "hidebutton" class = "button"><span id  = "hideshow">SHOW</span><br>MENU</div>
<div id = "margin">
    <div id = "marginbutton">⇳⇳⇳⇳⇳⇳⇳⇳⇳⇳⇳</div>
    <div id  = "mapsbox">
        <input id = "mapinput"/>
        <a id = "mapeditorlink" href = "mapeditor.html">
            <img style = "width:50px;display:block;margin:auto;padding-top:1em" src = "iconsymbols/edit.svg"/>
        </a>        
    </div>
</div>

<div class = "data" id = "mapdiv"><?php
    
if(isset($_GET["map"])){
    echo $_GET["map"];
}

?></div>

<script>

mode = "dark";
//mode = "light";


if(innerWidth > innerHeight){
    menuhide = false;
    mainmap = new Map(innerHeight,innerHeight,document.getElementById("mainmap"));

    document.getElementById("margin").style.left = (innerHeight).toString() + "px";


}
else{
    menuhide = true;

    mainmap = new Map(innerWidth,innerWidth,document.getElementById("mainmap"));    
    
    document.getElementById("margin").style.display = "none";
    document.getElementById("margin").style.height = (innerHeight - innerWidth - 150).toString() + "px";
    document.getElementById("margin").style.bottom = "0px";
    
}


document.getElementById("hidebutton").onclick = function(){
    menuhide = !menuhide;
    if(menuhide){
        document.getElementById("hideshow").innerHTML = "SHOW";
        document.getElementById("margin").style.display = "none";

    }
    else{
        document.getElementById("hideshow").innerHTML = "HIDE";
        document.getElementById("margin").style.display = "block";
    }
}


//mainmap.math = true;


filename = "maps/home";
mapname = "maps/home";
if(document.getElementById("mapdiv").innerHTML.length > 0){
    mapname = document.getElementById("mapdiv").innerHTML;
}
loadmap(mapname);

ismap = false;
localfile = true;

function loadmap(mapname){
    ismap = true;
    filename = mapname;
    if(filename.substring(0,5) == "maps/"){
        localfile = true;
    }
    else{
        localfile = false;
    }
    
    document.getElementById("mainmap").style.display = "block";
    document.getElementById("mapeditorlink").href = "mapeditor.php?map=" + filename;
        
    var httpc = new XMLHttpRequest();
    httpc.onreadystatechange = function(){
        if (this.readyState == 4 && this.status == 200) {
            
            var raw = this.responseText;
            if(raw.charAt(0) != "["){
                raw = raw.substring(raw.indexOf("["))
            }
            mainmap.array = JSON.parse(raw);
    

            N = mainmap.array.length;

            for(var index = 0;index < mainmap.array.length;index++){
                
            }
            
            mainmap.draw();
            //			MathJax.Hub.Typeset();//tell Mathjax to update the math
            for(var index = 0;index < mainmap.linkArray.length;index++){
                if(mainmap.array[index].maplinkmode == true){
                    
                    
                    mainmap.linkArray[index].onclick = function(){
                        var localmap = this.getElementsByClassName("maplink")[0].innerHTML;
                        loadmap(this.getElementsByClassName("maplink")[0].innerHTML);                               
                    }
                }
            }

        }
    };
    httpc.open("GET", "fileloader.php?filename=" + mapname, true);
    httpc.send();
}




document.getElementById("modebutton").onclick = function(){
    modeswitch();
}

modeswitch();
function modeswitch(){
    if(mode == "dark"){
        mode = "light";
        document.body.style.backgroundColor = "white";
        mainmap.linkColor = "blue";
        mainmap.textColor = "black";
        document.getElementById("mapinput").style.color = "black";
        document.getElementById("mapinput").style.backgroundColor = "white";
        
        document.getElementById("mapsbox").style.backgroundColor = "#ffd0d0";
        document.getElementById("mapsbox").style.color = "black";    
        
    }
    else{
        mode = "dark";
        document.body.style.backgroundColor = "black";
        mainmap.textColor = "#00ff00";
        mainmap.linkColor = "#ff2cb4";
        document.getElementById("mapinput").style.color = "#ff2cb4";
        document.getElementById("mapinput").style.backgroundColor = "black";
        document.getElementById("mapsbox").style.backgroundColor = "#602020";
        document.getElementById("mapsbox").style.color = "#00ff00";  

                

    }
}

maps = [];
var httpc8 = new XMLHttpRequest();
httpc8.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        maps = JSON.parse(this.responseText);
        for(var index = 0;index < maps.length;index++) {
            var newmapbutton = document.createElement("P");
            newmapbutton.className = "boxlink";
            newmapbutton.innerHTML = "maps/" + maps[index];
            document.getElementById("mapsbox").appendChild(newmapbutton);
            newmapbutton.onclick = function(){
                currentFile = this.innerHTML;
                loadmap(currentFile);
            }
        }
    };
}

httpc8.open("GET", "dir.php?filename=maps", true);
httpc8.send();



document.getElementById("mapinput").value = "";

document.getElementById("mapinput").onchange = function(){
    loadmap(this.value);
    this.value = "";
}

</script>
<style>
body{
    overflow:hidden;
    background-color:black
}
input{
    display:block;
    margin:auto;
    width:90%;
    font-family:courier;
    font-size:1.2em;
    background-color:white;
    color:black;
    border-color:#ff2cb4;
    border-width:8px;
}
.boxlink{
    padding-left:1em;
    cursor:pointer;
}
.boxlink:hover{
    background-color:#808080;
}
#mainmap{
    position:absolute;
    left:0px;
    top:0px;
    overflow:hidden;
}
#mainmap a{
    font-family:Helvetica;
    color:#ff2cb4;
}

.data{
    display:none;
}
h1,h2,h3,h4{
    text-align:center;
}
#modebutton{
    position:absolute;
    background-color:white;
    color:black;
    cursor:pointer;
    border:solid;
    border-radius:5px;
    text-align:center;
}
#hidebutton{
    position:absolute;
    background-color:white;
    color:black;
    cursor:pointer;
    border:solid;
    border-radius:5px;
    text-align:center;
}
.button:hover{
    background-color:green;
}
.button:active{
    background-color:yellow;
}
#margin{
    position:absolute;
    right:0px;
    bottom:0px;
    z-index:-1;
    overflow:hidden;
    background:#404040;
    font-size:1.2em;
}
#mapsbox{
    position:absolute;
    left:0px;
    top:0px;
    bottom:0px;
    right:0px;
    color:black;
    background-color:#ffd0d0;
    overflow:scroll;
}

@media only screen and (orientation: landscape) {
    #margin{
        top:0px;
    }
    #modebutton{
        right:5px;
        top:5px;
    }
    #hidebutton{
        display:none;
    }
}

@media only screen and (orientation: portrait) {
    #modebutton{
        right:0px;
        bottom:0px;
    }
    #margin{
        bottom:0px;
        left:0px;
    }
    #margin img{
        width:50px;
    }
    #hidebutton{
        left:0px;
        bottom:0px;
    }
    .button{
        font-size:2em;
    }
}
.data{
    display:none;
}
</style>
</body>
</html>