# ELAB18N7 Collezione di Dischi

Uno istituto di formazione musicale vuole creare una base di dati per la propria collezione di album di dischi. Nella base di dati devono essere presenti informazioni relative agli <font color="red">artisti</font>: <font color="green">nome, cognome, data di nascita, nome d'arte. </font><font color="blue">Ogni artista può aver inciso più album, ed un album può essere stato inciso da più artisti</font>. Di ogni <font color="red">album</font> si vuole sapere il <font color="green">titolo, l'anno di pubblicazione ed il genere</font> (da scegliere tra: rock, pop, dance, classica, blues, jazz, ...altro). Inoltre è necessario sapere se <font color="green">il supporto</font> dove il disco è memorizzato è un compact disc o un vinile, ovviamente un disco può essere disponibile per entrambi i supporti. <font color="blue">Ogni album viene pubblicato da una sola etichetta</font>.
<font color="red">Un'etichetta</font> può pubblicare più album. Di ogni etichetta si deve indicare il <font color="green">nome, <u>l'indirizzo</u> e il numero di telefono</font>.
<font color="blue">L'istituto organizza su richiesta, sedute di audizione di un album</font> da parte degli <font color="red"><u>interessati</u></font> (<font color="red">docenti</font> o <font color="red">studenti</font>) individuati da una <font color="green">matricola Nome, Cognome e <u>Indirizzo</u></font>. Nel caso degli studenti si riporta anche il <font color="green">corso a cui sono iscritti e l'anno di iscrizione</font>; nel caso dei docenti si riporta <font color="green">l'area disciplinare di insegnamento e la email interna</font>. Per ogni <font color="red">audizione</font> si conserva un <font color="green">numero progressivo di identificazione, data ed ora dell'audizione</font>. Ad ogni audizione, un docente o uno studente possono compilare un giudizio, di cui si riportano un <font color="green">commento generale</font> (1000 caratteri), <font color="green">il livello di gradimento</font> (alto, normale, basso).

**Legenda**

- <font color="red">Entità</font>
- <font color="red"><u>Entità composta</u></font>
- <font color="blue">Associazioni</font>
- <font color="green">Attributi</font>
- <font color="green"><u>Attributi composti</u></font>

---
## Progettazione concettuale

### Identificazione delle entità e delle associazioni

#### Entità 

##### Artista

> informazioni relative agli **artisti**: nome, cognome, data di nascita, nome d'arte

L'entità `Artista` è composta da quattro attributi. Il `nome` e il `cognome` dell'artista, la `data di nascita` e il `nome d'arte`. Il nome d'arte viene usato come identificatori, quindi deve essere unico. Tutti e quattro i campi sono obbligatori.

![artista][]

| Nome attributo  | Descrizione                                                | Tipo                                    |  ID  |
| --------------- | ---------------------------------------------------------- | --------------------------------------- | :--: |
| nome d'arte     | Il nome con cui l'artista è conosciuto dal grande pubblico | stringa<br />variabile<br />max 30 char |  si  |
| nome            | Il nome dell'artista                                       | stringa<br />variabile<br />max 20 char |  no  |
| cognome         | Il cognome dell'artista                                    | stringa<br />variabile<br />max 20 char |  no  |
| data di nascita | Giorno, mese e anno in cui è nato l'artista                | data                                    |  no  |

---

##### Album 

> Di ogni **album** si vuole sapere il titolo, l'anno di pubblicazione ed il genere...Inoltre è necessario sapere se il supporto dove il disco è memorizzato

L'entità `Album` è composta da quattro attributi. Il `titolo` dell'album, l'`anno` in cui è stato pubblicato e il `genere`. Quest'ultimo attributo può assumere uno dei seguenti valori: rock, pop, dance, classica, bluse, jazz, indie. Inoltre è presente anche l'attributo `supporto` che indica il supporto su cui è memorizzato l'album. Quest'attributo può assumere o il valore di vinile o di CD. Visto che un album può essere stato memorizzato su entrambi i supporti l'attributo supporto è multivalore.
Il titolo e l'anno di pubblicazione vengono usati come identificatori, quindi si possono avere due album con lo stesso titolo, ma pubblicati in anni diversi.
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

