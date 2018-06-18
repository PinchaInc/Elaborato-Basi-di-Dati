# ELAB18N7 Collezione di Dischi

Uno istituto di formazione musicale vuole creare una base di dati per la propria collezione di album di dischi. Nella base di dati devono essere presenti informazioni relative agli <font color="red">artisti</font>: <font color="green">nome, cognome, data di nascita, nome d'arte. </font><font color="blue">Ogni artista può aver inciso più album, ed un album può essere stato inciso da più artisti</font>. Di ogni <font color="red">album</font> si vuole sapere il <font color="green">titolo, l'anno di pubblicazione ed il genere</font> (da scegliere tra: rock, pop, dance, classica, blues, jazz, ...altro). Inoltre è necessario sapere se <font color="green">il supporto</font> dove il disco è memorizzato è un compact disc o un vinile, ovviamente un disco può essere disponibile per entrambi i supporti. <font color="blue">Ogni album viene pubblicato da una sola etichetta</font>.
<font color="red">Un'etichetta</font> può pubblicare più album. Di ogni etichetta si deve indicare il <font color="green">nome, l'indirizzo e il numero di telefono</font>.
<font color="blue">L'istituto organizza su richiesta, sedute di audizione di un album</font> da parte degli <font color="red">interessati</font> (<font color="red">docenti</font> o <font color="red">studenti</font>) individuati da una <font color="green">matricola Nome, Cognome e Indirizzo</font>. Nel caso degli studenti si riporta anche il <font color="green">corso a cui sono iscritti e l'anno di iscrizione</font>; nel caso dei docenti si riporta <font color="green">l'area disciplinare di insegnamento e la email interna</font>. Per ogni <font color="red">audizione</font> si conserva un <font color="green">numero progressivo di identificazione, data ed ora dell'audizione</font>. <font color="blue">Ad ogni audizione, un docente o uno studente possono compilare un giudizio, di cui si riportano un</font> <font color="green">commento generale</font> (1000 caratteri), <font color="green">il livello di gradimento</font> (alto, normale, basso).

**Legenda**

- <font color="red">Entità</font>
- <font color="blue">Associazioni</font>
- <font color="green">Attributi</font>

---
## Progettazione concettuale

### Identificazione delle entità e delle associazioni

#### Entità 

##### Artista

> informazioni relative agli artisti: nome, cognome, data di nascita, nome d'arte

