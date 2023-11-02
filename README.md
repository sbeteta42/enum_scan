# enum_scan
Scan d'énumération de cibles

# autoscan_nmap
Ce script scanne un réseau ou une @I ;
nmap -p- --min-rate 1000 "$target" : Cette partie de la commande utilise Nmap, un outil d'analyse réseau. Il analyse un hôte cible à la recherche de ports ouverts. Les options utilisées sont :

-p- : analyse les 65 535 ports TCP de l'hôte cible.
--min-rate 1000 : définit le taux d'analyse minimum à 1 000 paquets par seconde.
| grep "^ *[0-9]": Après avoir exécuté l'analyse Nmap, la sortie est redirigée vers grep pour filtrer les lignes commençant par un ou plusieurs espaces suivis d'un chiffre (numéro de port).

| grep "open" : un filtrage supplémentaire est effectué en utilisant grep pour inclure uniquement les lignes contenant le mot "open", qui indique les ports ouverts.

| cut -d '/' -f 1 : La commande cut est utilisée pour diviser chaque ligne en utilisant '/' comme délimiteur et extraire le premier champ (le numéro de port).

| tr '\n' ',' : la commande tr remplace les caractères de nouvelle ligne par des virgules, ce qui donne une liste de ports ouverts séparés par des virgules.

| sed 's/,$//' : Enfin, la commande sed est utilisée pour supprimer la virgule de fin de la liste.

- Récuperer le script autoscan-nmap.sh
```bash
chmod +x autoscan_nmap.sh
./autoscan_nmap.sh 
```

# Énumération du réseau
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
