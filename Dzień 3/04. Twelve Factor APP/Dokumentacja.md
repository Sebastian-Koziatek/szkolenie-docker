# Dwunasto składnikowa aplikacja

## 1.  Baza kodów
>Jedna baza kodu śledzona w ramach kontroli wersji, wiele wdrożeń

Aplikacja dwunastoskładnikowa jest zawsze śledzona w systemie kontroli wersji, takim jak Git, Mercurial lub Subversion. Kopia bazy danych śledzenia wersji jest znana jako repozytorium kodu, często skracane do repozytorium kodu lub po prostu repozytorium.

Baza kodu to dowolne pojedyncze repozytorium (w scentralizowanym systemie kontroli wersji, takim jak Subversion) lub dowolny zestaw repozytoriów, które współdzielą główne zatwierdzenie (w zdecentralizowanym systemie kontroli wersji, takim jak Git).

Jedna baza kodu mapuje do wielu wdrożeń

Zawsze istnieje korelacja jeden do jednego między bazą kodu a aplikacją:

    Jeśli istnieje wiele baz kodu, nie jest to aplikacja – to system rozproszony. Każdy składnik w systemie rozproszonym jest aplikacją, a każdy z nich może indywidualnie spełniać wymogi dwunastoczynnikowe.
    Wiele aplikacji udostępniających ten sam kod jest naruszeniem dwunastoczynnikowego. Rozwiązaniem jest tutaj rozłożenie kodu współdzielonego na biblioteki, które można dołączyć za pomocą menedżera zależności.

Istnieje tylko jedna baza kodu na aplikację, ale będzie wiele wdrożeń aplikacji. Wdrożenie to działające wystąpienie aplikacji. Jest to zazwyczaj lokacja produkcyjna i co najmniej jedna lokacja pomostowa. Ponadto każdy programista ma kopię aplikacji uruchomioną w swoim lokalnym środowisku programistycznym, z których każde również kwalifikuje się jako wdrożenie.

Baza kodu jest taka sama we wszystkich wdrożeniach, chociaż w każdym wdrożeniu mogą być aktywne różne wersje. Na przykład deweloper ma pewne zatwierdzenia, które nie zostały jeszcze wdrożone do przemieszczania; Staging ma pewne zatwierdzenia, które nie zostały jeszcze wdrożone w środowisku produkcyjnym. Ale wszystkie mają tę samą bazę kodu, dzięki czemu można je zidentyfikować jako różne wdrożenia tej samej aplikacji.

___

## 2. Zależności 
> Jawnie deklaruj i izoluj zależności

Większość języków programowania oferuje system pakowania do dystrybucji bibliotek pomocniczych, takich jak CPAN dla Perla lub Rubygems dla Ruby. Biblioteki instalowane za pośrednictwem systemu pakietów mogą być instalowane w całym systemie (znane jako „pakiety witryny”) lub ograniczone do katalogu zawierającego aplikację (znane jako „dostawca” lub „sprzedaż wiązana”).

Aplikacja dwunastoskładnikowa nigdy nie polega na niejawnym istnieniu pakietów systemowych. Deklaruje wszystkie zależności, kompletnie i dokładnie, za pomocą manifestu deklaracji zależności. Ponadto podczas wykonywania używa narzędzia do izolacji zależności, aby zapewnić, że żadne niejawne zależności nie „wyciekają” z otaczającego systemu. Pełna i jawna specyfikacja zależności jest stosowana jednolicie zarówno do produkcji, jak i programowania.

Na przykład Bundler for Ruby oferuje format manifestu `Gemfile` do deklarowania zależności i `Bundle Exec` do izolacji zależności. W Pythonie są dwa oddzielne narzędzia do tych kroków – Pip służy do deklaracji, a Virtualenv do izolacji. Nawet C ma Autoconf dla deklaracji zależności, a statyczne linkowanie może zapewnić izolację zależności. Bez względu na łańcuch narzędzi, deklaracja zależności i izolacja muszą być zawsze używane razem – tylko jedno lub drugie nie wystarcza do spełnienia dwunastoczynnikowego.

