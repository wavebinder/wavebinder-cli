# Wave Binder CLI

CLI tool per supportare lo sviluppo di **Wave Binder**, pensato per semplificare la creazione e la manutenzione del file di input JSON. L’obiettivo è ridurre al minimo gli errori manuali e rendere più rapido l’editing di strutture JSON anche complesse.

Il tool fornisce comandi guidati per aggiungere e modificare nodi, con validazioni di base e supporto interattivo quando necessario.

---

## Caratteristiche principali

* CLI dedicata alla gestione dell’input JSON di Wave Binder
* Aggiunta di nuovi nodi con tipologia esplicita (MULTI, COMPLEX, LIST, SIMPLE)
* Modifica dei nodi esistenti
* Selezione interattiva del file JSON se non specificato
* Output chiaro e feedback immediato sulle operazioni

---

## Prerequisiti

* **Node.js** >= 18 consigliato
* **npm**

Il pacchetto **non è pubblicato su npm registry**: l’installazione avviene tramite file `.tgz`.

---

## Installazione

Dato un pacchetto locale `wave-binder-cli-<version>.tgz`:

```bash
npm install ./wave-binder-cli-0.0.1.tgz
```

Questo renderà il binario disponibile per l’uso tramite `npx`.

> In alternativa, durante lo sviluppo locale, è possibile usare `npm link`, ma **non è il flusso consigliato** per l’utilizzo standard.

---

## Utilizzo

Il comando principale è `wbcli`.

In genere viene lanciato così:

```bash
npx wbcli <command> [options]
```

Se il file JSON di destinazione non viene specificato, la CLI chiederà interattivamente su quale file lavorare.

---

## Comandi disponibili

### `add`

Aggiunge un nuovo nodo al file JSON.

```bash
npx wbcli add <nodeName> <nodeType> [options]
```

**Argomenti**

* `nodeName` – nome del nodo da creare
* `nodeType` – tipo del nodo (`MULTI`, `COMPLEX`, `LIST`, `SIMPLE`)

**Opzioni**

* `-f, --father <node>`
  Specifica il nodo padre sotto cui inserire il nuovo nodo

* `-j, --json <file>`
  Percorso del file JSON di destinazione

**Esempio**

```bash
npx wbcli add tracks LIST -f root -j input.json
```

---

### `edit`

Modifica un nodo esistente nel file JSON.

```bash
npx wbcli edit <nodeName> [options]
```

**Argomenti**

* `nodeName` – nome del nodo da modificare

**Opzioni**

* `-t, --type <nodeType>`
  Imposta un nuovo tipo per il nodo

* `-j, --json <file>`
  Percorso del file JSON di destinazione

**Esempio**

```bash
npx wbcli edit tracks --type MULTI -j input.json
```

---

## Comportamento del tool

* Se il file JSON non viene passato tramite `--json`, il tool avvia una selezione interattiva
* Le modifiche vengono **salvate direttamente sul file**
* Al termine di ogni operazione viene stampato un riepilogo dell’esito

---

## Stato del progetto

Il progetto è in **fase iniziale** e pensato per uso interno o controllato. L’API della CLI e il formato dei nodi potrebbero evolvere.

---

## Licenza

Tutti i diritti riservati ai proprietari di Wave Binder.

---

## Note di sviluppo

* Basato su `commander` per il parsing dei comandi
* Prompt interattivi realizzati con `inquirer`
* Output colorato tramite `chalk`