> Di ogni **etichetta** si deve indicare il nome, l'indirizzo e il numero di telefono

L'entità `Etichetta` è composta da tre attributi. Il `nome` commerciale dell'etichetta, l'`indirizzo` della sede e il numero di `telefono`. Il nome dell'etichetta viene usato come identificatore, quindi deve essere unico.
Tutti i campi sono obbligatori.

![etichetta][]

| Nome attributo | Descrizione                                                  | Tipo                                    | ID   |
| -------------- | ------------------------------------------------------------ | --------------------------------------- | ---- |
| nome           | Nome commerciale con sui è conosciuta l'etichetta            | stringa<br />variabile<br />max 25 char | si   |
| indirizzo      | L'indirizzo della sede dell'etichetta. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto                                | no   |
| telefono       | Il numero, o i numeri di telefono appartenenti all'etichetta. L'etichetta deve possedere almeno un numero | intero                                  | no   |

---

##### Docente e studente

> (**docenti** o **studenti**) individuati da una matricola Nome, Cognome e Indirizzo. Nel caso degli studenti si riporta anche il corso a cui sono iscritti e l'anno di iscrizione; nel caso dei docenti si riporta l'area disciplinare di insegnamento e la email interna.

Le entità `Docente` e `Studente` sono entrambe individuate dal `nome`, dal `cognome` e dall'`indirizzo` e dalla `matricola`. Quest'ultima vine usata come identificatore.
Nel caso di un studente vengono aggiunti anche gli attributi `anno di iscrizione` e il `corso` a cui sono iscritti.
Nel caso di un docente vengono aggiunti anche gli attributi `area disciplinare` e `email` per l'email interna all'istituto.
Per rappresentate queste due entità si è scelto di utilizzare una generalizzazione totale ed esclusiva, in quanto nel dominio del problema non esistono altri interessati oltre ai docenti e agli studenti e uno studente non può essere anche un docente o viceversa.
Tutti i campi sono obbligatori.

![universitario][]

| Nome attributo    | Descrizione                                                  | Tipo                                    | ID   |
| ----------------- | ------------------------------------------------------------ | --------------------------------------- | ---- |
| matricola         | Codice identificativo all'interno dell'organizzazione        | intero                                  | si   |
| nome              | Nome del                                                     | stringa<br />variabile<br />max 20 char | no   |
| cognome           | Cognome del                                                  | stringa<br />variabile<br />max 20 char | no   |
| indirizzo         | L'indirizzo di residenza del. L'indirizzo è composto da tre sotto campi; via, n.ro civico e cap | composto                                | no   |
| area disciplinare | L'area di insegnamento del docente                           | stringa<br />variabile<br />max 30 char | no   |
| email             | L'email interna all'istituto                                 | stringa<br />variabile<br />max 50 char | no   |

---

##### Audizione

> Per ogni **audizione** si conserva un numero progressivo di identificazione, data ed ora dell'audizione

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

> Ogni artista può aver **inciso** più album, ed un album può essere stato **inciso** da più artisti

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

> Ogni album viene **pubblicato** da una sola etichetta

L'entità `Album` e l'entità `Etichetta` sono legati dall'associazione `Publicazione`.
Un album deve essere pubblicato da una sola etichetta per cui ha molteplicità $(1,1)$.
Un etichetta può pubblicare più album, cosicché può non averne pubblicati per cui ha molteplicità $(0,n)$.
Quest'associazione non ha attributi propri.

![pubblicazione][]

| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
| Album            | 1,1                     |
| Etichetta        | 0,n                     |

---

