[cite_start]Sinu IT-projekti **väärtuspakkumine** (Service Offering) on ametlik kirjeldus teenustest, mis on loodud vastama organisatsiooni (sihttarbijate) vajadustele[cite: 90, 91]. [cite_start]ITIL 4 kohaselt koosneb see pakkumine kolmest peamisest komponendist: kaupadest, juurdepääsust ressurssidele ja teenindustoimingutest[cite: 92, 93].



Siin on  rojekti väärtuspakkumise näidissõnastus:

---

## IT-terviklahenduse väärtuspakkumine (Service Offering)

[cite_start]Käesolev projekt pakub organisatsioonile täielikku digitaalset töömudelit, mis on suunatud tööprotsesside optimeerimisele, turvalisuse tagamisele ja tehniliste riskide maandamisele[cite: 5]. Meie väärtuspakkumine jaguneb kolmeks:

### 1. Kaubad (Goods)
[cite_start]Need on materiaalsed väljundid, mille omandiõigus ja vastutus edasise kasutamise eest läheb üle tarbijale[cite: 97, 98].
* [cite_start]**Kasutusvalmis klientarvutid:** Konfigureeritud Windows 11 ja Ubuntu masinad koos vajaliku tarkvaraga[cite: 99].
* **Võrgu infrastruktuur:** Paigaldatud Cisco ruuter ja kommutaator ning Ubiquiti Wifi tugijaam koos grupi poolt valmistatud võrgukaablitega.
* **Riistvaraline vundament:** Hooldatud ja uuendatud püsivaraga Supermicro/Fujitsu server koos RAIDZ-1 kettamassiiviga andmete turvalisuse tagamiseks.

### 2. Juurdepääs ressurssidele (Access to Resources)
[cite_start]Teenusepakkuja (IT-tiim) annab tarbijale õiguse kasutada ressursse kokkulepitud tingimustel, kuid omandiõigus jääb pakkujale[cite: 100, 101].
* **Keskne identiteedihaldus:** Juurdepääs AD domeenile ja sisselogimisteenusele individuaalsete kasutajakontode kaudu.
* **Failihaldus (DFS):** Ligipääs ühisele failihoidlale vastavalt kasutaja rollile (OU-le).
* [cite_start]**Võrguühendus:** Juurdepääs sisevõrgule ja külaliste Wifi-le läbi eraldatud VLAN-ide[cite: 102].
* **Infosüsteemid:** Pääs ettevõtte avalikule veebilehele ja siseveebile (Intranet).

### 3. Teenindustoimingud (Service Actions)
[cite_start]Toimingud, mida IT-meeskond teostab tarbija vajaduste rahuldamiseks ja teenuse kvaliteedi hoidmiseks[cite: 103, 104].
* **Tarkvara automaatne haldus:** Keskne tarkvara paigaldus ja uuendamine läbi GPO-de ja Ansible'i.
* **Turvaseire ja monitooring:** SIEM (Wazuh) ja monitooringu (Zabbix) kaudu teostatav pidev järelevalve süsteemi tervise üle.
* **Andmete kaitse:** Igapäevane automatiseeritud varundusprotsess kriitiliste andmete säilimise tagamiseks.
* [cite_start]**Kasutajatugi ja paroolihaldus:** Toetus teenuste kasutamisel ja ligipääsuinfo turvaline haldamine paroolihalduris[cite: 105].

---

## Pakutav väärtus (Value)

[cite_start]Selle väärtuspakkumise kaudu aitame organisatsioonil saavutada soovitud **tulemusi** (Outcomes), vähendades samal ajal nende kulusid ja riske[cite: 161]:
* [cite_start]**Toetatud tulemus:** Töötajad saavad teha oma tööd turvalises ja stabiilses keskkonnas ilma mureta tehnilise infrastruktuuri pärast[cite: 173].
* [cite_start]**Eemaldatud riskid:** Dubleeritud serverid (DC, DHCP) ja varundus vähendavad riski, et töö seiskub riistvara vea tõttu[cite: 205].
* [cite_start]**Optimeeritud kulud:** Keskselt hallatud tarkvara ja automatiseeritud OS-i paigaldus vähendavad IT-haldusele kuluvat aega ja inimressurssi[cite: 190].
