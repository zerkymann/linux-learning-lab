# GitHub SSH-konfiguration på Ubuntu

Jag ville kunna pusha mitt lokala Git-repository från Ubuntu till GitHub. Till en början försökte jag använda HTTPS med kommandot `git push -u origin main`, men GitHub accepterar inte längre vanliga kontolösenord för Git-operationer över HTTPS. Därför valde jag att konfigurera SSH-autentisering istället.

Först skapade jag en ny SSH-nyckel med kommandot `ssh-keygen -t ed25519 -C "zerkmann@proton.me"`. När terminalen frågade var nyckeln skulle sparas accepterade jag standardplatsen genom att trycka Enter. Detta skapade två filer i `~/.ssh/`: `id_ed25519`, som är den privata nyckeln, och `id_ed25519.pub`, som är den publika nyckeln. Den privata nyckeln ska aldrig delas eller laddas upp någonstans, medan den publika nyckeln kan användas för att identifiera min dator mot GitHub.

För att se den publika nyckeln använde jag kommandot `cat ~/.ssh/id_ed25519.pub`. Jag kopierade hela raden som började med `ssh-ed25519` och lade sedan in den på GitHub under Settings → SSH and GPG keys → New SSH key. Där sparade jag den som en Authentication Key.

Efter det testade jag anslutningen till GitHub med `ssh -T git@github.com`. Eftersom detta var första gången min Ubuntu-installation anslöt till GitHub via SSH fick jag frågan om jag litade på GitHubs host key. Jag svarade `yes`, vilket gjorde att GitHubs nyckel sparades i `~/.ssh/known_hosts`. Därefter bekräftade GitHub att autentiseringen fungerade.

Mitt Git-repository var från början kopplat till GitHub via HTTPS. Därför ändrade jag remote-adressen till SSH genom att gå till repot med `cd ~/devops-lab` och sedan köra `git remote set-url origin git@github.com:zerkymann/linux-learning-lab.git`. Med `git remote -v` kunde jag kontrollera att både fetch och push nu använde SSH-adressen.

När jag sedan körde `git push -u origin main` blev pushen nekad eftersom GitHub-repot redan innehöll commits som inte fanns lokalt. Felmeddelandet sade att jag behövde hämta remote-versionen först. Istället för att använda `git push --force`, vilket hade kunnat skriva över historiken på GitHub, använde jag `git pull --rebase origin main`. Rebase innebar att mina lokala commits placerades ovanpå de commits som redan fanns på GitHub, vilket gjorde att historiken kunde behållas utan en onödig merge-commit.

Efter att rebase var klar körde jag `git push -u origin main` igen och då lyckades pushen.

Det viktigaste jag lärde mig här är hur SSH-autentisering fungerar. GitHub har min publika nyckel, medan min privata nyckel stannar på min egen Ubuntu-dator. GitHub kan därmed verifiera att det verkligen är min dator som ansluter utan att jag behöver skicka mitt GitHub-lösenord.

Jag lärde mig också vad ett Git-remote är. `origin` är namnet på den remote som pekar på mitt GitHub-repository. I mitt fall pekar den på `git@github.com:zerkymann/linux-learning-lab.git`. `git push` skickar mina lokala commits till GitHub, medan `git pull` hämtar ändringar från GitHub. `git pull --rebase` kan användas när remote-repot innehåller commits som jag inte har lokalt och jag vill lägga mina egna commits ovanpå dessa.

Mitt normala arbetsflöde framöver blir därför ungefär: först går jag till repot med `cd ~/devops-lab`, sedan kontrollerar jag ändringar med `git status`, lägger till de filer jag vill committa med exempelvis `git add notes/week1.md`, skapar en commit med `git commit -m "Update week 1 Linux notes"` och skickar sedan ändringarna till GitHub med `git push`.

Eftersom SSH nu är konfigurerat behöver jag normalt inte skriva in GitHub-användarnamn eller lösenord varje gång jag pushar.
