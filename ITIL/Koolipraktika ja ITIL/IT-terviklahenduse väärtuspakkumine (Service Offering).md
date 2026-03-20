Sinu IT-projekti **väärtuspakkumine** (Service Offering) on ametlik kirjeldus teenustest, mis on loodud vastama organisatsiooni (sihttarbijate) vajadustele. ITIL 4 kohaselt koosneb see pakkumine kolmest peamisest komponendist: kaupadest, juurdepääsust ressurssidele ja teenindustoimingutest.



Siin on  rojekti väärtuspakkumise näidissõnastus:

---

## IT-terviklahenduse väärtuspakkumine (Service Offering)

Käesolev projekt pakub organisatsioonile täielikku digitaalset töömudelit, mis on suunatud tööprotsesside optimeerimisele, turvalisuse tagamisele ja tehniliste riskide maandamisele. Meie väärtuspakkumine jaguneb kolmeks:

### 1. Kaubad (Goods)
Need on materiaalsed väljundid, mille omandiõigus ja vastutus edasise kasutamise eest läheb üle tarbijale.
* **Kasutusvalmis klientarvutid:** Konfigureeritud Windows 11 ja Ubuntu masinad koos vajaliku tarkvaraga.
* **Võrgu infrastruktuur:** Paigaldatud Cisco ruuter ja kommutaator ning Ubiquiti Wifi tugijaam koos grupi poolt valmistatud võrgukaablitega.
* **Riistvaraline vundament:** Hooldatud ja uuendatud püsivaraga Supermicro/Fujitsu server koos RAIDZ-1 kettamassiiviga andmete turvalisuse tagamiseks.

### 2. Juurdepääs ressurssidele (Access to Resources)
Teenusepakkuja (IT-tiim) annab tarbijale õiguse kasutada ressursse kokkulepitud tingimustel, kuid omandiõigus jääb pakkujale.
* **Keskne identiteedihaldus:** Juurdepääs AD domeenile ja sisselogimisteenusele individuaalsete kasutajakontode kaudu.
* **Failihaldus (DFS):** Ligipääs ühisele failihoidlale vastavalt kasutaja rollile (OU-le).
* **Võrguühendus:** Juurdepääs sisevõrgule ja külaliste Wifi-le läbi eraldatud VLAN-ide.
* **Infosüsteemid:** Pääs ettevõtte avalikule veebilehele ja siseveebile (Intranet).

### 3. Teenindustoimingud (Service Actions)
Toimingud, mida IT-meeskond teostab tarbija vajaduste rahuldamiseks ja teenuse kvaliteedi hoidmiseks.
* **Tarkvara automaatne haldus:** Keskne tarkvara paigaldus ja uuendamine läbi GPO-de ja Ansible'i.
* **Turvaseire ja monitooring:** SIEM (Wazuh) ja monitooringu (Zabbix) kaudu teostatav pidev järelevalve süsteemi tervise üle.
* **Andmete kaitse:** Igapäevane automatiseeritud varundusprotsess kriitiliste andmete säilimise tagamiseks.
* **Kasutajatugi ja paroolihaldus:** Toetus teenuste kasutamisel ja ligipääsuinfo turvaline haldamine paroolihalduris.

---

## Pakutav väärtus (Value)

Selle väärtuspakkumise kaudu aitame organisatsioonil saavutada soovitud **tulemusi** (Outcomes), vähendades samal ajal nende kulusid ja riske:
* **Toetatud tulemus:** Töötajad saavad teha oma tööd turvalises ja stabiilses keskkonnas ilma mureta tehnilise infrastruktuuri pärast.
* **Eemaldatud riskid:** Dubleeritud serverid (DC, DHCP) ja varundus vähendavad riski, et töö seiskub riistvara vea tõttu.
* **Optimeeritud kulud:** Keskselt hallatud tarkvara ja automatiseeritud OS-i paigaldus vähendavad IT-haldusele kuluvat aega ja inimressurssi.
