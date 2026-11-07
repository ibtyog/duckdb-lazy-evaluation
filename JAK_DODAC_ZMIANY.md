# Jak dodać zmiany i stworzyć Pull Request (PR), to tez pisało AI

Krótki poradnik dla zespołu jak bezpiecznie wprowadzać zmiany do projektu i przesyłać je do repozytorium.

> ⚠️ **ZASADA NR 1: Nie pushujemy bezpośrednio do brancha `main`!**  
> Wszystkie zmiany zgłaszamy w formie **Pull Requesta (PR)**. Piotr sprawdzi kod/notatki i bezpiecznie zmerguje je do głównej gałęzi (`main`).

---

## 🛠️ Instrukcja krok po kroku (w terminalu / VS Code)

### Krok 1: Pobierz najnowszy stan projektu

Zanim zaczniesz cokolwiek robić, upewnij się, że masz aktualną wersję z `main`:

```bash
git checkout main
git pull origin main
```

---

### Krok 2: Stwórz własną gałąź (branch) dla swojego zadania

Nigdy nie pracuj na `main`. Stwórz branch o nazwie opisującej Twoje zadanie (np. nazwa ficzeru):

```bash
# Przykłady nazw gałęzi:
git checkout -b feat/nowe-query
# lub
git checkout -b cokolwiektaknaprawde
# lub
git checkout -b siemanko
```

Polecenie `-b` tworzy nową gałąź i od razu na nią przełącza.

---

### Krok 3: Wprowadź swoje zmiany

- Zmodyfikuj notatnik `duckdb_goated.ipynb`, dodaj pliki, zmień opisy itp.
- **Pamiętaj:** Nie wrzucaj do gita żadnych ciężkich plików danych (`.parquet`, `.db`). Plik `.gitignore` powinien je blokować, ale zawsze warto sprawdzić przed commitem.

---

### Krok 4: Sprawdź stan i dodaj zmienione pliki

Sprawdź, jakie pliki zostały zmodyfikowane:

```bash
git status
```

Dodaj zmienione pliki do zapisu (stagingu):

```bash
git add duckdb_goated.ipynb
# lub jeśli dodałeś/zmieniłeś tylko właściwe pliki:
git add .
```

---

### Krok 5: Zrób commit z czytelnym opisem

Zatwierdź swoje zmiany z krótką informacją o tym, co zostało zrobione:

```bash
git commit -m "Dodanie nowego zapytania biznesowego i wnioskow"
# lub
git commit -m "tez cokolwiek mozesz tu napisac"

```

---

### Krok 6: Wypchnij branch na GitHuba

Wyślij swoją gałąź do zdalnego repozytorium:

```bash
git push -u origin NAZWA_TWOJEJ_GAŁEZI
```

_(np. `git push -u origin feature/zapytanie-kinga`)_

---

### Krok 7: Utwórz Pull Request na GitHubie (obejdzie sie bez tego, ale spoko jakby było)

1. Wejdź na stronę repozytorium na **GitHubie**.
2. Na samej górze pojawi się żółto-zielony pasek z Twoim branchem i przyciskiem **`Compare & pull request`** – kliknij go.
3. Wpisz krótki tytuł i opis: co dodałeś/zmieniłeś.
4. Kliknij zielony przycisk **`Create pull request`**.
5. Gotowe! **Nie klikaj `Merge`** – daj znać Piotrowi, a on zweryfikuje zmiany i zmerguje je do `main`.

---

## 🔄 Co zrobić po tym, jak PR zostanie zmergowany?

Gdy Piotr zmerguje Twój Pull Request, zaktualizuj swój lokalny komputer:

```bash
git checkout main
git pull origin main
```

I przed kolejnym zadaniem ponownie utwórz nowy branch (wróć do Kroku 2).