L'entità `Artista` è composta da quattro attributi. Il `nome` e il `cognome` dell'artista, la `data di nascita` e il `nome d'arte`. Il nome d'arte viene usato come identificatore, quindi deve essere unico. Per il `nome` e il `cognome` sono stati preposti 20 caratteri, mentre per il `nome d'arte` ne sono stati destinati 30.
Tutti e quattro i campi sono obbligatori.

![artista][]

| Nome attributo  | Descrizione                                                | Tipo                                    |  ID  |
| --------------- | ---------------------------------------------------------- | --------------------------------------- | :--: |
| nome d'arte     | Il nome con cui l'artista è conosciuto dal grande pubblico | stringa<br />variabile<br />max 30 char |  si  |
| nome            | Il nome dell'artista                                       | stringa<br />variabile<br />max 20 char |  no  |
| cognome         | Il cognome dell'artista                                    | stringa<br />variabile<br />max 20 char |  no  |
| data di nascita | Giorno, mese e anno in cui è nato l'artista                | data                                    |  no  |

---

##### Album 

> Di ogni album si vuole sapere il titolo, l'anno di pubblicazione ed il genere...Inoltre è necessario sapere il supporto dove il disco è memorizzato

L'entità `Album` è composta da quattro attributi. Il `titolo` dell'album, l'`anno` in cui è stato pubblicato e il `genere`. Quest'ultimo attributo può assumere uno dei seguenti valori: rock, pop, dance, classica, blues, jazz, indie. Inoltre è presente anche l'attributo `supporto` che indica il supporto su cui è memorizzato l'album. Quest'attributo può assumere o il valore di vinile o di CD. Visto che un album può essere stato memorizzato su entrambi i supporti l'attributo potrà assumere anche il valore entrambi.
Il titolo e l'anno di pubblicazione vengono usati come identificatori, quindi si possono avere due album con lo stesso titolo, ma pubblicati in anni diversi.
Per il valore dell'attributo `titolo` sono stati garantiti 30 caratteri.
Tutti i campi sono obbligatori.

![album][]

| Nome attributo | Descrizione                                       | Tipo                                    | ID   |
| -------------- | ------------------------------------------------- | --------------------------------------- | ---- |
| titolo         | Il nome che è stato assegnato all'album           | stringa<br />variabile<br />max 30 char | si   |
| anno           | L'anno in cui è stato pubblicato l'album          | intero                                  | si   |
| genere         | Il genere di appartenenza delle tracce dell'album | enumerabile                             | no   |
| supporto       | Il supporto fisico su cui è stato inciso l'album  | enumerabile                             | no   |

---

##### Etichetta

> Di ogni etichetta si deve indicare il nome, l'indirizzo e il numero di telefono

L'entità `Etichetta` è composta da tre attributi. Il `nome` commerciale dell'etichetta, il numero di `telefono` e l'`indirizzo` della sede. Quest'ultimo viene ulteriormente scomposto in `via`, `numero civico` e `cap`. 
Il nome dell'etichetta viene usato come identificatore, quindi deve essere unico. Inoltre per il campo `nome` sono stati riservati 25 caratteri.
Visto che nel mondo reale non possono esistere due numeri di telefono uguali, allo stesso modo l'attributo `telefono` deve essere univoco.
Tutti i campi sono obbligatori.

![etichetta][]

| Nome attributo | Descrizione                                                  | Tipo                                    | ID   |
| -------------- | ------------------------------------------------------------ | --------------------------------------- | ---- |
| nome           | Nome commerciale con sui è conosciuta l'etichetta            | stringa<br />variabile<br />max 25 char | si   |
| indirizzo      | L'indirizzo della sede dell'etichetta. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto                                | no   |
| telefono       | Il numero, o i numeri di telefono appartenenti all'etichetta. L'etichetta deve possedere almeno un numero | intero                                  | no   |

---

##### Studente

> gli interessati(docenti o studenti) individuati da una matricola Nome, Cognome e Indirizzo. Nel caso degli studenti si riporta anche il corso a cui sono iscritti e l'anno di iscrizione; nel caso dei docenti si riporta l'area disciplinare di insegnamento e la email interna.

L'entità `Studente` è composta dagli attributi `nome`, `cognome`, `matricola`, `indirizzo`, `anno di iscrizione` e `corso`.
Per gli attributi `nome` e `cognome` sono stati destinati 20 caratteri.
L'attributo `matricola ` è un intero che viene utilizzato anche come identificatore.
L'attributo `indirizzo` è invece un attributo composto, formato a sua volta dagli attributi `via`, `numero civico` e `cap`.
L'attributo `anno di iscrizione` è un intero, mentre per l'attributo `corso` sono stati preposti 30 caratteri.
Tutti gli attributi sono obbligatori. 

###### Studente

| Nome attributo     | Descrizione                                                  | Tipo                                    | ID   |
| ------------------ | ------------------------------------------------------------ | --------------------------------------- | ---- |
| matricola          | Codice identificativo all'interno dell'organizzazione        | intero                                  | si   |
| nome               | Nome del                                                     | stringa<br />variabile<br />max 20 char | no   |
| cognome            | Cognome del                                                  | stringa<br />variabile<br />max 20 char | no   |
| indirizzo          | L'indirizzo di residenza del. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto                                | no   |
| anno di iscrizione | L'anno in cui lo studente si è iscritto                      | intero                                  | no   |
| corso              | Il corso a cui lo studente è iscitto                         | stringa<br />variabile<br />max 30 char | no   |

##### Docente

> gli interessati(docenti o studenti) individuati da una matricola Nome, Cognome e Indirizzo. Nel caso degli studenti si riporta anche il corso a cui sono iscritti e l'anno di iscrizione; nel caso dei docenti si riporta l'area disciplinare di insegnamento e la email interna.

L'entità `Docente` è composta dagli attributi `nome`, `cognome`, `matricola`, `indirizzo`, `area disciplinare` e `email`.
Per gli attributi `nome` e `cognome` sono stati preposti 20 caratteri.
L'attributo `matricola` è un intero, utilizzato anche come identificatore.
L'attributo `indirizzo` è un attributo composto, formato dagli attributi `via`, `numero civico` e `cap`.
Per l'attributo `area disciplinare` si hanno a disposizione 30 caratteri, mentre all'attributo `email` sono stati destinati 20 caratteri.
Tutti gli attributi sono obbligatori.

###### Docente

| Nome attributo    | Descrizione                                                  | Tipo                                    | ID   |
| ----------------- | ------------------------------------------------------------ | --------------------------------------- | ---- |
| matricola         | Codice identificativo all'interno dell'organizzazione        | intero                                  | si   |
| nome              | Nome del                                                     | stringa<br />variabile<br />max 20 char | no   |
| cognome           | Cognome del                                                  | stringa<br />variabile<br />max 20 char | no   |
| indirizzo         | L'indirizzo di residenza del. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto                                | no   |
| area disciplinare | L'area di insegnamento del docente                           | stringa<br />variabile<br />max 30 char | no   |
| email             | L'email interna all'istituto                                 | stringa<br />variabile<br />max 50 char | no   |

---

##### Universitario

> gli interessati(docenti o studenti) individuati da una matricola Nome, Cognome e Indirizzo. Nel caso degli studenti si riporta anche il corso a cui sono iscritti e l'anno di iscrizione; nel caso dei docenti si riporta l'area disciplinare di insegnamento e la email interna.

Dato che le entità `Studente` e `Docente` hanno diversi attributi in comune, possono essere generalizzate in una singola entità, definita come `Universitario`.
In base al dominio applicativo possiamo asserire che si tratti di una generalizzazione totale ed esclusiva, in quanto nel dominio del problema non esistono altri interessati oltre ai docenti e agli studenti e uno studente non può essere anche un docente o viceversa.
L'entità `Universitario` è composta dal `nome`, dal `cognome`, dall'`indirizzo` e dalla `matricola`, ovvero dagli attributi in comune tra `Studente` e `Docente`. 
Per gli attributi `nome` e `cognome` sono stati preposti 20 caratteri. 
L'attributo `matricola` è un intero che viene utilizzato anche come identificatore.
L'attributo `indirizzo` è un attributo composto dagli attributi `via`, `numero civico` e `cap`.
L'entità `Universitario` viene quindi specializzata in due sotto-entità: il `Docente` e lo `Studente`. Queste entità saranno formate soltanto dai propri attributi specifici.
Nel caso di uno studente, infatti,  vengono aggiunti gli attributi `anno di iscrizione` e il `corso` a cui sono iscritti. Per quest'ultimo attributo sono stati preposti 30 caratteri.
Nel caso di un docente vengono invece aggiunti gli attributi `area disciplinare` e `email` per l'email interna all'istituto. Per questi due attributi sono stati preposti rispettivamente 30 e 50 caratteri.
Tutti i campi sono obbligatori.

![universitario][]

---

###### Universitario

| Nome attributo    | Descrizione                                                  | Tipo                                    | ID   |
| ----------------- | ------------------------------------------------------------ | --------------------------------------- | ---- |
| matricola         | Codice identificativo all'interno dell'organizzazione        | intero                                  | si   |
| nome              | Nome del                                                     | stringa<br />variabile<br />max 20 char | no   |
| cognome           | Cognome del                                                  | stringa<br />variabile<br />max 20 char | no   |
| indirizzo         | L'indirizzo di residenza del. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto                                | no   |

###### Studente

| Nome attributo     | Descrizione                             | Tipo                                    | ID   |
| ------------------ | --------------------------------------- | --------------------------------------- | ---- |
| anno di iscrizione | L'anno in cui lo studente si è iscritto | intero                                  | no   |
| corso              | Il corso a cui lo studente è iscitto    | stringa<br />variabile<br />max 30 char | no   |

 ###### Docente

| Nome attributo    | Descrizione                        | Tipo                                    | ID   |
| ----------------- | ---------------------------------- | --------------------------------------- | ---- |
| area disciplinare | L'area di insegnamento del docente | stringa<br />variabile<br />max 30 char | no   |
| email             | L'email interna all'istituto       | stringa<br />variabile<br />max 50 char | no   |



##### Audizione

> Per ogni audizione si conserva un numero progressivo di identificazione, data ed ora dell'audizione

L'entità audizione è composta da tre attributi: l'`ID` che identifica univocamente l'audizione, quindi verrà usato come identificatore, la `data` e l'`ora` in cui è avvenuta l'audizione.
Tutti i campi sono obbligatori.

![audizione][]

| Nome attributo  | Descrizione                                               | Tipo    | ID   |
| --------------- | --------------------------------------------------------- | ------- | ---- |
| ID              | Codice identificativo dell'audizione                      | intero  | si   |
| data            | Giorno, mese, anno in cui si svolge l'audizione           | data    | no   |
| ora             | Ora in cui si svolge l'audizione                          | ora     | no   |

---

#### Associazioni

##### Incisione

> Ogni artista può aver inciso più album, ed un album può essere stato inciso da più artisti

L'entità `Album` e l'entità `Artista` sono legati dall'associazione `Incisione`. 
Un artista può aver inciso più album, come può non averne inciso nessuno per cui ha una molteplicità $(0,n)$.
Un album può essere stato inciso da più artisti, ma deve essere stato inciso da almeno un artista per cui ha molteplicità $(1,n)$.
Quest'associazione non ha attributi propri.

![incisione][]

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
|     Artista      |           0,n           |
|      Album       |           1,n           |

---

##### Pubblicazione

> Ogni album viene pubblicato da una sola etichetta

L'entità `Album` e l'entità `Etichetta` sono legati dall'associazione `Pubblicazione`.
Un album deve essere pubblicato da una sola etichetta per cui ha molteplicità $(1,1)$.
Un etichetta può pubblicare più album, cosicché può non averne pubblicati per cui ha molteplicità $(0,n)$.
Quest'associazione non ha attributi propri.

![pubblicazione][]

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
| Album            | 1,1                     |
| Etichetta        | 0,n                     |

---


##### Richiesta

> L'istituto organizza su richiesta, sedute di audizione di un album

L'entità `Universitario` e l'entità `Audizione` sono legati dall'associazione `Richiesta`.
Un universitario può richiedere più audizioni, così come può non richiederne alcuna; per questo ha molteplicità $(0,n)$.
Un'audizione può essere richiesta da più universitari, ma deve essere richiesta da almeno uno; per questo ha molteplicità $(1,n)$.
Quest'associazione non ha attributi propri.

![richiesta][]

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
|  Universitario   |           0,n           |
|    Audizione     |           1,n           |

---

##### Ascolto

> L'istituto organizza su richiesta, sedute di audizione di un album

L'entità `Album` e l'entità `Audizione` sono legati dall'associazione `Ascolto`.
Durante un audizione può essere ascoltato uno e un solo album, per cui ha molteplicità $(1,1)$.
Un album può essere ascoltato durante più audizioni o durante nessuna di esse per cui ha relazione $(0,n)$.
Quest'associazione non ha attributi propri.

![ascolto][]

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
|    Audizione     |           1,1           |
|      Album       |           0,n           |

---

##### Partecipazione

> Ad ogni audizione, un docente o uno studente possono compilare un giudizio, di cui si riportano un commento generale, il livello di gradimento.

L'entità `Universitario` e l'entità `Audizione` sono legati dall'associazione `Partecipazione`.
Ad una audizione deve partecipare almeno un universitario per cui ha molteplicità $(1,n)$.
Un universitario può naturalmente partecipare a più audizioni, così come non partecipare a nessuna audizione, per cui ha molteplicità $(0,n)$.
Quest'associazione ha due attributi: `commento`, un giudizio sull'audizione compreso in 1000 caratteri e `gradimento` un giudizio sintetico che può assumere i valori di basso, normale e alto.
Un universitario può anche decidere di non lasciar alcun commento o gradimento; per questo, la cardinalità di questi attributi è $(0,1)$ 

![partecipazione][]


| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
| docente/studente |           0,n           |
|    Audizione     |           1,n           |

| Nome attributo |            Descrizione            |                   Tipo                    |  ID  | Rapporto di cardinalità |
| :------------: | :-------------------------------: | :---------------------------------------: | :--: | :---------------------: |
|    commento    |  Giudizio esteso sull'audizione   | stringa<br />variabile<br />max 1000 char |  no  |           0,1           |
|   gradimento   | Giudizio sintetico sull'audizione |                enumerabile                |  no  |           0,1           |

---


### Vincoli e derivazioni

| Nome regola | Descrizione regola                                           |
| ----------- | ------------------------------------------------------------ |
| RV1         | `Artista.nome d'arte` deve essere unico.                     |
| RV2         | `Album.genere` può assumere uno dei seguenti valori: rock, pop, dance, classica, blues, jazz, indie. |
| RV3         | `Album.supporto` può assumere il valore vinile, il valore CD o entrambi. |
| RV4         | la combinazione `Album.anno` e `Album.titolo` deve essere unica |
| RV5         | `Etichetta.nome` deve essere unico.                          |
| RV6         | `Universitario.matricola` deve essere unica.                 |
| RV7         | `Audizione.ID` deve essere unico.                            |
| RV8         | `Partecipazione.gradimento` può assumere uno dei seguenti valori: basso, normale, alto. |
| RV9         | `Etichetta.telefono` deve essere unico                       |