##### Partecipazione

> L'istituto organizza su richiesta, sedute di audizione di un album da parte degli interessati

Le entità `Docenete` e `Studnete` e l'entità `Audizione` sono legati dall'associazione `Partecipazione`.
Ad una audizione deve partecipare almeno un studente/docente per cui ha molteplicità $(1,n)$.
Uno studente può naturalmente partecipare a più audizioni, così come non partecipare a nessuna audizione, per cui ha molteplicità $(0,n)$.
Quest'associazione ha due attributi: `commento`, un giudizio sull'audizione compreso in 1000 caratteri e `gradimento` un giudizio sintetico che può assumere i valori di basso, normale e alto.

![partecipazione][]


| Entità coinvolta | Rapporto di cardinalità |
| :--------------: | :---------------------: |
| docente/studente |           0,n           |
|    Audizione     |           1,n           |

| Nome attributo | Descrizione                       | Tipo                                      | ID   |
| -------------- | --------------------------------- | ----------------------------------------- | ---- |
| commento       | Giudizio esteso sull'audizione    | stringa<br />variabile<br />max 1000 char | no   |
| gradimento     | Giudizio sintetico sull'audizione | enumerabile                               | no   |

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
| audizione        | 1,1                     |
| Album            | 0,n                     |

---

### Vincoli e derivazioni

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

### Modello E-R

![er][]

## Progettazione logica

### Trasformazioni preliminari

#### Trasformazioni di attributi composti in attributi semplici

L'entità `Etichetta` e l'entità `Unversitario` presentano tra i loro attributi l'attributo complesso `indirizzo` per poter passare dalla progettazione concettuale a quella logica dobbiamo eliminare questo attributo composto; per fare ciò si è scelto di scogliere l'attributo complesso in più attributi semplici.
Per cui l'entità `Etichetta` sarà così trasformata:

![etichetta-bis][]

Allo stesso modo l'entità `Universitario` diventa:

![universitario-bis][]

#### Trasformazione degli attributi multivalore

L'entità `Album` presenta l'attributo multivalore `supporto`. Per poter eseguire la progettazione logica dobbiamo trasformare l'attributo in un'associazione.

![supporto][]

#### Trasformazione della generalizzazione

Durante la progettazione concettuale le entità `Studente` e `Docente` sono state generalizzate nell'entità `Universitario`, ma per poter passare alla progettazione logica incontriamo la necessita di eliminare la generalizzazione.
Visto che ci troviamo difronte ad una generalizzazione totale ed esclusiva possiamo scegliere tra tre opzioni; trasformare la generalizzazione in un'associazione, far assorbire il padre nei figli e assorbire i figli nel padre. In questo caso abbiamo scelto di seguire quest'ultima opzione.
I due figli(studente e docente) vengono eliminati, e i loro attributi aggiunti a quelli dell'entità padre. Questi nuovi attributi possono assumere il valore $NULL$. Inoltre all'entità `Universitario` viene aggiunto anche l'attributo `tipo`. Trovandoci in una generalizzazione totale ed esclusiva l'attributo `tipo` può assumere solo il valore docente e studente.

![universitario-tris][]

### Traduzione di entità

#### Artista

L'entità `Artista` presenta un identificatore interno per cui viene tradotta in una relazione avete lo stesso nome, ma al plurale, gli stessi attributi e come chiave primaria l'identificatore dell'entità.
$$
\text{artisti} \equiv \{\underline{\text{nome_arte}} \text{, nome, cognome, data di nascita}\}
$$

#### Album

L'entità `Album` presenta un identificatore interno per cui viene tradotta in una relazione avete lo stesso nome, gli stessi attributi e come chiave primaria gli identificatori dell'entità.
$$
\text{album} \equiv \{\underline{titolo} \text{, } \underline{anno} \text{, genere}\}
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



#### Supporto

