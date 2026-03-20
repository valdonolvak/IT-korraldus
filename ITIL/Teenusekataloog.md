# Teenusekataloog (v1.0)

> **Raamistik:** ITIL 4 – väärtuse koosloomine, teenusepakkumised, outputs vs outcomes, utility & warranty. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

## 0. Ülevaade ja põhimõtted

- **Eesmärk.** Kirjeldada koolipraktika käigus loodud IT-teenused, nende väärtus (*utility*), tagatustasemed (*warranty*), SLO-d, sõltuvused ja mõõdikud. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)
- **Mõisted.**
  - **Utility** – mida teenus teeb (sobivus otstarbele). **Warranty** – kuidas teenus toimib (sobivus kasutamiseks: kättesaadavus, võimekus, järjepidevus, turvalisus). [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)
- **Juhtpõhimõtted.** Keskendu väärtusele; alusta sealt, kus oled; edene iteratiivselt tagasiside abil; tee koostööd ja edenda läbipaistvust; mõtle ja tegutse terviklikult; hoia asjad lihtsad ja praktilised; optimeeri ja automatiseeri. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

---

## 1. Identiteedi- ja ligipääsuteenused (AD, DNS, DHCP)

**Utility.** Domeen, autentimine/autoriseerimine, nimeteenus ja IP jaotus kõigile seadmetele. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Warranty / SLO.** Kättesaadavus ≥ 99% (koolipäevadel 08:00–18:00); DHCP failover DC1↔DC2; DNS vastus LAN-is p90 < 50 ms. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Kliendid.** Kõik domeeniseadmed ja kasutajad.  
**Komponendid.** DC1 (GUI), DC2 (Core), DNS tsoonid, DHCP scope + failover.  
**Sõltuvused.** Proxmox, võrk/VLAN-id, varundus.  
**Tellimine/muutmine.** Konto/OU/grupi taotlus Git-issue kaudu; DoD: sisselogimine toimib, õigused rakendunud.  
**Riskid & kontrollid.** GPO „Turvaline parool“ (keerukus/ajalugu), 2×DC, regulaarne süsteemiriistvara-sõltumatu varundus.  
**Mõõdikud.** Domeeniliitumise edukus %, DHCP scope utilization, DNS NXDOMAIN/REFUSED osakaal.

---

## 2. Töökoha elutsükli teenus (WDS/MDT, GPO, MDM)

**Utility.** Masspaigaldus (PXE), põhisofti ja poliitikate jaotus GPO-ga, seadme inventuur ja compliance MDM-i kaudu. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Warranty / SLO.** „Uus töökoht“ ≤ 30 min (golden image + GPO põhikomplekt); GPO-de rakendumine < 2 h; MDM inventuur < 15 min pärast agenti.  
**Komponendid.** MDT/WDS, GPO paketid (ID-kaardi tarkvara, Chrome, 7-Zip, LibreOffice), FleetDM vms.  
**Sõltuvused.** AD/DNS/DHCP, pildihoidla, võrguühendus.  
**Riskid & kontrollid.** Allkirjastatud skriptid, kontrollitud tarkvarapaketid, standardiseeritud kujutised.  
**Mõõdikud.** Paigalduse läbimisaeg, paigaldusõnnestumise %, drift (MDM compliance).

---

## 3. Faili- ja koostööteenus (DFS)

**Utility.** OU-põhised jagamised: `\\grupinimi\Dokumendid\OU`; failitüüpide piirangud (.exe, .msi, .bat, .ps1) turberiski vähendamiseks. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Warranty / SLO.** Kättesaadavus ≥ 99% (08–18); igapäevane varundus, 5 viimast koopiat; testtaaste kord kuus; RPO 24 h, RTO 1–4 h. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Riskid & kontrollid.** NTFS/ACL, deny-list, kvodid (vajadusel).  
**Mõõdikud.** Jaotuste kättesaadavus, varunduse edukus %, taastetesti läbimine.

---

## 4. Paroolide ja ligipääsuinfo teenus (self-hosted password manager)

**Utility.** Turvaline paroolivaramu koos tiimijagamisega; offline varu (KeePassXC) katkestuste puhuks. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Warranty / SLO.** MFA nõutud; öine varundus; offline varu sünkroon ≤ 7 päeva; rollipõhine ligipääs.  
**Mõõdikud.** MFA-aktsepteerimine %, auditilogi kattuvus, varuversiooni vanus.

---

## 5. Veebiteenus (NGINX + PHP + WordPress; HAProxy; eraldi andmebaas)

