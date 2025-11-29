# 📚 IT-halduse Protsessid: Muudatuste, Intsidendi-, Probleemi- ja Teenustehalduse Protsessid

IT-halduse protsessid, eriti need, mis on seotud **IT-teenuste infrastruktuuri raamistikega** (nagu **ITIL** - Information Technology Infrastructure Library), on iga kaasaegse IT-organisatsiooni edukuse jaoks hädavajalikud. Need tagavad stabiilsuse, prognoositavuse ja kvaliteetse teenuse osutamise.

---

## 1. Muudatuste Haldus (Change Management) 📝

Muudatuste halduse protsessi eesmärk on **kontrollida ja juhtida kõikide IT-teenustega seotud muudatuste tegemist**, et minimeerida nende negatiivset mõju. Muudatus on mis tahes teenuse komponendi (nt. server, võrguseade, tarkvara) lisamine, eemaldamine või modifitseerimine.

### Põhieesmärgid:
* Vähendada muudatustest tingitud intsidentide arvu.
* Tagada muudatuste dokumenteerimine ja planeerimine.
* Hinnata muudatuse riske ja potentsiaalset mõju.

### Peamised sammud:
1.  **Muudatuse Taotlus (Request for Change - RFC):** Muudatuse algatamine, kirjeldades selle eesmärki ja ulatust.
2.  **Muudatuse Hindamine:** Hinnatakse riske, mõju ja vajalikke ressursse. Sageli teostab seda **Muudatuste Nõuandev Kogu (Change Advisory Board - CAB)**.
3.  **Muudatuse Planeerimine:** Koostatakse detailne juurutuskava, tagasipöördekava (rollback) ja testiplaan.
4.  **Muudatuse Juurutamine:** Muudatuse teostamine planeeritud ajal ja viisil.
5.  **Muudatuse Järelhindamine (Post-Implementation Review - PIR):** Kontrollitakse, kas muudatus oli edukas ja täitis oma eesmärgi, ning kas intsidente ei tekkinud.

### **Päriselu Näited (Muudatuste Haldus)**

1.  **Uuenduse juurutamine (Kooli praktika stsenaarium):**
    * **Muudatus:** **CentOS 10 Server 1** (Docker host) peab saama **uue versiooni Ansible'i** tarkvarast.
    * **Protsess:** Luuakse RFC. CAB (tiimi liikmed) hindab, et uue versiooni paigaldamine võib rikkuda olemasolevaid *playbook'e*. Otsustatakse teha uuendus esmalt eraldi **testkeskkonnas (Stage)**, varundada olemasolev konfiguratsioon ning leppida kokku *maintenance window* (näiteks öötundidel) juurutamiseks. Pärast edukat juurutamist ja testide läbimist suletakse RFC.
2.  **Võrguseadete muutmine:**
    * **Muudatus:** **Fortigate ruuterile** on vaja lisada uus **VLAN 40** (nt. arendusmeeskonnale) ja seadistada sellele vastav ruutimisreegel.
    * **Protsess:** Luuakse RFC, et vältida olemasoleva liikluse häirimist. Määratakse, et muudatust tohib teha vaid **Cisco kommutaatori** ja **Fortigate**'i konfiguratsioonide varundamise järel ning seda kontrollib teine tiimiliige (peer review), et vältida *loop*-i või *broadcast storm*'i teket.
3.  **Virtuaalmasina parameetrite suurendamine:**
    * **Muudatus:** **Windows 2025 Server DC1** (Graafiline server) vajab lisaks 4GB RAM-i (kokku 12GB).
    * **Protsess:** RFC loomine. Hinnatakse, et muudatus nõuab **Proxmox**'i hüperviisoril VM-i seiskamist. Planeeritakse 15-minutiline seisak väljaspool tööaega. Pärast käivitamist kontrollitakse süsteemi logisid ja RAM-i kasutust.

---

## 2. Intsidendihaldus (Incident Management) 🚨

Intsidendihalduse eesmärk on **taastada tavapärane teenuse osutamine võimalikult kiiresti**, minimeerides negatiivset mõju äritegevusele. **Intsident** on sündmus, mis katkestab või halvendab teenuse kvaliteeti.

### Põhieesmärgid:
* Teenuse kiire taastamine.
* Intsidentide dokumenteerimine.
* Kasutajate teavitamine ja ootuste haldamine.

