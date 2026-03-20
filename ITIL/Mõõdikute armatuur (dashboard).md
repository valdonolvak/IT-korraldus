# Mõõdikute armatuur (SLI/SLO, visualiseeringud)

> ITIL 4 kohaselt aitab nähtavus ja koostöö otsuseid parandada; utility + warranty raamivad väärtuse mõõtmise loogika. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

## 0. Andmeallikad

- **Monitooring:** Zabbix (hostide tervis, kättesaadavus, ressursid)
- **SIEM:** Wazuh/Graylog (logid, reeglid, alertid)
- **Platvormid:** Proxmox API, Portainer API
- **Windows/AD:** Event log, gpresult/jnlp aruanded
- **Varundus:** backup-skripti logid ja testtaaste protokollid

---

## 1. Kättesaadavus ja töökindlus

**1.1 Teenuste kättesaadavus (Availability)**  
- **SLI.** Aeg % ajast, mil teenus on „UP“ (HTTP 200 või ping/port OK).  
- **SLO.** ≥ 99% (08–18) teenustele: AD/DNS, DFS, `veeb.xxx.xxx`, HAProxy, Proxmox GUI, Portainer, `monitor.xxx.xxx`, `siem.xxx.xxx`.  
- **Visual.** Päevane/kuine tulbikaar + heatmap; SLA ribad.  
- **ITIL seos.** Warranty: kättesaadavus. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

**1.2 MTTD / MTTR**  
- **SLI.**  
  - **MTTD:** Keskmine avastamise aeg (alerti ajatempli – rikke alguse ajatempli erinevus).  
  - **MTTR:** Keskmine taastamise aeg (taastumise ajatempli – rikke alguse ajatempli erinevus).  
- **SLO.** MTTD < 10 min; MTTR < 30–60 min (olenevalt teenusest).  
- **ITIL seos.** Iteratiivne parendamine; nähtavus. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

---

## 2. Töökoha elutsükkel

