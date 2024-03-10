# Lezione 1: Introduzione
## Orari
- MARTEDI: 10.45 - 12.30 CELORIA 208
- GIOVEDI: 13.30 - 16.30 AULA MAGNA

## Jupyter
- link: github.com/dariomalchiodi/superhero-datascience
- per visualizzare un notebook bisogna fare `jupiter nootebook` nella dir in cui ci sono i notebook
- per avviare jupyter: `jupyter lab`

## Roba di Python subdola
### Slicing e accesso posizionale
- "Gli slicing basati su indice comprenderanno il primo e l'ultimo valore specificato mentre gli slice basati su posizione escluderanno l'ultimo elemento.
    - ```first_appearance['Wonder Girl':'Wonder Woman']```
    - ```first_appearance[60:63]```
- L'accesso posizionale può anche fare riferimento a numeri negativi, contando in analogia a liste e tuple a partire dall'ultimo elemento
    - ```first_appearance[-5:]```
- L'accesso alle liste può anche essere fatto specificando una lista (ma non una tupla) di posizioni al posto di una sola posizione, con l'effetto di ottenere i corrispondenti elementi.
    - ```first_appearance[[1, 42, 709]]```
- vi sono anche funzioni come .head() e .tail()
si può utilizzare una lista di valori booleani in cui True indica gli elementi da estrarre e False quelli da filtrare:
    - ```first_appearance[[1970 <= y <1975 for y in first_appearance]]```
- Infine, è possibile effettuare delle query su una serie specificando tra parentesi quadre un'espressione logica che indica quali elementi visualizzare, utilizzando la serie come simbolo che ne indica un suo generico elemento:
    - ```first_appearance[first_appearance > 2010]```
    - Se voglio fare altre condizioni, devo per forza utilizzare l'and bitwise:
    - ```first_appearance[(first_appearance>2010)and(first_appearance%2==1)]``` NON VA BENE
    - ```first_appearance[(first_appearance>2010)&(first_appearance%2==1)]```
    -  

  
## PANDAS
### Series
- Una delle classi principali implementate in pandas è Series.
- Le sue istanze rappresentano serie di osservazioni di un certo carattere fatto su un insieme di individui:
    ```
    years = [int(h[7]) if h[7] else None for h in heroes]
    names = [h[0] for h in heroes]
    first_appearance = pd.Series(years, index = names)
    ```
- possiamo filtrare roba come visto negli appunti sopra su python
- ```value_counts()``` restituisce un'altra serie in cui gli indici sono i valori osservati e i valori le corrispondenti frequenze assolute, ordinate in senso non crescente:

    ```
    1964.0    18
    1963.0    18
    1965.0    14
    2004.0    11
    1975.0    10
            ..
    2013.0     1
    1983.0     1
    1933.0     1
    1948.0     1
    1988.0     1
    Name: count, Length: 71, dtype: int64
    ```
### Visualizzazione grafica serie
- ```.plot()``` permette di visualizzare graficamente i contenuti di una serie, utilizzando matplotlib dietro le quinte; in particolare, il metodo bar visualizza un grafico a barre
- ```.show()``` permette di mostrarlo poi a video
- fare solamente cosi molte volte fa schifo, il grafico viene illeggibile. Lavorare con i valori assoluti molte volte e' meglio
- Cosi ancora non è il massimo. Son necessarie piu informazioni:

    ```
    years = np.arange(1945, 2010, 10)
    index_pos = [first_app_freq.index.get_loc(y) for y in years]
    first_app_freq.plot.bar()
    plt.xticks(index_pos, years)
    plt.ylim((0, 18.5))
    plt.show()
    ```
- Per generare il grafico precedente è necessario utilizzare alcune funzionalità avanzate delle librerie considerate: 
  - `np.arange` permette di costruire un array i cui valori vanno di dieci in dieci partendo da 1945 e arrivando a 2005; la proprietà 
  - `index` di una serie permette di estrarne l'indice e il metodo 
  - `get_loc` di quest'ultimo restituisce la posizione corrispondente a un dato valore dell'indice. 
  - Infine, il metodo `xticks` di matplotlib permette di specificare quali valori evidenziare sull'asse delle ascisse e quali etichette utilizzare.
