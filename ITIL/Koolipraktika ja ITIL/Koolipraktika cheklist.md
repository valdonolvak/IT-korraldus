Siin on põhjalik ITIL 4 juhtpõhimõtetel põhinev kontroll-leht, mis on kohandatud spetsiaalselt sinu IT-projekti vajadustele. [cite_start]See tööriist aitab sul dokumentatsioonis tõendada, et sa ei tegele lihtsalt "kaablite vedamisega", vaid juhid süsteemi vastavalt rahvusvahelistele parimatele praktikatele.

---

## 📋 ITIL 4 Juhtpõhimõtete Kontroll-leht

[cite_start]See tabel on mõeldud kasutamiseks projekti igas etapis, et tagada ühtne lähenemine ja vältida "silode" tekkimist.

| ITIL Juhtpõhimõte | Kontrollküsimus projekti kohta | Seos Sinu ülesandega | Tehtud (Jah/Ei) |
| :--- | :--- | :--- | :--- |
| **1. [cite_start]Keskendu väärtusele**  | [cite_start]Kas iga seadistatud teenus (nt GPO, DFS) toetab otseselt lõppkasutaja vajadusi?  | [cite_start]GPO-d on määratud õigetele OU-dele (nt ID-kaardi tarkvara töötajatele).  | |
| **2. [cite_start]Alusta sealt, kus oled**  | [cite_start]Kas olemasolev riistvara on kontrollitud ja ette valmistatud enne uue tarkvara lisamist?  | [cite_start]Serveri füüsiline hooldus ja BIOS-i/RAID-i püsivara uuendus on tehtud.  | |
| **3. [cite_start]Edenege iteratiivselt**  | [cite_start]Kas lahendust on testitud väikeste osadena (MVP), enne kui see massiliselt kasutusele võeti?  | [cite_start]Windows 11 paigaldust on testitud esmalt ühel "tühjal masinal" läbi WDS-i.  | |
| **4. [cite_start]Tee koostööd**  | [cite_start]Kas kogu info on tiimile nähtav ja kättesaadav, et vältida oletusi ja viivitusi?  | [cite_start]Dokumentatsioon asub Google Sites lehel ja kõik skriptid on GitHubi repositooriumis.  | |
| **5. [cite_start]Tööta terviklikult**  | [cite_start]Kas on arvestatud, kuidas muudatus ühes osas (nt VLAN-id) mõjutab süsteemi teisi osi?  | [cite_start]IP-plaan ja topoloogia joonised katavad nii servereid, kliente kui ka võrguseadmeid.  | |
| **6. [cite_start]Hoia asjad lihtsad**  | [cite_start]Kas on välditud liigset keerukust ja iga samm protsessis loob reaalset väärtust?  | [cite_start]Kasutajate loomine toimub automaatselt skriptiga, vältides sadu manuaalseid ja vigaseid liigutusi.  | |
| **7. [cite_start]Optimeeri ja automatiseeri**  | [cite_start]Kas inimressurssi on säästetud korduvate tegevuste automatiseerimisega?  | [cite_start]Ansible playbookid ja WDS masspaigaldus vähendavad vajadust manuaalseks sekkumiseks.  | |

---

## 💡 Olulised selgitused dokumentatsiooni jaoks

Selleks, et su esitlus oleks eriti "itililik", võid lisada kontroll-lehe juurde järgmised kommentaarid:

* [cite_start]**Väärtuse koosloome (Co-creation):** Me ei ehita süsteemi endale, vaid loome keskkonna, kus "Raamatupidamine" ja "IT-osakond" saavad koostöös väärtust toota.
* [cite_start]**Tagasisideahelad (Feedback loops):** Iga iteratsiooni (nt esimene veebiserveri püstitamine) järel kogusime tagasisidet (testisime kättesaadavust), et parandada järgmisi samme.
* [cite_start]**Kasulikkus vs Garantii:** AD sisselogimine pakub **kasulikkust** (utility - "fit for purpose"), samas kui dubleeritud DC-d ja DHCP serverid tagavad teenuse **garantii** (warranty - "fit for use"), kättesaadavuse ja turvalisuse.



---

[cite_start]**Kas soovid, et ma aitaksin sul sõnastada ka projekti "Väärtuspakkumise" (Service Offering) osa, mis kirjeldaks, milliseid kaupu ja ressursse sa lõppkasutajale tarnid?** 
