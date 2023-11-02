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

- Récuperer le script autoscan_nmap.sh dans files

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

- Récuperer le script autoscan_nmap.sh dans files
```bash
chmod +x autoscan_smtp.sh
./autoscan_smtp.sh @ip_a_scanner
```
# autoscan_pop3_pop3s

La script fourni est une commande nmap utilisée pour analyser les serveurs POP3 (Post Office Protocol version 3) afin de recueillir des informations sur leurs capacités ou les détails d'authentification NTLM (NT LAN Manager). - Voici une répartition de la commande :

- nmap : Il s'agit de l'utilitaire de ligne de commande pour la découverte du réseau et l'audit de sécurité.

--script pop3-capabilities ou pop3-ntlm-info : il spécifie la sélection du script Nmap. Vous pouvez choisir d'exécuter soit le script "pop3-capabilities", soit le script "pop3-ntlm-info". Ces scripts rassemblent des informations spécifiques sur les serveurs POP3. Vous pouvez remplacer « ou » par « et » pour exécuter les deux scripts simultanément.

-sV : Cette option active la détection de version, qui permet d'identifier le service et sa version exécuté sur le port spécifié.

-p 110,993 : Il spécifie les numéros de port à analyser. POP3 fonctionne généralement sur le port 110 pour les communications en texte clair et sur le port 993 pour les communications cryptées (POP3S).

- Le $1 est un espace réservé pour l'adresse IP ou le nom d'hôte cible. Remplacez $1 par l'adresse cible réelle lors de l'utilisation de la commande.

- En résumé, cette commande nmap est conçue pour analyser les serveurs POP3, identifier leurs capacités et collecter des informations sur l'authentification NTLM. Il peut être un outil utile pour les administrateurs réseau et les professionnels de la sécurité pour évaluer la sécurité des services POP3 sur un réseau.

- Récuperer le script autoscan_nmap.sh dans files
```bash
chmod +x autoscan_pop3.sh
./autoscan_pop3.sh @ip_a_scanner
```

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
# Enumération sur les Ports SMB 139 445

- Port 139 NetBIOS signifie Network Basic Input Output System.
- Il s'agit d'un protocole logiciel qui permet aux applications, aux PC et aux ordinateurs de bureau d'un réseau local (LAN) de communiquer avec le matériel réseau et de transmettre des données sur le réseau.
- Les applications logicielles qui s'exécutent sur un réseau NetBIOS se localisent et s'identifient mutuellement via leurs noms NetBIOS.
- Un nom NetBIOS comporte jusqu'à 16 caractères et est généralement distinct du nom de l'ordinateur.
- 2 applications démarrent une session NetBIOS lorsque l'une (le client) envoie une commande pour « appeler » un autre client (le serveur) via le port TCP 139. 

- Le Port 445 Alors que le port 139 est techniquement connu sous le nom de « NBT sur IP », le port 445 est « SMB sur IP ».
- SMB signifie « Server Message Blocks ».
- Le bloc de messages du serveur en langage moderne est également connu sous le nom de Common Internet File System.
- Le système fonctionne comme un protocole réseau de couche application principalement utilisé pour offrir un accès partagé aux fichiers, imprimantes, ports série et autres types de communications entre les nœuds d'un réseau.

- Les lignes de commande fournies sont des exemples d'utilisation de l'outil Nmap pour effectuer diverses analyses d'énumération et de vulnérabilité SMB (Server Message Block) sur un hôte distant utilisant le port 445.
- SMB est un protocole réseau utilisé pour partager des fichiers, des imprimantes et d'autres ressources sur un réseau.

## Voici une répartition des commandes :


nmap --script smb-enum-shares.nse -p445 $IP
- : cette commande utilise le script Nmap smb-enum-shares.nse pour énumérer les ressources partagées sur l'hôte cible sur le port 445.

nmap –script smb-enum-users.nse -p445 $IP 
: Cette commande utilise le script Nmap smb-enum-users.nse pour énumérer les utilisateurs sur le serveur SMB cible via le port 445.

nmap --script smb-enum-domains.nse, smb-enum-groups.nse, smb-enum-processes.nse, smb-enum-services.nse, smb-enum-sessions.nse, smb-enum-shares. nse,smb-enum-users.nse -p445 $IP : ici, plusieurs scripts Nmap sont utilisés pour collecter diverses informations sur les domaines, les groupes, les processus, les services, les sessions, les partages et les utilisateurs sur le serveur SMB cible via le port 445.

nmap --script smb-vuln-conficker.nse,smb-vuln-cve2009-3103.nse,smb-vuln-cve-2017-7494.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07- 029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse,smb-vuln-regsvc- dos.nse,smb-vuln-webexec.nse -p445 $IP : Cette commande est utilisée pour identifier les vulnérabilités potentielles sur le serveur SMB. Il vérifie les vulnérabilités connues telles que Conficker et divers CVE à l'aide de différents scripts Nmap.

nmap --script smb-vuln-cve-2017-7494 --script-args smb-vuln-cve-2017-7494.check-version -p445 $IP : cette commande vérifie spécifiquement la vulnérabilité CVE-2017-7494 et également tente d'identifier la version du logiciel qui peut être affectée.


Veuillez noter que pour utiliser ces commandes, vous devez remplacer $IP par l'adresse IP réelle de l'hôte cible que vous souhaitez analyser. De plus, ces commandes doivent être utilisées de manière responsable et uniquement sur les systèmes que vous êtes autorisé à analyser.
