### `1. Destrukturyzacja`

Jeśli wasza aplikacja opiera się na usługach zewnętrznych (tj. bazie danych, proxy nginx lub kolejce wiadomości), usługi te powinny teraz działać we własnym kontenerze. Oczywiście ten krok nie dotyczy tylko kontenerów; jest to typowy krok w przypadku każdej złożonej aplikacji. Aplikacja Birdwatch składa się z dwóch głównych komponentów. Aplikacja jest zbudowana przy użyciu frameworka Play i opiera się na indeksie ElasticSearch. Dlatego zaprojektuję architekturę z wykorzystaniem dwóch kontenerów: jednego dla aplikacji i jednego dla elastycznego wyszukiwania. Ta implementacja ma kilka zalet:

    ElasicSearch może być wykorzystany przez kilka aplikacji
    Każdy obraz może być niezależnie w wersji
    Serwery proxy mogą zostać dodane do architektury później

Alternatywą byłoby utworzenie jednego obrazu zawierającego wszystkie komponenty. Choć może się to wydawać prostsze, ma te same wady, co tworzenie monolitycznej czarnej skrzynki — wszelkie zmiany komponentu będą wymagały nowego obrazu całej aplikacji. Im większy obraz, tym większe pobieranie, co będzie miało negatywny wpływ na wdrożenie.

### `2. Znajdź wiarygodne obrazy podstawowe`

Wyszukiwanie w rejestrze Dockera dostarczy listę możliwych obrazów, na których można oprzeć aplikację. Trudność polega na określeniu, którego użyć. Społeczność może oznaczyć obraz gwiazdką, który może posłużyć do określenia popularności obrazu. Rejestr pokazuje również, ile razy obraz został pobrany, ale te pomiary są subiektywne, dlatego znajdują obrazy o następujących cechach:

    - czy obraz zawiera tag inny niż najnowszy?
    - czy obraz zawiera plik docker?
    - czy obrazy mają wspólną podstawę?

Używanie obrazu z tagiem zapewnia kontrolę wersji aplikacji. Najnowszy tag to wersja tocząca się, która konsekwentnie pobiera najnowszy obraz i dlatego może wprowadzić przełomową zmianę w aplikacji. Plik Dockerfile to kompletny przepis obrazu do sprawdzania poprawności całego kodu i działań zawartych w obrazie. Posiadanie wspólnego obrazu podstawowego usprawni cykl rozwoju, ponieważ będą one wykorzystywać pamięć podręczną obrazów. Przeczytaj artykuł Praca z pamięcią podręczną obrazów platformy Docker, aby dowiedzieć się więcej. Nasza aplikacja Birdwatch wymaga obrazu ElasticSearch w wersji 1.1 lub nowszej. Wyszukiwanie w Rejestrze hasła „elasticsearch” dało 236 wyników. Pierwszy wpis to zaufany obraz, ma plik Dockerfile, ale zawiera tylko najnowszy tag.

> Pamiętajcie też o opcji skanowania `docker scan image` w celu diagnostyki bod wzgledem podatnosci

### `3. Zarządzaj konfiguracją`

Aplikacje wymagają pewnej konfiguracji. Może to obejmować:

    - Poziomy i lokalizacja dzienników
    - Lokalizacja bazy danych i dane uwierzytelniające
    - Informacja bezpieczeństwa
    - Ustawienia aplikacji

Aplikacja działająca w kontenerze będzie wymagała tej samej konfiguracji. Te dane konfiguracyjne mogą być zapieczętowane w kontenerze; lub lepszym podejściem jest dostarczenie konfiguracji w czasie wykonywania. Obecnie istnieją trzy metody zapewniania konfiguracji środowiska wykonawczego.

### `4. Logging`

Obecną najlepszą praktyką w przypadku rejestrowania jest zapisywanie do standardowego wyjścia. Dzienniki dziennika i kontenera przechwytują te dane i można je przeglądać w przypadku awarii aplikacji. Ten temat jest daleki od zakończenia, wiele dyskusji krąży wokół zdolności kontenera do dostarczania danych logowania. Aplikacja Birdwatch korzystała z logowania systemowego i pliku dziennika, więc dostęp do danych dziennika nie wymagał żadnych zmian w bazie kodu.

`5.  Injecting Code`

Do utworzenia obrazu należy użyć pliku Dockerfile. Ten plik przedstawia wszystkie kroki wymagane do zbudowania obrazu. W tym artykule nie będziemy omawiać optymalizacji obrazów. Świetną dyskusję na temat optymalizacji obrazu można znaleźć tutaj. Kluczowym poleceniem dodawania kodu jest polecenie ADD. Posiada dwa parametry src i dest. Parametr src jest prawidłową ścieżką podczas budowania obrazu. Parametr dest jest ścieżką bezwzględną w kontenerze. Jeśli chcesz zignorować pliki lub katalogi podczas dodawania plików, umieść .dockerignore w katalogu głównym. Działa podobnie do pliku .gitignore. Po utworzeniu obrazu można go dodać do Docker Hub. Nasza aplikacja Birdwatch ma dość skomplikowany proces budowania. Każdy z frameworków UI musi być najpierw zbudowany, a następnie aplikacja może zostać zbudowana. Można to obsłużyć w skrypcie, który byłby wykonywany podczas kompilacji, ale do tej demonstracji zdecydowałem się uruchomić te kroki poza procesem budowania dockera i dodać tylko wynikowy skompilowany kod. Dodałem plik .dockerignore, aby ignorować katalogi .git i logs.

