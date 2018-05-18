# ELAB18N7 Collezione di Dischi

Uno istituto di formazione musicale vuole creare una base di dati per la propria collezione di album di dischi. Nella base di dati devono essere presenti informazioni relative agli **artisti**: nome, cognome, data di nascita, nome d'arte. Ogni artista può aver inciso più **album**, ed un album può essere stato inciso da più artisti. Di ogni album si vuole sapere il titolo, l'anno di pubblicazione ed il genere (da scegliere tra: rock, pop, dance, classica, blues, jazz, ...altro). Inoltre è necessario sapere se il supporto dove il disco è memorizzato è un compact disc o un vinile, ovviamente un disco può essere disponibile per entrambi i supporti. Ogni album viene pubblicato da una sola **etichetta**.
Un'etichetta può pubblicare più album. Di ogni etichetta si deve indicare il nome, l'indirizzo e il numero di telefono.
L'istituto organizza su richiesta, sedute di audizione di un album da parte degli interessati (**docenti** o **studenti**) individuati da una matricola Nome, Cognome e Indirizzo. Nel caso degli studenti si riporta anche il corso a cui sono iscritti e l'anno di iscrizione; nel caso dei docenti si riporta l'area disciplinare di insegnamento e la email interna. Per ogni **audizione** si conserva un numero progressivo di identificazione, data ed ora dell'audizione. Ad ogni audizione, un docente o uno studente possono compilare un giudizio, di cui si riportano un commento generale (1000 caratteri), il livello di gradimento (alto, normale, basso).

## Entità 

### Artista

> informazioni relative agli **artisti**: nome, cognome, data di nascita, nome d'arte

L'entità `Artista` è composta da quattro attributi. Il `nome` e il `cognome` dell'artista, la `data di nascita` e il `nome d'arte`. Il nome d'arte viene usato come identificatori, quindi deve essere unico. Tutti e quattro i campi sono obbligatori.

### Album 

> Di ogni **album** si vuole sapere il titolo, l'anno di pubblicazione ed il genere...Inoltre è necessario sapere se il supporto dove il disco è memorizzato

L'entità `Album` è composta da quattro attributi. Il `titolo` dell'album, l'`anno` in cui è stato pubblicato e il `genere`. Quest'ultimo attributo può assumere uno dei seguenti valori: rock, pop, dance, classica, bluse, jazz, indie. Inoltre è presente anche l'attributo `supporto` che indica il supporto su cui è memorizzato l'album. Quest'attributo può assumere o il valore di vinile o di CD. Visto che un album può essere stato memorizzato su entrambi i supporti l'attributo supporto è multivalore.
Il titolo e l'anno di pubblicazione vengono usati come identificatori, quindi si possono avere due album con lo stesso titolo, ma pubblicati in anni diversi.
Tutti i campi sono obbligatori.

### Etichetta

> Di ogni **etichetta** si deve indicare il nome, l'indirizzo e il numero di telefono

L'entità `Etichetta` è composta da tre attributi. Il `nome` commerciale dell'etichetta, l'`indirizzo` della sede e il numero di `telefono`. Il nome dell'etichetta viene usato come identificatore, quindi deve essere unico.
Tutti i campi sono obbligatori.

### Docente e studente

> (**docenti** o **studenti**) individuati da una matricola Nome, Cognome e Indirizzo. Nel caso degli studenti si riporta anche il corso a cui sono iscritti e l'anno di iscrizione; nel caso dei docenti si riporta l'area disciplinare di insegnamento e la email interna.

Le entità `Docente` e `Studente` sono entrambe individuate dal `nome`, dal `cognome` e dall'`indirizzo` e dalla `matricola`. Quest'ultima vine usata come identificatore.
Nel caso di un studente vengono aggiunti anche gli attributi `anno di iscrizione` e il `corso` a cui sono iscritti.
Nel caso di un docente vengono aggiunti anche gli attributi `area disciplinare` e `email` per l'email interna all'istituto.
Per rappresentate queste due entità si è scelto di utilizzare una generalizzazione totale ed esclusiva, in quanto nel dominio del problema non esistono altri interessati oltre ai docenti e agli studenti e uno studente non può essere anche un docente o viceversa.
Tutti i campi sono obbligatori.

### Audizione

> Per ogni **audizione** si conserva un numero progressivo di identificazione, data ed ora dell'audizione

L'entità audizione è composta da tre attributi: l'`ID` che identifica univocamente l'audizione, quindi verrà usato come identificatore, la `data` e l'`ora` in cui è avvenuta l'audizione.
Tutti i campi sono obbligatori.

## Associazioni

### Incisione

> Ogni artista può aver inciso più album, ed un album può essere stato inciso da più artisti

L'entità `Album` e l'entità `Artista` sono legati dall'associazione `Incisione`. 
Un artista può aver inciso più album, come può non averne inciso nessuno per cui ha una molteplicità $(0,n)$.
Un album può essere stato inciso da più artisti, ma deve essere stato inciso da almeno un artista per cui ha molteplicità $(1,n)$.
Quest'associazione non ha attributi propri.

### Pubblicazione

> Ogni album viene pubblicato da una sola etichetta

L'entità `Album` e l'entità `Etichetta` sono legati dall'associazione `Publicazione`.
Un album deve essere pubblicato da una sola etichetta per cui ha molteplicità $(1,1)$.
Un etichetta può pubblicare più album, cosicché può non averne pubblicati per cui ha molteplicità $(0,n)$.
Quest'associazione non ha attributi propri.

### Partecipazione