### Modello E-R

![er][]

---

## Progettazione logica

### Trasformazioni preliminari

#### Trasformazioni di attributi composti in attributi semplici

L'entità `Etichetta` e l'entità `Unversitario` presentano tra i loro attributi l'attributo complesso `indirizzo` per poter passare dalla progettazione concettuale a quella logica dobbiamo eliminare questo attributo composto; per fare ciò si è scelto di sciogliere l'attributo complesso in più attributi semplici.
Per cui l'entità `Etichetta` sarà così trasformata:

![etichetta-bis][]

Allo stesso modo l'entità `Universitario` diventa:

![universitario-bis][]

#### Trasformazione della generalizzazione

Durante la progettazione concettuale le entità `Studente` e `Docente` sono state generalizzate nell'entità `Universitario`, ma per poter passare alla progettazione logica incontriamo la necessita di eliminare la generalizzazione.
Visto che ci troviamo difronte ad una generalizzazione totale ed esclusiva possiamo scegliere tra tre opzioni; trasformare la generalizzazione in un'associazione, far assorbire il padre nei figli e assorbire i figli nel padre. In questo caso abbiamo scelto di seguire quest'ultima opzione.
I due figli(studente e docente) vengono eliminati, e i loro attributi aggiunti a quelli dell'entità padre. Questi nuovi attributi possono assumere il valore $NULL$. Inoltre all'entità `Universitario` viene aggiunto anche l'attributo `tipo`. Trovandoci in una generalizzazione totale ed esclusiva l'attributo `tipo` può assumere solo il valore docente o studente, ma non entrambi.

