# Week 3 - Linux Networking

## Network interfaces and IP addresses

Ett nätverksinterface är den anslutning som datorn använder för att kommunicera över nätverk, till exempel WiFi eller Ethernet.

En IP-adress används för att identifiera en nätverksanslutning så att data kan skickas till rätt destination.

Jag använde:

`ip -br addr`

för att se vilka nätverksinterface som finns och vilka IP-adresser de har.

---

## Default gateway and routing

En default gateway är normalt routern eller nästa nätverksenhet som datorn skickar trafik till när den inte har en mer specifik route till destinationen.

Jag använde:

`ip route`

för att se datorns routingtabell och hitta raden som börjar med:

`default via`

Det visar vilken gateway som används som standard.

---

## Private and public IP addresses

En privat IP-adress används inne i ett lokalt nätverk och är inte direkt routbar på det publika internet.

Exempel på privata adresser är ofta:

`192.168.x.x`

eller

`10.x.x.x`

En publik IP-adress används för kommunikation ut på internet och kan ses av externa tjänster.

---

## NAT

NAT betyder Network Address Translation.

I ett vanligt hemnätverk kan flera enheter ha privata IP-adresser men ändå använda samma publika IP-adress ut mot internet.

Routern hanterar översättningen mellan det privata nätverket och internet.

---

## Localhost and loopback

`localhost` betyder den egna datorn.

IPv4-adressen för localhost är normalt:

`127.0.0.1`

Linux använder ett loopback-interface, vanligtvis `lo`, för kommunikation med den egna datorn.

Det betyder att trafik till localhost inte behöver gå via routern eller internet.

---

## Ports

En IP-adress används för att hitta rätt maskin, medan en port används för att hitta rätt tjänst på den maskinen.

Exempel:

`localhost:8000`

betyder att man kontaktar sin egen dator på port 8000.

Vanliga portar:

- 22 = SSH
- 80 = HTTP
- 443 = HTTPS

---

## Client and server

En client är programmet som tar initiativet och kontaktar en tjänst.

En server är programmet eller tjänsten som väntar på och tar emot förfrågningar.

Exempel:

`curl` kan fungera som client och kontakta en webbserver.

---

## DNS

DNS betyder Domain Name System.

DNS används för att översätta domännamn till IP-adresser.

Exempel:

`example.com`

kan översättas till en IP-adress som datorn sedan använder för kommunikationen.

DNS gör att människor kan använda domännamn istället för att behöva komma ihåg IP-adresser.

---

## Commands I used

`ip -br addr`

Visar nätverksinterface och deras IP-adresser i ett mer kompakt format.

`ip route`

Visar routingtabellen och vilken default gateway datorn använder.

`ping -c 4 1.1.1.1`

Skickar fyra ICMP-förfrågningar till en IP-adress och används för att kontrollera om destinationen svarar.

`ping -c 4 example.com`

Testar både namnuppslagning och om destinationen svarar på ping.

`resolvectl query example.com`

Används för att undersöka DNS och se vilken IP-adress ett domännamn översätts till.

`curl https://example.com`

Gör en HTTP/HTTPS-förfrågan till en webbtjänst.

`curl -I https://example.com`

Hämtar HTTP-headers istället för hela innehållet på webbsidan.

`ss -tuln`

Visar bland annat nätverkstjänster som lyssnar på portar.

---

## Local web server lab

Jag skapade en enkel lokal webbserver med Python.

Jag skapade först en enkel fil:

`echo "Hello from my DevOps web server" > index.html`

Sedan startade jag webbservern med:

`python3 -m http.server --bind 127.0.0.1 8000`

Det startade en Python-process som fungerade som webbserver och lyssnade på port 8000 på localhost.

I en annan terminal testade jag servern med:

`curl http://localhost:8000`

Curl fungerade som client och gjorde en HTTP-förfrågan till webbservern.

Jag använde sedan:

`ss -tuln`

för att kontrollera att port 8000 faktiskt lyssnade.

När jag stoppade webbservern med `Ctrl+C` slutade port 8000 att lyssna och curl kunde inte längre ansluta.

---

## Troubleshooting

Ett viktigt felsökningssätt jag lärde mig är att testa nätverket steg för steg.

Om:

`ping 1.1.1.1`

fungerar men:

`ping example.com`

inte fungerar på grund av namnuppslagning, är DNS ett rimligt område att undersöka.

Om ping fungerar men:

`curl https://example.com`

inte fungerar, kan problemet ligga närmare själva webbtjänsten istället för den grundläggande IP-kommunikationen.

Om:

`curl http://localhost:8000`

inte fungerar, behöver det inte betyda att internet är nere. Det kan istället bero på att ingen lokal server lyssnar på port 8000.

---

## What I learned

Jag har fått en bättre förståelse för hur Linux kommunicerar över nätverk och hur flera delar hänger ihop.

Jag förstår bättre skillnaden mellan IP-adress och port, vad localhost betyder, hur DNS används och hur man kan felsöka nätverksproblem genom att testa olika delar var för sig.

Jag har också testat att starta en lokal webbserver och sett hur en process kan lyssna på en port och ta emot förfrågningar från en client.

---

## Things I found difficult

Det som varit svårast är att skilja på exakt vad olika nätverkskommandon testar.

Till exempel är det viktigt att komma ihåg att `ping` inte bevisar att en webbtjänst fungerar, utan bara att destinationen svarar på ICMP.

Jag behöver också fortsätta använda routing, DNS och portar praktiskt för att de ska kännas helt naturliga.
