**Muudatuste-, intsidendi-, probleemi- ja teenustehaldus**

---

# 1. **Teenuste haldus (Service Management – SM)**

**Teenuste haldus (SM – Service Management)** on metoodika ja juhtimispraktikate kogum, mille eesmärk on tagada, et IT-teenused toetavad ettevõtte äriprotsesse usaldusväärselt, efektiivselt ja turvaliselt. ITIL (ITIL – *Information Technology Infrastructure Library*) on selle kõige tuntum raamistik.

---

## 1.1. Mis on IT-teenus?

**IT-teenus** ei ole lihtsalt tarkvara või server – see on kombinatsioon:

* infrastruktuurist (serverid, võrgud, andmebaasid)
* tarkvarast ja rakendustest
* protsessidest
* tugiteenustest
* kasutajatoest

Näide teenusest:

* “E-posti teenus” → sisaldab e-posti serverit, webmail'i, autentimist (LDAP – *Lightweight Directory Access Protocol*), spämmitõrjet, varundust jne.

### Oluline on mõista:

**Kasutaja ei vaja serverit. Ta vajab teenust (nt e-posti).**
Seetõttu peab IT korraldama teenuseid tervikuna, mitte ainult üksikuid komponente.

---

## 1.2. Teenuste halduse kolm kokkuleppe tüüpi

### 1) **SLA (Service-Level Agreement – teenustaseme kokkulepe)**

Kokkulepe IT ja äri vahel teenuse kvaliteedi kohta.

Tüüpilised SLA näitajad:

* kättesaadavus (availability): nt 99,9%
* probleemidele reageerimise aeg
* lahendamise aeg
* hooldusaknad (maintenance window)

### 2) **OLA (Operational-Level Agreement – operatsioonitaseme kokkulepe)**

Kokkulepe IT-osakonna *sisemiste* tiimide vahel.

Näide:
Serveritiimi OLA võrgutiimiga:

* “Serverite hooldusaknad tuleb kooskõlastada 48 h ette.”
* “Võrgutiim tagab 1h jooksul ühenduse taastamise P1 intsidentide puhul.”

### 3) **UC (Underpinning Contract – teenust toetav leping)**

Kui IT kasutab väliseid teenuseid.

Näide:

* Pilveteenuse pakkuja lubab 99,95% uptime’i.
* Varundusteenuse pakkuja lubab 24h taastusvõimekust.

---

## 1.3. Teenuste halduse põhikomponendid

### • **Service Portfolio (teenuste portfell)**

Kõigi teenuste nimekiri – nii aktiivsed, arendamisel kui lõpetatud teenused.

### • **Service Catalog (teenusekataloog)**

Ainult aktiivsete teenuste kirjeldused.

Iga teenuse juures:

* eesmärk
* SLA
* omanik
* komponentide loend
* vastutused

### • **Service Owner (teenuse omanik)**

Äri- või IT-isik, kes vastutab teenuse toimimise eest tervikuna.

### • **Process Owner (protsessi omanik)**

Näiteks intsidentihalduse omanik, probleemihalduse omanik jne.

---

# 📌 **Teenuste halduse reaalne näide**

Ettevõttes on “Failiserveri teenus”.
Teenuse omadused:

* SLA: 99,9%
* Kasutajatoe reageerimisaeg: 15 min
* Failide varundus 1x ööpäevas
* AD-grupid (Active Directory – kasutajahaldus) määravad õigused

Kui failid kaovad:
→ töötab intsidentihaldus
Kui failid kaovad iga nädal:
→ töötab probleemihaldus
Kui varundussüsteemi uuendatakse:
→ töötab muutmishaldus

Kõik on osa teenuste haldusest.

---

# 2. **Intsidendihaldus (Incident Management – IM)**

## 2.1. Mis on intsident?

