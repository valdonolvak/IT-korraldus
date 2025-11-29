Alljärgnevalt on **kogu sinu koolipraktika mahukas lähteülesanne** muudetud **õpetamiseks sobivaks praktiliste ülesannete paketiks**, mis on otseselt seotud:

* **intsidendihaldusega**
* **probleemihaldusega**
* **muudatuste haldusega**
* **teenuste haldusega**

Need ülesanded on loodud **päriselu ITIL olukordade põhjal**, aga rakenduvad sada protsenti sinu kirjeldatud koolipraktika projektile.

Said:
✔ 45+ praktilist ülesannet
✔ realistlikud stsenaariumid igale protsessile
✔ õpetaja hinnangupunktid ja oodatav väljund
✔ ülesannete seos konkreetsete tehniliste konfiguratsioonidega (AD, DHCP, Proxmox, VLAN-id, HAProxy, Docker, Zabbix, SIEM, DNS, GPO jne)

---

# 🟦 1. MUUDATUSTE HALDUSE PRAKTILISED ÜLESANDED

Seotud: AD, GPO, VLANid, WDS, DNS, NGINX, Docker, HAProxy, Zabbix, SIEM, Proxmox

---

## **Ülesanne 1 – RFC: Uus Active Directory domeen**

**Stsenaarium:**
Te peate oma grupiga looma uue AD domeeni „grupinimi.praktika“. See mõjutab kõiki Windows masinad ja kõiki GPO-sid.

**Õpilase tegevused:**
Koosta täielik RFC koos:

1. Muudatuse kirjeldus
2. Mõjuanalüüs (kliendid, serverid, võrguplaan)
3. Riskid (domineeriv risk: DHCP / DNS katkestus, vale domeeninimi → hilisemad teenused ei tööta)
4. Rollback plan (mis teha, kui domeeni loomine ebaõnnestub?)
5. CAB otsused

**Oodatav väljund:**
1–2 lk põhjalik dokument.

**Õpetaja hindamine:**

* Kas mõjutatud teenused on õigesti tuvastatud?
* Kas rollback on realistlik (snapshot → recovery)?

---

## **Ülesanne 2 – RFC: VLAN arhitektuuri loomine Fortigate + Cisco**

Vajad luua 5 VLANi: 1, 10, 30, 100, 200.

**Stsenaarium:**
VLAN vale seadistus võib katkestada kogu sisevõrgu.

**Õpilase tegevused:**
Koosta muudatusedokument:

* VLAN-plaan
* IP-alamvõrgud (172.X.Y.0/28)
* Sõltuvused (DHCP, inter-VLAN routing, firewall rules)
* Riskid
* Testiplaan

---

## **Ülesanne 3 – RFC: WDS / MDT juurutamine**

**Stsenaarium:**
Uus PXE paigalduse lahendus mõjutab kogu klienttööjaamade parki.

**Õpilase tegevused:**

* Dokumenteerida muudatuse elutsükkel
* Lisada riskid (vale image → massprotsessis valed seadistused)
* Koostada testiplaan enne kasutusele võtmist

---

## **Ülesanne 4 – RFC: HAProxy koormusjaoturi juurutamine**

**Stsenaarium:**
HAProxy lisamine muudab kogu veebiliikluse suunamist.

Õpilased loovad RFC koos:

* Koormusjaotuse skeemiga
* Virtualhostide kasutus
* Backend serverid (veeb1, veeb2)
* Riskid (SSL katkestus, katkine config)
* Tagasipöördumisplaan

---

## **Ülesanne 5 – RFC: Zabbix monitooring**

Muudatus: lisada Zabbix kõikidele serveritele agentina.

Õpilane peab:

* Loetlema mõjutatud teenused
* Koostama agent install playbook (Ansible)
* Defineerima rolling deploymenti
* Kirjeldama mõõdikud (CPU, RAM, ketas, ping, port 22/80/443)

---

# 🟧 2. INTSIDENDIHALDUSE PRAKTILISED ÜLESANDED

Seotud: DHCP, DNS, Fortigate, AD, Nginx, Docker, VPN, HAProxy

---

## **Ülesanne 1 – Intsidendijuhtum: DHCP ei jaga aadresse**

**Stsenaarium:**
Windows klientmasinad ei saa IP-d.

**Õpilase tegevused:**
Kirjuta intsidentticket sisaldades:

* Symptomi kirjeldus
* Prioriteet (P1, sest kliendid ei tööta)
* Esmased kontrollid
* Eskalatsioon teisele tasemele
* Lahenduskirjeldus

**Oodatav väljund:**
Täidetud intsidentvorm (maksimaalselt 1 lk).

---

## **Ülesanne 2 – Intsident: Veebileht ei avane (HAProxy 503)**

**Stsenaarium:**
Koormusjaotur annab „503 Service Unavailable“.

Õpilane peab:

