# Analisi dei componenti principali (PCA)
---

https://github.com/HarshMishra2002/pca 

PCA è una tecnica di estrazione delle funzionalità.  
Riduce la dimensione dei tuoi dati e ti salva dalla maledizione della dimensionalità.


INTUIZIONE GEOMETRICA:

Per prima cosa dobbiamo capire come funziona la selezione delle funzionalità.  
Dipende completamente dalla varianza dei dati.

![](https://miro.medium.com/max/700/1*_yML3ofvvkYhZKF397pjJg.png)

Se osserviamo il grafico sopra: possiamo vedere chiaramente che d >> d1 cioè la varianza dei dati sull'asse x è maggiore dei dati sull'asse y quindi sceglieremo la caratteristica che è sull'asse x e rilasceremo che è sull'asse y. Ma questa tecnica di selezione delle caratteristiche sembra fallire quando i dati su entrambi gli assi hanno variazioni simili.

![](https://miro.medium.com/max/700/1*yNN3JVBkyfZm7g9GuwL-DA.png)	

ora in questo caso d = d1 quindi la varianza delle colonne di dati su ciascun asse è la stessa. Non è possibile utilizzare la tecnica di cui sopra per selezionare una caratteristica dei dati e rifiutarne un'altra. Quindi ecco che arriva PCA: facciamo ruotare l'asse originale in modo da ottenere la massima varianza su un asse. Questi nuovi assi sono chiamati **Componenti principali**.
Quindi proiettiamo i dati originali sul componente principale per ottenere i nostri nuovi punti dati e questi punti dati sono il nostro nuovo set di dati che contiene informazioni critiche sui dati.  
In PCA creiamo nuovi dati invece di eliminarne alcuni e conservarne alcuni.
![](https://miro.medium.com/max/700/1*XHgJ4VJgz1RN2xpx4GX7cQ.png)
Dopo aver ruotato l'asse originale abbiamo ottenuto un nuovo asse cioè Asse Principale 1 e Asse Principale 2 e ora per i nuovi punti dati (che abbiamo ottenuto proiettando i vecchi sul PC) abbiamo diverse varianti cioè d nuovo >> d1 nuovo.


## Cosa non fa la PCA

Sebbene PCA sia spesso utilizzato per la progettazione delle funzionalità, ci sono limiti a ciò che può fare. Ad esempio, se il set di dati è leggermente allungato e il margine di separazione è piccolo tra di loro (come nell'esempio seguente), PCA non fornirà una rappresentazione in cui la differenza tra le classi è più netta. 



# PCA con In Python

![](https://miro.medium.com/max/2000/1*eDDVjbUrGdWaJ57n5cTXDQ.png)


Passaggio 1: ridimensionamento dei dati (centratura media): Ridimensioniamo i dati, ovvero portiamo tutte le colonne in un intervallo di valori simile. Qui applicheremo la libreria standardscaler di sklearn.
![](https://miro.medium.com/max/2000/1*HJAqf8qBNvyVy7nclSeDSA.png)
Passaggio 2: trovare la matrice di covarianza: Lo svantaggio di trovare una varianza è che posso trovare la varianza di una colonna con un solo asse. Quindi, quando si tratta di trovare la relazione tra due variabili, usiamo qualcosa chiamato covarianza.  
Una matrice di covarianza è una matrice quadrata che fornisce la covarianza tra ciascuna coppia di elementi di un dato vettore casuale.   
![](https://miro.medium.com/max/2000/1*7l6LXyEyu7YxVd7w_P4pHg.png)

Passaggio 3: trovare vettori Eigen e valori Eigen

Gli autovettori sono quei vettori quando applichiamo una trasformazione su di esso, cambia solo la dimensione e non la direzione.

I valori di Eigen sono la misura della riduzione o dell'allungamento del vettore di Eigen dopo la trasformazione.

La trasformazione qui discussa è la trasformazione applicata alla matrice di covarianza. Fondamentalmente troviamo autovettori e autovalori della matrice di covarianza che abbiamo trovato sopra.

Ogni autovettore ha un autovalore, il vettore con il valore più alto è il nostro PC 1 (primo componente principale) e così via..
![](https://miro.medium.com/max/2000/1*a7c3nUTpmMm5SkUWtc37Zg.png)


![](https://miro.medium.com/max/1254/1*Od6KxIr9Ypuu7hUufdz_aA.png)

Passaggio 4: selezionare il PC e trasformare di conseguenza i vecchi dati

Qui sceglierò i primi due PC cioè sto convertendo i miei dati 3D in dati 2D. Quindi trasformeremo i vecchi dati proiettandoli sul nuovo asse (PC).

![](https://miro.medium.com/max/2000/1*8mty-mEKIhq1KSiT_1HU3Q.png)


![](https://miro.medium.com/max/1400/1*WqqTSubA4KZCGtHUZJKqoQ.png)


----------------------------------------------------------------------------------------------------
1. Dati di trama: Supponiamo che i nostri dati appaiano come di seguito. A sinistra, sono le caratteristiche x, yez. Sulla destra, questi punti vengono tracciati. Supponiamo che i punti dei dati tracciati siano ridimensionati.
2. Trova il centro dei dati:Questa è la media di ogni caratteristica: x, yez.
3. Sposta i punti dati in modo che il centro sia ora a (0,0) Nota che la posizione relativa dei punti dati non cambia.
4. Trova la linea più adatta. La linea di miglior adattamento si chiama PC1 (componente principale 1). PC1 massimizza la somma delle distanze al quadrato da dove i punti incontrano la linea di miglior adattamento ad angolo retto. PC1 è una combinazione lineare di x, yez, il che significa che contiene parti di ogni x, yez.
5. Trova PC2: PC2 è la linea più adatta perpendicolare (interseca ad angolo retto) a PC1. PC2 è anche una combinazione lineare di ogni x,yez. PC1 e PC2 ora spiegano entrambi alcune delle variazioni nelle nostre funzionalità. È possibile misurare l'importanza relativa x, yez in ogni PC calcolando i "punteggi di caricamento".
6. Ruota il grafico in modo che PC1 sia l'asse x e PC2 sia l'asse y: Dopo la rotazione, i nostri dati sono ora in sole 2 dimensioni! E i cluster sono facili da individuare.
7. E se avessi più di 3 dimensioni per cominciare? Ci sono tanti PC quante sono le caratteristiche o gli esempi minori nel tuo set di dati. È possibile calcolare la varianza spiegata di ciascun PC confrontando gli autovalori (somma dei quadrati delle distanze dall'origine) e costruendo un ghiaione . Per definizione, PC2 spiega meno varianza di PC1 e PC3 spiega meno varianza di PC2. Decidi quanti PC tenere. Nel nostro esempio abbiamo deciso di escludere PC3. Il numero di PC rimanenti determinerà il numero di dimensioni nel grafico finale. 

![](https://miro.medium.com/max/700/1*MJlSXELJ6-zNJibG5CtqIg.png)
![](https://miro.medium.com/max/700/1*1BiMkGksH0JBOEOlf1tBTg.png)
![](https://miro.medium.com/max/700/1*m3gnAUA9dBFQlbgWAziu3A.png)
![](https://miro.medium.com/max/700/1*OjfIsQ5mxzfWoh3wtoBDBA.png)
![](https://miro.medium.com/max/700/1*oRj5G874ukOev-uLrsq7LQ.png)
![](https://miro.medium.com/max/700/1*juLo2GtiuLdHhJOaNljyqw.png	)
![]()
----------------------------------------------------------------------------------------------------


# [Comprensione della PCA ](https://towardsdatascience.com/understanding-pca-90f7b1961fa4)
![](https://miro.medium.com/max/700/1*BSqBACgT24ZWGXjZDzG8dQ.png)
![](https://miro.medium.com/max/700/1*zYuvlDCWUdOCsbqYs2uSSg.png)
![](https://miro.medium.com/max/700/1*2irBt7dlU8xk8e3CKbbMRw.png)

Per vedere come si comporta su dati reali, vedremo come si comporta PCA sul famoso set di [dati Iris](https://scikit-learn.org/stable/auto_examples/datasets/plot_iris_dataset.html)
 ! Questo set di dati è costituito da quattro caratteristiche (lunghezza del sepalo, larghezza del sepalo, lunghezza del petalo, larghezza del petalo) da tre diversi tipi di iris Setosa, Versicolor e Virginica. Ecco come appare il set di dati.
![](https://miro.medium.com/max/700/1*LIjySiVTG_Y0FcB2BH15EA.png)
Applichiamo la PCA per vedere cosa fa con il nostro set di dati! 
![](https://miro.medium.com/max/700/1*3T82Qv_O3KY64Po3fJc9oA.png)
I primi due componenti principali descrivono quasi completamente il set di dati, mentre il 3° e il 4° possono essere omessi senza una notevole perdita di informazioni. Anche la matrice di covarianza sembra molto migliore. È essenzialmente diagonale, quindi le caratteristiche non sono correlate tra loro. 




 Quali sono i vantaggi del PCA?

    Metodo popolare per la riduzione della dimensionalità
    Aiuta a superare il problema della multicollinearità
    Quando ci sono troppe variabili e non sai quali eliminare

Svantaggi

    Il limite maggiore è l'assunzione di linearità.
    Ed è utile per dati quantitativi, non consigliato per dati qualitativi.
    Interpretare i PC è difficile rispetto alle variabili originali


## Come eseguire PCA in Python con un esempio

Vediamo come eseguire PCA in sklearn utilizzando il set di dati iris.
![](https://1.bp.blogspot.com/-7FhZqpnRRO4/XYyTmBS3QzI/AAAAAAAABF4/Q1W_oxp8r7UfAGutRUDTz4JrnCc21G-lACLcBGAsYHQ/s640/9.PNG)

Poiché PCA è influenzato dalle unità di funzionalità, è necessario standardizzare le funzionalità prima di eseguire PCA.
![](https://1.bp.blogspot.com/-Kt4_nXGdZe4/XYyTlCtQqqI/AAAAAAAABFw/E7idOLaLGWAyabtiX1JxQFTWlejbctXHgCEwYBhgL/s640/10.PNG)

Il numero di componenti può essere lasciato vuoto durante l'esecuzione di PCA per la prima volta poiché non conosceremo la varianza spiegata da ciascuno dei PC.
![](https://1.bp.blogspot.com/-dZASFruIm70/XYyTlM1U4eI/AAAAAAAABFs/3D_u_eRx8vs4PPhuhpNMKtj_T0DVBCmpwCEwYBhgL/s640/11.PNG)

Nel nostro caso, il 73% delle informazioni spiegate dal primo PC, mentre il secondo PC spiega il 23% delle informazioni.
![](https://1.bp.blogspot.com/-rb5QDrv0l_o/XYyTla1pe_I/AAAAAAAABF0/efwT5CQADfkpP5ZhekPIeXqxA9srdVCMgCEwYBhgL/s640/12.PNG)




----------------------------------------------------------------------------------------------------
# PCA con R

Impostare

Per questo articolo utilizzeremo come dati il ​​set di dati sul cancro al seno Wisconsin dal repository di machine learning UCI . Vai avanti e caricalo per te se vuoi seguire:

	wdbc <- read.csv("wdbc.csv", header = F) 
	features <- c("raggio", "trama", "perimetro", "area", "uniformità", "compattezza", "concavità", "concave_points", "symmetry", "fractal_dimension") 
	names( wdbc ) <- c(" id ", " diagnostic ", paste0( features ," _mean "), paste0( features ," _se "), paste0( features , " _peggiore ")) 

Il codice sopra caricherà semplicemente i dati e nominerà tutte e 32 le variabili. L' ID , la diagnosi e le dieci caratteristiche distintive (30). Dall'UCI:

“La media , s t andard errore , e‘ peggiore ’o più grande (media dei tre valori più grandi) di queste caratteristiche sono stati calcolati per ogni immagine, con conseguente 30 caratteristiche . Ad esempio, il campo 3 è il raggio medio, il campo 13 è il raggio SE, il campo 23 è il raggio peggiore.

## Perché PCA?

Bene, ora abbiamo caricato i nostri dati e ci troviamo con 30 variabili (escludendo quindi la nostra risposta "diagnosi" e la variabile ID irrilevante).

Ora alcuni di voi potrebbero dire "30 variabili sono tante" e altri potrebbero dire "Pfft.. Solo 30? Ho lavorato con MIGLIAIA!!” ma ti assicuro che questo è ugualmente applicabile in entrambi gli scenari..!

Ci sono alcuni buoni motivi per usare PCA. Il grafico all'inizio dell'articolo è un ottimo esempio di come si potrebbero tracciare dati multidimensionali utilizzando PCA, in realtà 63,3% catturiamo il (Dim1 44,3% + Dim2 19%) di varianza nell'intero set di dati semplicemente usando quelli due componenti principali , abbastanza buoni se si considera che i dati originali consistevano in 30 caratteristiche che sarebbe impossibile tracciare in modo significativo.

Una considerazione molto importante è riconoscere che non abbiamo mai specificato una variabile di risposta o qualsiasi altra cosa nel nostro grafico PCA che indicasse se un tumore fosse " benigno " o " maligno ". Si scopre semplicemente che quando proviamo a descrivere la varianza nei dati utilizzando le combinazioni lineari della PCA troviamo un raggruppamento e una separazione piuttosto ovvi tra i tumori benigni " " e " maligni "! Questo è un ottimo caso per lo sviluppo di un modello di classificazione basato sulle nostre caratteristiche!

Un'altra importante "caratteristica" (nessun gioco di parole) di PCA è che può effettivamente migliorare direttamente le prestazioni dei tuoi modelli, dai un'occhiata a questo fantastico articolo per saperne di più:

## Cos'è la PCA e come funziona?

Tiriamo fuori qualcosa immediatamente, lo scopo principale della PCA è NON come un modo per rimuovere le funzionalità! PCA può ridurre la dimensionalità ma non ridurrà il numero di caratteristiche/variabili nei dati. Ciò significa che potresti scoprire che puoi spiegare il 99% della varianza nel tuo set di dati di 1000 funzionalità semplicemente utilizzando 3 componenti principali ma hai ancora bisogno di quelle 1000 funzionalità per costruire quei 3 componenti principali, questo significa anche che nel caso di previsione sui dati futuri hai ancora bisogno di quelle stesse 1000 caratteristiche sulle tue nuove osservazioni per costruire i corrispondenti componenti principali.
Giusto, abbastanza giusto, come funziona?

Poiché questo è puramente introduttivo, salterò la matematica e ti darò una rapida carrellata del funzionamento di PCA:

*    Standardizzare i dati (Centro e scala).
*    Calcola gli autovettori e gli autovalori dalla matrice di covarianza o dalla matrice di correlazione (si potrebbe anche usare la decomposizione vettoriale singolare).
*    Ordina gli autovalori in ordine decrescente e scegli i K autovettori più grandi (dove K è il numero desiderato di dimensioni del nuovo sottospazio di feature k ≤ d).
*    Costruisci la matrice di proiezione W dagli selezionati K autovettori .
*    Trasforma il set di dati originale X tramite W per ottenere un K sottospazio di feature -dimensionale Y. 

Questo potrebbe sembrare un po 'complicato se non hai avuto alcuni corsi di algebra, ma l'essenza è trasformare i nostri dati dal suo stato iniziale X in un sottospazio Y con K dimensioni dove K è - il più delle volte - meno rispetto alle dimensioni originali di X . Per fortuna questo è fatto facilmente usando R!

## PCA sui nostri dati sul tumore

Quindi ora capiamo un po' come funziona la PCA e questo dovrebbe essere sufficiente per ora. Proviamolo concretamente:

	wdbc.pr <- prcomp(wdbc[c(3:32)], centro = VERO, scala = VERO) 
	summary(wdbc.pr) 

Questo è abbastanza autoesplicativo, la funzione " prcomp " esegue PCA sui dati che gli forniamo, nel nostro caso è " wdbc[c(3:32)] " che sono i nostri dati escludendo l'ID e le variabili di diagnosi, quindi diciamo R per centrare e ridimensionare i nostri dati ( così standardizzando i dati). Infine chiediamo un riassunto:
![I valori delle prime 10 componenti principali](https://miro.medium.com/max/2400/1*8Ljjg9rQSLrribGmySVmFg.png)

Ricordiamo che una proprietà di PCA è che i nostri componenti sono ordinati dal più grande al più piccolo rispetto alla loro deviazione standard ( Autovalori ). Quindi diamo un senso a questi:

*    Deviazione standard: questi sono semplicemente gli autovalori nel nostro caso poiché i dati sono stati centrati e scalati ( standardizzati )
*    Proporzione di varianza : questa è la quantità di varianza che il componente tiene conto nei dati, ad es. PC1 rappresenta >44% della varianza totale nei soli dati!
*    Proporzione cumulativa : questa è semplicemente la quantità accumulata della varianza spiegata, ad es. se usassimo le prime 10 componenti saremmo in grado di rappresentare >95% della varianza totale nei dati. 

Giusto, quindi quanti componenti vogliamo? Ovviamente vogliamo essere in grado di spiegare quanta più varianza possibile ma per farlo avremmo bisogno di tutti e 30 i componenti, allo stesso tempo vogliamo ridurre il numero di dimensioni quindi vogliamo decisamente meno di 30!

Poiché abbiamo standardizzato i nostri dati e ora abbiamo gli autovalori corrispondenti di ciascun PC, possiamo effettivamente usarli per tracciare un confine per noi. Poiché un autovalore <1 significherebbe che il componente in realtà spiega meno di una singola variabile esplicativa, vorremmo scartarli. Se i nostri dati sono adatti per la PCA , dovremmo essere in grado di scartare questi componenti mantenendo almeno il 70-80% della varianza cumulativa . Tracciamo e vediamo:

	screeplot(wdbc.pr, type = "l", npcs = 15, main = "Screeplot dei primi 10 PC") 
	abline(h = 1, col="rosso", lty=5) 
	legend("in alto a destra", legend=c("Autovalore = 1"), 
	col=c("rosso"), lty=5, cex=0.6) cumpro <- cumsum(wdbc.pr$sdev^2 / sum(wdbc.pr$sdev^2)) 
	plot(cumpro[0:15], xlab = "PC #", ylab = "Importo della varianza spiegata", main = "Grafico della varianza cumulativa") 
	abline(v = 6, col="blu", lty=5) 
	abline(h = 0,88759, col="blu", lty=5) 
	legend("topleft", legend=c("Cut-off @ PC6"), 
	col=c("blu"), lty=5, cex=0.6) 

![Screeplot grafico degli autovalori dei primi 15 PC (a della sinistra ) e varianza cumulativa (a destra)](https://miro.medium.com/max/700/1*vEZjZOscRQV0uuksWK_ryw.png)

Notiamo che i primi 6 componenti hanno un autovalore >1 e spiegano quasi il 90% della varianza , questo è fantastico! Possiamo efficacemente ridurre la dimensionalità da 30 a 6 mentre "perdiamo" solo il 10% circa della varianza!

Notiamo anche che possiamo effettivamente spiegare più del 60% della varianza solo con le prime due componenti. Proviamo a tracciare questi:

	plot(wdbc.pr$x[,1],wdbc.pr$x[,2], xlab="PC1 (44,3%)", ylab = "PC2 (19%)", main = "PC1 / PC2 - plot ") 

![](https://miro.medium.com/max/700/1*Sv08OjZ8QR1MeT06NhB_pg.png)

Va bene, questo non è molto indicativo, ma considera per un momento che questo rappresenta il 60%+ della varianza in un set di dati a 30 dimensioni. Ma cosa vediamo da questo? Ci sono alcuni raggruppamenti in corso in alto/centro-destra. Consideriamo anche per un momento quale sia effettivamente l'obiettivo di questa analisi. Vogliamo spiegare la differenza tra tumori maligni e benigni . Aggiungiamo effettivamente la variabile di risposta ( diagnosi ) al grafico e vediamo se riusciamo a capirlo meglio:

	libreria ("fatto extra") 
	fviz_pca_ind(wdbc.pr, geom.ind = "punto", forma punti = 21, 
	dimensione dei punti = 2, 
	fill.ind = wdbc$diagnosis, 
	col.ind = "nero", 
	tavolozza = "jco", 
	addEllipses = TRUE, 
	etichetta = "var", 
	col.var = "nero", 
	respingere = VERO, 
	legend.title = "Diagnosi") + 
	ggtitle("Plot 2D PCA da 30 feature dataset") + 
	tema(plot.title = element_text(hjust = 0.5)) 

![](https://miro.medium.com/max/700/1*oSOHZMoS-ZfmuAWiF8jY8Q.png)

Questa è essenzialmente la stessa identica trama con alcune ellissi fantasiose e colori corrispondenti alla diagnosi del soggetto e ora vediamo la bellezza di PCA . Con solo i primi due componenti possiamo vedere chiaramente una certa separazione tra i tumori benigni e maligni . Questa è una chiara indicazione che i dati sono adatti per un qualche tipo di di modello classificazione (come l' analisi discriminante ).
Qual è il prossimo?

Il nostro prossimo obiettivo immediato è costruire una sorta di modello utilizzando i primi 6 componenti principali per prevedere se un tumore è benigno o maligno e quindi confrontarlo con un modello utilizzando le 30 variabili originali.


# [Capitolo 4 Analisi delle Componenti Principali (PCA) e Analisi Fattoriale Esplorativa (EFA)](http://www.r-project.it/_book/analisi-delle-componenti-principali-pca-e-analisi-fattoriale-esplorativa-efa.html)

![](http://www.r-project.it/_book/32-dimreduction-PCA-EFA_files/figure-html/02b-graphlifesummary1-1.png)


----------------------------------------------------------------------------------------------------

# [Biplot]()

![](https://i.stack.imgur.com/0ko8W.png)
![](http://www.sthda.com/english/sthda-upload/figures/principal-component-methods/006-principal-component-analysis-color-individuals-and-variables-by-groups-1.png)
----------------------------------------------------------------------------------------------------

È un proiezione metodo di in quanto proietta osservazioni da uno spazio p-dimensionale con p variabili a uno spazio k-dimensionale (dove k < p) in modo da conservare la massima quantità di informazioni (l'informazione è qui misurata attraverso la varianza totale del df) dalle dimensioni iniziali

Le PCA dimensioni sono anche chiamate assi o fattori . Se le informazioni associate ai primi 2 o 3 assi rappresentano una percentuale sufficiente della variabilità totale del grafico a dispersione, le osservazioni potrebbero essere rappresentate su un grafico a 2 o 3 dimensioni, rendendo così molto più facile l'interpretazione.

Ci sono diversi usi per questo, tra cui:

Lo studio e la visualizzazione delle correlazioni tra variabili per poter eventualmente limitare il numero di variabili da misurare successivamente;
Ottenere fattori non correlati che sono combinazioni lineari delle variabili iniziali in modo da utilizzare questi fattori in metodi di modellazione come la regressione lineare, la regressione logistica o l'analisi discriminante.
    Visualizzazione di osservazioni in uno spazio bidimensionale o tridimensionale al fine di identificare gruppi di osservazioni uniformi o atipici. 

diversi trattamenti di dati da utilizzare sui input dati di prima dei calcoli dell'analisi delle componenti principali:

* Pearson, il classico PCA, che standardizza automaticamente i dati prima dei calcoli per evitare di gonfiare l'impatto delle variabili con varianze elevate sul risultato.

* Covarianza, che funziona su varianze e covarianze non standardizzate (le variabili con varianze elevate giocheranno un ruolo più forte negli output.

* Policorico, per dati ordinali. 
    
## centroidi di categoria
    
## ellissi di confidenza attorno alle categorie. 

Rotazioni: Varimax e altri

Le rotazioni possono essere applicate sui fattori. Sono disponibili diversi metodi tra cui Varimax, Quartimax, Equamax, Parsimax, Quartimin e Oblimin e Promax.
Risultati per l'analisi dei componenti principali in XLSTAT

La funzione XLSTAT PCA fornisce risultati relativi alle variabili e alle osservazioni.
Cosa sono le matrici di correlazione/covarianza?

Questa tabella mostra i dati da utilizzare successivamente nei calcoli. Il tipo di correlazione dipende dall'opzione scelta nella Generale scheda nella finestra di dialogo. Per le correlazioni, le correlazioni significative sono visualizzate in grassetto.
Qual è il test di sfericità di Bartlett in PCA?

Vengono visualizzati i risultati del test di sfericità di Bartlett . Servono per rifiutare o meno l'ipotesi secondo la quale le variabili non sono correlate.

XLSTAT propone anche il test Kaiser - Meyer - Olkin (KMO).
Cosa sono gli autovalori e l'inerzia?

Gli autovalori sono la quantità di informazioni ( inerzia ) riassunte in ogni dimensione. La prima dimensione contiene la maggiore quantità di inerzia, seguita dalla seconda, quindi dalla terza e così via. XLSTAT visualizza gli autovalori in una tabella e in un grafico (scree plot). Il numero di autovalori è uguale al numero di autovalori non nulli.
Cosa sono i contributi?

I contributi (detti anche contributi assoluti) rappresentano la misura in cui ciascuna variabile ha contribuito alla costruzione dell'asse PCA corrispondente. Aiutano nell'interpretazione.
Come interpretare i coseni quadrati per le variabili

I coseni quadrati riflettono la rappresentazione qualità di di una variabile su un asse PCA. Come in altri metodi fattoriali, l'analisi del coseno quadrato viene utilizzata per evitare errori di interpretazione dovuti agli effetti di proiezione. Se il coseno al quadrato di una variabile associata ad un asse è basso, la posizione della variabile su questo asse non deve essere interpretata.
Cosa sono i punteggi dei fattori?

I punteggi dei fattori sono le coordinate delle osservazioni sulle dimensioni PCA. Sono visualizzati in una tabella XLSTAT. Se sono stati selezionati dati supplementari, questi vengono visualizzati alla fine della tabella.

Per quanto riguarda i risultati relativi alle variabili, XLSTAT visualizza i contributi delle osservazioni (cioè il loro contributo nella costruzione degli assi PCA) così come i coseni quadrati (cioè la loro qualità di rappresentazione sui diversi assi).
Risultati con rotazioni

Se è stata richiesta una rotazione, i risultati della rotazione vengono visualizzati con la matrice di rotazione applicata per prima ai carichi dei fattori. Seguono le percentuali di variabilità modificate associate a ciascuno degli assi coinvolti nella rotazione. Le coordinate, i contributi ei coseni delle variabili e le osservazioni dopo la rotazione sono visualizzati nelle tabelle seguenti.
Grafici XLSTAT per l'analisi dei componenti principali in Excel
Il cerchio di correlazione o grafico delle variabili

Il cerchio di correlazione (o grafico delle variabili) mostra le correlazioni tra i componenti e le variabili iniziali. Le variabili supplementari possono essere visualizzate anche sotto forma di vettori.

Cerchio di correlazione PCA di analisi dei componenti principali in Excel
Le tabelle delle osservazioni

I grafici delle osservazioni rappresentano le osservazioni nello spazio PCA.

Analisi dei componenti principali in Excel, grafico delle osservazioni

 
I Biplot

I biplot rappresentano le osservazioni e le variabili simultaneamente nel nuovo spazio. Anche qui le variabili supplementari possono essere rappresentate sotto forma di vettori. Esistono diversi tipi di biplot:

    Biplot di correlazione
    Biplot distanza
    Biplot simmetrico 

XLSTAT permette di scegliere il coefficiente la cui radice quadrata deve essere moltiplicata per le coordinate delle variabili. Questo coefficiente consente di regolare la posizione dei punti variabili nel biplot per renderlo più leggibile. Se impostato diverso da 1, la lunghezza dei vettori variabili non può più essere interpretata come deviazione standard (biplot di correlazione) o contributo (biplot di distanza).

 
Tutorial su come eseguire PCA in Excel utilizzando il software XLSTAT

Analisi dei componenti principali Biplot PCA in Excel

Questo tutorial ti aiuterà a eseguire un'analisi dei componenti principali all'interno di Excel utilizzando il software XLSTAT. 


# Agglomerative hierarchical clustering (AHC)
vedi dendrogramma



# togliere € o % ad un numero
df$currency <- gsub("\\€", "", df$currency)
df$percentages <- gsub("\\%", "", df$percentages)

# trasformare il formato della colonna da currency o percentage a numeric
df$currency <- as.numeric(df$currency)
df$percentages <- as.numeric(df$percentages)



https://bjnnowak.netlify.app/2021/09/15/r-pca-with-tidyverse/

![](https://bjnnowak.netlify.app/Tidy_Billboard.png)


https://bayesbaes.github.io/2021/01/28/PCA-tutorial.html  

![](https://bayesbaes.github.io/figures/PCA-tutorial/unnamed-chunk-13-1.png)