![universitario-tris][]

---

### Traduzione di entità

#### Artista

L'entità `Artista` presenta un identificatore interno per cui viene tradotta in una relazione avete lo stesso nome, ma al plurale, gli stessi attributi e come chiave primaria l'identificatore dell'entità.
$$
\text{artisti} \equiv \{\underline{\text{nome_arte}} \text{, nome, cognome, data di nascita}\}
$$

#### Album

L'entità `Album` presenta un identificatore interno per cui viene tradotta in una relazione avete lo stesso nome, gli stessi attributi e come chiave primaria gli identificatori dell'entità.
$$
\text{album} \equiv \{\underline{titolo} \text{, } \underline{anno} \text{, genere, supporto}\}
$$

#### Etichetta

L'entità `Etichetta` presenta un identificatore interno per cui viene tradotta in una relazione avete lo stesso nome, ma al plurale, gli stessi attributi e come chiave primaria l'identificatore dell'entità.
$$
\text{etichette} \equiv \{\underline{nome} \text{, telefono, via, numero_civico, cap}\}
$$

#### Audizione

L'entità `Audizione` presenta un identificatore interno per cui viene tradotta in una relazione avete lo stesso nome, ma al plurale, gli stessi attributi e come chiave primaria l'identificatore dell'entità.
$$
\text{audizioni} \equiv \{\underline{id} \text{, data, ora}\}
$$