#### LOV VS ILOC

# LEZIONE 4

- Ripartizione Empirica -> Diagramma a scalini (Funzione costante a tratti)
- CAMPIONE = insieme di dati su cui mi baso per le mie analisi statistiche
    - Ripartizione Empirica ci permette di generare un grafico a scaletta. Prende anche il nome di Funzione di distribuzione cumulativa empirica

- scegliere un campione in modo rappresentativo significa non fare "favoritismi". Non posso estrarre chi mi fa comodo, tutti devono avere la stessa chance di finire nel mio campione.

## POSIZIONE E CENTRALITA
### MEDIA CAMPIONARIA
- calcolabile solamente per i dati **quantitativi**
- mi permette di rappresentare qualcosa con un solo valore.
- caratteristiche
    - Non equivale spesso a nessuno dei valori che usiamo per calcolarla
    - **Traslazione:** Se ho una media di alcuni valori X e poi devo calcolare la media di alcuni valori che sono x+a (traslazione) mi basta aggiungere a alla media calcolata prima. Viene mantenuta la traslazione
    - **Scalabilità**: Stessa cosa vale per la scalabilità. 
    - **Trasformazioni affini**: Stessa cosa vale per le trasformazioni affini.
- queste proprietà sono utili, perche permettono di fare calcoli in modo semplificato. Se ho valori molto alti di media tutti sopra una soglia, io sottraggo la soglia da ogni valore, calcolo la media e poi alla fine sommo la soglia alla media.
- ha fatto tutto un esempio lungo per dire che alla fine quello che posso fare per calcolare la media è sommare tutti i prodotti del xi per la sua frequenza assoluta / numero totale di osservazioni
- ci possono spesso essere **outliers** oppure **valori fuori scala** che sminchiano tutto il nostro calcolo e le nostre valutazioni.

### MEDIANA CAMPIONARIA
- se ne sbatte i coglioni degli outlier
- la mediana è il valore precisamente al centro del mio campione **ordinato**
- se il valore è pari non ho un valore centrale bensi due quindi in quel caso bisogna **calcolare la media dei due valori**
va bene per i dati di tipo **quantitativi e qualitativi**

### MODA CAMPIONARIA


## DISPERSIONE
### VARIANZA CAMPIONARIA
- Consideriamo:
    - Campione A = {1,2,5,6,6}
    - Campione B = {-40,0,5,20,35}

- media campionaria A = 4
- media campionaria B = 4
- Entrambi i valori si concentrano su 4 ma si disperdono in modo completamente diverso
- per calcolare la dispersione utilizziamo la formula della **varianza campionaria** (guarda la formula sul foglio oppure online, non so scriverla qua)
-  **SCALABILITA** = Se voglio verificare la scalablità per un valore b, ottengo che la varianza campionaria scala come b^2
- **TRASLAZIONE** = Invariata, la traslazione di valori del campione non comporta alcuna modifica con la varianza.
- questa varianza, viene identificata con "s" e il suo valore ha come unita di misura quella base al quadrato. 
- se voglio ottenere una vairanza con unita di misura uguale all'originale, calcolo la radice quadrata. Cosi facendo ottengo la **deviazione standard**

### Deviazione Standard
- **TRASLAZIONE** = Invariata
- **SCALABILITA** = assoluto(b)*s

### Coeff. di variazione

s/abs(media)

## PERCENTILE CAMPIONARIO
- dipende dal "livello" p dove questo p è un numero che esprime una percentuale.
- se al posto di percentuale, il livello lo esprimo in
    - 0, ... ,1  -> parlo di **quantili**
    - 0, ... ,4 ->  parlo di **quartili**
    - 0, ... ,10 -> parlo di **decili**

### BOX PLOT
- rappresentazione grafica della centralita e la dispersione. Quest'ultima viene definita dal **range interquartle** che non è altro che la differenza tra il terzo ed il terzo e il primo quartile.