**Intsident (Incident)** on *ootamatu katkestus* või teenuse kvaliteedi oluline langus.
Oluline: intsident võib olla ka *märkimisväärne aeglustumine*, mitte ainult täielik katkestus.

Näited:

* e-post ei tööta
* serveri CPU 100%
* andmebaas vastab aeglaselt
* printer ei prindi
* kasutaja ei saa sisse logida

---

## 2.2. Intsidentihalduse peamine eesmärk

👉 **Taastada teenuse normaalne töö võimalikult kiiresti**, minimeerides mõju ärile.

Intsidendihaldus ei keskendu põhjustele – see teeb probleemihaldus.

---

## 2.3. Intsidentide prioriteerimine (P1–P4)

Prioriteet sõltub:

* mõjust (impact)
* kiirusest / mahust (urgency)

### P1 – kriitiline

Täielik teenuse seisak, väga suur äriline mõju.
• Näide: maksesüsteem ei tööta e-poes → müük peatub.

### P2 – kõrge

Osaline katkestus või oluline mõju.
• Näide: müügiosakond ei pääse CRM-i.

### P3 – keskmine

Üksiku kasutaja probleem.
• Näide: ühe kasutaja Outlook ei ava e-kirju.

### P4 – madal

Väike ebamugavus või kosmeetiline viga.
• Näide: tarkvaras ikoon ei kuva korrektselt.

---

## 2.4. Intsidendi elutsükkel (IMLC)

1. **Avastamine ja registreerimine**
   Tavaliselt helpdeski süsteemis (nt JIRA Service Management, OTRS, GLPI).

2. **Klassifitseerimine**
   Kategooria määramine: võrk / server / printer / e-post / turvalisus jne.

3. **Prioriteetide seadmine (P1–P4)**

4. **Diagnostika (First-Line Support – FLS)**
   Esmatugi lahendab 60–80% juhtudest.

5. **Eskalatsioon (Second-Line SLS, Third-Line TLS)**
   SLS – spetsialistid
   TLS – süsteemi arendajad või tootja

6. **Lahendamine ja kontroll**

7. **Sulgemine**

---

# 📌 **Intsidendihalduse reaalne juhtum**

**Staatus:** P1
**Probleem:** ettevõtte andmebaas ei tööta, e-pood on täiesti maas.

**Protsess:**

1. Süsteem tuvastab alarmi – monitoring (Zabbix, Prometheus).
2. Esmatugi registreerib P1 intsidenti.
3. Kohene eskalatsioon andmebaasitiimile.
4. DBA (database administrator – andmebaasi administraator) tuvastab:

   * RAID-ketas on maas
5. Failover (üleviimine teisele serverile) taastab töö 5 minutiga.
6. Intsident suletakse, kuid:
7. Algatatakse **probleemihaldus**, et uurida miks kettarike toimus.

---

# 3. **Probleemihaldus (Problem Management – PM)**

## 3.1. Mis on probleem?

**Probleem (Problem)** on intsidentide juurpõhjus või potentsiaalne juurpõhjus.
See võib olla avaldunud või varjatud.

Näited:

* tarkvaraviga, mis põhjustab serveri restarti
* riknenud võrgujuhe, mis põhjustab aeg-ajalt katkestusi
* mälu leke (memory leak) veebirakenduses
* vigane konfiguratsioon Firewalls

---

## 3.2. Probleemihalduse eesmärgid

1. **Leida põhjus (RCA – Root Cause Analysis)**
2. **Lõplikult kõrvaldada korduv intsident**
3. **Ennetada tulevasi intsidente**
4. **Luua workaroundid**, kuni lahendus on valmis

---

## 3.3. KEDB – Known Error DataBase

**KEDB (Known Error DataBase)** sisaldab:

* tuntud viga
* selle põhjus (kui teada)
* workaround (ajutine lahendus)
* seotud juhtumid

KEDB aitab esmastugil kiiremini lahendada korduvaid probleeme.

---

## 3.4. RCA (Root Cause Analysis)

