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