#### Universitario

L'entità `Universitario` presenta un identificatore interno per cui viene tradotta in una relazione avete lo stesso nome, ma al plurale, gli stessi attributi e come chiave primaria l'identificatore dell'entità.
$$
\text{universitari} \equiv \{\underline{matricola} \text{, nome, cognome, via, numero_civico, cap, tipo, area_disciplinare, email, corso, anno_iscrizione}\}
$$



### Traduzione delle associazioni

#### Incisione

L'associazione `Incisione` è un'associazione molti a molti, per cui si traduce in una relazione che avrà lo stesso nome dell'associazione. Non avendo attributi propri la lista degli attributi sarà costituita solo dagli identificatori delle entità associate, con annotazione dell'ovvio vincolo di referenza esterna.
Inoltre gli identificatori esterni faranno anche da chiave primaria della relazione.
$$
\text{incisioni} \equiv \{\underline{artista} \text{, } \underline{titolo} \text{, } \underline{anno}\}
$$
dove:
- `artista` presenta un vincolo di referenza esterna a `nome d'arte` nella relazione `artisti`
- `titolo` presenta un vincolo di referenza esterna a `titolo` nella relazione `album`
- `anno` presenta un vincolo di referenza esterna a `anno` nella relazione `album`

#### Pubblicazione

