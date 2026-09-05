# Linux Vecka 1
## learning the basics

Linux använder sig av / som "root", alltså starten för hela systemet. Tilde-key "~" används för att direkt
navigera tillbaka till "hem" (e.g. /home/zerkmann).

För att byta filer eller område använder man cd ("change directory"). För att skapa ett nytt område använder man
kommando mkdir "make directory" och det namn som skall användas.

"touch" skapar en ny fil inuti ett område, t. ex. "touch text.txt". Man kan sedan använda cp ("copy") för att
kopiera vald fil, använd sedan mv (move) för att flytta på filen eller byta namn på filen.

Exempel mv:

mv text.txt text-copy.txt (byta namn på fil)
cp text.txt text-copy.txt (kopierar text.txt och döper kopain till text-copy.txt)

För att ta bort en fil använder man kommando rm ("remove"), och likadant för områden "rmdir" ("remove directory").
Linux använder inte en varning för att radera, utan gör detta utan diskriminering.

rm -f (force) kan därför vara farligt att använda.

Inuti ett direktiv kan man använda kommando som t. ex. ls (list) för att lista objekt. Du kan även använda kommandot
ls -a ("all") för att lista även dolda objekt. Dolda objekt börjar oftast med ".XXX" (punkt). 

Man kan även använda ls -l för att få mer information om objekten. Kombinera då även ls -la för att lista alla
objekt med mer information.

nano skapar upp en textfil som är redigerbar direkt i terminalen. Detta använder jag för att föra anteckningar inuti
den miljö jag har skapat för min DevOps resa.

Ett annat fiffigt kommando är att använda head or tail, där head ("huvud") visar de första objekten i ett dir, medan
tail visar de sista filerna i ett dir. "tail" kan jag även använda med "tail -l" för att visa ett live flöde.

Jag kan även, vid större kataloger/dir, använda mig av less (e.g. less /etc/services) för att visa filerna på ett
mer strukturerat sätt.

tree använder jag för att på ett enklare sätt strukturera upp ett dir som är mindre. Jag kan även använda cat.

De kommando som jag lärt mig under basics är:

- pwd (visar mitt nuvarande område/dir)
- rm (remove, tar bort filer)
- rmdir (remove dir, tar bort områden)
- mkdir (skapar dir)
- touch (skapar filer)
- cp (kopiera filer)
- mv (flytta eller döpa om filer)
- nano (intern anteckning)
- ls (lista objekt)
- ls -a (lista dolda objekt)
- ls -l (lista objekt med mer information)
- head (visa första objekten i ett dir)
- tail (visa sista objekten i ett dir)

Det är även viktigt att tänka på absolut vs relativ sökning. Linux söker alltid relaterat till var man befinner sig,
och det är därför viktigt att veta hur strukturerat man behöver söka. Till exempel, om jag befinner mig i ett känt
direktiv (som t.ex. /home/zerkmann) där jag vet att jag har ett dir, så kan jag bara använda "cd /namnpådir" för att
flytta dit. Men befinner jag mig inte i närheten av detta dir, så kan jag behöva söka mig fram genom att använda
Tilde "~" och mer fullständiga söknamn.


LÖRDAG 5/9/26

Övningar med nano och bash/scripts. Jag förstod först inte varför ./hello.sh gav Permission denied. Problemet var att filen saknade execute-permission. Efter chmod +x hello.sh kunde scriptet köras.
Lärt mig fler kommandon i min Linux-resa, bl. a.

./ (som i princip betyder kör denna fil i denna sökväg)
