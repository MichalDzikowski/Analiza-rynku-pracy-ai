# Analiza-rynku-pracy-ai

Projekt ten stanowi szczegółową analizę zbioru danych "AI Workforce Data Overview" (Kaggle), obejmującego 2000 ofert pracy z sektora sztucznej inteligencji. Analiza skupia się na czyszczeniu danych (Data Cleaning), inżynierii cech (Feature Engineering) oraz analizie tekstu w celu zidentyfikowania kluczowych trendów w zatrudnieniu i wynagrodzeniach w branży AI.

Źródło: https://www.kaggle.com/datasets/minahilfatima12328/ai-workforce-data-overview

## 1. Cel Projektu

Głównym celem projektu było przekształcenie surowych, "brudnych" danych z ofert pracy w konkretne, strategiczne wnioski, odpowiadając na następujące pytania:
1.  Jakie umiejętności są najbardziej poszukiwane przez pracodawców w branży AI?
2.  Które branże** (`industry`) najaktywniej rekrutują i oferują najlepsze wynagrodzenie?
3.  Jak poziom doświadczenia (`Entry`, `Mid`, `Senior`) i stanowisko (`job_title`) wpływają na "widełki" wynagrodzeń?
4.  Czy wielkość firmy (`Small`, `Medium`, `Large`) jest  czynnikiem wpływającym na wysokość pensji?

Analiza została przeprowadzona w notatniku Jupyter i składała się z trzech głównych etapów:

### Etap I: Czyszczenie Danych i Inżynieria Cech

1.  **Wczytanie Danych:** Załadowanie pliku `ai_job_market.csv` do `pandas`.
2.  **Czyszczenie Pensji:** Kolumna `salary_range_usd` (np. "92860-109598") została **rozdzielona (`.str.split()`)** na dwie nowe kolumny: `min_salary_usd` i `max_salary_usd`. Obie zostały przekonwertowane na typ numeryczny.
3.  **Inżynieria Cech:** Stworzono nową, kluczową metrykę `avg_salary_usd` (średnia z widełek płacowych), która była podstawą do wszystkich późniejszych analiz zarobków.
4.  **Czyszczenie Dat:** Kolumna `posted_date` została przekonwertowana z `object` na poprawny format `datetime`.

### Etap II: Analiza Tekstu (Wymagane Umiejętności)

To był kluczowy element analizy. Zamiast agregować gotowe kategorie, dane zostały wydobyte z surowego tekstu.
1.  Zdefiniowano listę 20+ kluczowych umiejętności (np. `Python`, `SQL`, `AWS`, `PyTorch`, `TensorFlow`, `Power BI` itd.).
2.  Kolumna `skills_required` została przeszukana (`.str.contains()`) dla każdej umiejętności z listy.
3.  Zliczono wystąpienia, aby stworzyć ranking najbardziej pożądanych kompetencji na rynku.

### Etap III: Analiza Eksploracyjna (EDA)

1.  Wykorzystano agregacje (`.groupby()`, `.value_counts()`) do obliczenia mediany `avg_salary_usd` w podziale na:
    * `industry` 
    * `job_title` 
    * `experience_level`
    * `company_size` 
2.  Stworzono interaktywne wizualizacje (wykresy słupkowe i pudełkowe) przy użyciu `Altair`.

## 3. Główne Wnioski Analityczne

### Wniosek 1: Dominacja C++ i R
Analiza tekstu przyniosła zaskakujące wyniki. W przeciwieństwie do powszechnych oczekiwań, najbardziej poszukiwanymi umiejętnościami w tym zbiorze danych nie są Python czy SQL. Zamiast tego, dwie umiejętności absolutnie zdominowały rynek, pojawiając się w ponad 80% wszystkich ofert:
1.  **C++** (1816 wystąpień)
2.  **R** (1769 wystąpień)

Dopiero daleko za nimi znajduje się duża, gęsta grupa technologii AI, chmurowych i analitycznych, z których prawie wszystkie mają bardzo podobną liczbę wystąpień (w okolicach 400-450). W tej drugiej grupie znajdują się m.in. **TensorFlow** (452), **Excel** (432), **Pandas** (427), a także **SQL** (408), **AWS** (404) i sam **Python** (402).

**Implikacja:** Ten zbiór danych jest prawdopodobnie silnie przechylony w stronę specyficznych ról, takich jak Quant Researcher (badacz ilościowy w finansach) lub inżynieria wysokiej wydajności (HPC), gdzie `C++` jest kluczowy dla szybkości obliczeń, a `R` jest tradycyjnie silny w modelowaniu statystycznym.

<img width="858" height="417" alt="top_ai_skills" src="https://github.com/user-attachments/assets/fcfd0c52-f357-4aba-9dbe-cb63e99d2e87" />

### Wniosek 2: Rozkład Zarobków (Stanowisko i Doświadczenie)
Analiza zarobków (na podstawie obliczonej `avg_salary_usd`) pokazała wyraźne trendy:
* **Wg Stanowiska:** Wśród 10 najpopularniejszych ról, stanowiska związane bezpośrednio z modelowaniem (np. "Machine Learning Engineer") oferują wyższą medianę pensji niż bardziej ogólne role analityczne.
* **Wg Doświadczenia:** Wykresy pudełkowe udowodniły, że nie ma dużego skoku finansowy między poziomem `Mid` a `Senior` 
<img width="869" height="471" alt="salary_vs_job_title" src="https://github.com/user-attachments/assets/9568c3b1-cf83-4638-8662-5a0da926eda6" />

<img width="669" height="383" alt="salary_vs_experience" src="https://github.com/user-attachments/assets/590335a2-7942-4b46-967c-c375c5b26a15" />

### Wniosek 3: Gdzie Płyną Pieniądze (Branże i Wielkość Firmy)
* **Wielkość Firmy:** Duże firmy (`Large`) oferują  **najwyższą medianę** wynagrodzeń, wyprzedzając firmy średnie i startupy. Sugeruje to, że w branży AI korporacje są w stanie zaoferować najwięcej, prawdopodobnie ze względu na większą skalę projektów i większe budżety.
<img width="569" height="382" alt="salary_vs_company_size" src="https://github.com/user-attachments/assets/7db8f8cf-7bf0-4fde-bb30-690dff3f8914" />


## 4. Wykorzystane Technologie

* **Język:** Python 3.x
* **Środowisko:** Jupyter Notebook
* **Analiza Danych:**
    * **Pandas** 
* **Wizualizacja Danych:**
    * **Altair** 