Levinud analüüsimeetodid:

* **5 Why’s (Miks? Miks? Miks?)**
* **Ishikawa diagramm (kalasaba diagramm)**
* **FMEA (Failure Mode and Effects Analysis)**
* **Logianalüüs**

---

# 📌 **Probleemihalduse reaalne juhtum**

**Sümptom:**
Igal hommikul kell 8 muutub andmebaas aeglaseks.

**Intsident:**
SLS tuvastab, et CPU kasutus tõuseb 100% peale.

**Probleemihaldus:**

* Logianalüüs näitab, et üks plaanitud raporti päring (query) koormab kogu süsteemi.
* Probleem: SQL päring on ebaoptimeeritud.
* Workaround:
  Raporti käivitusaeg lükatakse 02:00 peale.
* Püsiv lahendus:
  Päring kirjutatakse optimeeritult ümber.

---

# 4. **Muutmishaldus (Change Management – CM)**

## 4.1. Mis on muutus?

**Muutus (Change)** on *kõik*, mis:

* lisab midagi uue süsteemi
* muudab olemasolevat
* eemaldab midagi

Muutus võib mõjutada teenuse jõudlust, turvalisust või stabiilsust.

---

## 4.2. Muutuste tüübid

### ● **Standard Change (standardne muutus)**

* korduv
* madala riskiga
* automaatselt heaks kiidetud

Näited:

* kasutaja parooli lähtestamine
* uue printeri lisamine
* uue töötaja e-konto loomine

### ● **Normal Change (tavaline muutus)**

* vajab riskide hindamist
* läbib CAB-i

### ● **Emergency Change (erakorraline muutus)**

* rakendatakse kohe
* CAB kinnitab hiljem tagantjärele

Näited:

* kriitilise turvavea lappimine
* firewall'i reegli muutmine ründe ajal

---

## 4.3. CAB (Change Advisory Board – muutusenõukogu)

CAB liikmed:

* teenuse omanik
* süsteemiadministraator
* infoturbe esindaja
* arhitekt
* äri esindaja

CAB roll:

* analüüsib riske
* hindab mõju
* kinnitab või lükkab tagasi muudatused

---

## 4.4. Muutuse elutsükkel (CHLC – Change Lifecycle)

1. **RFC (Request for Change – muudatusetaotlus)**
   Kirjeldab muudatust, ajakava, riske, taastamisplaani.

2. **Hindamine**
   Kuidas see mõjutab teisi teenuseid?

3. **CAB-i heakskiit**

4. **Rakendamine**
   Tihti hooldusaknal (maintenance window).

5. **Testimine**

6. **Sulgmine ja dokumenteerimine**

---

# 📌 **Reaalne muutmishalduse juhtum**

**Muutus:**
Turvapaikude paigaldus Linuxi serverile.

**Riskid:**

* teenus võib maha kukkuda
* kernel update võib nõuda restarti
* teenuse katkestus võib olla pikem kui SLA lubab

**a) Standard change?**
Ei, sest kõrge risk.

**b) Normal change?**
Jah.

**Protsess:**

1. Admin täidab RFC.
2. CAB arutab: “Kas on varuserver olemas?”
3. Muutus teostatakse ööl vastu pühapäeva.
4. Teenus testitakse.
5. Muutus suletakse.

---

# 5. **Protsesside omavaheline seos (kuidas kõik koos töötab)**

Teenuste haldus = suur pilt
Intsidendihaldus = kiire tulekahju kustutamine
Probleemihaldus = korduvate tulekahjude lõpetamine
Muutmishaldus = muudatuste ohutu ja kontrollitud tegemine

**Tüüpiline töövoog:**

1. Tekib intsident (server maas)
2. Probleemihaldus tuvastab põhjuse (toiteploki rike)
3. Muutmishaldus rakendab lahenduse (serveri asendamine)
4. Teenuse omanik jälgib SLA täitmist

---
