# Explo-Ducks


# A játék
## Játékleírás
A játék egy 2 dimenziós pályán játszódik, amely négyzet alakú mezőkből áll. A játékot 2 játékos játsza,
akiknek 1-1 bomberman figurát irányítva céljuk, hogy egyedüliként maradjanak életben. A játékpálya
mezőin fal elemek, dobozok, szörnyek és maguk a játékosok figurái helyezkednek el. A játékosok
bombákat lehelyezve felrobbanthatják a dobozokat, szörnyeket és a játékosokat (akár saját magukat
is). Egy játékos veszt (és ezáltal ellenfele győz), ha felrobban, vagy ha egy szörny elkapja.

## Controls
|  | Játékos 1 | Játékos 2 |
|----------|----------|----------|
| Mozgás  | nyilak   | WASD   |
| Bombalerakás   | Enter   | Space  |

## Falak
A fal elemek felrobbanthatatlanok, és néhány (a választható részfeladatokban részletezett) kivételtől
eltekintve se a játékosok, se a szörnyek nem léphetnek rájuk. A játékpályát fal veszi körül (így arról
kilépni nem lehet).

## Játékosok
A játékosok 1-1 bomberman figurát irányítanak, amelyekkel balra, jobbra, felfele és lefele lehet lépni.
Speciális akcióként a játékosok egy bombát is lehelyezhetnek azon mezőre, amelyen állnak. Egy
játékosnak egyszerre csak 1 lehelyezett bombája lehet (lásd a Dobozok részt ennek kiegészítéséhez).
A játékosok a karakterüket a billenytűzet segítségével irányíthatják.

## Bombák
A lehelyezett bombák egy rövid idő után felrobbanak, és az aktuális mezőn kívül mind a 4 irányba
(balra, jobbra, felfele, lefele) 2-2 mező távolságban hatnak. A falak nem felrobbanthatóak és a
robbanás nem terjed tovább rajtuk keresztül. A dobozok felrobbanthatóak, de a robbanás erejét
megtörik, a robbanás nem terjed tovább rajtuk keresztül. A bombák egymást is az időzítőjük lejárta
előtt felrobbantják, így láncreakció jöhet létre. A robbanás ugyan gyorsan terjed, de nem azonnali,
tehát a bomba robbanásának pozíciójától a távolsággal arányos módon, kis késleltetéssel fejtse csak
ki egy robbanás a hatását a távolabbi mezőkre. A felrobbanó bomba a robbanásban érintett mezőkön
lévő játékosokat és szörnyeket elpusztítja.
A bombákra néhány (a választható részfeladatokban részletezett) kivételtől eltekintve nem léphetnek
rá se a játékosok, se a szörnyek. (A játékosok maguk “alá” helyezik le a bombát, amelyről ilyenkor
még leléphetnek, de utána visszalépni az adott mezőre nem tudnak, amíg a bomba ott van.)

## Dobozok
A dobozok felrobbanthatóak, és néhány (a választható részfeladatokban részletezett) kivételtől
eltekintve se a játékosok, se a szörnyek nem léphetnek rájuk. Ha egy doboz felrobbantásra kerül,
előkerülhet belőle egy “power-up”, amelyre ha bármely játékos rálép, karaktere bónuszt kap az adott
játékra. A lehetséges bónuszok:
* Bombák száma: a játékos által lehelyezhető bombák száma 1-gyel növekszik.
* Robbanás hatótáva: a játékos bombáinak hatótávja mind a 4 irányba 1-1 mezővel növekszik.

## Szörnyek
A játékpályán szörnyek is bolyonganak, amelyek bármely játékos karakterével azonos mezőre lépve, a
játékos meghal. Az alapfeladatban a szörnyek egyszerű heurisztikával rendelkezzenek: akadályba
ütközéskor véletlenszerűen váltsanak irányt. Néha meglepetésszerűen is változtassanak a haladási
irányukon, hogy mozgásuk kevésbé legyen kiszámítható.