Jedną z zalet jawnej deklaracji zależności jest to, że upraszcza ona konfigurację dla deweloperów nowych w aplikacji. Nowy programista może wyewidencjonować bazę kodu aplikacji na swoim komputerze deweloperskim, wymagając jedynie zainstalowania środowiska uruchomieniowego języka i menedżera zależności jako wymagań wstępnych. Będą mogli skonfigurować wszystko, co jest potrzebne do uruchomienia kodu aplikacji za pomocą deterministycznego polecenia kompilacji. Na przykład polecenie budowania dla Ruby/Bundler to `bundle install`, podczas gdy dla Clojure/Leiningen jest to `lein deps`.

Aplikacje dwunastoczynnikowe również nie opierają się na niejawnym istnieniu jakichkolwiek narzędzi systemowych. Przykłady obejmują wyłuskiwanie do ImageMagick lub curl. Chociaż narzędzia te mogą istnieć w wielu, a nawet większości systemów, nie ma gwarancji, że będą one istnieć we wszystkich systemach, na których aplikacja może działać w przyszłości, ani czy wersja znaleziona w przyszłym systemie będzie z nią zgodna. Jeśli aplikacja musi zostać przekazana do narzędzia systemowego, narzędzie to powinno zostać dostarczone do aplikacji.

## 3. Konfiguracja
> Przechowuj konfigurację w środowisku

Konfiguracja aplikacji to wszystko, co może się różnić między wdrożeniami (staging, produkcja, środowiska deweloperskie itp.). To zawiera:

- Zasoby do bazy danych, Memcached i innych usług wspierających
- Poświadczenia do usług zewnętrznych, takich jak Amazon S3 czy Twitter
- Wartości dla każdego wdrożenia, takie jak kanoniczna nazwa hosta dla wdrożenia
___
## 4. Usługi tworzenia kopii zapasowych
> Traktuj usługi tworzenia kopii zapasowych jako dołączone zasoby

Usługi tworzenia kopii zapasowych
Traktuj usługi tworzenia kopii zapasowych jako dołączone zasoby

Usługa tworzenia kopii zapasowych to dowolna usługa używana przez aplikację w sieci w ramach normalnego działania. Przykłady obejmują magazyny danych (takie jak MySQL lub CouchDB), systemy przesyłania wiadomości/kolejkowania (takie jak RabbitMQ lub Beanstalkd), usługi SMTP dla wychodzącej poczty e-mail (takie jak Postfix) oraz systemy buforowania (takie jak Memcached).

Usługi tworzenia kopii zapasowych, takie jak baza danych, są tradycyjnie zarządzane przez tych samych administratorów systemów, którzy wdrażają środowisko wykonawcze aplikacji. Oprócz tych usług zarządzanych lokalnie aplikacja może również oferować usługi świadczone i zarządzane przez strony trzecie. Przykłady obejmują usługi SMTP (takie jak Postmark), usługi gromadzenia metryk (takie jak New Relic lub Loggly), usługi zasobów binarnych (takie jak Amazon S3), a nawet usługi konsumenckie dostępne za pośrednictwem interfejsu API (takie jak Twitter, Google Maps lub Last .fm).

Kod aplikacji dwunastoskładnikowej nie rozróżnia usług lokalnych i usług stron trzecich. Oba są dołączonymi do aplikacji zasobami, do których można uzyskać dostęp za pośrednictwem adresu URL lub innego lokalizatora/poświadczeń przechowywanych w konfiguracji. Wdrożenie aplikacji dwunastoskładnikowej powinno umożliwić zamianę lokalnej bazy danych MySQL na bazę zarządzaną przez stronę trzecią (taką jak Amazon RDS) bez żadnych zmian w kodzie aplikacji. Podobnie lokalny serwer SMTP można zamienić na usługę SMTP innej firmy (taką jak Postmark) bez zmiany kodu. W obu przypadkach należy zmienić tylko uchwyt zasobu w konfiguracji.