### Peamised sammud:
1.  **Intsidendi Avastamine ja Logimine:** Intsidendi avastamine (nt. kasutaja teade, monitooringusüsteemi alarm) ja selle registreerimine.
2.  **Klassifitseerimine ja Prioriseerimine:** Intsidendi tüübi, mõju ja kiireloomulisuse määramine. **Prioriteet (Priority)** = Mõju (Impact) + Kiireloomulisus (Urgency).
3.  **Esmane Diagnostika ja Lahendamine:** Esimese taseme (L1) spetsialist proovib intsidendi lahendada, kasutades olemasolevaid teadmisi.
4.  **Eskaleerimine:** Kui L1 ei suuda lahendada, antakse intsident edasi kõrgema taseme (L2, L3) spetsialistile.
5.  **Sulgemine:** Pärast teenuse taastamist kinnitab kasutaja lahenduse ja intsident suletakse.



[Image of Incident Management Flowchart]


### **Päriselu Näited (Intsidendihaldus)**

1.  **Veebiserveri kättesaamatus:**
    * **Intsident:** Monitooringusüsteem **(CentOS 10 Server 3 - monitor)** annab alarmi, et **veeb.xxx.praktika** (veebiserverite **veeb1** ja **veeb2** teenus) ei ole kättesaadav.
    * **Protsess:** Intsident registreeritakse **Prioriteediga 1 (Kriitiline)**. Esimese taseme kontroll näitab, et **koormusjaotur (Ubuntu 24.04 LTS server 3)** on maas. L1 spetsialist taaskäivitab koormusjaoturi, teenus taastub. Intsident lahendatakse.
2.  **Kasutaja sisselogimise probleem:**
    * **Intsident:** Kasutaja 'jperenaine' OU Töötajad alt teatab, et ta ei saa **Windows 11** kliendimasinasse sisse logida.
    * **Protsess:** Intsident **Prioriteediga 3 (Madal mõju, Keskmine kiireloomulisus)**. L1 spetsialist kontrollib **Active Directory's (DC1/DC2)** kasutaja kontot ja avastab, et konto on lukustatud liigsete ebaõnnestunud sisselogimiste tõttu. Konto lukustus eemaldatakse, sisselogimine taastub.
3.  **Wi-Fi rike:**
    * **Intsident:** Kontoritöötajad ei saa ühenduda **Ubiquiti AP** kaudu sisevõrgu Wi-Fi võrku.
    * **Protsess:** Intsident **Prioriteediga 2 (Kõrge)**. Kontrollitakse, kas **Ubiquiti halduskonsool (Docker Centos 1)** on töökorras. Selgub, et **Cisco kommutaatori** pordil, millega AP on ühendatud, on VLAN'i *tag* kadunud. Konfiguratsioon parandatakse, teenus taastub.

---

## 3. Probleemihaldus (Problem Management) 🔍

Probleemihalduse eesmärk on **identifitseerida intsidentide algpõhjused (Root Cause)** ja pakkuda lahendusi nende täielikuks eemaldamiseks või intsidendi kordumise vähendamiseks. **Probleem** on ühe või mitme intsidendi teadmata põhjus.

### Põhieesmärgid:
* Vähendada korduvate intsidentide arvu.
* Leida ja dokumenteerida intsidentide algpõhjused (Root Cause Analysis - RCA).
* Luua **Ajutised Lahendused (Workarounds)** ja **Püsivad Lahendused (Known Errors)**.

### Peamised sammud:
1.  **Probleemi Avastamine:** Intsidentide analüüsi (nt. 5 korda kordunud *DHCP time-out* intsidendid) või suure intsidendi järel.
2.  **Algpõhjuse Analüüs (RCA):** Kasutatakse tehnikaid nagu 5 *Whys* (5 Miksi) või kala-skeemi.
3.  **Ajutise Lahenduse (Workaround) Registreerimine:** Luuakse juhend, kuidas intsidendi kordumisel kiiresti teenus taastada, enne kui püsiv lahendus on valmis.
4.  **Püsiva Lahenduse väljatöötamine ja juurutamine:** Püsiva lahenduse planeerimine, mis käivitatakse läbi **Muudatuste Halduse** protsessi.
5.  **Probleemi sulgemine:** Pärast püsiva lahenduse juurutamist.

### **Päriselu Näited (Probleemihaldus)**

1.  **Korduv serveri ülekoormus:**
    * **Intsidendid:** Korduvad **CentOS 10 Server 4 (SIEM)** serveri jõudluse intsidentid (CPU kasutus 100%) iga öö kell 2.
    * **Probleem:** Algpõhjuse analüüs näitab, et kell 2 käivitub automaatne logide arhiveerimise skript, mis koormab süsteemi üle.
    * **Lahendus:** Muudatuste halduse kaudu luuakse plaan, mis nihutab logide arhiveerimise skripti käivitumise kellale 4, mil tööaeg on lõppenud ja SIEM lahendus ei ole kriitiliselt kasutusel.