**2.1 Uue töökoha läbimisaeg**  
- **SLI.** PXE start → domeenilogin + põhikomplekti olemasolu.  
- **SLO.** ≤ 30 min; **Eesmärk:** 95% installidest täidab SLO.  
- **Visual.** Gaant + jaotusgraafik.  
- **ITIL seos.** Utility (standardtöökoht), Warranty (ajad). [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

**2.2 GPO rakendumise aeg**  
- **SLI.** GPO poliitikate jõustumise aeg uuel seadmel.  
- **SLO.** < 2 h 95. protsentiil.  
- **Visual.** Boxplot / p95 joon. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

**2.3 MDM compliance**  
- **SLI.** Vastavuses olevate seadmete % (kriptimine, agent, poliitikad).  
- **SLO.** ≥ 98% aktiivsetest seadmetest.  
- **ITIL seos.** Optimeeri & automatiseeri; riskide vähendamine. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

---

## 3. Võrk ja WiFi

**3.1 L2 latents (p90)**  
- **SLI.** p90 < 2 ms VLAN sees.  
- **SLO.** Vastab p90 sihile kõigis põhivõrkudes (1/10/30/100/200).  
- **Visual.** VLAN‑i kaupa joon + lävend.  

**3.2 DHCP ja DNS tervis**  
- **SLI.** DHCP lease success rate; scope utilization; DNS päringu vastus p90.  
- **SLO.** Lease success ≥ 99.5%; scope < 85%; DNS p90 < 50 ms.

**3.3 Külalisvõrgu isolatsioon**  
- **SLI.** Blokeeritud sisevõrgu sihtmärkide % testpakettidest.  
- **SLO.** 100% blokeeritud.  
- **ITIL seos.** Warranty (turvalisus ja järjepidevus). [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

---

## 4. Veeb ja andmebaas

**4.1 HTTP vastusaeg (p90)**  
- **SLI.** `veeb.xxx.xxx` p90 < 300 ms LAN-is.  
- **SLO.** 95% päevadest vastab p90 sihile.  
- **ITIL seos.** Warranty (võimekus/jõudlus). [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

**4.2 HAProxy tervis**  
- **SLI.** Aktiivsete backend’ide %; automaatse failover’i edukus.  
- **SLO.** ≥ 1 aktiivne backend; failover test kord kuus „PASS“.

**4.3 DB jõudlus**  
- **SLI.** p90 query latency < 50 ms; connection errors %.  
- **SLO.** Vastab p90 sihile; vead < 0.1%.

---

## 5. Varundus ja taastamine

**5.1 Varunduse edukus**  
- **SLI.** Edukalt lõpetatud job’ide %.  
- **SLO.** ≥ 98% kuu lõikes.  

**5.2 RPO / RTO vastavus**  
- **SLI.** RPO ≤ 24 h (viimase eduka varunduse vanus); RTO (testtaaste kestus).  
- **SLO.** RPO täidetud 100%; RTO 1–4 h (olenevalt teenusest).  
- **ITIL seos.** Warranty (järjepidevus), outputs→outcomes (taastatavus). [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

---

## 6. Turve ja SIEM

**6.1 Agentide katvus**  
- **SLI.** Agentidega hostide osakaal kõigist hostidest.  
- **SLO.** ≥ 99%.  

**6.2 Kriitiliste alertide MTTD**  
- **SLI.** Keskmine avastamise aeg kriitilistes reeglites.  
- **SLO.** ≤ 5–10 min.  
- **Visual.** Viivise histogramm.

**6.3 Paroolivaramu tervis**  
- **SLI.** MFA-ga kaitstud kasutajate %; offline varu viimane sünkroniseerimine (päevades).  
- **SLO.** MFA ≥ 100%; varu ≤ 7 päeva vana.  
- **ITIL seos.** Riskide eemaldamine, warranty (turvalisus). [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

---

## 7. Platvormid ja CI/CD

**7.1 Proxmox hosti tervis**  
- **SLI.** CPU/RAM/IOPS varu, host uptime, kriitiliste sündmuste arv.  
- **SLO.** Püsib rohelises tsoonis ≥ 95% ajast.

**7.2 Portainer juurutuste edukus**  
- **SLI.** Deploy success rate; restart loopide arv.  
- **SLO.** Edukus ≥ 98%; restart loop 0.

---

## 8. Raporteerimine ja vastutus

- **Sagedus.** Nädalane „ops health“ raport; kuine SLO aruanne.
- **Rollid.** Teenuseomanik (Service Owner) koondab; tehnilised omanikud per teenus.
- **Pidev parendamine.** Iga kõrvalekalle → „improvement item“ Kanbanis; prioriteet väärtusmõjult. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

``
## Sõnastik (lühendid ja mõisted)

Absoluutselt! Allpool on **Mõõdikute armatuuri lühendite sõnastik**—eesti- ja ingliskeelsed täisnimed koos lühikese selgitusega, mida iga mõiste tähendab ja kuidas seda praktikas tõlgendada/mõõta. Saad selle plokina lisada oma `Mõõdikute armatuur` faili lõppu eraldi peatükina “**Sõnastik**”.

***

## Sõnastik (mõõdikud ja lühendid)

| Lühend        | Täisnimi (ET)                         | Full name (EN)                                   | Lühiselgitus (mis & kuidas mõõta/tõlgendada)                                                                                                                                                                             |
| ------------- | ------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **SLI**       | Teenuse taseme indikaator             | **Service Level Indicator**                      | Konkreetne **mõõdetav näitaja** teenuse käitumisest (nt kättesaadavus %, p90 vastusaeg). SLI on **toores mõõtmine**: kogud numbrid andmeallikatest (Zabbix, SIEM, logid) ja arvutad väärtuse määratletud ajavahemikus.   |
| **SLO**       | Teenusetaseme eesmärk                 | **Service Level Objective**                      | **Sihtväärtus SLI‑le** (nt „kättesaadavus ≥ 99% tööpäeviti 08–18“). SLO ei ole leping, vaid **eesmärk**, mille täitmist jälgitakse ja millest kõrvalekalded käivitavad parendusalgatused.                                |
| **SLA**       | Teenusleping                          | **Service Level Agreement**                      | **Lepinguline kokkulepe** teenusetasemetest ja sanktsioonidest/kompensatsioonidest. Praktika tööraames kasuta pigem SLO‑sid; SLA on formaalne leping (vajalik päriskeskkonnas).                                          |
| **MTTD**      | Keskmine avastamise aeg               | **Mean Time To Detect**                          | Keskmine aeg **rikkest** või **intsidendist** **esimese usaldusväärse tuvastuseni** (häire/alert). Arvutus: keskmine( `tuvastuse_aeg – rikke_algus` ). Väiksem on parem; sõltub jälgimise katvusest ja häirelävenditest. |
| **MTTR**      | Keskmine taastamise aeg               | **Mean Time To Restore/Repair/Resolve**          | Keskmine aeg **teenuse taastamiseni** (või vea lahenduseni) alates rikke algusest. Arvutus: keskmine( `taastumise_aeg – rikke_algus` ). Mõõdab operatiivset efektiivsust; eesmärk on trendi vähendada.                   |
| **RPO**       | Taastepunkti eesmärk                  | **Recovery Point Objective**                     | **Maksimaalne lubatud andmekadu ajas** (nt 24 h). Kui RPO=24h, peavad varukoopiad olema vähemalt kord ööpäevas, et halvimal juhul kaoks ≤ 24 h andmeid.                                                                  |
| **RTO**       | Taastamisaja eesmärk                  | **Recovery Time Objective**                      | **Maksimaalne lubatud seisakuaeg** kuni teenuse taastumiseni (nt 4 h). Mõjutab varunduse/testtaaste protseduuri, personali ja automatiseerimise taset.                                                                   |
| **p90 / p95** | 90./95. protsentiil                   | **90th/95th percentile**                         | Näitab, millise väärtuse **90%/95% mõõtmistest ei ületa** (nt vastusaeg). Protsentiil on parem kui lihtne keskmine, sest **ignoreerib ekstreeme** ja peegeldab enamiku kasutajate kogemust.                              |
| **Uptime**    | Töövalmidus / Kättesaadavus           | **Uptime / Availability**                        | Aeg, mil teenus oli **kasutatav** (UP). Arvutus (lihtsustatud): `(UP aeg / koguaeg) × 100%` kindla mõõteakna sees. Täpsusta tööaknad (nt 08–18) ja välista planeeritud hooldus, kui nii on kokkulepitud.                 |
| **EPS**       | Sündmusi sekundis                     | **Events Per Second**                            | SIEM‑i **logimahu kiirus** (nt Wazuh/Graylog). Aitab hinnata **läbilaskevõimet** ja hoiatada logitormidest või anomaaliatest.                                                                                            |
| **MFA**       | Mitmefaktoriline autentimine          | **Multi‑Factor Authentication**                  | Turvameede, mis nõuab lisaks paroolile teist faktorit (kood, FIDO võti). Mõõdikuna kasuta **MFA kasutuse määra** (% kasutajaid/võtmerolle).                                                                              |
| **RBAC**      | Rollipõhine ligipääsukontroll         | **Role‑Based Access Control**                    | Õigused määratakse rollide kaudu, mitte üksikutele isikutele. Mõõda nt **„admin‑rollide osakaal“**, **„käsitsi erandite“ arv**.                                                                                          |
| **CI/CD**     | Pidev integratsioon / pidev tarnimine | **Continuous Integration / Continuous Delivery** | Automatiseeritud ehitus/test/juurutus. Armatuuri kontekstis mõõda nt **deploy success rate** või **rollbackide arv**.                                                                                                    |
| **API**       | Rakendusliidese programm              | **Application Programming Interface**            | Süsteemiliides mõõdikute/oleku pärimiseks (nt Proxmox, Portainer API). Kasuta armatuuri andmeallikana.                                                                                                                   |
| **DB**        | Andmebaas                             | **Database**                                     | Mõõdikud: päringu **latents** (p90), vigade % ja ühenduste arv—aitavad hinnata jõudlust ja ressursside vajadust.                                                                                                         |
| **HTTP**      | Hüpperteksti edastusprotokoll         | **Hypertext Transfer Protocol**                  | Teenuse „elutervise“ kontroll (HTTP 200) ja **vastusajad**; armatuuris kasutatakse nii **UP/Down** kui **latentsi** mõõtmiseks.                                                                                          |

***

### Kiirkokkuvõtted ja praktilised tõlgendused

*   **SLI vs SLO vs SLA**
    *   **SLI** = „mida me tegelikult mõõdame“ (toorandmete põhine näitaja).
    *   **SLO** = „siht“, millest allapoole ei taheta langeda (nt kättesaadavus ≥ 99%).
    *   **SLA** = „leping“, kus sihid on juriidiliselt kokku lepitud (trahvid/kompensatsioonid).  
        *Praktikas*: kooliprojekti faasis kasuta **SLO‑sid** ja raporteeri nende täitmist; kui tegu oleks päris kliendiga, vormistaksid **SLA**.

*   **RPO vs RTO**
    *   **RPO** mõõdab **andmekadu** (kui „vana“ varukoopia võib kõige halvemal juhul olla).
    *   **RTO** mõõdab **aega teenuse taastamiseni** (kui kaua võib teenus maas olla).  
        *Praktikas*: Kui RPO = 24 h ja RTO = 4 h, siis varunda vähemalt kord päevas ja **harjuta** taastamist nii, et jõuad 4 tunniga sihile.

*   **p90/p95**
    *   Keskendumine protsentiilidele annab realistliku pildi **enamiku kasutajate** kogemusest.
    *   Kui p90 vastusaeg on 280 ms, siis 90% päringutest on **kiiremad kui 280 ms**—hea, kuid jälgi ka sabasid (p99), kui vaja.

*   **MTTD/MTTR**
    *   **MTTD** sõltub **katvusest ja häirelävenditest**— liiga madal lävend = false positive; liiga kõrge lävend = hiline avastus.
    *   **MTTR** paraneb läbi **automatiseeritud taastetoimingute** (protseduurid, skriptid, runbook’id) ja **õigete eskalatsioonide**.

*   **EPS (SIEM)**
    *   Äkiline EPS tõus võib viidata **rünnakule** või **logitormile** (nt vigase agendi lõputu retry). Kasuta lävendi‑hoiatusi ja sujuvat „rate limiting’ut“.

***