Każda odrębna usługa tworzenia kopii zapasowych jest zasobem. Na przykład baza danych MySQL jest zasobem; dwie bazy danych MySQL (używane do shardingu w warstwie aplikacji) kwalifikują się jako dwa różne zasoby. Aplikacja dwunastoczynnikowa traktuje te bazy danych jako dołączone zasoby, co wskazuje na ich luźne połączenie z wdrożeniem, do którego są dołączone.

Wdrożenie produkcyjne połączone z czterema usługami pomocniczymi.

Zasoby można dowolnie dołączać i odłączać od wdrożeń. Na przykład, jeśli baza danych aplikacji działa nieprawidłowo z powodu problemu ze sprzętem, administrator aplikacji może uruchomić nowy serwer bazy danych przywrócony z ostatniej kopii zapasowej. Obecną produkcyjną bazę danych można było odłączyć, a nową dołączyć – wszystko bez żadnych zmian w kodzie.
___
## 5. Build, release, run
> Ściśle oddziel etapy budowania i uruchamiania

Buduj, wydawaj, uruchamiaj
Ściśle oddziel etapy budowania i uruchamiania

Baza kodu jest przekształcana we wdrożenie (niedeweloperskie) w trzech etapach:

    Etap kompilacji to transformacja, która konwertuje repozytorium kodu na wykonywalny pakiet znany jako kompilacja. Korzystając z wersji kodu w zatwierdzeniu określonym przez proces wdrażania, etap kompilacji pobiera zależności dostawców i kompiluje pliki binarne i zasoby.
    Na etapie wydania kompilacja wytworzona na etapie kompilacji łączy się z bieżącą konfiguracją wdrożenia. Otrzymane wydanie zawiera zarówno kompilację, jak i konfigurację i jest gotowe do natychmiastowego wykonania w środowisku wykonawczym.
    Etap uruchamiania (znany również jako „runtime”) uruchamia aplikację w środowisku wykonawczym, uruchamiając pewien zestaw procesów aplikacji w wybranym wydaniu.

Kod staje się kompilacją, która w połączeniu z konfiguracją tworzy wydanie.

Aplikacja dwunastoczynnikowa wykorzystuje ścisłe rozdzielenie etapów kompilacji, wydania i uruchamiania. Na przykład nie można wprowadzać zmian w kodzie w czasie wykonywania, ponieważ nie ma możliwości propagowania tych zmian z powrotem do etapu kompilacji.

Narzędzia do wdrażania zazwyczaj oferują narzędzia do zarządzania wydaniami, w szczególności możliwość przywrócenia poprzedniej wersji. Na przykład narzędzie wdrażania Capistrano przechowuje wydania w podkatalogu o nazwie wydania, gdzie bieżąca wersja jest dowiązaniem symbolicznym do katalogu bieżącego wydania. Jego polecenie wycofania ułatwia szybkie przywrócenie poprzedniej wersji.

Każde wydanie powinno zawsze mieć unikalny identyfikator wydania, taki jak sygnatura czasowa wydania (np. 2011-04-06-20:32:17) lub numer inkrementacyjny (np. v100). Wydania są księgą tylko do dołączania, a wydania nie można zmutować po utworzeniu. Każda zmiana musi tworzyć nowe wydanie.

Kompilacje są inicjowane przez programistów aplikacji po każdym wdrożeniu nowego kodu. Natomiast wykonanie w czasie wykonywania może nastąpić automatycznie w przypadkach, takich jak ponowne uruchomienie serwera lub ponowne uruchomienie uszkodzonego procesu przez menedżera procesów. Dlatego etap uruchamiania powinien być ograniczony do jak najmniejszej liczby ruchomych części, ponieważ problemy uniemożliwiające uruchomienie aplikacji mogą spowodować jej awarię w środku nocy, gdy nie ma pod ręką programistów. Etap kompilacji może być bardziej złożony, ponieważ dla programisty, który kieruje wdrożeniem, zawsze na pierwszym planie są błędy.
___

## 6. Procesy
> Uruchom aplikację jako jeden lub więcej procesów bezstanowych

Aplikacja jest wykonywana w środowisku wykonawczym jako jeden lub więcej procesów.