2.  **Wordpressi sagedane rike:**
    * **Intsidendid:** Nii **veeb1** kui ka **veeb2** veebiserverid lähevad korra nädalas kättesaamatuks.
    * **Probleem:** RCA näitab, et WordPressi lehe andmebaasi ühendus **Centos 10 Server 2 (andmebaas)** serveriga on korduvate lühikeste katkestuste tõttu katkenud ja ei taastu automaatselt.
    * **Lahendus:** **Ajutine lahendus:** L1 meeskond taaskäivitab veebiserveril PHP teenuse. **Püsiv lahendus:** Muudatuste halduse kaudu juurutatakse *keep-alive* seadistused andmebaasi ühenduse jaoks ja luuakse **monitor** serverisse *health-check*, mis taaskäivitab PHP teenuse automaatselt.
3.  **Korduv DHCP probleem:**
    * **Intsidendid:** Kasutajad teatavad korduvatest probleemidest võrguseadete (IP aadress, DNS) saamisega **Windows 11 klientmasinates**.
    * **Probleem:** RCA näitab, et **Fortigate ruuteril** on **DHCP *snooping*** reegel, mis on liiga range ja blokeerib aeg-ajalt ka seaduslike **DC1/DC2** serverite pakette, kuigi kommutaatoril on **DHCP snooping** reegel lubatud.
    * **Lahendus:** Püsiv lahendus: Eemaldatakse DHCP snooping reegel Fortigate ruuterilt, kuna kommutaator tagab juba nõutava turvalisuse.

---

## 4. Teenuste Haldus (Service Management - näit. Service Request Fulfillment) ⚙️

Teenuste haldus hõlmab kõiki protsesse, mis on seotud klientidele IT-teenuste osutamisega. **Teenusepäring (Service Request)** on kasutaja taotlus saada midagi uut (nt. juurdepääs ressursile, uus tarkvara, uue parooli loomine) või muuta midagi standardset.

### Põhieesmärgid:
* Standardsete teenusepäringute efektiivne ja kiire täitmine.
* Kasutajate juhendamine ja eneseabi propageerimine.

### Peamised sammud:
1.  **Teenusepäringu Avastamine ja Logimine:** Kasutaja sisestab päringu iseteenindusportaali.
2.  **Autoriseerimine:** Kontrollitakse, kas kasutajal on õigus seda teenust saada.
3.  **Täitmine:** Päringu lahendamine vastavalt eelnevalt defineeritud juhistele (nt. skripti käivitamine uue kasutaja loomiseks).
4.  **Sulgemine:** Päring täidetakse ja kasutaja saab kinnituse.

### **Päriselu Näited (Teenuste Haldus)**

1.  **Juurdepääs DFS-i:**
    * **Teenusepäring:** Kasutaja 'jperenaine' OU Töötajad alt palub ligipääsu **OU Staff** kataloogile DFS failiserveris **\\grupinimi\Dokumendid\OU Staff**.
    * **Protsess:** Päring registreeritakse. Kontrollitakse **Active Directory'st**, et ta kuulub OU Töötajad alla. Päring **lükatakse tagasi**, kuna poliitika kohaselt ei tohi Töötajad grupi liikmed saada ligi teise grupi dokumentidele.
2.  **Uue tarkvara paigaldus:**
    * **Teenusepäring:** IT meeskonna liige taotleb **CentOS 10 Server 1 (docker)** masinasse paigaldada lisaks **Pythoni** arenduskeskkonna.
    * **Protsess:** Päring registreeritakse. Autoriseerimine: Jah, IT meeskonna liikmel on selleks õigus. Täitmine: **Ansible playbook** (mille arendasite Centos 1-l) käivitatakse, et paigaldada vajalik tarkvara.
3.  **Uue kasutaja loomine (Standardne päring):**
    * **Teenusepäring:** HR taotleb uue töötaja "Kati Karu" konto loomist OU Raamatupidamine alla.
    * **Protsess:** Päring registreeritakse. Kasutatakse **PowerShelli skripti** (mille lõite **DC1** serveril CSV faili alusel), mis loob automaatselt konto, lisab selle õigesse OU-sse (Raamatupidamine) ja määrab esmase parooli. *Teenusepäring täidetud.*

---

## 🛠️ Praktilised Ülesanded (Koolipraktika Lähteülesande Alusel)

