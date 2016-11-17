---
layout: post
title:  "Bra eller dåligt med Pre-compiled CSS med mera"
date:   2016-11-14 10:39:51
categories: precompiled css
---
##Vad tycker jag om förkompilerade css:er?

Det finns både för- och nackdelar med förkompilerade css-filer, jag tycker det kan vara bra att använda i en produktionsmiljö då det minskar antalet http-anrop.
I utvecklingsstadiet är det bra eftersom man enklare kan strukturera upp css:er, man undviker på ett bra sätt att återupprepa kod vilket annars är ett vanlig problem med css:er.

Nackdelarna är att man måste ändra i koden och kompilera för att få fram en ny fil, det går att gå in direkt på servern och ändra den levererade css:en men då kommer den skrivas över vid nästa leverans (det ska man egentligen aldrig göra men i nödfall om det är kris och panik så...).
En annan nackdel är att om någon nu går in och ändrar i den kompilerade filen så kommer den skrivas över vid nästa kompilering.

###Tekniker
 Jag valde att använda sass eftersom man rekommenderade det i kursen, jag har använt less vid något tillfälle tidigare utan att riktigt själv förstått det,
 och grunt för att minifiera css-koden.

###Fördelar och nackdelar mot vanliga css-filer:

####Fördelar
 - Mindre kod
 - Man har möjlighet att ha flera css-filer under kodning som sedan läggs ihop till en fil,
   på så vis slipper man en massa onödiga HTTP-anrop till servern.
 - Möjlighet att använda varisbler och funktioner, så t.ex. egenskaper ligger i variabler och på så sätt behöver man endast
   ändra på ett ställe då fler element ska ändra färg.

####Nackdelar
 - Krångligt, utvecklaren måste lära sig ett nytt (nåja) språk
 - Koden måste kompileras, det går att direkt ändra i den kompilerade koden som ligger på servern men vid nästa kompilering
   kommer den då att skrivas över
 - Oläsbar levererad css-kod

##Static site generators
 Är bra för sidor vars innehåll inte ändras så mycket, t.ex. bloggar, sidor med information m.m. Det passar mindre bra för
 sidor med interaktion från användare, med ett backend med databas vars information ändras.
 Sidorna är statiska HTML-sidor, därav blir de snabba (ingen webbserver som ska rendera sidor varje gång de öppnas). En annan fördel är att det inte finns något att hacka sig in i (admin, databas m.m.).
 Det går väldigt snabbt att ändra eller få ut nytt innehåll.

##robots.txt
 robots.txt används för att berätta för sökmotorer (t.ex. google) vad som ska och inte ska indexeras,
 jag konfigurerade robots.txt att inte indexera något alls, det gjorde jag genom följande kod:

    User-agent: *
    Disallow: /

 vilket betyder att alla sökmotorer saknar tilåtelse att spindla igenom rooten och allt därunder.

##humans.txt
 humans.txt är en fil där man kan skriva vilka som medverkat till att skapa en sida, även info om senaste release och lite annat
 kan läggas till.

 Inget jag använt tidigare.

##Implementation av kommentarer till blogginlägg
 Jag valde att använda disqus, jag registrerade ett konto och en site på deras hemsida, sedan gick jag igenom en step-by-step beskrivning om hur man skulle göra.
 Jag la till ett script, först i blog-sidan men då kommenterade man inte inlägg utan hela bloggen vilket inte riktigt var tanken, jag la då in script-koden i
 post.html som genereras för varje blogginlägg, då dök möjligheten att kommentera upp under varje blogginlägg.
 I utvecklingsfasen satte jag variabeln disqus_developer till true vilket gör att det fungerar under localhost, vid driftsättning avmarkerar jag raden.

##Implementation av Open Graph
 Open Graph är ett facebook-påhitt för att kunna dela inlägg på sociala medier (facebook och twitter).
 Jag la in det i bloggen så besökare kan dela mina framtida briljanta inlägg på facebook.
