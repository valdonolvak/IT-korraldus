Siin on detailne pideva parendamise (Continual Improvement) käsitlus  projekti kolme kriitilise valdkonna kohta.ITIL 4 kohaselt on pidev parendamine korduv tegevus, mis toetab organisatsiooni arengut ja tagab teenuste vastavuse ootustele igal etapil.

Parendusprotsessi selgitamiseks kasutame **ITIL-i pideva parendamise mudelit**, mis koosneb sammudest: *Mis on visioon?* -> *Kus me oleme praegu?* -> *Kuhu me tahame jõuda?* -> *Kuidas me sinna jõuame?* -> *Tee tegevus* -> *Kas me jõudsime kohale?* -> *Kuidas hoida hoogu?*

---

### 1. Monitooring ja SIEM (Zabbix & Wazuh)
[cite_start]Monitooringu eesmärk on tagada süsteemi **garantii** ehk sobiv kättesaadavus ja turvalisus.

***Teooria:** Parendamine põhineb tagasisideahelatel. Esmane seadistus on tihti "mürarikas" (liiga palju ebaolulisi teavitusi), mis viib tähelepanu hajumiseni.Pidev parendamine tähendab seirelävendite (thresholds) peenhäälestamist reaalsete andmete põhjal.
***Praktiline rakendus:** Analüüsitakse kogutud logisid ja intsidente, et eristada kriitilised vead tavapärasest süsteemi käitumisest.
* **Detailne näide:**
    * **Hetkeseis:** Wazuh annab ööpäevas 500 madala prioriteediga hoiatust, millest enamik on valepositiivsed.
    ***Parendusamm:** Analüüsitakse andmeid  ja muudetakse SIEM-i reegleid nii, et teavitus saadetakse ainult korduvate ebaõnnestunud sisselogimiste korral.
    * **Tulemus:** IT-tiimi reaktsioonikiirus tõuseb, kuna nad tegelevad ainult reaalsete ohtudega.

### 2. Varundussüsteem
[cite_start]Varundus on osa **teenusepakkumisest**, pakkudes tarbijale kindlustunnet andmete säilimise osas.

***Teooria:** Alustatakse sealt, kus ollakse (olemasolevad skriptid), kuid edanetakse iteratiivselt, testides mitte ainult varundamist, vaid ka taastamist.
***Praktiline rakendus:** Varundusprotsessi optimeeritakse, et see tarbiks vähem ressursse (aeg, kettamaht) ja pakuks kiiremat taastet.
* **Detailne näide:**
    * **Hetkeseis:** Igapäevane täisvarundus (Full Backup) täidab 3TB HDD kettamassiivi liiga kiiresti.
    ***Parendusamm:** Viiakse sisse inkrementaalne varundus.Lisaks viiakse läbi regulaarsed taastamistestid (Restore tests), et veenduda väljundi kvaliteedis.
    * **Tulemus:** Kettasääst on 70% ja taastekindlus on tõestatud testidega.

### 3. Võrguseadmed ja Wifi (Cisco & Ubiquiti)
[cite_start]Võrk on kriitiline **ressurss**, mis võimaldab ligipääsu kõigile teistele teenustele.

***Teooria:** Võrgu haldamisel tuleb mõelda ja töötada terviklikult.Wifi katvus ja turvalisus VLAN-ide vahel peavad vastama kasutajate tegelikule liikumisele ja vajadustele.
***Praktiline rakendus:** Kasutatakse tarbijate tagasisidet ja võrguanalüüsi tööriistu, et tuvastada "pudeliaelu" või turvaauke.
* **Detailne näide:**
    * **Hetkeseis:** Külaliste Wifi (VLAN 200) segab sisevõrgu kiirust ja Ubiquiti tugijaama signaal on teatud ruumides nõrk.
    ***Parendusamm:** Optimeeritakse Ubiquiti halduskonsoolis raadiokanalite sagedusi ja seadistatakse Cisco ruuteris QOS (Quality of Service) reeglid, mis prioriseerivad kontori klientide (VLAN 10) liiklust.
    * **Tulemus:** Wifi kvaliteet paraneb ja kriitilised äriprotsessid on eelisjärjekorras.



---