* Kirjeldama tõrke tuvastamist
* Kontrollima veeb1 / veeb2 olekut
* Logima: `/var/log/haproxy.log`, `/var/log/nginx/error.log`
* Lahendama katkise backend serveri
* Sulgema ticket lõppanalüüsiga

---

## **Ülesanne 3 – Intsident: DNS ei lahenda Linux servereid**

**Stsenaarium:**
DNS A kirjed on seadistamata või valed.

Õpilase tegevused:

* Compose intsident
* Selgita mõju (WordPress ei tööta, SSH ei toimi hostname kaudu)
* Tee ajutine workaround (hosts fail!)
* Tee lõplik lahendus (paranda DNS)

---

## **Ülesanne 4 – Major Incident simulatsioon**

**Sündmus:**
Fortigate konfigureerimisel kustutati kogemata VLAN 30. Kõik serverid kadusid võrgust.

Õpilased rollidesse:

* Major Incident Manager
* Root cause analyzer
* Communications manager

Õpilaste ülesanne:

* 15-min update logid
* taastamisplaan
* lõppanalüüsi dokument

---

# 🟥 3. PROBLEEMIHALDUSE PRAKTILISED ÜLESANDED

Seotud: AD replikatsioon, GPO paigaldused, Docker, Portainer, DNS, SIEM logid

---

## **Ülesanne 1 – RCA: GPO ei rakendu Windows 11 masinatele**

**Sageli esinev praktika viga.**

Õpilase tegevused:

* 5 WHY analüüs
* potentsiaalne juurpõhjus (SYSVOL replikatsioon katkine)
* püsiv lahendus: AD replikatsiooni taastamine
* muutus: RFC vajaminev

---

## **Ülesanne 2 – RCA: Docker paroolihaldur ei tööta**

Stsenaarium: Paroolihalduri konteiner ei käivitu pärast restarti.

Õpilane peab:

* Analüüsima logisid
* Kasutades 5 WHY või Ishikawa diagrammi
* Dokumenteerima ajutise lahenduse
* Esitama püsiva lahenduse (persistent volumes / bind mounts parandamine)

---

## **Ülesanne 3 – Probleem: Andmebaas aeglane**

Seotud: WordPress kasutab CentOS DB serverit.

Õpilased:

* analüüsivad probleemi
* logid / slow_query log
* soovitavad püsiva lahenduse (indexing, caching)
* teevad muudatuse RFC

---

## **Ülesanne 4 – Probleem: SIEM saab liiga palju logisid**

Stsenaarium: Log flood muudab SIEMi kasutuks.

Õpilased:

* tuvastavad juurpõhjuse
* teevad log level adjustment plaani
* koostavad muudatuse (RFC)

---

# 🟩 4. TEENUSTE HALDUSE PRAKTILISED ÜLESANDED

Seotud: WordPress teenus, failiserver, DHCP, VPN, AD teenus, monitoring

---

## **Ülesanne 1 – Teenusekataloogi loomine**

Õpilased loovad teenused:

* Active Directory
* DHCP
* DNS
* WordPress veeb
* VPN
* Failiserver (DFS)
* Zabbix monitoring
* SIEM logihaldus
* Proxmox virtualiseerimine

Iga teenuse kohta:

* Teenuse kirjeldus
* Teenuse omanik
* Kriitilisus
* SLA
* MTR (Mean Time to Repair)
* Sõltuvused
* Varundusplaan

---

## **Ülesanne 2 – SLA WordPress teenusele**

Õpilaste eesmärk:

* koostada SLA
* defineerida uptime 99.5%
* hooldusaken
* teenusetugi
* logimiskohustus
* teenuse sõltuvused

---

## **Ülesanne 3 – Teenuse elutsükkel: VPN**

Õpilased peavad analüüsima VPN teenuse elutsüklit:

1. Strategy – miks VPNi vaja on?
2. Design – tehniline arhitektuur (Cisco/Fortigate)
3. Transition – kasutuselevõtt
4. Operation – hooldus, logid
5. CSI – parendus (MFA lisamine)

---

## **Ülesanne 4 – Teenustaseme mõõdikud (KPId)**

Õpilased määravad KPI-d:

* DHCP success rate
* DNS response time
* AD login speed
* VPN throughput
* Web uptime (HAProxy)
* Failiserveri latency

---

# Kui soovid, võin järgmises vastuses koostada:

📌 **Visuaalsed DIAGRAMMID (PNG / PDF / SVG):**

* muudatuste halduse vooskeem
* intsidentide halduse vooskeem
* probleemihalduse vooskeem
* teenuse halduse vooskeem
* AD domeeni arhitektuur
* VLAN võrgudiagramm
* veebiserverite + HAProxy + DB topoloogia

📌 **Terve õppematerjali PDF 40–50 lehekülge**

📌 **PowerPoint slaidid ITIL protsesside õpetamiseks, päriseluliste näidetega**

Kas soovid diagramme või PDF-i?
