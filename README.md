### SVEUČILIŠTE U SPLITU

### FAKULTET ELEKTROTEHNIKE, STROJARSTVA I

### BRODOGRADNJE

### Split, siječanj 2021.

```
Ugradbeni računalni sustavi
```
BUS Tracker

![28-512](https://user-images.githubusercontent.com/37696656/109654713-ceb65780-7b62-11eb-85a9-6b981dbf0281.png)

```
Luka Rosić
Davor Bazina
```

## Sadržaj

- 1. Uvod
- 2. Problem i rješenje
- 3. Proizvod
   - 3. 1. Arduino GPS Tracker
   - 3. 2. Mobilna aplikacija
   - 3. 3. Sučelje za vozače
   - 3. 4. Semafori na stanicama
- 4. Prvi potencijalni korisnici
- 5. Poslovni model


## 1. Uvod

Bus Tracker je osmišljen kao sustav za praćenje vozila javnog prijevoza koji će se, za razliku
od konkurencije bazirati na praćenju geografskog položaja vozila umjesto na vremenskom
predviđanju dolaska autobusa. Budući da je ipak riječ o predviđanju, ne može se ostvarivati
stopostotnu efikasnost jer se uvijek mogu pojaviti određeni problemi u prometu poput gužvi,
nesreće ili nepovoljnih vremenskih uvjeta.

Sam sustav podijeljen je u 3 dijela: GPS trackera koji će se postaviti u svako vozilo
prijevoznika, mobilne aplikacije koja će biti dostupna široj masi ljudi, odnosno turistima u
nepoznatom gradu i lokalnim stanovnicima za olakšanje svakodnevnog radnog dana te treći
dio sučelje za vozače kojim će se određivati linija koja se trenutno vozi.

Tim koji sudjeluje na izradi ovog sustava sastavljen je od dvojice članova: Luka Rosić koji je
primarno zadužen za hardverski dio poslova i Davor Bazina koji je zadužen softverske
poslove. Ovo je okvirna podjela poslova, što znači da su oba člana tima ravnopravni u izradi
projekta te imaju jednaka prava u sugeriranju pri rješenju, korekciji izrađenih segmenata, ali i
pravo na veto u nekim ključnim odlukama.


## 2. Problem i rješenje

Na lokalnoj razini, odnosno primarno grad Split, ali i prostor cijele Hrvatske, ne postoji sustav
koji bi precizno određivao vrijeme dolaska autobusa na određenu postaju. Jedini takav sustav
u cijeloj Hrvatskoj postoji u Zagrebu, ali se vrijeme dolaska određuje na temelju pretpostavke
čime su oscilacije u kašnjenju vrlo česte te je ovo rješenje sve nepouzdanije rastom broja
osobnih automobila u gradskom prometu.

Ovaj problem može se vrlo jednostavno i efikasno riješiti promjenom načina razmišljanja,
odnosno umjesto baziranja na vremenskoj pretpostavci, promatra se geografska lokacija
samog autobusa. Mreža svih autobusnih linija bit će prikazana korisniku na aplikaciji na
njegovom pametnom telefonu te će uz svaku liniju biti prikazane osnovne informacije o
svakoj liniji.

Prednost ovakvog rješenja je dostupnost sustava široj masi ljudi, relativno jeftino rješenje u
donosu na slične konkurentske sustave. Primjena je vrlo jednostavna, stoga ne bi trebalo biti
problema u korištenju samog sustava. Također je i prednost oslanjanje na geografski položaj
autobusa što je spomenuto ranije. Ovakav proizvod se vrlo ekspresno može staviti u funkciju i
prihvaćen svakodnevnoj primjeni prosječnog korisnika.

![image](https://user-images.githubusercontent.com/37696656/109655122-34a2df00-7b63-11eb-9483-f2e99b3e2501.png "Slika 1. Mreža gradskih linija prijevoznika Promet Split")
*Slika 1. Mreža gradskih linija prijevoznika Promet Split*

## 3. Proizvod

### Kao što je i spomenuto u uvodnom poglavlju, sam proizvod sastoji se od tri dijela: Arduino

GPS Trackera, mobilne aplikacije primjerene za prosječne korisnike sustava te sučelja za
vozače. Ovim trima dijelovima eventualno se može pridružiti semafori koji bi bili postavljeni
na frekventnijim stanicama. S obzirom da je ova tehnologija vrlo skupa, a nije ni od pretežne
važnosti za funkcioniranje sustava, može se i zanemariti u prvoj fazi.

### 3. 1. Arduino GPS Tracker

Arduino GPS Tracker je jednostavni komad hardverske opreme koju bi se ugradio u svaki
autobus pojedinog prijevoznika. Glavna stavka ovog hardvera je Arduino UNO kojeg se
proširuje sa stavkom Arduino GPS/LTE Shieldom (Botletic SIM7500 4G LTE). Preko njega
će se sklop povezivati sa serverom.

![image](https://user-images.githubusercontent.com/37696656/109655214-4e442680-7b63-11eb-91cf-f5f1540d3311.png "Slika 2. Arduino Uno")

*Slika 2. Arduino Uno*

Preko ovog uređaja svaki od autobusa komunicirat će sa serverom na način da šalje svoju
trenutnu lokaciju na server u vremenskim intervalima od otprilike 10 sekundi. Taj vremenski
interval bi trebao biti dostatan za slanje geografske lokacije samog vozila. Ukoliko bi se
ispitivanjem sustava u praksi uvidjelo da je 10 sekundi previše (ili premalo), trebalo bi
prilagoditi sustav traženim uvjetima.

Samo slanje podataka na server odvijat će se u urbanim područjima preko LTE mreže, a na
ruralnim krajevima i općenito lokacijama gdje je pokrivenost LTE mreže manja, koristit će se
redom dostupne mreže – 3G ili 2G. Budući da je na većini prometnica u Republici Hrvatskoj
zastupljena LTE mreža, ne bi trebalo doći do korištenja sporijih mreža. S obzirom da je razvoj
5G mreže ubrzano teče, trebat će sustav redizajnirati radi ubrzanja rada našeg sustava.


![image](https://user-images.githubusercontent.com/37696656/109655427-8f3c3b00-7b63-11eb-87a6-57fed6469b01.png "Slika 3. Arduino LTE/GPS Shield")

*Slika 3. Arduino LTE/GPS Shield*

Podaci o geografskoj širini i dužini autobusa šalju se na iznajmljeni server (npr. firme Google,
Amazon i sl.) zbog pouzdanosti i jednostavnog proširenja kapaciteta ako sustav bude to
zahtijevao. Na serveru se podaci obrađuju te se šalju svakom pojedinačnom korisniku na
njegov mobilni uređaj te na semafore na autobusnim satnicama.

![image](https://user-images.githubusercontent.com/37696656/109655531-a8dd8280-7b63-11eb-9db0-3fb1309786ac.png "Slika 4. Dijagram rada sustava")

*Slika 4. Dijagram rada sustava*

Prilikom osmišljavanje cijelog dijagrama rada sustava, namjerno je izostavljena stavka sučelja
za vozače autobusa jer bi taj proces trebalo osmisliti na način da bude automatiziran. Da je i ta
stavka uključena u dijagram, također bi preko Arduino GPS Trackera komunicirala sa
serverom šaljući podatke o liniji.


### 3. 2. Mobilna aplikacija

Mobilna aplikacija centralni je dio cjelokupnog sustava. Svi ostali dijelovi podređeni su
aplikaciji te bi aplikacija trebala biti dostupna na više platformi. Na aplikaciji trebala bi se
nalaziti karta sa svim autobusnim linijama koje su trenutno aktivne. Prikaz autobusa trebao bi
biti u realnom vremenu, što znači da geografska lokacija mora biti točna u tom trenutkom s
toleriranim vremenskim odstupanjem od maksimalno 10 sekundi.

Što se tiče funkcionalnosti, korisniku bi trebala biti dostupna na karti vlastita lokacija, a uz
kartu autobusa trebaju biti dostupne lokacije svih autobusnih stanica. Pritiskom da pojedinu
stanicu, trebala bi se korisniku prikazati lista svih linja koje se zaustavljaju na toj stanici. A
pritiskom na pojedinu liniju na karti trebale bi biti vidljive sve potrebne informacije o liniji –
broj, vrijeme polaska, ruta, točna distanca do korisnika, itd. Na slikama ispod dani su primjeri
mobilnih aplikacija.

![image](https://user-images.githubusercontent.com/37696656/109655604-c1e63380-7b63-11eb-97a2-df055fe3f4f5.png "Slika 5. Primjer mobilne aplikacije")

*Slika 5. Primjer mobilne aplikacije*

![image](https://user-images.githubusercontent.com/37696656/109655707-de826b80-7b63-11eb-9821-1fbcda88ab65.png "Slika 6. Primjer mobilne aplikacije")

*Slika 6. Primjer mobilne aplikacije*

### 3. 3. Sučelje za vozače

Ovo je najproblematičniji dio sustava. Ideja je da pri ulasku u autobus, odnosu neposredno
prije polaska, vozač na sučelju koji bi bilo implementirano na tabletu, odabere liniju i vrijeme
polaska. Sam tablet bi služio kao sredstvo komunikacije sa GPS trackerom ugrađenim u samo
vozilo. Očit je problem koji se javlja u samom procesu, a to je utjecaj ljudskom faktora čime
se povećava razina vjerojatnosti da dođe do nenamjerne pogrješke.

Pretpostavka je da jedno vozilo u javnom prijevozniku može voziti više linija u jednom danu,
stoga je nemoguće primijeniti bijekciju, odnosno točno jednom autobusu pridružiti točno
jednu liniju. Jedno od potencijalnih rješenja je uvođenje umjetne inteligencije na način da se
automatizira sam proces odabira linije i vremena polaska. U daljnjem razvoju sustava, trebalo
bi ispitati sva potencijalna rješenje te njihove prednosti i mane.

### 3. 4. Semafori na stanicama

Semafori nisu neophodni za samo funkcioniranje sustava te su financijski veliki trošak, stoga
se u početnoj fazi mogu zanemariti. Oni bi služili primarno starijim ljudima koji se ne služe
najbolje mobitelima. Na samom trodimenzionalnom semaforu bila bi prezentacija sa
prikazom karte autobusnih linija u blizini stanice, vozni red autobusa, ali moguće je i osigurati
reklamni prostor čime bi potencijalni kupac ovog sustava ostvario dodatni prihod.


## 4. Prvi potencijalni korisnici

Budući da sustav ima jasan naziv, popis potencijalnih kupaca je limitiran, odnosno ovaj
proizvod može se ponuditi samo autobusnim prijevoznicima poput Promet Split, ZET, Promet
Makarska i slični manji ili veći prijevoznici koje će ovakav sustav učinit jedinstvenima na
tržištu i potencijalno mogu ostvariti reklamu uvođenjem ovog sustava.

Daljnjim razvojem sustava, može se proširiti krug potencijalnih kupaca. Uz minimalne
korekcije u postojećem sustavu koji je namijenjen autobusima, može se doći do sustava za
dostavna vozila, vlakove, ali i eventualno za tvrtke koje se bave prijevozom tereta. Postoji još
sličnih situacija u kojima bi se mogao primijeniti ovakav i sličan sustav, stoga je očito da će
se i krug kupaca širiti.


## 5. Poslovni model

Poslovni model sastoji se procesa izrade samog sustava počevši od nabavke hardwarea do
izrade softwareske aplikacije. Zatim u poslovni model spada prodaja proizvoda kupci,
implementacija prodanog sustava u stvarnu primjenu te suradnja s autobusnim prijevoznicima
u svrhu daljnjeg razvoj i ažuriranja sustava s ciljem unaprjeđenja samog sustava.

Tržišni potencijal proizvoda je vrlo visok s obzirom na činjenicu da nema konkurencije na
lokalnoj razini. Zarada se primarno ostvaruje prodajom samog sustava, a dodatna zarada
preko reklama na trodimenzionalnim semaforima. Cijena proizvoda ovisi o broju autobusa u
prijevozniku. Daljnjim razvojem sustava i uvođenjem novih aplikacija, rast će i cijena
prvobitnog sustava.

![image](https://user-images.githubusercontent.com/37696656/109655832-04a80b80-7b64-11eb-9cb3-edfc63eedc1d.png "Slika 7. Primjer konkurencije koja nije ostvarila potnecijal")

*Slika 7. Primjer konkurencije koja nije ostvarila potnecijal*

Ukoliko se pretpostavi da se ovaj sustav treba prodati lokalnom javnom prijevozniku Promet
Split, pretpostavlja se da u svojoj garaži Promet Split ima 150 autobusa. Za svaki autobus
treba po jedan Arduino GPS Tracker koji po komadu košta oko 50€ te sučelje za vozače u
vidu tableta koji koštaju oko 150€ po komadu. A izrada mobilne aplikacije će ovisiti o broju
radnih sati. Suma cijele investicije bi iznosila minimalno 30 000€.
