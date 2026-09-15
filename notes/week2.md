# Week 2 - Linux users, permissions, processes and services

## Users and groups

Förklara:
- vad en user är

En user är en användare på ett Linux system, för att se en själv kan man använda whoami

- vad en group är

En group är en grupp av användare, t. ex. "utvecklare", eller "admins". Det är egentligen bara en beteckning för en grupp användare.

- vad whoami, id och groups gör

whoami visar den nuvarande användarens namn
id visar den nuvarande användarens ID (UID), grupper hen tillbehör och primärt grupp-ID
groups visar vilka grupper användaren tillhör

## Permissions

Förklara:
- r = read
read betyder att en användare kan läsa en fil, men inget annat.
- w = write
write betyder att användaren kan ändra i filen, t. ex. vid en textfil
- x = execute
execute betyder att användaren kan köra filen
- owner / group / others
owner = ägaren/skaparen av filen, group = vilken grupp som filen tillhör, others = användare

Exempel:
-rwxr-xr--

Texten ovan betyder att det är en vanlig fil (-) där owner kan läsa, skriva och köra, group kan läsa, köra  och saknar sedan behörighet, och others kan endast läsa, sedan saknas behörigheter.
För att bryta ned detta:

- | rwx | r-x | r--
    owner group others

## chmod

Förklara vad:
chmod +x
chmod -x

chmod +x lägger till behörigheten "kör" för en fil
chmod -x tar bort behörigheten "kör" för en fil

## Processes

Förklara skillnaden mellan:
- program = program är en kod/fil som ligger läsbart i ett system
- process = process är ett program som aktivt körs, t. ex. något som Google Chrome
- PID = process ID, vilket nummer processen har i det aktiva systemet

Kommandon jag testade:
- ps
- ps aux
- pgrep
- kill
- top / htop

## Pipes

Förklara med egna ord vad:

ps aux | grep sleep

gör.

först låter ps aux skapa en lista över processer, sedan skickar | den texten vidare till grep sleep, som filtrerar fram rader som innehåller sleep.

## Services and systemd

Förklara:
- vad en service är
- vad systemd är
- vad systemctl används till

Service är en tjänst som körs av systemet, t. ex. nätverkshantering/nätverkstjänster.
systemd är tjänsthanteraren i systemet
systemctl används för att kunna prata med systemd som en användare

Skillnaden mellan:
- start = starta en service
- stop = stanna en service
- restart = starta om en service
- enable = konfigurera autostart för framtida boot av en tjänst

## What I learned

Upplägget i Linux för hur tjänster och processer existerar och hanteras av en användare har blivit mycket tydligare.

## Things I found difficult

Pipe-kommandon är fortfarande lite klurigt, men kommer sätta sig mer med framtida labb.
