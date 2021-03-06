# 4BBot [BETA]

4BBot is a Discord Bot that was created for serving the 4BHIF Discord Server. Here it is open-sourced. Feel free to PR Features or create issues, I will see them.

4BBot was created based off of 3BBot. Its code can be downloaded from [this release](https://github.com/lucas-walter/4BBot/releases/tag/3bbot-final).

## Running the Bot
To run the bot you will need the following:
- A Discord Server
- A Discord Bot Token, you can get this from https://discordapp.com/developers/applications/ -> Application -> Bot -> Token
- A Sentry.io Project and its DSN, see https://docs.sentry.io/error-reporting/quickstart/?platform=node
- (Kind of required, unless you want to comment out parts of the code) A MySQL Database and a user for it.

Rename `config.example.js` to `config.js` and set the values inside it.
You can run `database-init-script.sql` to create the Database along with its required Tables.

Your Discord Server needs the following:

- A channel called `termine`
- A channel called `hü`
- A channel called `termin-archiv`
- A channel called `hü-archiv`
- A channel called `logs`

Then you should be ready to go, just start the bot using `node 3bbot.js`!

There **are** some hardcoded values in the Bot at the moment, mainly User IDs (Namely mine with the !exec command because [you shouldn't trust anyone with that](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval#Do_not_ever_use_eval!)). Everything should™ work without changing that though.

I also would recommend running the Bot with [PM2](http://pm2.keymetrics.io/), which is what I currently use in Production and what this Bot is almost solely tested on. This Bot hardly writes anything into the console, except if it dies from a Syntax Error or anything that happens before initializing Sentry.

## Bot Features [DE]

### !HÜ

Hausaufgaben werden im #hü Channel als Embed angezeigt und in der `aufgaben` Datenbank gespeichert. Später werden diese auch über einen Command oder Notifications abrufbar sein.

Der Command lautet:
```
!hü #englishy Buch : 52 1-2, 55, 56, 57 bis Montag
       Fach   Titel:        Details     bis Text oder "3d" für 3 Tage
```

![Anzeige im HÜ Channel](https://i.imgur.com/0CZLV4E.png)

### !TERMIN

Generell dasselbe wie !hü, nur werden Termine in #termine angezeigt und in der `termine` Datenbank gespeichert.

Der Command lautet:
```
!termin #deutsch Schularbeit : Leserbrief am 20.2.2019
           Fach     Titel    :   Details  am Datum
```

### ANWESEND

Retourniert ein zufälliges Synonym für "anwesend" aus einer vorgefertigten Liste von 76 Synonymen. Ich übernehme keine Haftung für humorlose Lehrer, die den Witz nicht kapieren oder falsch eingetragene Fehlstunden.

### !EXEC

Exec lässt den Botowner JavaScript über Discord ausführen, unter anderem `!exec process.exit()`, um den Bot zu beenden (oder mittels PM2 neu zu starten).

### AUTOMOD

Der Bot erkennt Commands für Dank Memer und löscht diese. Dies erscheint in #logs als DEL_COMMANDS.
Auch postet er (meistens) gelöschte Termine im #termin-archiv.
