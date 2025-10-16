# Pytorch Neural Network testen

## 🧠 Wat doet deze code eigenlijk?
Je code bouwt, traint en test een neuraal netwerk dat leert om bloemen te herkennen op basis van hun eigenschappen (lengte en breedte van bloem en kelk).
Het netwerk probeert dus te raden of een bloem een:
- **Setosa (0),** 
- **Versicolor (1), of** 
- **Virginica (2) is.** 

### 🔹 Stap 1: De data
Het Iris-dataset bevat 150 bloemen met deze kolommen:
sepal.length	sepal.width	petal.length	petal.width	variety
5.1	3.5	1.4	0.2	Setosa
6.2	2.8	4.8	1.8	Virginica
👉 Jij hebt de tekstlabels omgezet in cijfers (0, 1, 2) zodat het model ermee kan rekenen.
### 🔹 Stap 2: Het netwerk (de “hersenen”)
Je model heeft drie lagen:
```
4 → 8 → 9 → 3
```
- **4 invoer-neuronen: voor de 4 bloemkenmerken**
- **8 neuronen in de eerste verborgen laag**
- **9 neuronen in de tweede verborgen laag**
- **3 uitvoer-neuronen: één voor elke bloemsoort**
Elke verbinding tussen twee lagen heeft gewichten (weights).
Die gewichten bepalen hoe belangrijk elk kenmerk is bij het bepalen van de bloemsoort.
Aanvankelijk zijn die gewichten willekeurig.
### 🔹 Stap 3: De “forward pass”
```
y_pred = model(X_train)
```
Het netwerk krijgt de trainingsdata, berekent voorspellingen (zoals "ik denk dat dit een 0 is") en geeft die door aan de loss-functie.
### 🔹 Stap 4: De “loss” meten
loss = criterion(y_pred, y_train)
De loss (foutwaarde) geeft aan hoe slecht de voorspellingen zijn.
Een hoge loss = veel fouten, een lage loss = beter model.
In het begin is de loss groot, want het model raadt maar wat.
🔹 Stap 5: Backpropagation (leren)
optimizer.zero_grad()
loss.backward()
optimizer.step()
Dit is waar het leren gebeurt:
loss.backward() → rekent uit hoeveel schuld elk gewicht heeft aan de fout.
optimizer.step() → past die gewichten een klein beetje aan (in de richting die de fout verlaagt).
Dit proces wordt 100 keer herhaald (dat zijn de 100 epochs).
Bij elke ronde (epoch) wordt de loss kleiner — het netwerk leert dus van zijn fouten!
🔹 Stap 6: De grafiek
plt.plot(range(epochs), losses)
Hiermee zie je visueel dat de loss in de loop van de epochs daalt.
Dat betekent:
📉 De fout van het netwerk neemt af
📈 Het netwerk wordt beter in voorspellen
🔹 Alles in één stuk code?
Ja ✅
Al deze losse cellen kun je gewoon in één groot Python-script zetten.
In Colab is het handig om het in stappen te doen (om makkelijk te debuggen),
maar in principe kun je dit allemaal in één cell doen — het resultaat is hetzelfde.
🧩 Visuele uitleg
Hier is een eenvoudige schematische weergave van wat er gebeurt:
         Invoer (X)
     ┌─────────────────┐
     │ sepal_length    │
     │ sepal_width     │
     │ petal_length    │
     │ petal_width     │
     └─────────────────┘
               │
               ▼
         [ Hidden Layer 1 ]
         8 neuronen (met ReLU)
               │
               ▼
         [ Hidden Layer 2 ]
         9 neuronen (met ReLU)
               │
               ▼
         [ Output Layer ]
         3 neuronen (scores voor 3 bloemsoorten)
               │
               ▼
         Vergelijk met echte labels (y_train)
               │
               ▼
         Bereken fout (loss)
               │
               ▼
     Backpropagation → Gewichten aanpassen
               │
               ▼
         Loss daalt per epoch (model leert)
En de grafiek aan het einde:
Loss/Error
│\
│ \
│  \
│   \
│    \__
│_______\___________ Epochs →
Hier zie je de fout dalen — het bewijs dat je netwerk leert.
💡 In gewone woorden
Een neuraal netwerk leert net zoals mensen leren:
Je maakt in het begin veel fouten (hoge loss),
Je kijkt wat er fout ging (backpropagation),
Je past jezelf een beetje aan (optimizer),
Na een tijdje word je beter (loss daalt).
