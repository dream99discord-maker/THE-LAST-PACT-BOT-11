# Bot Discord The Last Pact Guardian

Questa cartella contiene il runtime Discord e i suoi servizi, migrazioni e script. Non include la dashboard React/Vite né il server API Fastify del progetto originale.

## Requisiti

- Node.js 24.17 o successivo
- Un'applicazione e un bot configurati nel Discord Developer Portal
- I permessi Discord richiesti dalle funzioni che si vogliono usare

## Avvio

1. Copia `.env.example` in `.env`.
2. Inserisci `BOT_TOKEN` e `DISCORD_CLIENT_ID`. Non pubblicare il file `.env`.
3. Dal terminale, nella cartella `discord-bot`, esegui:

   ```powershell
   npm install
   npm run dev
   ```

Per eseguire la versione compilata:

```powershell
npm run build
npm start
```

I dati e il database predefiniti vengono creati nella cartella `data`. Le migrazioni SQL vengono eseguite automaticamente all'avvio.

## Comandi Discord

Registra i comandi slash globali dopo aver configurato `BOT_TOKEN` e `DISCORD_CLIENT_ID`:

```powershell
npm run register-commands
```

Per importare la configurazione iniziale per un server:

```powershell
npm run config:import -- ID_SERVER
```

## Arresto

`Ctrl+C`, `SIGTERM` e `SIGBREAK` avviano l'arresto controllato. Nel terminale locale sono disponibili `bot stop` e `app stop`. Il bot smette di accettare nuovi lavori, attende le operazioni attive fino al limite `SHUTDOWN_TIMEOUT_MS`, salva nel database le operazioni incomplete e chiude Discord e SQLite. Al successivo avvio recupera le operazioni registrate.

## Rapporto con il sito

Questa è una copia bot-only del runtime, distinta dal progetto originale. La dashboard e l'API originali continuano a usare il bot avviato dal progetto principale: avviare entrambe le copie con lo stesso token non le collega e può duplicare l'elaborazione degli eventi. Questa cartella usa un database separato per impostazione predefinita. Per mantenere la dashboard collegata, continua ad avviare il progetto principale oppure realizza un collegamento tra processi prima di distribuire il bot separatamente.