Need ülesanded on seotud teie meeskonnale antud koolipraktika lähteülesandega. Nende eesmärk on rakendada õpitud IT-halduse protsesse (Muudatused, Intsidendid, Probleemid, Teenused) teie loodud IT-keskkonnas.

### **Ülesanne 1: Muudatuste Haldus (RFC & CAB)**

**Stsenaarium:** Peate oma lahenduse turvalisust parandama ja lisama kõigile Linuxi serveritele (3x Ubuntu, 4x CentOS) **Tulemüüri teenuse (nt. `firewalld` või `ufw`)** ja avama ainult minimaalselt vajalikud pordid (SSH, Veebiserveri pordid, Andmebaasi pordid, Monitooringu pordid jne). See on kriitiline muudatus, mis võib kergesti katkestada teenuste kättesaadavuse.

**Tegevused:**
1.  **Loo RFC:** Koostage detailne **Muudatuse Taotlus (RFC)** (nt. Google Docs lehel), mis sisaldab:
    * Muudatuse eesmärk (Miks?).
    * Mõju hindamine (Milliseid teenuseid puudutab? Riskid?).
    * Juurutuskava (Millises järjekorras, millised käsud?).
    * Tagasipöördekava (Kuidas eelmise oleku taastad?).
    * Testiplaan (Kuidas kontrollid, et kõik töötab?).
2.  **Teosta CAB Koosolek:** Simuleerige lühike meeskonnasisene **CAB** koosolek, kus kõik liikmed (IT tiimi liikmed) peavad andma muudatusele heakskiidu ja kinnitama tagasipöördekava.
3.  **Juuruta Muudatus:** Kasutage selle muudatuse juurutamiseks **Ansible Playbook'i** (mille te loote ja hoiate oma **Git** repositooriumis).
4.  **Järelhindamine:** Pärast juurutamist kontrollige teenuseid ja dokumenteerige tulemused RFC-sse (PIR).

### **Ülesanne 2: Intsidendi- ja Probleemihaldus (L1, RCA, Workaround)**

**Stsenaarium:** Saite teate **monitor.xxx.praktika (CentOS 10 Server 3)** monitooringult, et **DC2 (Windows 2025 Core server)** on korra päevas käinud **10 minutit *Offline***. See on korduv intsident, mis tekib ebaregulaarselt, kuid häirib DFS replikatsiooni.