**Utility.** Välisveeb ja intranet; WordPress rakendus virtuaalhostis `veeb.xxx.xxx`. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Warranty / SLO.** Kättesaadavus ≥ 99% (08–18); TLS-toega; p90 vastusaeg LAN-is < 300 ms; HAProxy tervisekontrollid ja failover.  
**Sõltuvused.** DNS, andmebaasiteenus, varundus, koormusjaotur.  
**Riskid & kontrollid.** Patch’id (Ansible), rollipõhine admin, regulaarne varundus (failid+DB), taastetest.

---

## 6. Varundus ja taastamine

**Utility.** Igapäevased koopiad veebifailidest ja andmebaasist, rotatsioon 5 koopiat; automaatne ajastus. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Warranty / SLO.** RPO 24 h, RTO 1–4 h; igakuine testtaaste; logid + teavitused.  
**Mõõdikud.** Varunduse edukus %, keskmine taastamise aeg, testtaaste läbimine.

---

## 7. Võrgu- ja ühenduvusteenus (ruuter, kommutaator, VLAN-id, WiFi)

**Utility.** Segmenteerimine (VLAN 1/10/30/100/200), DHCP relay, SNMP, SSH; kaks SSID-d (sise/külaline), hotspot-portaal.  
**Warranty / SLO.** L2 latents p90 < 2 ms; külalisvõrk eraldatud (ei näe sisevõrku); DHCP snooping; dokumenteeritud port forward’id.  
**Riskid & kontrollid.** ACL-id, haldus juurdepääs ainult SSH kaudu, varukonfid ja audit.  
**Mõõdikud.** Latents, paketikaotus, rogue DHCP tuvastus, WiFi assotsiatsioonide õnnestumine %.

---

## 8. Monitooringuteenus (Zabbix vms)

**Utility.** Võrguliikluse, CPU/RAM/kettamahtude ja teenuste kättesaadavuse jälgimine; avalik vaade `monitor.xxx.xxx`. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Warranty / SLO.** MTTD < 10 min; alertid e-posti/Teamsi kaudu; metrikute säilitus ≥ 30 päeva.  
**Mõõdikud.** Host uptime, alertide arv/kuus, MTTD, „false positive“ suhe.

---

## 9. SIEM teenus (Wazuh/Graylog)

**Utility.** Logide tsentraliseerimine, reeglipõhine tuvastus, hoiatused; nähtav `siem.xxx.xxx`.  
**Warranty / SLO.** Logi saabumise viide < 2 min; kriitilise sündmuse teavitus ≤ 5 min; rollipõhine juurdepääs.  
**Mõõdikud.** EPS (events per second), kriitiliste alertide MTTD/MTTR, katvuse % (agentidega hostid).

---

## 10. Virtualiseerimisplatvorm (Proxmox)

**Utility.** VM-de majutus, SSD RAIDZ‑1 töökoormustele, HDD varundustele; veebihaldus ja SSH.  
**Warranty / SLO.** Halduspaneel kättesaadav; hosti püsivara ajakohane; planeeritud hooldusaknad dokumenteeritud.  
**Mõõdikud.** VM uptime, hosti kasutus (CPU/RAM/IOPS), backup job’ide edukus.

---

## 11. Konteineriteenused (Docker + Portainer + Unifi Controller + paroolihaldur)

**Utility.** Konteinerite haldus, rakenduste elutsükkel Portaineri kaudu; Unifi Controller konteinerina.  
**Warranty / SLO.** Konteinerid taastuvad automaatselt; RBAC Portaineris; auditilogi.  
**Mõõdikud.** Konteinerite restart’ide arv, tervisekontrollide seis, juurutuse edukus %.

---

## 12. Andmebaasiteenus (Alma Linux)

**Utility.** WP ja monitooringu andmebaasid, kasutajad, õigused.  
**Warranty / SLO.** Varundus; p90 päringu aeg LAN-is < 50 ms; ressursside jälgimine.  
**Mõõdikud.** Query latency, ühenduste arv, backup edukus %.

---

## 13. Tugiteenused: Ansible, dokumentatsioon, konfiguratsioonihaldus

**Ansible (utility).** Turvapaikade ja uuenduste automatiseerimine; (warranty) „dry-run“ enne tootmist, nädalagraafik. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Dokumentatsioon (utility).** Google Sites – „üks tõevallikas“, iteratiivne uuendus; (warranty) värskendus igal iteratsioonil. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)  
**Konfiguratsioonihaldus (utility).** Git/GitLab – versioonilugu ja PR-review; (warranty) märgendused, rollback-protseduur. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)
