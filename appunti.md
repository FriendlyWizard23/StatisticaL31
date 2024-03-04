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