**Tegevused:**
1.  **Intsidendi Haldus:**
    * **L1 Reageerimine:** Registreerige see kui **Prioriteet 2 (Kõrge)** intsident. Tehke esimene diagnostika (nt. vaadake Proxmox'i logisid, kas see on seotud mingi automaatse Proxmoxi ülesandega). Eeldame, et L1 lahendust ei leia.
    * **Eskaleerimine:** Eskaleerige intsident Probleemihaldusele (IT meeskond).
2.  **Probleemihaldus (RCA):**
    * **Algpõhjuse Analüüs (RCA):** Avastage, et server **DC2** läheb *offline* täpselt samal ajal, kui **DC1** serveris käivitub **kriitiliste teenuste varundus** (mille te teostate). Varundus koormab füüsilist RAID1 ketast ja põhjustab lühikese katkestuse virtualiseerimiskeskkonnas.
    * **Ajutine Lahendus (Workaround):** Looge kirjalik juhend L1 meeskonnale: "Intsidendi kordumisel oota 10 minutit, seejärel kontrolli DFS replikatsiooni olekut ja vajadusel käivita see käsitsi."
    * **Püsiv Lahendus:** Tehke **Muudatuste Taotlus (RFC)**, et muuta varunduse aega näiteks 4 tundi hilisemaks või optimeerida varundusprotsessi, et see koormaks vähem ketast.

### **Ülesanne 3: Teenuste Haldus (Service Request Fulfillment)**

**Stsenaarium:** Uus töötaja on vaja lisada süsteemi: **Jüri Jõgi, IT osakond.**

**Tegevused:**
1.  **Teenusepäringu Loomine:** Kirjeldage, millist standardset tegevust see nõuab (uue AD kasutaja loomine, lisamine õigesse OU-sse KASUTAJAD/IT, uue parooli loomine, ligipääs DFS-i IT kaustale).
2.  **Täitmine:** Käivitage loodud **PowerShelli skript** (mis toetab CSV-st kasutajate importi) uue kasutaja loomiseks ja **kontrollige, et ta saaks ligi \\grupinimi\Dokumendid\IT kaustale, aga ei saaks ligi \\grupinimi\Dokumendid\Raamatupidamine kaustale.**
3.  **Dokumentatsioon:** Dokumenteerige teenusepäringu täitmise logi (nt. **SIEM (CentOS 10 Server 4)** logides), et see protsess on korrektselt teostatud ja vastab turvanõuetele.

---

## ✅ Näidisülesanne Valmis Lahendusega (Teenusepäring)

See näide annab selge arusaama, kuidas ülesannet teostada ja dokumenteerida.

### **Lähteülesanne:** *Keskne tarkvara paigaldus (GPO’de abil).*

> Seadistage GPO, mis kõikidesse OU ARVUTID all olevatele arvutitele paigaldab **7zip** ja **Google Chrome Enterprise** tarkvarad.

### **Näidisülesanne: Teenusepäringu Täitmine - Uue Tarkvara paigaldamine GPO abil**

#### **1. Muudatuse Taotlus (RFC 2025-001) - Turvalisuse Parandamine**

| Väli | Väärtus |
| :--- | :--- |
| **Muudatuse Nimetus** | 7zip ja Chrome Enterprise tarkvara paigaldus kõigile klientarvutitele. |
| **Muudatuse Tüüp** | Standardne (kinnitatakse eeldusel, et testitud) |
| **Eesmärk** | Tagada standardne tarkvaravalik ja parem turvalisus (7zip toetab krüpteerimist, Chrome Enterprise pakub paremat haldust). |
| **Mõju** | Väike - puudutab ainult OU ARVUTID all olevaid Windows 11 masinaid. Nõuab arvuti taaskäivitust. |
| **Juurutuskava** | 1. Lae alla `.msi` failid. 2. Loo GPO objekt **DC1** serveris. 3. Testi paigaldust **Windows 11-3 (PXE paigaldatud masinal)**. 4. Seosta GPO **OU ARVUTID**-ga. 5. Tõsta GPO tootmisse. |
| **Tagasipöördekava** | Eemalda GPO seos **OU ARVUTID**-ga ja oota *Group Policy update* (*`gpupdate /force`*). Tarkvara eemaldatakse paigaldatud rakenduste loendist. |
| **Testiplaan** | Logi sisse **Windows 11-3** masinasse, käivita *`gpupdate /force`*, taaskäivita. Kontrolli, kas **7zip** ja **Chrome** on paigaldatud. |
| **Heakskiit (CAB)** | Tiimiliige 1 (Kinnitatud), Tiimiliige 2 (Kinnitatud) |

#### **2. Teostus (Windows 2025 Server DC1)**

1.  **Lae alla ja jaga tarkvara:**
    * Laaditakse alla **7zip** ja **Google Chrome Enterprise** `.msi` failid.
    * Failid kopeeritakse **DC1** serveris asuvasse jagatud võrgukataloogi, näiteks: *`\\DC1\NetInstall\Software`*.

2.  **Loo GPO:**
    * Avatakse **Group Policy Management Console**.
    * Luukse uus **GPO (Group Policy Object)** nimega *`Tarkvara_7zip_Chrome`*.
    * Navigeeritakse: *`Computer Configuration`* $\rightarrow$ *`Policies`* $\rightarrow$ *`Software Settings`* $\rightarrow$ *`Software installation`*.
    * Lisatakse Chrome ja 7zip **paigalduspaketid (.msi)** võrguteelt: *`\\DC1\NetInstall\Software\7z.msi`* ja *`\\DC1\NetInstall\Software\ChromeEnterprise.msi`*. Valitakse *`Assigned (Required)`* paigaldus.

3.  **Seosta GPO:**
    * Seostatakse *`Tarkvara_7zip_Chrome`* GPO **OU ARVUTID**-ga.

#### **3. Testimine ja Järelhindamine (Windows 11-3)**

1.  **Testi arvutis:**
    * Logitakse sisse **Windows 11-3** klientmasinasse (mis on **OU ARVUTID** all).
    * Käivitatakse *`gpupdate /force`*.
    * Taaskäivitatakse masin.

2.  **Kontroll:**
    * Pärast taaskäivitust kontrollitakse **Installed Programs** nimekirjast, et **7zip** ja **Google Chrome Enterprise** on olemas.
    * *Tulemus: **Edukalt paigaldatud.***

#### **4. Sulgemine**

* RFC 2025-001 märgitakse olekusse **Tehtud/Suletud**.
* **Git** repositooriumisse lisatakse **GPO seadistuse ekraanipildid** ja **paigaldamise logi Windows 11-st** kui **PIR** dokumentatsioon.