W najprostszym przypadku kod jest samodzielnym skryptem, środowiskiem wykonawczym jest lokalny laptop programisty z zainstalowanym środowiskiem wykonawczym języka, a proces jest uruchamiany z wiersza poleceń (na przykład python my_script.py). Z drugiej strony, wdrożenie produkcyjne zaawansowanej aplikacji może wykorzystywać wiele typów procesów, utworzonych w postaci zerowej lub większej liczby uruchomionych procesów.

Procesy dwunastoczynnikowe są bezstanowe i nie dzielą się niczym. Wszelkie dane, które muszą być trwałe, muszą być przechowywane w stanowej usłudze tworzenia kopii zapasowych, zwykle w bazie danych.

Przestrzeń pamięci lub system plików procesu może być używany jako krótka pamięć podręczna dla pojedynczej transakcji. Na przykład pobranie dużego pliku, operowanie na nim i przechowywanie wyników operacji w bazie danych. Aplikacja dwunastoczynnikowa nigdy nie zakłada, że ​​cokolwiek zbuforowane w pamięci lub na dysku będzie dostępne w przyszłym żądaniu lub zadaniu – przy wielu uruchomionych procesach każdego typu istnieje duże prawdopodobieństwo, że przyszłe żądanie będzie obsługiwane przez inny proces. Nawet w przypadku uruchomienia tylko jednego procesu ponowne uruchomienie (wyzwolone przez wdrożenie kodu, zmianę konfiguracji lub środowisko wykonawcze przenoszące proces do innej fizycznej lokalizacji) zazwyczaj wyczyści cały stan lokalny (np. pamięć i system plików).

Pakowacze zasobów, takie jak django-assetpackager, używają systemu plików jako pamięci podręcznej dla skompilowanych zasobów. Aplikacja dwunastoczynnikowa woli wykonywać tę kompilację na etapie kompilacji. Pakowacze zasobów, takie jak Jammit i Rails, można skonfigurować do pakowania zasobów na etapie kompilacji.

Niektóre systemy internetowe opierają się na „trwałych sesjach” – czyli buforowaniu danych sesji użytkownika w pamięci procesu aplikacji i oczekiwaniu, że przyszłe żądania od tego samego odwiedzającego będą kierowane do tego samego procesu. Sesje lepkie są naruszeniem dwunastu czynników i nigdy nie powinny być używane ani na nich polegać. Dane o stanie sesji są dobrym kandydatem na magazyn danych, który oferuje wygaśnięcie czasu, taki jak Memcached lub Redis.
___

## 7. Port binding
>Eksportuj usługi przez wiązanie portów

Aplikacje internetowe są czasami wykonywane w kontenerze serwera WWW. Na przykład aplikacje PHP mogą działać jako moduł w Apache HTTPD lub aplikacje Java mogą działać w Tomcat.

Aplikacja dwunastoskładnikowa jest całkowicie samowystarczalna i nie polega na wstrzykiwaniu serwera WWW do środowiska wykonawczego w celu utworzenia usługi dostępnej w Internecie. Aplikacja sieci Web eksportuje protokół HTTP jako usługę przez powiązanie z portem i nasłuchiwanie żądań przychodzących przez ten port.

W lokalnym środowisku programistycznym deweloper odwiedza adres URL usługi, taki jak http://localhost:5000/, aby uzyskać dostęp do usługi wyeksportowanej przez ich aplikację. We wdrożeniu warstwa routingu obsługuje żądania routingu z publicznie dostępnej nazwy hosta do procesów internetowych związanych z portami.

Jest to zwykle implementowane przy użyciu deklaracji zależności w celu dodania do aplikacji biblioteki serwera WWW, takiej jak Tornado dla Pythona, Thin dla Ruby lub Jetty dla Javy i innych języków opartych na JVM. Dzieje się to całkowicie w przestrzeni użytkownika, czyli w kodzie aplikacji. Umowa ze środowiskiem wykonawczym jest powiązana z portem do obsługi żądań.

HTTP nie jest jedyną usługą, którą można wyeksportować przez powiązanie portu. Prawie każdy rodzaj oprogramowania serwerowego można uruchomić poprzez proces wiążący się z portem i oczekujący na przychodzące żądania. Przykłady obejmują ejabberd (mówiąc w XMPP) i Redis (mówiąc w protokole Redis).