## A játék vége
Amennyiben valamelyik játékos felrobban vagy egy szörny elkapja, a játék még egy rövid ideig
(például a bombák időzítésének megfelelő ideig) folytatódjon. Ha ezen idő alatt a másik játékos
életben tud maradni, akkor megnyerte a játszmát. Ha a másik játékos is meghal ezen idő alatt, akkor
a játék döntetlen eredménnyel végződik.

## A játék indítása
Új játék indításakor választhassunk legalább 3, előre elkészített, különböző pálya közül. Az egyes
pályákon a falak és a dobozok pozíciója előre definiált lehet, azonban az, hogy mely dobozok rejtenek
bónuszt (és milyet), az dinamikusan, futási időben eldöntött legyen. A pályák alapterülete lehet
téglalap, de más alakzatú is.
Adhassuk azt is meg, hogy a játékot hány megnyert játszmáig szeretnénk folytatni. Minden játszma
után kerüljön megjelenítésre az aktuális játék eredménye, továbbá, hogy melyik játékos hány nyert játszmánál tart. (A döntetlen mindkét játékos szempontjából vereségnek számít.) Az utolsó játék után a végeredményt is jelenítsük meg.

## Kiegészítő funkciók
### Intelligens szörnyek
A játékpályákon többféle szörnnyel is találkozhassunk, amelyek eltérő sebességgel és heurisztika
szerint mozogjanak. Az egyes szörnyek vizuálisan is eltérően jelenjenek meg. Legalább 4 különböző
szörny implementálása szükséges:
1. Az alapfeladatban szereplő szörny.
2. Az alapfeladatban szereplőhöz hasonló szörny, amely a falakon és dobozokon át tud menni.
(De a bombákon nem.) Amennyiben akadályhoz, azaz falhoz vagy dobozhoz érkezik és
egyenes továbbhaladással van még nem akadály mező a pályán, akkor bizonyos eséllyel ne
irányt váltson, hanem folytassa haladási irányát. Ilyenkor, ha több akadály mező is van
egymás után, akkor azokon már irányváltás nélkül haladjon végig. Mozogjon lassabban az
alap szörnyhöz képest.
3. Az alapfeladatban szereplőhöz hasonló szörny, azonban akadályba ütközéskor bekövetkező
irányváltáskor olyan irányt válasszon, hogy a legrövidebb út alapján a hozzá legközelebb eső
játékos felé induljon el. (Ha egyik játékost sem tudja elérni a pályán lévő akadályok miatt,
akkor véletlenszerűen bolyongjon.) Mozogjon gyorsabban az alap szörnyhöz képest.
4. Az előzőhöz hasonló szörny, azonban útelágazásnál válthasson irányt a leírt heurisztika
alapján. Bizonyos eséllyel hozzon hibás döntést és válasszon rossz utat. Mozogjon az alap
szörnnyel egyező sebességgel.

### Haladó bónuszok 
Az alapfeladatban definiált 2 power-up mellett további, komplexebb bónuszok is legyenek elérhetőek
a felrobbantott dobozok helyén.
* **Detonátor:** a játékos által lehelyezett bomba / bombák ne időzítő hatására robbanjanak fel,
hanem az utolsó bomba lehelyezése után, a bomba lehelyezés funkciót még egyszer
használva, az összes bombája robbanjon fel a játékosnak.
* **Görkorcsolya:** a játékos karakterének sebessége növekedjen meg. Nem halmozható, az
esetleges második és további görkorcsolyák felvételének nincs hatása.
* **Sérthetetlenség:** egy rövid ideig a játékos karaktere legyen sérthetetlen. Vizuálisan is jelöljük,
hogy a játékos jelenleg sérthetetlen, és azt is, ha hamarosan véget ér a hatása.
* **Szellem:** egy rövid ideig a játékos karaktere legyen képes a falakon, a dobozokon és a
bombákon is áthaladni. Vizuálisan is jelöljük, hogy a játékos rendelkezik a képességgel és azt
is, ha hamarosan véget ér a hatása. Ha a játékos a képesség végekor egy doboz vagy egy fal
mezőn tartózkodik, akkor meghal. (Bombáról leléphet.)
* **Akadály:** a játékos helyezhessen le akadályokat, amelyek játéklogikailag úgy viselkednek, mint
a dobozok, azonban ezekből bónusz (power-up) sosem kerül elő. Maximálisan 3 akadály
legyen egy játékos által lehelyezhető. (Ha felrobbantásra kerülnek, lehelyezhető új.) Ez a
képesség legyen halmozható, azaz a bónusz esetleges második felvételével 6 akadály legyen
lehelyezhető, stb.

