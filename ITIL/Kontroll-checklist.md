# Kontroll-checklist (installeerimisest käituseni)

> Lähtub ITIL 4 põhimõtetest: nähtavus, iteratiivsus, lihtsus, automatiseerimine. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

## 1. Üldkontrollid

- [ ] IP‑plaan kinnitatud; loogiline + füüsiline topoloogia joonised repos.
- [ ] Kaablid crimp’itud, **tester PASS**, kaablid märgistatud.
- [ ] Proxmox uuendatud 8.3 → 9.1; BIOS/RAID püsivarad ajakohased.
- [ ] Backup-kettapind eraldatud; skript ajastatud; rotatsioon **5**; **testtaaste** tehtud (DoD).
- [ ] Google Sites ja Git repo olemas; skriptid kommenteeritud; link kataloogis. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)

## 2. Võrk

- [ ] Cisco **ruuter**: RX; WAN IP; LAN 172.X.Y.0/28; VLAN 1/10/30/100/200 alamliidesed; **DHCP relay**; **SNMP**; **SSH**; port forward’id (Proxmox Web/SSH, RDP W2K22, SSH Linux, välisveeb).
- [ ] Cisco **kommutaator**: SWXY; haldus IP; VLAN-id; **DHCP snooping**; SNMP; SSH.
- [ ] **Ubiquiti AP**: tehaseseadistus → controller; 2 SSID (sise/külaline); captive-portal.

## 3. AD/DNS/DHCP

- [ ] DC1: domeen *grupinimi.praktika*; DHCP scope; DNS A-kirjed kõigile Linuxi masinatele ja võrguvahenditele.
- [ ] Kasutajad CSV-st imporditud skriptiga; OU-struktuur korras (Staff/IT/Kontor/…).
- [ ] GPO-d: „ID‑kaardi tarkvara“, „LibreOffice“, „Google Chrome + 7-Zip“.
- [ ] Kasutaja‑GPO-d: „Avaleht“, „Taustapilt“, „Peida kasutaja“, „Turvaline parool“.
- [ ] DC2: teine domeenikontroller; DHCP **failover** OK; **DFS** target lisatud.

## 4. Töökoha elutsükkel

- [ ] WDS/MDT PXE töötab; **Windows 11-3** paigaldatud üle võrgu; domeeniga liidetud.
- [ ] GPO paketid rakenduvad; MDM ja SIEM agendid peal; DFS võrguketas mountitud; failipiirangud kehtivad.

## 5. Serverid ja rakendused

- [ ] **veeb1/veeb2**: SSH võtmega; NGINX+PHP; vhost `veeb.xxx.xxx`; WordPress → DB Alma serveris.
- [ ] **koormusjaotur**: HAProxy health-check; vajadusel sticky; fallback testitud.
- [ ] **docker**: Docker, Portainer CE; Unifi Controller konteinerina; paroolihaldur konteinerina; backup-skript ajastatud; **Ansible** inventar + playbook („update all“) dry-run ok.
- [ ] **andmebaas**: DB (WP/monitor), kasutajad/õigused; tulemüür; DNS kirje.
- [ ] **monitor**: monitooring nähtav `monitor.xxx.xxx`; hostid lisatud; andmebaas Alma2.
- [ ] **siem**: SIEM nähtav `siem.xxx.xxx`; kõik hostid ja kliendid agentidega liidestatud.

## 6. Turvalisus

- [ ] SSH ainult võtmega (serverites); parooliga ainult lokaalne konsool.
- [ ] RBAC: paroolihaldur, Portainer, SIEM, monitooring.
- [ ] DFS failitüübi piirangud jõus.
- [ ] TLS sertifikaadid kehtivad; uuendusprotseduur dokumenteeritud.
- [ ] SIEM reeglid ja teavitused testitud.

## 7. Smoke‑testid / DoD

- [ ] **Domeeniliitumine** uuele seadmele < 10 min.
- [ ] **Uue töökoha** ettevalmistus (PXE → GPO tarkvara) ≤ 30 min.
- [ ] **HAProxy failover**: katkesta `veeb1`; teenus püsib läbi `veeb2`.
- [ ] **Taaste**: kustuta testfail → taasta viimase varunduse abil.
- [ ] **SIEM/monitooring**: testintsidendist teavitus ≤ 10 min.
- [ ] **Külalis‑WiFi**: klient ei näe sisevõrgu ressursse.

> Märkus: checklisti fookus on **lihtsus** ja **praktilisus**; iga punkt loob otsest väärtust (kiired võidud) ning on hallatav iteratiivselt. [1](https://onedrive.live.com/personal/f51c2e2b4e1508fd/_layouts/15/doc.aspx?resid=372fc7f1-eb41-474b-81d4-6d29968d6cf0&cid=f51c2e2b4e1508fd)