L'associazione `Pubblicazione` è un'associazione uno a molti, in questo caso si è scelto di operare l'assorbimento nella relazione dell'entità dal lato uno.
Visto che l'associazione non presenta attributi propri, alla relazione `album` vene aggiunto solo il campo `etichetta` con vincolo di referenza esterna a `nome` nella relazione `etichette`.
$$
\text{album} \equiv \{\underline{titolo} \text{, } \underline{anno} \text{, genere, etichetta}\}
$$

#### Ascolto

L'associazione `Ascolto` è un'associazione uno a molti, in questo caso si è scelto di operare l'assorbimento nella relazione dell'entità dal lato uno.
Visto che l'associazione non presenta attributi propri, alla relazione `audizione` vengono aggiunti solo i campi `titolo`, con vincolo di referenza esterna a `titolo` nella relazione `album`, e `anno`, con vincolo di referenza esterna a `anno` della relazione `album`.
$$
\text{audizioni} \equiv \{\underline{id} \text{, data, ora, titolo, anno}\}
$$

#### Partecipazione

L'associazione `Partecipazione` è un'associazione molti a molti, per cui si traduce in una relazione che avrà lo stesso nome dell'associazione. Come lista degli attributi i propri attributi con l'aggiunta degli identificatori delle entità associate, con annotazione dell'ovvio vincolo di referenza esterna.
Inoltre gli identificatori esterni faranno anche da chiave primaria della relazione.
$$
\text{partecipazioni} \equiv \{\underline{partecipante} \text{, } \underline{audizione} \text{, gradimento, commento}\}
$$
dove:
- `partecipante` presenta un vincolo di referenza esterna a `matricola` nella relazione `universitari`
- `audizione` presenta un vincolo di referenza esterna a `id` della relazione `audizione`

#### Richiesta

L'associazione `Richiesta` è un'associazione molti a molti, per cui si traduce in una relazione che avrà lo stesso nome dell'associazione. Come lista degli attributi solo gli identificatori delle entità associate, con annotazione dell'ovvio vincolo di referenza esterna, in quanto non presenta attributi propri.
Inoltre gli identificatori esterni faranno anche da chiave primaria della relazione.
$$
\text{richieste} \equiv \{\underline{richiedente} \text{, } \underline{audizione}\}
$$
dove:
- `richiedente` presenta un vincolo di referenza esterna a `matricola` nella relazione `universitari`
- `audizione` presenta un vincolo di referenza esterna a `id` della relazione `audizione`

### Schema del database

$$
\text{artisti} \equiv \{\underline{\text{nome_arte}} \text{, nome, cognome, data di nascita}\}
$$

$$
\text{etichette} \equiv \{\underline{nome} \text{, telefono, via, numero_civico, cap}\}
$$

