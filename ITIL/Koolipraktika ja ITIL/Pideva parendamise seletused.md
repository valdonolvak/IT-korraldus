[cite_start]ITIL 4 kontekstis ei tähenda süsteemi valmimine töö lõppu, vaid **pideva parendamise (Continual Improvement)** algust.Pidev parendamine on korduv tegevus, mille eesmärk on tagada, et teenuse toimivus vastaks alati sidusrühmade ootustele.See tugineb iteratsioonidele ja tagasisidele, et tuvastada uusi võimalusi ja probleeme.

Siin on pideva parendamise selgitused iga sinu projektis paigaldatava põhiteenuse kohta:

---

### 1. AD Domeen ja DHCP (Keskne haldus)
* **Parendus:** Regulaarne kasutajakontode ja organisatsiooniüksuste (OU) struktuuri audit.
***Selgitus:** Kasutades monitooringu tagasisidet, saab optimeerida DHCP aadressivahemikke, kui seadmete hulk võrgus muutub.Iteratiivselt saab täiendada skripte, mis lisavad kasutajaid, et need kontrolliksid veelgi põhjalikumalt andmete korrektsust.

### 2. GPO (Tarkvara ja turvapoliitikad)
* **Parendus:** Tarkvaraversioonide ja turvasätete pidev ajakohastamine.
***Selgitus:** Tagasiside põhjal, kus kasutajad vajavad uusi tööriistu, saab luua uusi GPO-sid.Parendusprotsess tagab, et paroolipoliitikad ja töölaua piirangud vastavad alati organisatsiooni uusimatele turvastandarditele.

### 3. DFS Failihoidla
* **Parendus:** Kettaruumi kasutuse analüüs ja ligipääsuõiguste täpsustamine.
***Selgitus:** Jälgides failiserveri koormust, saab optimeerida andmete liikumist DC1 ja DC2 vahel.Pidev parendamine tähendab siin ka failifiltrite (File Screening) täiendamist, et tõkestada uute ohtlike failitüüpide salvestamist.

### 4. Veebiserverid ja Koormusjaotur (HAProxy)
* **Parendus:** Veebiliikluse analüüs ja jõudluse tuunimine.
***Selgitus:** Kasutades koormusjaoturi logisid, saab tuvastada "pudelikaelu" ja muuta HAProxy reegleid nii, et liiklus jaguneks veebiserverite vahel veelgi efektiivsemalt.See on iteratiivne protsess teenuse kättesaadavuse ja garantii tõstmiseks.

### 5. Docker ja Portainer
* **Parendus:** Konteinerite ressursside piiramine ja turvapaigad.
***Selgitus:** Pidevalt tuleb jälgida, et konteinerid (nt Ubiquiti konsool) ei tarbiks liigselt serveri mälu.Parendamine hõlmab ka konteinerite kujutiste (images) regulaarset uuendamist turvakaalutlustel.

### 6. Monitooring (Zabbix) ja SIEM (Wazuh)
* **Parendus:** Hoiatuste (alerts) täpsustamine ja "müra" vähendamine.
* **Selgitus:** Alguses seadistatud monitooring võib anda liiga palju tühiseid teavitusi.Pidev parendamine tähendab lävendite (thresholds) peenhäälestamist, et IT-tiim saaks teavitusi ainult kriitiliste sündmuste kohta.

### 7. OS Masspaigaldus (WDS) ja MDM (FleetDM)
* **Parendus:** Operatsioonisüsteemi kujutiste (images) ja tarkvarapakettide värskendamine.
***Selgitus:** Kogudes tagasisidet uute arvutimudelite kohta, saab WDS-i lisada vajalikud draiverid.MDM lahendust täiendatakse uute kontrollreeglitega (compliance policies), et tagada masinate vastavus turvanõuetele.

### 8. Varundussüsteem
* **Parendus:** Taasteprotsessi (Restore) regulaarne testimine ja optimeerimine.
***Selgitus:** Parendamine tähendab varundusskriptide muutmist nii, et need teeksid varukoopiaid kiiremini või tarbiksid vähem kettaruumi (nt deduplikatsioon), tagades samas andmete säilimise garantii.

### 9. Võrguseadmed ja Wifi (Cisco, Ubiquiti)
* **Parendus:** Võrgu segmentatsiooni ja Wifi katvuse parandamine.
***Selgitus:** Kasutades SIEM-i ja monitooringu andmeid, saab tuvastada ebatavalist liiklust VLAN-ide vahel ja karmistada tulemüüri reegleid.Wifi leviala saab parandada tuginedes kasutajate tagasisidele "surnud tsoonide" kohta kontoris.



---
