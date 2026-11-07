# Jak dodać zmiany i stworzyć Pull Request (PR), to tez pisało AI

Krótki poradnik dla zespołu jak bezpiecznie wprowadzać zmiany do projektu i przesyłać je do repozytorium.

> ⚠️ **ZASADA NR 1: Nie pushujemy bezpośrednio do brancha `main`!**  
> Wszystkie zmiany zgłaszamy w formie **Pull Requesta (PR)**. Piotr sprawdzi kod/notatki i bezpiecznie zmerguje je do głównej gałęzi (`main`). (xd)

---

## 🛠️ Instrukcja krok po kroku (w terminalu / VS Code)

### Krok 0: Konfiguracja Git i logowanie do GitHuba (tylko za pierwszym razem)

Jeśli robisz to pierwszy raz na swoim komputerze, musisz się przedstawić Gitowi oraz połączyć swoje konto GitHub.

#### 1. Ustawienie podpisu:
```bash
git config --global user.name "Twoje Imie i Nazwisko"
git config --global user.email "twoj_email_do_githuba@example.com"
```

#### 2. Logowanie do GitHuba (Hasło do konta NIE działa – GitHub wymaga Tokena lub CLI):

Wybierz **jedną** z dwóch opcji:

##### Opcja A: Personal Access Token (PAT) – najczęstsza metoda
GitHub od kilku lat nie pozwala wpisywać zwykłego hasła do konta w terminalu. Wymaga wygenerowania tzw. **Tokena (PAT)**:
1. Zaloguj się na [github.com](https://github.com).
2. W prawym górnym rogu kliknij swój awatar ➔ **Settings**.
3. Na samym dole menu po lewej kliknij **Developer settings** ➔ **Personal access tokens** ➔ **Tokens (classic)**.
4. Kliknij **Generate new token** ➔ **Generate new token (classic)**.
5. Wpisz nazwę (np. *Laptop Studia*), zaznacz uprawnienie **`repo`** (dostęp do repozytoriów).
6. Zjedź na dół i kliknij **Generate token**.
7. **Skopiuj wygenerowany token** (zaczyna się od `ghp_...`). *Zapisz go sobie, bo po odświeżeniu strony już go nie zobaczysz!*
8. Gdy podczas `git push` lub `git clone` terminal zapyta Cię o dane:
   * **Username:** wpisz swój login na GitHubie.
   * **Password:** wklej ten **skopiowany token** (znaki mogą się nie wyświetlać – to normalne, po prostu wklej `Ctrl+V` / `Cmd+V` i kliknij `Enter`).

> 💡 **Tip:** Aby nie wklejać tokena za każdym razem, zapisz go w systemie:
> * Na macOS: `git config --global credential.helper osxkeychain`
> * Na Windows: `git config --global credential.helper wincred`

---

##### Opcja B: Przez GitHub CLI (`gh`) – automatycznie i bez kopiowania tokenów
Jeśli wolisz zainstalować oficjalne narzędzie od GitHuba:
1. Zainstaluj GitHub CLI:
   * **macOS:** `brew install gh`
   * **Windows:** `winget install --id GitHub.cli` (lub pobierz instalator z [cli.github.com](https://cli.github.com))
2. Wpisz w terminalu:
   ```bash
   gh auth login
   ```
3. Wybierz: `GitHub.com` ➔ `HTTPS` ➔ `Yes` (autoryzuj Git) ➔ `Login with a web browser`.
4. Wpisz wyświetlony kod jednorazowy w przeglądarce i zatwierdź. Gotowe!

---

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
