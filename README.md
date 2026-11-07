# Tak, tą instrukcję pisał agent, bo pewnie nie kazdy ma UV

> 📢 **Dla zespołu (jak pracować z projektem):**  
> Zanim zaczniesz wprowadzać zmiany, przeczytaj: **👉 [Poradnik: Jak dodać zmiany i stworzyć Pull Request](JAK_DODAC_ZMIANY.md)**.  
> **Ważne:** Nie pushujemy bezpośrednio do brancha `main` – pracujemy na własnych gałęziach i tworzymy PR-y, a Piotr je później zmerguje!

## Analiza wydajności: DuckDB vs Pandas na dużym zbiorze danych (2 GB / ~67M wierszy)

Projekt laboratoryjny porównujący wydajność podejścia **Lazy Evaluation** (DuckDB) oraz **Eager Evaluation** (Pandas) przy przetwarzaniu dużego zbioru danych `AdventureWorks` (~1.8 GB w formacie Parquet, 66.7 mln rekordów).

---

## ⚠️ Ważna uwaga dotycząca danych (`.parquet`)

Zbiór danych `SalesOrderDetail_upsampled_2GB.parquet` waży około **1.8 GB** i ze względu na limity platformy GitHub (maksymalny rozmiar pliku: 100 MB) **nie znajduje się w repozytorium** (jest dodany do `.gitignore`).

> **Przed uruchomieniem notatnika:**  
> Upewnij się, że plik `SalesOrderDetail_upsampled_2GB.parquet` znajduje się w głównym katalogu tego repozytorium (obok pliku `duckdb_goated.ipynb`).

---

## 🚀 Instrukcja uruchomienia projektu (Krok po kroku)

Wybierz jedną z dwóch metod instalacji środowiska:

---

### Opcja A: Z użyciem `uv` (Rekomendowane, najszybsze)

[`uv`](https://github.com/astral-sh/uv) to nowoczesny, błyskawiczny menedżer pakietów i środowisk Python.

#### 1. Instalacja `uv` (jeśli jeszcze nie posiadasz):

- **macOS / Linux:**
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  # lub przez Homebrew (macOS):
  brew install uv
  ```
- **Windows (PowerShell):**
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```

#### 2. Klonowanie i przejście do repozytorium:

```bash
git clone https://github.com/ibtyog/duckdb-lazy-evaluation.git
cd duckdb-lazy-evaluation
```

#### 3. Automatyczna synchronizacja środowiska:

`uv` sam pobierze odpowiednią wersję Pythona oraz zainstaluje wszystkie wymagane pakiety z `uv.lock`:

```bash
uv sync
```

---

### Opcja B: Bez użycia `uv` (Tradycyjny Python + `venv` + `pip`)

Jeśli wolisz klasyczne podejście ze standardowym Pythonem (wymagany Python w wersji 3.10, 3.11, 3.12 lub 3.13):

#### 1. Klonowanie i przejście do repozytorium:

```bash
git clone https://github.com/ibtyog/duckdb-lazy-evaluation.git
cd duckdb-lazy-evaluation
```

#### 2. Utworzenie środowiska wirtualnego:

```bash
python3 -m venv .venv
```

_(Na Windows w PowerShellu wpisz `python -m venv .venv`)_

#### 3. Aktywacja środowiska:

- **macOS / Linux:**
  ```bash
  source .venv/bin/activate
  ```
- **Windows (PowerShell):**
  ```powershell
  .venv\Scripts\Activate.ps1
  ```
- **Windows (Command Prompt `cmd`):**
  ```cmd
  .venv\Scripts\activate.bat
  ```

#### 4. Instalacja zależności z pliku `requirements.txt`:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

---

## 📓 Jak odpalić i wykonać notatnik (`duckdb_goated.ipynb`)

Masz do wyboru dwa wygodne sposoby:

### Sposób 1: W edytorze kodu (VS Code / Cursor / PyCharm) – **NAJWYGODNIEJSZY**

1. Otwórz folder projektu w **VS Code** lub **Cursorze**.
2. Zainstaluj w edytorze rozszerzenia: **Python** oraz **Jupyter**.
3. Otwórz plik [duckdb_goated.ipynb](duckdb_goated.ipynb).
4. W prawym górnym rogu notatnika kliknij **Select Kernel** (Wybierz jądro).
5. Wybierz **Python Environments...** i wskaż środowisko `.venv` znajdujące się w tym folderze.
6. Uruchamiaj komórki przyciskiem ▶️ lub kliknij **Run All**.

---

### Sposób 2: Przez przeglądarkę (Jupyter Notebook / JupyterLab) - nie polecam, Piotr

- **Jeśli korzystasz z `uv`:**
  ```bash
  uv run --with notebook jupyter notebook
  ```
- **Jeśli korzystasz ze standardowego `venv` (po jego aktywacji):**
  ```bash
  pip install notebook
  jupyter notebook
  ```
  W oknie przeglądarki kliknij plik `duckdb_goated.ipynb`.

---

## 💡 O czym warto pamiętać podczas uruchamiania testów:

1. **Test DuckDB (KROK 1–3):**
   - Wykonuje się błyskawicznie.
   - Dzięki leniwej ewaluacji zużycie pamięci RAM prawie nie wzrasta (DuckDB wczytuje z dysku tylko potrzebną kolumnę, ignorując resztę).
2. **Test Pandas (Eager Evaluation):**
   - Pandas próbuje załadować do pamięci RAM wszystkie 66.7 miliona wierszy i 11 kolumn.
   - Może to zająć od kilkunastu do kilkudziesięciu sekund i zużyć **ponad 5–8 GB RAM**.
   - Jeśli Twój komputer ma mniej niż 16 GB pamięci RAM, komórka może zgłosić błąd `MemoryError (OOM)` – **jest to zachowanie zamierzone**, które demonstruje problem wydajnościowy tradycyjnych bibliotek DataFrame.
3. **Wykresy końcowe:**
   - Ostatnia komórka generuje wykresy porównawcze zużycia RAM oraz czasu wykonania.

---

## 📁 Zawartość repozytorium

| Plik / Folder         | Przeznaczenie                                                |
| :-------------------- | :----------------------------------------------------------- |
| `duckdb_goated.ipynb` | Główny notatnik Jupyter z kodem eksperymentu i porównaniem   |
| `pyproject.toml`      | Konfiguracja projektu i deklaracja zależności                |
| `uv.lock`             | Dokładne wersje zależności zablokowane dla `uv`              |
| `requirements.txt`    | Lista zależności dla użytkowników klasycznego `pip`          |
| `.python-version`     | Wskazana wersja interpretera Pythona                         |
| `assets/`             | Grafiki i memy wykorzystywane w notatniku                    |
| `.gitignore`          | Reguły ignorowania plików tymczasowych i ciężkich baz danych |
| `JAK_DODAC_ZMIANY.md` | Instrukcja tworzenia gałęzi i zgłaszania Pull Requestów      |
| `README.md`           | Niniejsza dokumentacja i instrukcja uruchomienia             |