Należy również zauważyć, że podejście powiązania portów oznacza, że ​​jedna aplikacja może stać się usługą tworzenia kopii zapasowych dla innej aplikacji, podając adres URL aplikacji tworzącej kopię zapasową jako dojście do zasobu w konfiguracji dla aplikacji zużywającej.

___
## 8. Konkurencja
>Skaluj poprzez model procesu

Każdy program komputerowy po uruchomieniu jest reprezentowany przez jeden lub więcej procesów. Aplikacje internetowe przybierają różne formy realizacji procesów. Na przykład procesy PHP są uruchamiane jako procesy potomne Apache, uruchamiane na żądanie w zależności od wielkości żądań. Procesy Javy przyjmują odwrotne podejście: JVM zapewnia jeden ogromny uberproces, który rezerwuje duży blok zasobów systemowych (procesora i pamięci) podczas uruchamiania, z wewnętrznie zarządzaną współbieżnością za pośrednictwem wątków. W obu przypadkach uruchomione procesy są tylko minimalnie widoczne dla twórców aplikacji.

Skala jest wyrażona jako uruchomione procesy, różnorodność obciążenia jest wyrażona jako typy procesów.

W aplikacji dwunastoczynnikowej procesy są obywatelami pierwszej klasy. Procesy w aplikacji dwunastoczynnikowej pobierają silne wskazówki z modelu procesów uniksowych do uruchamiania demonów usług. Korzystając z tego modelu, programista może zaprojektować swoją aplikację pod kątem obsługi różnych obciążeń, przypisując każdy typ pracy do typu procesu. Na przykład żądania HTTP mogą być obsługiwane przez proces sieciowy, a długotrwałe zadania w tle obsługiwane przez proces roboczy.

Nie wyklucza to obsługi przez poszczególne procesy ich własnego wewnętrznego multipleksowania za pośrednictwem wątków wewnątrz maszyny wirtualnej środowiska uruchomieniowego lub modelu asynchronicznego/zdarzenia występującego w narzędziach takich jak EventMachine, Twisted lub Node.js. Jednak pojedyncza maszyna wirtualna może rosnąć tylko do tak dużych rozmiarów (skala pionowa), więc aplikacja musi również być w stanie objąć wiele procesów działających na wielu fizycznych maszynach.

Model procesu naprawdę błyszczy, gdy przychodzi czas na skalowanie. Brak współdzielenia, poziomy partycjonowalny charakter dwunastoczynnikowych procesów aplikacji oznacza, że ​​dodanie większej liczby współbieżności jest prostą i niezawodną operacją. Tablica typów procesów i liczba procesów każdego typu jest znana jako tworzenie procesu.

Dwunastoczynnikowe procesy aplikacji nigdy nie powinny demonizować ani zapisywać plików PID. Zamiast tego polegaj na menedżerze procesów systemu operacyjnego (takim jak systemd, menedżer procesów rozproszonych na platformie w chmurze lub narzędzie takie jak Foreman w fazie rozwoju), aby zarządzać strumieniami wyjściowymi, reagować na awarie procesów i obsługiwać uruchamiane przez użytkownika restarty i zamknięcia.

___
## 9. Jednorazowość
> Maximize robustness with fast startup and graceful shutdown

Procesy aplikacji dwunastoczynnikowej są jednorazowe, co oznacza, że ​​można je uruchomić lub zatrzymać w mgnieniu oka. Ułatwia to szybkie elastyczne skalowanie, szybkie wdrażanie zmian kodu lub konfiguracji oraz niezawodność wdrożeń produkcyjnych.

Procesy powinny dążyć do minimalizacji czasu uruchamiania. W idealnym przypadku proces trwa kilka sekund od momentu wykonania polecenia uruchomienia do momentu, gdy proces jest gotowy do odbierania żądań lub zadań. Krótki czas uruchamiania zapewnia większą elastyczność procesu wydania i skalowania; i zwiększa niezawodność, ponieważ kierownik procesu może łatwiej przenieść procesy na nowe maszyny fizyczne, gdy jest to uzasadnione.

