# NOTES ABOUT THE PROJECT

### 9 Nov. 2023 - DB
Penso ci siano problemi nel calcolo della width/height dei prodotti che sono stati riconosciuti, perché, ad esempio, nell'immagine e5, STEP_A, viene trovato il prodotto 25 ma l'altezza calcolata (in pixel) è maggiore dell'altezza dell'immagine. Non so se ci sia un problema nel calcolo, o semplicemente non è stato fatto un corretto tuning dei parametri (flann, sift...): in particolare magari vengono scartati troppi match nella funzione find_match (lista -good-) <- Lowe's ratio test.

Non so se ci siano problemi nel calcolo del centro del prodotto, in quanto non ho controllato.

Non ho ben capito se è richiesto solo l'output testuale, o anche l'immagine della scena con le varie bounding box. Nell'ultimo caso, non ho implementato la stampa della bounding box sulla scena. Quest'ultima feature, anche se FORSE non richiesta dal testo, potrebbe essere utile per controllare che i prodotti vengano riconosciuti bene.


### 10 Nov. 2023 - DB
Ho fatto refactoring del codice per lo step A, creando un oggetto Simple_Finder che effettua la ricerca di multipli prodotti in una scena, come da specifiche.

Sembra funzionare perfettamente eccetto per un caso: confonde i prodotti 1 e 11, perché sostanzialmente uguali eccetto per una piccola scritta e per il colore. Possibili idee, non so se perseguibili, sono:

* cercare di mantenere la feature della piccola scritta (cambiando parametri di sift/flann) che è l'unica differenza (in scala di grigi) tra le due scatole.
* valutare se si può fare un match in base al colore -> controllare se i descrittori sift possono mantenere l'informazione del colore.