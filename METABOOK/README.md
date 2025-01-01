# [metabook](https://github.com/LafeLabs/metabook)

Metadata for a physical book


# index.html:

```
    <!doctype html>
    <html lang="en">
    <head>
       <meta charset="utf-8">
       <!--
    
    TRASH MAGIC!


       -->
       <!--Stop Google:-->
       <META NAME="robots" CONTENT="noindex,nofollow">
  
      <link href="data:image/x-icon;base64,AAABAAEAEBAQAAEABAAoAQAAFgAAACgAAAAQAAAAIAAAAAEABAAAAAAAgAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAP//AP///wANAP8A5Dz6ABueRwAAt/8A6BonABo86AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAREREREREREREREAAAEREREREQCIgREREd3dwAAB3d3d3d3d3d3d3d3d3d3d3d3d3VVVVVVVQAFVVAAVVVQIiBRAiIBEQIAIBECAAERAgAgFgIABmYCIiBmAiIGZgIiIGYCIgZmYCIAaIAAMzMzAAiIiIiIiIiIiIiIiIiIiIiIgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA" rel="icon" type="image/x-icon" />
      
       <title>TRASH MAGIC NETWORK</title>    
       <script src = "https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
       <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.2.6/ace.js" type="text/javascript" charset="utf-8"></script>       
       <script src = "trashmagic.js"></script>
    </head>
    <body>  
<H1>
    <a href = "edit.html">EDIT THIS PAGE</a>
</H1>
<h1 id = "title">METABOOK</h1>

<div id = "qrcode"></div>

<UL id = "LIST"></UL>


<pre id = "jsonpre"></pre>



<script>
rainbowstring(document.getElementById("title"));

METABOOK = {};
METABOOK.NAME = "METABOOK";
METABOOK.TITLE = "The American Evasion of Philosophy";
METABOOK.AUTHOR = "Cornel West";
METABOOK.DATE = "1989";
METABOOK.PUBLISHER = {};
METABOOK.PUBLISHER.NAME = "THE UNIVERSITY OF WISCONSIN PRESS";
METABOOK.PUBLISHER.LOCATION = "MADISON, WISCONSIN";
METABOOK.PUBLISHER.URL = "https://uwpress.wisc.edu/";
METABOOK.URLS = ["https://uwpress.wisc.edu/books/0541.htm","https://trashrobot.net/The_American_Evasion_of_Philosophy/"]
METABOOK.URL = "https://trashrobot.net/The_American_Evasion_of_Philosophy/";
METABOOK.ISBN = "0-299-11964-5";
METABOOK.WATERSHED = "SOUTH PLATTE RIVER";
METABOOK.STREET = "US ROUTE 36";
METABOOK.CITY = "NEODENVER";
METABOOK.LIBRARIAN = {};
METABOOK.LIBRARIAN.NAME = "DIRT WIZARD";
METABOOK.LIBRARIAN.URL = "HTTPS://WWW.TRASHROBOT.NET";
METABOOK.LIBRARIAN.FEDIVERSE = "https://cyberpunk.lol/@dirtwizard666";
METABOOK.FORMAT = "6X9 PERFECTBOUND, 279 PAGES"
METABOOK.MANIFESTO = "EVERYTHING FREE FOR EVERYONE EVERYWHERE RIGHT NOW!"
METABOOK.TAGLINE = "FREE PHILOSOPHY BOOK!";
METABOOK.NOTES = "I BOUGHT THIS BOOK BECAUSE I LIKE PROFESSOR WEST'S OTHER WORK BUT IT IS TOO ACADEMIC FOR ME SO I AM PASSING IT ALONG TO SOMEONE WHO CAN REALLY APPRECIATE THIS DEEP DIVE INTO AMERICAN PHILOSOPHICAL HISTORY";
METABOOK.WALL = "THIS IS THE WALL. IT IS WHERE WE WRITE LITTLE NOTES TO ONE ANOTHER ABOUT THIS BOOK AND ABOUT METABOOK.";
METABOOK.MAGIC = ["TRASH","DIRT","BOOK","CHAOS","WEB","SUN","WATER","STREET"];

document.getElementById("jsonpre").innerHTML = JSON.stringify(METABOOK,null,"    ");

savejson();

var httpc3 = new XMLHttpRequest();
httpc3.onreadystatechange = function(){
    if (this.readyState == 4 && this.status == 200) {
        book = JSON.parse(this.responseText);
        loadjsonvals();
    }
};
httpc3.open("GET", "fileloader.php?filename=book.txt", true);
httpc3.send();

function loadjsonvals(){
    document.getElementById("LIST").innerHTML = "";
    for(var attribute in METABOOK){
        if(attribute != "NAME"){
            var newli = document.createElement("LI");
            document.getElementById("LIST").appendChild(newli);
            if(typeof METABOOK[attribute] === 'object'){
                var newul = document.createElement("UL");
                newli.innerHTML = attribute + ":";
                newli.appendChild(newul);
                for(subattribute in METABOOK[attribute]){
                    var newsubli = document.createElement("LI");
                    newul.appendChild(newsubli);
                    if(subattribute == "URL" || attribute == "URLS"){
                        newsubli.innerHTML = "<a href = \"" + METABOOK[attribute][subattribute] + "\">" + subattribute + ":" + METABOOK[attribute][subattribute] + "</a>";
                    }
                    else{
                        newsubli.innerHTML = subattribute + ":" + METABOOK[attribute][subattribute];
                    }

                    
                }        
            }
            else{
                if(attribute == "URL"){
                    newli.innerHTML = "<a href = \"" + METABOOK[attribute] + "\">" + attribute + ":" + METABOOK[attribute] + "</a>";
                }
                else{
                    newli.innerHTML = attribute + ":" + METABOOK[attribute];
                }
            }
        }
    }
    rainbow(document.getElementsByTagName("LI"));
}


function savejson(){

    var url = "filesaver.php";        
    var httpc2 = new XMLHttpRequest();
    httpc2.open("POST", url, true);
    httpc2.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
    httpc2.send("data="+encodeURIComponent(JSON.stringify(METABOOK,null,"    "))+"&filename=METABOOK.txt");//send text to filesaver.php

}


    codesquaresize = 170;
    marginsize = 40;
    fontsize = 12;
    //globalurl = "http://www.trashrobot.org/qrcode.html";
    globalurl = window.location.href;
    qrcode = new QRCode(document.getElementById("qrcode"), {
    	text: globalurl,
    	width: codesquaresize,
    	height: codesquaresize,
    	colorDark : "#000000",
    	colorLight : "#ffffff",
    	correctLevel : QRCode.CorrectLevel.H
    });
    
</script>

<STYLE>
h1{
    font-size:4em;
    font-family:arial;
}
    body{
        background-color:#404040;
        font-size:1em;
    }
    li{
        font-family:arial;
        border-radius:5px;
        margin:1em 1em 1em 1em;
        padding:1em 1em 1em 1em;

    }
    pre{
        width:80%;
        display:block;
        margin:auto;
        font-family:courier;
        background-color:black;
        color:#00ff00;
        overflow:scroll;
        padding: 1em 1em 1em 1em;
    }
    IMG{
        display:block;
        text-align:center;
        max-width:60%;
        margin:auto;
    }
    H1{
        TEXT-ALIGN:CENTER;
    }
    a{
        color:blue;
    }
</STYLE>

    </body>
    </html>
    
    

```