# PHM_North_America_2024__A2

Questo repository fornisce una soluzione completa alla **PHM North America 2024 Conference Data Challenge**, con un workflow end-to-end implementato all’interno di un singolo notebook Google Colab.

---

## 📖 Descrizione della Challenge

La PHM North America 2024 Data Challenge è un anomaly detection su motori turboshaft da elicottero basata su dati operativi. L’obiettivo ufficiale è:

1. **Calcolare il _Torque Margin_**  
   Per ogni punto operativo, il _Torque Margin_ è definito come
   
   $100 \times \frac{\text{Torque Measured} - \text{Torque Target}}{\text{Torque Target}}$
   
   e va fornito in output.  
3. **Stimare una PDF attorno ai valori di _Torque Margin_**  
   Il punteggio di regressione si ottiene valutando la densità di probabilità del valore reale all’interno della PDF scelta (Normal, Laplace, Cauchy, Logistic o Uniforme).  
4. **Classificare lo stato _healthy_ vs. _faulty_**  
   Occorre inviare per ogni osservazione:
   - la label predetta (0=healthy, 1=faulty),  
   - un _confidence score_ nell’intervallo [0,1].
     
   Il modello viene penalizzato soprattutto per i falsi negativi ad alta confidenza, per riflettere il rischio di trascurare un guasto.

Tutti i dettagli sul task e i dataset ufficiali (training, test, validation) sono disponibili qui:  
https://data.phmsociety.org/phm2024-conference-data-challenge/

---

## 🚀 Struttura del Repository

├── challenge.ipynb # Notebook Colab con l’intera implementazione

├── PHM_North_America_2024--A2.pdf # Relazione finale

└── README.md # Questo file di istruzioni


Tutto il codice (preprocessing, regressione, PDF fitting, classificazione, analisi dei risultati) è contenuto in **Challenge.ipynb**.

---

## ⚙️ Setup e Esecuzione

1. **Prepara il dataset**  
   - Scarica il dataset di **Training** dal sito [PHM2024](https://data.phmsociety.org/phm2024-conference-data-challenge/).  
   - Carica l’intera cartella `TrainingDataset` (con i CSV forniti) in Google Drive sotto:  
     ```
     ~/MyDrive/PHM2024/Dataset/TrainingDataset/
     ```

2. **Apri il notebook in Colab**  
   - Vai su [colab.research.google.com](https://colab.research.google.com)  
   - Seleziona “File → Apri notebook” e carica `Challenge.ipynb`.

3. **Esegui tutte le celle**  
   Colab installerà automaticamente le librerie necessarie e lancerà:
   - Caricamento dati da `/content/drive/MyDrive/PHM2024/Dataset/TrainingDataset/`
   - Preprocessing & feature engineering
   - Regressione su `trq_target`
   - Calcolo del `trq_margin_pred`
   - Fitting delle PDF sui residui + KS-Test
   - Classificazione con stacking ensemble + confidence score
   - Analisi dei falsi negativi ad alta confidenza
   - Salvataggio di modelli, grafici e report in Drive

4. **Verifica gli output**  
   Alla fine del run, in `drive/MyDrive/PHM2024/Outputs/` troverai:
   - Modelli serializzati (`.pkl`)
   - Grafici (scatter plots, PDF fits, confusion matrix)
   - Report testuali e CSV con risultati e configurazioni
  
---

## Contributors

| Contributor Name      | GitHub                                  |
|:----------------------|:----------------------------------------|
| ⭐ **Biccheri Emanuele**  | [Click here](https://github.com/Emanuele1087650) |
| ⭐ **Fares Emanuele**   | [Click here](https://github.com/AlessioGiacconi) |
| ⭐ **Giacconi Alessio**   | [Click here](https://github.com/FaresEmanuele) |