Procesy są bezpiecznie zamykane, gdy otrzymują sygnał SIGTERM od menedżera procesów. W przypadku procesu internetowego łagodne zamknięcie jest osiągane przez zaprzestanie nasłuchiwania na porcie usługi (tym samym odrzucając wszelkie nowe żądania), pozwalając na zakończenie wszystkich bieżących żądań, a następnie zamknięcie. Niejawnym w tym modelu jest to, że żądania HTTP są krótkie (nie dłuższe niż kilka sekund) lub w przypadku długiego odpytywania klient powinien bezproblemowo próbować ponownie nawiązać połączenie, gdy połączenie zostanie utracone.

W przypadku procesu roboczego bezpieczne zamknięcie jest osiągane przez zwrócenie bieżącego zadania do kolejki roboczej. Na przykład na RabbitMQ pracownik może wysłać NACK; w Beanstalkd zadanie jest automatycznie zwracane do kolejki po rozłączeniu się pracownika. Systemy oparte na blokadach, takie jak opóźnione zadanie, muszą zwolnić blokadę w rekordzie zadania. Niejawnym w tym modelu jest to, że wszystkie zadania są wielokrotne, co zwykle osiąga się poprzez zawinięcie wyników w transakcję lub uczynienie operacji idempotentną.

Procesy powinny być również odporne na nagłą śmierć w przypadku awarii podstawowego sprzętu. Chociaż jest to znacznie rzadsze zjawisko niż pełne wdzięku zamknięcie za pomocą SIGTERM, nadal może się zdarzyć. Zalecanym podejściem jest użycie niezawodnego zaplecza kolejkowania, takiego jak Beanstalkd, który zwraca zadania do kolejki, gdy klient się rozłączy lub przekroczy limit czasu. Tak czy inaczej, aplikacja dwunastoskładnikowa jest zaprojektowana do obsługi nieoczekiwanych, niewdzięcznych zakończeń. Projekt „tylko w przypadku awarii” prowadzi tę koncepcję do logicznego zakończenia.

___
## 10. 
>Parzystość deweloperów/producentów
Utrzymuj jak najbardziej zbliżony rozwój, etapy i produkcję

Historycznie istniały znaczne luki między programowaniem (programista dokonujący edycji na żywo w lokalnym wdrożeniu aplikacji) a produkcją (działającym wdrożeniem aplikacji, do której uzyskują dostęp użytkownicy końcowi). Luki te przejawiają się w trzech obszarach:

- Przerwa czasowa: programista może pracować nad kodem, którego wdrożenie do produkcji zajmuje dni, tygodnie, a nawet miesiące.
- Luka kadrowa: programiści piszą kod, inżynierowie ops wdrażają go.
- Luka w narzędziach: programiści mogą używać stosu takiego jak Nginx, SQLite i OS X, podczas gdy wdrożenie produkcyjne wykorzystuje Apache, MySQL i Linux.
___

## 11. Logi
>Traktuj dzienniki jako strumienie zdarzeń

Dzienniki zapewniają wgląd w zachowanie działającej aplikacji. W środowiskach serwerowych są one zwykle zapisywane w pliku na dysku („plik dziennika”); ale to jest tylko format wyjściowy.

Dzienniki to strumień zagregowanych, uporządkowanych w czasie zdarzeń zebranych ze strumieni wyjściowych wszystkich uruchomionych procesów i usług zapasowych. Dzienniki w swojej surowej formie są zwykle w formacie tekstowym z jednym zdarzeniem na wiersz (chociaż ślady wyjątków mogą obejmować wiele wierszy). Dzienniki nie mają ustalonego początku ani końca, ale przepływają w sposób ciągły, dopóki aplikacja działa.

Aplikacja dwunastoczynnikowa nigdy nie zajmuje się routingiem ani przechowywaniem strumienia wyjściowego. Nie powinien próbować zapisywać ani zarządzać plikami dziennika. Zamiast tego każdy uruchomiony proces zapisuje swój strumień zdarzeń, niebuforowany, na standardowe wyjście. Podczas rozwoju lokalnego programista będzie wyświetlać ten strumień na pierwszym planie swojego terminala, aby obserwować zachowanie aplikacji.

