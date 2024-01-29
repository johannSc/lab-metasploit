# lab-metasploit

## Intro

Metasploit est un outil de test de pénétration très utilisé qui rend le piratage plus facile qu'avant. En effet le framework déployé au sein du projet permet de tester des failles très simplement. Kali intègre metasploit de manière native, nous avons donc une bonne excuse pour le tester...

### La console msf

La console se démarre via la commande suivante:

```
 msfconsole
```

 Dès lors, il est possible d’exécuter des commandes en ayant au préalable interrogé l’interface afin de connaitre leurs options :

```
 help
```

Il existe de nombreux modules que l’on peut ajouter à l’utilitaire Metasploit. Ces modules sont téléchargeables depuis le site www.rapid7.com. Ils sont contenus dans une base interne permettant d’interroger à la fois les bases Common Vulnerabilities and Exposures (abrégée en CVE).

### Avant d'attaque

Rappelez vous, avant d’exploiter une quelconque faille de sécurité, il faut bien évidemment effectuer un scan de vulnérabilités pour trouver l'angle d'attaque. Si vous avez une piste vous pouvez dans un premier temps rechercher la ou les CVE associée(s), ou encore un mot clé. Exemple de recherche:

- Prise d'infos

Elle peut se faire via pas mal d'outils: nikto, nmap, spiders... Le but est de trouver un service utilisé, un port ouvert ou encore une version applicative.

- L'info trouvée

Prenons l'exemple de la faille MS08-067 de chez Microsoft. Pour avoir les informations coté metasploit:

```
search ms08-067
```

Dès lors, on peut rechercher des précisions quant à ce module pré-intégré, puisque l’on dispose du chemin d’accès mentionné ci-dessus exploit/windows/smb/ms08_067_netapi, en exécutant l’instruction suivante 

```
info exploit/windows/smb/ms08_067_netapi
```

Pour de plus amples informations:

```
show options
```

## TP

### Mise en place coté cible (metasploitable)

Pensez tout d'abord à prendre l'ip de la machine Debian:

```
ip a
```

Depuis votre machine Debian, installez Docker:

```
apt update
apt install docker.ce
```

Puis téléchargez l'image suivante (disponible sous AMD64 et ARM) et exécurtez la:

```
docker run --name vsftpd-2.3.4 -it clintmint/vsftpd-2.3.4:1.0 sh -c "start-vsftpd && sh"
```

Si le conteneur est bien lancé, vous aurez cet intitulé en début de prompt:

```
vsftpd-2.3.4
```

ça vous donne idée de la faille... Sur cette machine on ne touche plus à rien.

### Coté KALI

Lancez la console metasploit et tentez de faire une recherche sur vsftpd. Il vous faut comprendre comment lancer l'exploit, indiquer les infos du payload pour que ça puisse fonctionner...

```
search vsftp
```

Il faut également trouver comment préciser l'ip de la victime, que vous aurez préalablement noté. Une fois l'exploit lancé et validé, que se passe t il?