### Hátráltató bónuszok
A dobozokból kerülhessenek elő hátráltatással bíró “bónuszok” is. Ebben az esetben a játékosok
számára ne legyen előre ismert a konkrét hátráltatás, hanem ugyanaz a grafika jelölje az összeset (pl.
az eredeti játékban koponya). A tényleges hátráltatásra annak felvétele után empirikus úton jöhet rá
a felhasználó.
* A játékos karakterének sebessége egy időre csökkenjen le.
* A játékos által lehelyezett bombák hatótávja mindössze 1 mező legyen egy adott ideig.
* A játékos ne tudjon bombákat lehelyezni egy ideig.
* A játékos karaktere azonnal helyezze le a bombákat, amint tudja (szabad mezőn áll és tud
lehelyezni bombát). Ez a hátráltatás is csak egy adott ideig fejtse ki hatását.

### Bónuszok hatása egymással

|| PlusBomb|PlusRadius|Detonator|SpeedBonus|Invincibility|Ghost|Barrier|SlowPowerUp|ReducedRadius|NoBomb|PlaceBomb|
|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
|**PlusBomb**|-|-|Detonator mukodik rendesen|-|-|-|plusz bomba, de barrier szama marad|-|-|nem tud lerakni bombat|plusz bombakat helyezel le|
|**Plus Radius**|-|-|-|-|-|-|-|-|radius = 1|-|-|
|**Detonator**|plusz bombat tudsz egyszerre|-|nincs plusz hatas|-|-|-|elso lerakasra robbant|-|-|szopas|be tudod robbantani|
|**SpeedBonus**|-|-|-|nem növel többet|-|gyorsabban repkedsz|-|visszatersz alap gyorsasagra|-|-|-|
|**Invincibility**|-|-|-|-|idős!|nagyon op|-|-|-|-|-|
|**Ghost**|-|-|-|gyorsabban repkedsz|nagyon op|idős!|lerakós!|lassabban repkedsz|-|-|lerakós!|
|**Barrier**|-|-|-|-|-|lerakós!|barrierek száma nő|-|-|barriert tudsz lerakni|barriert tudsz lerakni|
|**SlowPowerUp**|-|-|-|nem hat|-|lassabban repkedsz|-|idős!|-|-|-|
|**ReducedRadius**|-|nem hat|-|-|-|-|-|-|idős!|no bomb|-|
|**NoBomb**|nem hat|felveszi|ha nem nyomod el, addig marad, amig el nem nyomod|-|-|-|barriert tudsz lerakni|-|-|idős!|nem raksz le bombát|
|**PlaceBomb**|plusz bombát raksz le|-|be tudod robbantani|-|nem halsz bele a saját bombáidba legalább|lerakós!|barriert tudsz lerakni|-|-|-|idős!|

### Folyamatos mozgás
A játékosok és a szörnyek mozgása a játékpálya mezői között ne ugrásszerű, hanem folyamatos
legyen. A karakterek ettől még logikailag lehetnek mindig kizárólagosan egyetlen mezőn, de
mozgatásuk a mezők között igényelje a vezérlő gombok többszöri lenyomását (vagy nyomva tartását).

### Testreszabható vezérlés
Az alkalmazáson belül legyen lehetőség a játékosok irányításához rendelt billentyűkiosztás
testreszabására. Ez a beállítás kerüljön megőrzésre is, az alkalmazás későbbi indításakor az utoljára
mentett beállítása legyen érvényben.