Podczas wdrażania etapowego lub produkcyjnego każdy strumień procesu zostanie przechwycony przez środowisko wykonawcze, zestawiony ze wszystkimi innymi strumieniami z aplikacji i skierowany do jednego lub większej liczby docelowych miejsc docelowych w celu przeglądania i długoterminowej archiwizacji. Te archiwalne miejsca docelowe nie są widoczne ani konfigurowalne przez aplikację, a zamiast tego są całkowicie zarządzane przez środowisko wykonawcze. W tym celu dostępne są routery logów typu open source (takie jak Logplex i Fluentd).

Strumień zdarzeń aplikacji może być kierowany do pliku lub oglądany w terminalu w czasie rzeczywistym. Co najważniejsze, strumień można wysłać do systemu indeksowania i analizy dzienników, takiego jak Splunk, lub ogólnego systemu hurtowni danych, takiego jak Hadoop/Hive. Systemy te zapewniają dużą moc i elastyczność w zakresie introspekcji zachowania aplikacji w czasie, w tym:

    Znajdowanie konkretnych wydarzeń z przeszłości.
    Wykresy trendów na dużą skalę (takie jak żądania na minutę).
    Aktywne alertowanie zgodnie z heurystyką zdefiniowaną przez użytkownika (np. alert, gdy liczba błędów na minutę przekroczy określony próg).

___
## 12. Admin processes
>Uruchamiaj zadania administracyjne/zarządcze jako jednorazowe procesy

Tworzenie procesu to szereg procesów, które są używane do wykonywania zwykłych czynności biznesowych aplikacji (takich jak obsługa żądań internetowych) podczas jej działania. Oddzielnie programiści często chcą wykonywać jednorazowe zadania administracyjne lub konserwacyjne dla aplikacji, takie jak:

    Przeprowadzanie migracji baz danych (np. manage.py migrate w Django, rake db:migrate w Rails).
    Uruchamianie konsoli (znanej również jako powłoka REPL) do uruchamiania dowolnego kodu lub sprawdzania modeli aplikacji w aktywnej bazie danych. Większość języków zapewnia REPL, uruchamiając interpreter bez żadnych argumentów (np. python lub perl) lub w niektórych przypadkach ma osobne polecenie (np. irb dla Ruby, konsola rails dla Rails).
    Uruchamianie jednorazowych skryptów wprowadzonych do repozytorium aplikacji (np. php scripts/fix_bad_records.php).

Jednorazowe procesy administracyjne powinny być uruchamiane w identycznym środowisku, jak zwykłe, długotrwałe procesy aplikacji. Działają w stosunku do wydania, używając tej samej bazy kodu i konfiguracji, co każdy proces uruchamiany w tym wydaniu. Kod administratora musi być dostarczony z kodem aplikacji, aby uniknąć problemów z synchronizacją.

Te same techniki izolacji zależności powinny być stosowane we wszystkich typach procesów. Na przykład, jeśli proces webowy Ruby używa polecenia bundle exec thin start, migracja bazy danych powinna używać bundle exec rake db:migrate. Podobnie program Pythona używający Virtualenv powinien używać dostarczonego przez dostawcę bin/pythona do uruchamiania zarówno serwera internetowego Tornado, jak i wszelkich procesów administracyjnych manage.py.

Dwunastoczynnikowy zdecydowanie faworyzuje języki, które dostarczają powłokę REPL po wyjęciu z pudełka i ułatwiają uruchamianie jednorazowych skryptów. W lokalnym wdrożeniu programiści wywołują jednorazowe procesy administracyjne za pomocą bezpośredniego polecenia powłoki w katalogu kasowym aplikacji. We wdrożeniu produkcyjnym programiści mogą używać ssh lub innego mechanizmu zdalnego wykonywania poleceń dostarczonego przez środowisko wykonawcze tego wdrożenia, aby uruchomić taki proces.