Le entità `Docenete` e `Studnete` e l'entità `Audizione` sono legati dall'associazione `Partecipazione`.
Ad una audizione deve partecipare almeno un studente/docente per cui ha molteplicità $(1,n)$.
Uno studente può naturalmente partecipare a più audizioni, così come non partecipare a nessuna audizione, per cui ha molteplicità $(0,n)$.
Quest'associazione ha due attributi: `commento`, un giudizio sull'audizione compreso in 1000 caratteri e `gradimento` un giudizio sintetico che può assumere i valori di basso, normale e alto.

### Ascolto

> L'istituto organizza su richiesta, sedute di audizione di un album

L'entità `Album` e l'entità `Audizione` sono legati dall'associazione `Ascolto`.
Durante un audizione può essere ascoltato uno e un solo album, per cui ha molteplicità $(1,1)$.
Un album può essere ascoltato durante più audizioni o durante nessuna di esse per cui ha relazione $(0,n)$.
Quest'associazione non ha attributi propri.

## Tabella delle entità

### Artista

| Nome attributo  | Descrizione                                                | Tipo    | ID   |
| --------------- | ---------------------------------------------------------  | ------- | :--: |
| nome d'arte     | Il nome con cui l'artista è conosciuto dal grande pubblico | stringa | si   |
| nome            | Il nome dell'artista                                       | stringa | no   |
| cognome         | Il cognome dell'artista                                    | stringa | no   |
| data di nascita | Giorno, mese e anno in cui è nato l'artista                | data    | no   |

### Album

| Nome attributo  | Descrizione                                               | Tipo        | ID   |
| --------------- | --------------------------------------------------------- | -------     | ---- |
| titolo          | Il nome che è stato assegnato all'album                   | stringa     | si   |
| anno            | L'anno in cui è stato pubblicato l'album                  | intero      | si   |
| genere          | Il genere di appartenenza delle tracce dell'album         | enumerabile | no   |
| supporto        | Il supporto fisico su cui è stato inciso l'album          | enumerabile | no   |

### Etichetta

| Nome attributo  | Descrizione                                                                                               | Tipo     | ID   |
| --------------- | ---------------------------------------------------------                                                 | -------  | ---- |
| nome            | Nome commerciale con sui è conosciuta l'etichetta                                                         | stringa  | si   |
| indirizzo       | L'indirizzo della sede dell'etichetta. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap  | composto | no   |
| telefono        | Il numero, o i numeri di telefono appartenenti all'etichetta. L'etichetta deve possedere almeno un numero | intero   | no   |

### Docente

| Nome attributo    | Descrizione                                                  | Tipo     | ID   |
| ----------------- | ------------------------------------------------------------ | -------- | ---- |
| matricola         | Codice identificativo all'interno dell'organizzazione        | intero   | si   |
| nome              | Nome del                                                     | stringa  | no   |
| cognome           | Cognome del                                                  | stringa  | no   |
| indirizzo         | L'indirizzo di residenza del. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto | no   |
| area disciplinare | L'area di insegnamento del docente                           | stringa  | no   |
| email             | L'email interna all'istituto                                 | stringa  | no   |

### Studente

| Nome attributo     | Descrizione                                                  | Tipo     | ID   |
| ------------------ | ------------------------------------------------------------ | -------- | ---- |
| matricola          | Codice identificativo all'interno dell'organizzazione        | intero   | si   |
| nome               | Nome del                                                     | stringa  | no   |
| cognome            | Cognome del                                                  | stringa  | no   |
| indirizzo          | L'indirizzo di residenza del. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto | no   |
| anno di iscrizione | L'anno in cui lo studente si è iscritto                      | intero   | no   |
| corso              | Il corso a cui lo studente è iscitto                         | stringa  | no   |

### Audizione

| Nome attributo  | Descrizione                                               | Tipo    | ID   |
| --------------- | --------------------------------------------------------- | ------- | ---- |
| ID              | Codice identificativo dell'audizione                      | intero  | si   |
| data            | Giorno, mese, anno in cui si svolge l'audizione           | data    | no   |
| ora             | Ora in cui si svolge l'audizione                          | ora     | no   |

## Tabelle delle associazioni

### Incisione

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
|     Artista      |           0,n           |
|      Album       |           1,n           |

### Pubblicazione

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
| Album            | 1,1                     |
| Etichetta        | 0,n                     |

### Partecipazione

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
| docente/studente |           0,n           |
|    Audizione     |           1,n           |

| Nome attributo  | Descrizione                                               | Tipo        | ID   |
| --------------- | --------------------------------------------------------- | -------     | ---- |
| commento        | Giudizio esteso sull'audizione                            | stringa     | no   |
| gradimento      | Giudizio sintetico sull'audizione                         | enumerabile | no   |

### Ascolto

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
| audizione        | 1,1                     |
| Album            | 0,n                     |

## Vincoli e derivazioni

| Nome regola     | Descrizione regola                                                                                   |
| --------------- | ---------------------------------------------------------                                            |
| RV1             | `Artista.nome d'arte` deve essere unico.                                                             |
| RV2             | `Album.genere` può assumere uno dei seguenti valori: rock, pop, dance, classica, blues, jazz, indie. |
| RV3             | `Album.supporto` può assumere o il valore vinile o il valore CD.                                     |
| RV4             | la combinazione `Album.anno` e `Album.titolo` deve essere unica                                      |
| RV5             | `Etichetta.nome` deve essere unico.                                                                  |
| RV6             | `Persona.matricola` deve essere unica.                                                               |
| RV7             | `Audizione.ID` deve essere unico.                                                                    |
| RV8             | `Partecipazione.gradimento` può assumere uno dei seguenti valori: basso, normale, alto.              |
| RV9             | `Partecipazione.commento` può essere al massimo lungo 1000 caratteri.                                |
