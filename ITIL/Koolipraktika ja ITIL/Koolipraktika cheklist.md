Siin on põhjalik ITIL 4 juhtpõhimõtetel põhinev kontroll-leht, mis on kohandatud spetsiaalselt sinu IT-projekti vajadustele. See tööriist aitab sul dokumentatsioonis tõendada, et sa ei tegele lihtsalt "kaablite vedamisega", vaid juhid süsteemi vastavalt rahvusvahelistele parimatele praktikatele.

---

## 📋 ITIL 4 Juhtpõhimõtete Kontroll-leht

See tabel on mõeldud kasutamiseks projekti igas etapis, et tagada ühtne lähenemine ja vältida "silode" tekkimist.

| ITIL Juhtpõhimõte | Kontrollküsimus projekti kohta | Seos Sinu ülesandega | Tehtud (Jah/Ei) |
| :--- | :--- | :--- | :--- |
| **1. Keskendu väärtusele**  | Kas iga seadistatud teenus (nt GPO, DFS) toetab otseselt lõppkasutaja vajadusi?  | GPO-d on määratud õigetele OU-dele (nt ID-kaardi tarkvara töötajatele).  | |
| **2. Alusta sealt, kus oled**  | Kas olemasolev riistvara on kontrollitud ja ette valmistatud enne uue tarkvara lisamist?  | Serveri füüsiline hooldus ja BIOS-i/RAID-i püsivara uuendus on tehtud.  | |
| **3. Edenege iteratiivselt**  | Kas lahendust on testitud väikeste osadena (MVP), enne kui see massiliselt kasutusele võeti?  | Windows 11 paigaldust on testitud esmalt ühel "tühjal masinal" läbi WDS-i.  | |
| **4. Tee koostööd**  | Kas kogu info on tiimile nähtav ja kättesaadav, et vältida oletusi ja viivitusi?  | Dokumentatsioon asub Google Sites lehel ja kõik skriptid on GitHubi repositooriumis.  | |
| **5. Tööta terviklikult**  | Kas on arvestatud, kuidas muudatus ühes osas (nt VLAN-id) mõjutab süsteemi teisi osi?  | IP-plaan ja topoloogia joonised katavad nii servereid, kliente kui ka võrguseadmeid.  | |
| **6. Hoia asjad lihtsad**  | Kas on välditud liigset keerukust ja iga samm protsessis loob reaalset väärtust?  | Kasutajate loomine toimub automaatselt skriptiga, vältides sadu manuaalseid ja vigaseid liigutusi.  | |
| **7. Optimeeri ja automatiseeri**  | Kas inimressurssi on säästetud korduvate tegevuste automatiseerimisega?  | Ansible playbookid ja WDS masspaigaldus vähendavad vajadust manuaalseks sekkumiseks.  | |

---

## 💡 Olulised selgitused dokumentatsiooni jaoks

Selleks, et su esitlus oleks eriti "itililik", võid lisada kontroll-lehe juurde järgmised kommentaarid:

* **Väärtuse koosloome (Co-creation):** Me ei ehita süsteemi endale, vaid loome keskkonna, kus "Raamatupidamine" ja "IT-osakond" saavad koostöös väärtust toota.
* **Tagasisideahelad (Feedback loops):** Iga iteratsiooni (nt esimene veebiserveri püstitamine) järel kogusime tagasisidet (testisime kättesaadavust), et parandada järgmisi samme.
* **Kasulikkus vs Garantii:** AD sisselogimine pakub **kasulikkust** (utility - "fit for purpose"), samas kui dubleeritud DC-d ja DHCP serverid tagavad teenuse **garantii** (warranty - "fit for use"), kättesaadavuse ja turvalisuse.



---

**Kas soovid, et ma aitaksin sul sõnastada ka projekti "Väärtuspakkumise" (Service Offering) osa, mis kirjeldaks, milliseid kaupu ja ressursse sa lõppkasutajale tarnid?** 