L'entità `Supporto` presenta un identificatore interno per cui viene tradotta in una relazione avente lo stesso nome, ma al plurale, gli stessi attributi e come chiave primaria l'identificatore dell'entità.
$$
\text{supporti} \equiv \{\underline{tipo}\text{, dimensione}\}
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



####Memoria

L'associazione `Memoria` è un'associazione uno a molti, in questo caso si è scelto di operare l'assorbimento nella relazione dell'entità dal lato uno.
Visto che l'associazione non presenta attributi propri, alla relazione `supporti` vengono aggunti solo i campi `titolo`, con vincolo di referenza esterna a `titolo` nella relazione `album`,  e `anno`, con vincolo di referenza esterna a `anno` nella relazione `album`.
$$
\text{supporti} \equiv \{\underline{tipo} \text{, dimensione, titolo, anno}\}
$$


### Tabelle di relazione

#### Artisti

| Nome attributo | Tipo        |             | Vincoli |
| -------------- | ----        | ----        | ------- |
| nome_arte      | varchar(30) | primary key |         |
| nome           | varchar(20) | not null    |         |
| cognome        | varchar(20) | not null    |         |
| data_nascita   | date        | not null    |         |

#### Album

| Nome attributo | Tipo        |             | Vincoli        |
| -------------- | ----------- | ----------- | -------------- |
| titolo         | varchar(30) | primary key |                |
| anno           | integer     | primary key |                |
| genere         | varchar(10) | not null    |                |
| etichetta      | varchar(25) | not null    | etichette.nome |

#### Etichette

| Nome attributo | Tipo        |                   | Vincoli |
| -------------- | ----        | ----              | ------- |
| nome           | varchar(25) | primary key       |         |
| telefono       | varchar(15) | not null - unique |         |
| via            | varchar(25) | not null          |         |
| numero_civico  | integer     | not null          |         |
| cap            | integer     | not null          |         |

#### Audizioni

| Nome attributo | Tipo        |             | Vincoli      |
| -------------- | ----------- | ----------- | ------------ |
| id             | integer     | primary key |              |
| data           | date        | not null    |              |
| ora            | ?           | not null    |              |
| titolo         | varchar(30) | not null    | album.titolo |
| anno           | integer     | not null    | album.anno   |

#### Universitari

| Nome attributo    | Tipo        |             | Vincoli |
| ----------------- | ----------- | ----------- | ------- |
| matricola         | integer     | primary key |         |
| nome              | varchar(20) | not null    |         |
| cognome           | varchar(20) | not null    |         |
| via               | varchar(25) | not null    |         |
| numero_civico     | integer     | not null    |         |
| cap               | integer     | not null    |         |
| tipo              | varchar(10) | not null    |         |
| area_disciplinare | varchar(30) |             |         |
| email             | varchar(50) |             |         |
| anno_iscrizione   | integer     |             |         |
| corso             | varchar(30) |             |         |

####Incisioni

| Nome attributo | Tipo        |          | Vincoli             |
| -------------- | ----------- | -------- | ------------------- |
| artista        | varchar(30) | not null | artisti.nome_d'arte |
| titolo         | varchar(30) | not null | album.titolo        |
| anno           | integer     | not null | album.anno          |

####Partecipazioni

| Nome attributo | Tipo          |             | Vincoli                |
| -------------- | ------------- | ----------- | ---------------------- |
| partecipante   | integer       | primary key | universitari.matricola |
| audizione      | integer       | primary key | audizioni.id           |
| gradimento     | varchar(10)   |             |                        |
| commento       | varchar(1000) |             |                        |



#### Supporti

| Nome attributo | Tipo        |             | Vincoli      |
| -------------- | ----------- | ----------- | ------------ |
| tipo           | varchar(10) | primary key |              |
| dimensione     | integer     | not null    |              |
| titolo         | varchar(30) | not null    | album.titolo |
| anno           | integer     | not null    | album.anno   |
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
