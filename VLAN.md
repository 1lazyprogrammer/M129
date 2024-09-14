 
- [[#1.1 HTTP-Server konfigurieren (über CLI)|1.1 HTTP-Server konfigurieren (über CLI)]]
- [[#1.2 DHCP-Server konfigurieren|1.2 DHCP-Server konfigurieren]]
- [[#1.3 PC-Prod Konfigueriern|1.3 PC-Prod Konfigueriern]]
- [[#2.1 VLANs auf Switches erstellen|2.1 VLANs auf Switches erstellen]]

# 1.0 Grundkonfiguration der Netzwerkkomponenten
- HTTP-Server (IP: 192.168.0.10/24)
- DHCP-Server (IP: 192.168.0.1/24)
- Client1 und Client2 (IP per DHCP ab 192.168.0.100/24)
- PCProd (IP: IP: 192.168.0.40/24)
- Switch0 und Switch1

![[VLAN-20240914151158903.png]]


### 1.1 HTTP-Server konfigurieren (über CLI)

**1. HTTP Server Konfigurieren**
->  HTTP-Server Öffnen und zu > Desktop > IP Configuration und setze folgende Konfiguration.

![[VLAN-20240912224119056.png]]

**2. HTTP-Dienst Aktivieren**
-> HTTP-Server Öffnen und dann zu Services Navigieren und HTTP Service aktivieren

![[VLAN-20240910220947693.png]]

**3. HTML-Seite anpassen**
-> Nun können wir  das Index.html beatbeiten

![[VLAN-20240910222837057.png]]

### 1.2 DHCP-Server konfigurieren

**1. DHCP-Server Konfigurieren**
->  DHCP-Server Öffnen und zu > Desktop > IP Configuration und setze folgende Konfiguration.
![[VLAN-20240914151529224.png]]

**2. DHCP Service Aktivieren**
-> Zu Services Navivgieren und DHCP Pool ausfüllen wie im Bild und dann den Service Aktivieren.
![[VLAN-20240914170339521.png]]

**3. DHCP-Server Testen**
->
![[VLAN-20240914170245358.png]]

### 1.3 PC-Prod Konfigueriern
**1. PC-Prod folgende  IP-Addresse zuweise siehe bild**

![[VLAN-20240914214310772.png]]



# 2.0 Switch Konfigurieren und VLAN-Konfiguration.
### 2.1 VLANs auf Switches erstellen
**1. VLAN 10 für Clientnetzwerk erstellen**
-> gebe folgende befehle ein 
```arduino
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Clientnetz
Switch(config-vlan)# exit
```

**2. Ports dem VLAN 10 zuordnen:**
->Weise die Ports, an denen **Client1** und **Client2** angeschlossen sind, dem VLAN 10 zu:
```arduino
Switch(config)# interface range fastEthernet 0/1-2 
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit
```

**3. VLAN 20 für Produktionsnetzwerk erstellen:**
-> Wiederhole die Schritte für VLAN 20 auf Switch1, das für das Produktionsnetzwerk genutzt wird:
```arduino
Switch> enable
Switch# configure terminal
Switch(config)# vlan 20
Switch(config-vlan)# name Produktion
Switch(config-vlan)# exit

```

**4. Port für Produktions-PC zu VLAN 20 zuordnen:**
-> Weise den Port, an dem der **PCProd** angeschlossen ist, dem VLAN 20 zu: