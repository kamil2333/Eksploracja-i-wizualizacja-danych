# Segmentacja klientów kart kredytowych

Akademicki projekt z obszaru data science skupiający się na automatycznej segmentacji klientów i wykrywaniu anomalii przy użyciu technik uczenia maszynowego bez nadzoru (unsupervised learning) oraz redukcji wymiarowości.

## O projekcie
Aby rozwiązać problem segmentacji klientów i odkryć ukryte wzorce zakupowe, zbudowano i poddano ewaluacji różne algorytmy klasteryzacji (K-Means, Agglomerative Hierarchical, DBSCAN) przy użyciu biblioteki **Scikit-learn**.

Proces analizy danych został podzielony na trzy główne etapy:
* **Preprocessing danych i EDA** - obsługa braków danych (imputacja medianą), usuwanie duplikatów, transformacja logarytmiczna silnie skośnych zmiennych finansowych oraz standaryzacja (StandardScaler). Wykorzystano inżynierię cech (Feature Engineering), aby stworzyć nowe metryki biznesowe (np. wskaźnik wykorzystania limitu).
* **Redukcja wymiarowości** - zastosowanie algorytmu PCA (wyjaśniającego 80% wariancji danych) oraz t-SNE do wizualizacji złożonych, wielowymiarowych struktur w przestrzeni 2D.
* **Klasteryzacja i ewaluacja** - wyznaczenie optymalnej liczby klastrów za pomocą metody łokciowej (Elbow Method), wskaźnika sylwetki (Silhouette Score) oraz Gap Statistic.

## Zidentyfikowane Segmenty Klientów
Na podstawie algorytmu K-Means (k=4), zbiór danych został z powodzeniem podzielony na cztery odrębne profile biznesowe:

| Klaster | Nazwa Segmentu | Kluczowe Cechy |
|:---:|:---|:---|
| **0** | **Aktywni na raty** | Wysokie zakupy ratalne (527), niska gotówka, wysoka częstotliwość zakupów (0.71). |
| **1** | **Użytkownicy gotówki** | Najwyższe wypłaty gotówkowe (2195), prawie zerowe zakupy, wysoki bilans na koncie. |
| **2** | **Premium Shoppers** | Najwyższe ogólne zakupy (2338), najwyższy limit kredytowy, wysoka aktywność (34 trx/klient). |
| **3** | **Jednorazowi kupujący** | Prawie wyłącznie zakupy jednorazowe, umiarkowany profil ryzyka. |

## Technologie
* Python
* Pandas & NumPy (Przetwarzanie danych)
* Scikit-learn (Machine Learning: K-Means, PCA, Isolation Forest)
* Matplotlib & Seaborn (Wizualizacja danych)

## Wyniki modeli
Algorytmy zostały ocenione za pomocą wewnętrznych metryk klasteryzacji. Metody K-Means oraz klasteryzacji hierarchicznej dostarczyły najbardziej stabilnych i łatwych do interpretacji wyników dla 4 klastrów. Poniżej znajdują się szczegółowe metryki oraz wykresy ewaluacyjne.

### Metryki Ewaluacyjne
| Algorytm | Silhouette Score (↑) | Davies-Bouldin Index (↓) | Wykryte Klastry |
|-----------|----------------------|--------------------------|-------------------|
| **K-Means** | 0.3621 | 1.1591 | 4 (Zadane) |
| **Hierarchical** | 0.3630 | 1.1820 | 4 (Zadane) |
| **DBSCAN** | 0.1472 | 2.0035 | 2 (Automatyczne) |


## Jak uruchomić projekt lokalnie
1. Sklonuj to repozytorium.
2. Pobierz zbiór danych z [Kaggle](https://www.kaggle.com/datasets/arjunbhasin2013/ccdata) i umieść plik `CC GENERAL.csv` w głównym folderze projektu.
3. Zainstaluj wymagane pakiety bibliotek:
   ```bash
   pip install -r requirements.txt