$$
\text{album} \equiv \{\underline{titolo} \text{, } \underline{anno} \text{, genere, etichetta}\}
$$

$$
\text{audizioni} \equiv \{\underline{id} \text{, data, ora, titolo, anno}\}
$$

$$
\text{universitari} \equiv \{\underline{matricola} \text{, nome, cognome, via, numero_civico, cap, tipo, area_disciplinare, email, corso, anno_iscrizione}\}
$$

$$
\text{incisioni} \equiv \{\underline{artista} \text{, } \underline{titolo} \text{, } \underline{anno}\}
$$

$$
\text{partecipazioni} \equiv \{\underline{partecipante} \text{, } \underline{audizione} \text{, gradimento, commento}\}
$$

$$
\text{richieste} \equiv \{\underline{richiedente} \text{, } \underline{audizione}\}
$$

---

### Tabelle di relazione

#### Artisti

| Nome attributo | Tipo        | Primo/Not null/Univocità | Vincoli |
| -------------- | ----------- | ------------------------ | ------- |
| nome_arte      | varchar(30) | primary key              |         |
| nome           | varchar(20) | not null                 |         |
| cognome        | varchar(20) | not null                 |         |
| data_nascita   | date        | not null                 |         |

#### Album

| Nome attributo | Tipo        | Primo/Not null/Univocità | Vincoli        |
| -------------- | ----------- | ------------------------ | -------------- |
| titolo         | varchar(30) | primary key              |                |
| anno           | integer     | primary key              |                |
| genere         | varchar(8)  | not null                 |                |
| supporto       | varchar(8)  | not null                 |                |
| etichetta      | varchar(25) | not null                 | etichette.nome |

#### Etichette

| Nome attributo | Tipo        | Primo/Not null/Univocità | Vincoli |
| -------------- | ----------- | ------------------------ | ------- |
| nome           | varchar(25) | primary key              |         |
| telefono       | varchar(15) | not null - unique        |         |
| via            | varchar(25) | not null                 |         |
| numero_civico  | integer     | not null                 |         |
| cap            | integer     | not null                 |         |

---

#### Audizioni

| Nome attributo | Tipo        | Primo/Not null/Univocità | Vincoli      |
| -------------- | ----------- | ------------------------ | ------------ |
| id             | integer     | primary key              |              |
| data           | date        | not null                 |              |
| ora            | text        | not null                 |              |
| titolo         | varchar(30) | not null                 | album.titolo |
| anno           | integer     | not null                 | album.anno   |

#### Universitari

| Nome attributo    | Tipo        | Primo/Not null/Univocità | Vincoli |
| ----------------- | ----------- | ------------------------ | ------- |
| matricola         | integer     | primary key              |         |
| nome              | varchar(20) | not null                 |         |
| cognome           | varchar(20) | not null                 |         |
| via               | varchar(25) | not null                 |         |
| numero_civico     | integer     | not null                 |         |
| cap               | integer     | not null                 |         |
| tipo              | varchar(8)  | not null                 |         |
| area_disciplinare | varchar(30) |                          |         |
| email             | varchar(50) |                          |         |
| anno_iscrizione   | integer     |                          |         |
| corso             | varchar(30) |                          |         |

#### Incisioni

| Nome attributo | Tipo        | Primo/Not null/Univocità | Vincoli             |
| -------------- | ----------- | ------------------------ | ------------------- |
| artista        | varchar(30) | not null                 | artisti.nome_d'arte |
| titolo         | varchar(30) | not null                 | album.titolo        |
| anno           | integer     | not null                 | album.anno          |

---

#### Partecipazioni

| Nome attributo | Tipo          | Primo/Not null/Univocità | Vincoli                |
| -------------- | ------------- | ------------------------ | ---------------------- |
| partecipante   | integer       | primary key              | universitari.matricola |
| audizione      | integer       | primary key              | audizioni.id           |
| gradimento     | varchar(7)    |                          |                        |
| commento       | varchar(1000) |                          |                        |

#### Richieste

| Nome attributo | Tipo          | Primo/Not null/Univocità | Vincoli                |
| -------------- | ------------- | ------------------------ | ---------------------- |
| richiedente   | integer       | primary key              | universitari.matricola |
| audizione      | integer       | primary key              | audizioni.id           |

