# enum_scan
Des Scans d'énumération de cibles en bash

# autoscan_nmap
- Ce script scanne un réseau ou une @IP
   
nmap -p- --min-rate 1000 "$target" 
Cette partie de la commande utilise Nmap, un outil d'analyse réseau. Il analyse un hôte cible à la recherche de ports ouverts. Les options utilisées sont :

-p- 
: analyse les 65535 ports TCP de l'hôte cible.

--min-rate 1000 
: définit le taux d'analyse minimum à 1 000 paquets par seconde.

: | grep "^ *[0-9]"
: Après avoir exécuté l'analyse Nmap, la sortie est redirigée vers grep pour filtrer les lignes commençant par un ou plusieurs espaces suivis d'un chiffre (numéro de port).

| grep "open" 
: un filtrage supplémentaire est effectué en utilisant grep pour inclure uniquement les lignes contenant le mot "open", qui indique les ports ouverts.

| cut -d '/' -f 1 
: La commande cut est utilisée pour diviser chaque ligne en utilisant '/' comme délimiteur et extraire le premier champ (le numéro de port).

| tr '\n' ',' 
: la commande tr remplace les caractères de nouvelle ligne par des virgules, ce qui donne une liste de ports ouverts séparés par des virgules.

| sed 's/,$//' 
: Enfin, la commande sed est utilisée pour supprimer la virgule de fin de la liste.

- Récuperer le script autoscan-nmap.sh dans files
```bash
chmod +x autoscan_nmap.sh
./autoscan_nmap.sh @ip_a_scanner
```
  
# autoscan_smtp

- Ce script execute une commande nmap scan utilisée pour évaluer la sécurité d'un serveur SMTP (Simple Mail Transfer Protocol) sur le port 25.
- Cette commande inclut des scripts NSE (Nmap Scripting Engine) spécifiques pour effectuer diverses vérifications sur le serveur SMTP :

--script=smtp-commands : ce script vérifie les commandes SMTP prises en charge sur le serveur.

--script=smtp-enum-users : Il énumère les comptes d'utilisateurs sur le serveur SMTP.

--script=smtp-vuln-cve2010-4344 : Vérifie les vulnérabilités liées à CVE-2010-4344.

--script=smtp-vuln-cve2011-1720 : vérifie les vulnérabilités liées à CVE-2011-1720.

--script=smtp-vuln-cve2011-1764 : vérifie les vulnérabilités liées à CVE-2011-1764.

- Cette script peut être utilisée par les administrateurs réseau et les professionnels de la sécurité pour évaluer la sécurité des serveurs SMTP en identifiant les commandes prises en charge, en énumérant les utilisateurs et en recherchant les vulnérabilités connues.
- Il est crucial d'effectuer de telles analyses avec l'autorisation appropriée pour éviter les problèmes juridiques et éthiques.
- Veuillez noter que le $1 dans la commande doit être remplacé par l'adresse IP cible ou le nom d'hôte que vous souhaitez analyser.


# Énumération du réseau en ligne de commande
```bash
ping $IP #63 ttl = linux #127 ttl = windows
```

```bash
nmap -p- --min-rate 1000 $IP
nmap -p- --min-rate 1000 $IP -Pn #désactive la commande ping et analyse uniquement les ports
```

```bash
nmap -p <ports> -sV -sC -A $IP
```

# Stealth Scan
```bash
nmap -sS -p- --min-rate=1000 10.11.1.229 -Pn #stealth scans
```
