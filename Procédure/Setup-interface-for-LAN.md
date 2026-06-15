# Documentation Technique : Modification du MTU à 1450 (Environnement VXLAN)

Cette documentation regroupe les procédures pour modifier le MTU (Maximum Transmission Unit) à **1450** sur différents systèmes d'exploitation et équipements réseau afin d'éviter la fragmentation ou les pertes de paquets HTTP/HTTPS liées à l'encapsulation VXLAN.

## Sommaire (Liens d'accès rapide)
* [🎛️ PfSense](#-pfsense)
* [🛡️ Fortigate](#-fortigate)
* [🪟 Windows (Server & Client)](#-windows-server--client)
* [🤠 Linux Rocky / RHEL](#-linux-rocky--rhel)
* [🐧 Linux Ubuntu / Debian](#-linux-ubuntu--debian)

---

## 🎛️ PfSense

Sur PfSense, la modification s'effectue directement depuis l'interface Web (WebGUI).

1. Connectez-vous à l'interface d'administration de PfSense.
2. Allez dans le menu **Interfaces** et sélectionnez l'interface connectée au réseau VXLAN (ex: `LAN`, `OPT1`).
3. Cherchez le champ **MTU** (généralement vide par défaut, ce qui équivaut à 1500).
4. Saisissez la valeur `1450`.
5. Descendez en bas de la page et cliquez sur **Save**.
6. Cliquez sur le bandeau supérieur **Apply Changes** pour valider la configuration.

---

## 🛡️ Fortigate

Sur un Fortigate, il est recommandé d'ajuster le MTU de l'interface, mais également le **MSS TCP** pour garantir le bon fonctionnement des flux HTTPS.

### 1. Modification du MTU de l'interface (CLI)
Remplacez `portX` par le nom réel de votre interface :
```text
config system interface
    edit <portX>
        set mtu-override enable
        set mtu 1450
    next
end
```
## 🪟 Windows (Server & Client)

```
netsh interface ipv4 show subinterfaces
netsh interface ipv4 set subinterface "Ethernet0" mtu=1450 store=persistent
netsh interface ipv4 show subinterfaces
```

## 🤠 Linux Rocky / RHEL

```
nmcli connection show
nmcli connection modify "System eth0" 802-3-ethernet.mtu 1450
nmcli connection up "System eth0"
ip link show
```

🐧 Linux Ubuntu / Debian

```
ls /etc/netplan/
sudo nano /etc/netplan/01-netcfg.yaml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: true
      mtu: 1450  # <-- Ajoutez cette ligne au bon niveau d'indentation
sudo netplan apply
ip link show eth0
```