## Progettazione fisica

Per la realizzazione del nostro database abbiamo scelto di utilizzate SQLite.

Per le operazioni di **delete**, ovvero la cancellazione di tuple all'interno di una tabella, abbiamo optato per l'utilizzo dell'opzione **no action**, la quale non permette la cancellazione di una tupla se questa contiene degli attributi riferiti in altre relazioni. In questo modo, possiamo evitare la cancellazione erronea di tuple, che porterebbero ad un database incompleto. 

Per le operazioni di **update**, che permettono l'aggiornamento dei valori in una tupla, abbiamo scelto di usare l'opzione **cascade**, che propaga l'aggiornamento anche agli attributi che si riferiscono alla tupla modificata. Così facendo, è sufficiente aggiornare solo una volta il valore di un attributo, senza dover modificare singolarmente ogni tupla.

### Creazione delle tabelle

#### Album

```sql lite
create table album (
  titolo varchar(30) not null,
  anno integer not null,
  genere varchar(8) default 'altro' check ( genere in ('rock', 'pop', 'dance', 'classica', 'bluse', 'jazz', 'indie', 'altro')) not null,
  supporto varchar(8) not null check(supporto in ("cd", "vinile", "entrambi")),
  etichetta varchar(25) not null references etichette (nome) on update cascade,
  primary key (titolo, anno)
);
```

#### Artisti

```sql lite
create table artisti (
  nome_arte varchar(30) not null primary key,
  nome varchar(20) not null,
  cognome varchar(20) not null,
  data_nascita date not null
);
```

#### Audizioni

```sql lite
create table audizioni(
  id integer not null primary key,
  data date not null,
  ora text not null,
  titolo varchar(30) not null,
  anno integer not null,
  foreign key (titolo, anno) references album(titolo, anno) on update cascade
);
```

####Etichette

```sql lite
create table etichette (
  nome varchar(25) not null primary key,
  telefono varchar(15) not null unique,
  via varchar(25) not null,
  numero_civico integer not null,
  cap integer not null
);
```

#### Incisioni

```sql lite
create table incisioni(
  artista varchar(30) not null,
  titolo varchar(30) not null,
  anno integer not null,
  foreign key (titolo, anno) references album (titolo, anno) on update cascade,
  foreign key (artista) references artisti (nome_arte) on update cascade,
  primary key (artista, titolo, anno)
);
```

#### Partecipazioni

```sql lite
create table partecipazioni(
  partecipante integer not null references universitari(matricola) on update cascade,
  audizione integer not null references audizioni(id) on update cascade,
  gradimento varchar(7) check(gradimento in ("alto", "normale", "basso")),
  commento varchar(1000),
  primary key(partecipante, audizione)
);
```

#### Richieste

```sql lite
create table richieste(
  richiedente integer not null references universitari(matricola) on update cascade,
  audizione integer not null references audizioni(id) on update cascade,
  primary key(richiedente, audizione)
);
```

#### Universitari

```sql lite
create table universitari(
  matricola integer not null primary key,
  nome varchar(20) not null, 
  cognome varchar(20) not null,
  via varchar(25) not null,
  numero_civico integer not null,
  cap integer not null,
  tipo varchar(8) not null check(tipo in ("studente", "docente")),
  area_disciplinare varchar(30),
  email varchar(50),
  anno_iscrizione integer,
  corso varchar(30)
);
```





[studente]: img/Studente.png
[album]: img/Album.png
[audizione]: img/Audizione.png
[universitario]: img/Universitario.png
[artista]: img/Artista.png
[etichetta]: img/Etichetta.png
[incisione]: img/Incisione.png
[pubblicazione]: img/Pubblicazione.png
[partecipazione]: img/Partecipazione.png
[ascolto]: img/Ascolto.png
[er]: img/ER.png
[etichetta-bis]: img/Etichetta-bis.png
[universitario-bis]: img/Universitario-bis.png
[universitario-tris]: img/Universitario-tris.png
[supporto]: img/Supporto.png
[richiesta]: img/Richiesta.png

