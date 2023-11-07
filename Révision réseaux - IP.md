---


---

<h1 id="réseaux-ip">Réseaux IP</h1>
<p>Rappel du modèle OSI :<br>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/OSI_Model_v1.svg/langfr-495px-OSI_Model_v1.svg.png" alt="OSI model"></p>
<h2 id="normes-ip">Normes IP</h2>
<p>💡 Format <strong>IPV6</strong> : 16 octets (128 bits)</p>
<hr>
<h3 id="paquet-ip--contenu">Paquet IP : contenu</h3>
<ul>
<li>
<p><strong>Version :</strong> 4 pour ipv4 et 6 ipv6</p>
</li>
<li>
<p><strong>Services différencier :</strong> priorité du paquet (<mark>0</mark> par défaut)</p>
</li>
<li>
<p><strong>Time to live (TTL) :</strong> Evite les boucles de routage</p>
</li>
<li>
<p><strong>IP source / destination</strong></p>
</li>
<li>
<p><strong>Protocoles :</strong> TCP / UDP</p>
</li>
<li>
<ul>
<li>💡 <mark>UDP</mark> (User Datagram Protocol) :<br>
✔️<strong>Rapide</strong> et <strong>moins de ressources</strong> utilisées<br>
✔️<strong>Peu de champs</strong> dans un segment UDP<br>
❌Vérification d’erreur<br>
❌Vérification de bonne reception des données<br>
❌Session de connexion</li>
</ul>
</li>
<li></li>
<li>
<ul>
<li>💡 <mark>TCP</mark> (Transmission Control Protocol) :	<br>
✔️Permet d’établir une connexion fiable entre 2 hôtes<br>
✔️Création d’une <strong>session de connexion (SYN - SYN/ACK - ACK)</strong>,<br>
✔️ Vérification que les <strong>paquets sont bien transmis</strong>,<br>
✔️ <strong>Contrôle des flux</strong> et <strong>gestion des erreurs</strong><br>
❌Lent</li>
</ul>
</li>
</ul>
<hr>
<h3 id="et-logique">ET logique</h3>
<p><strong>Adresse hôte binaire</strong> : 10101100 00010000 10000100 01000110 -&gt; 172.16.132.70<br>
<strong>Masque sous réseau binaire</strong> : 11111111 11111111 11110000 11100000 -&gt; 255.255.240.0<br>
<strong>Adresse réseau</strong> : 10101100 00010000 10000000 0000000 -&gt; 172.16.128.0</p>
<hr>
<h3 id="ipv4">IPV4</h3>
<p>📍 Nombre adresses utilisables : <strong>2^n -2</strong></p>
<p>📍 Classes d’adresse :</p>
<ul>
<li>Classe <mark>A</mark> : <strong>/8</strong></li>
<li>Classe <mark>B</mark> : <strong>/16</strong></li>
<li>Classe <mark>C</mark> : <strong>/24</strong></li>
</ul>
<p>📍 Types d’adresse :</p>
<ul>
<li>
<p>Adresses <mark>privées</mark> :<br>
▶️ <strong>10</strong>.0.0.0 à 10.255.255.255<br>
▶️ <strong>172.16</strong>.0.0 à 172.31.255.255<br>
▶️ <strong>192.168</strong>.0.0 à 192.168.255.255</p>
</li>
<li>
<p>Adresse <mark>boucle locale</mark> :<br>
🔄 <strong>127</strong>.0.0.0 à 127.255.255.255</p>
</li>
<li>
<p>Adresses <mark>liaison locale (APIPA)</mark> :<br>
🔂 <strong>169.254</strong>.0.0 à 169.254.255.255</p>
</li>
<li>
<p>Adresses <mark>publiques</mark> : routables sur <strong>Internet</strong></p>
</li>
</ul>
<hr>
<h2 id="segmentation-ip">Segmentation IP</h2>
<h3 id="avec-nombre-de-sous-réseaux">Avec nombre de sous-réseaux</h3>
<ol>
<li>Calcul en <mark>puissance de 2</mark> le nombre de bits à allouer</li>
<li>Ajouter ce nombre au <mark>masque actuel</mark></li>
</ol>
<p>❓ Exemple : créer <strong>6</strong> sous-réseaux dans l’adresse <em>192.168.0.0/24</em> :</p>
<ul>
<li>
<p>2^3 = 8, nous devons utiliser <strong>3 bits</strong>, donc 24 + 3 = 27. Le nouveau masque est donc en <strong>/27</strong></p>
</li>
<li>
<p>💻 1er sous-réseau : 192.168.0.<mark>000</mark>0 0000 <strong>/27</strong> == 192.168.0.<mark>0</mark><br>
💻 2eme sous-réseau : 192.168.0.<mark>001</mark>0 0000 <strong>/27</strong> == 192.168.0.<mark>32</mark><br>
💻 3eme sous-réseau : 192.168.0.<mark>010</mark>0 0000 <strong>/27</strong> == 192.168.0.<mark>64</mark><br>
💻 …</p>
</li>
</ul>
<hr>
<h3 id="avec-nombre-dhôtes-par-sous-réseaux">Avec nombre d’hôtes par sous-réseaux</h3>
<ol>
<li>Calcul en <mark>puissance de 2</mark> le nombre de bits à allouer</li>
<li>Faire l’opération suivante : <mark>32 - puissance de 2</mark></li>
</ol>
<p>❓ Exemple : créer des sous-réseaux de <strong>1 000</strong> (+2, réseau + diffusion ) postes dans l’adresse <em>172.16.0.0 /16</em></p>
<ul>
<li>
<p>2^10 = 1024, nous devons utiliser <strong>10 bits</strong>, donc 32 - 10 = 22. Le nouveau masque est donc en <strong>/22</strong></p>
</li>
<li>
<p>💻 1er sous-réseau : 172.16.<mark>0000 00</mark>00.0 == 172.16.<mark>0</mark>.0 <strong>/22</strong><br>
💻 2eme sous-réseau : 172.16.<mark>0000 01</mark>00.0 == 172.16.<mark>4</mark>.0 <strong>/22</strong><br>
💻 3eme sous-réseau : 172.16.<mark>0000 10</mark>00.0 == 172.16.<mark>8</mark>.0 <strong>/22</strong></p>
</li>
</ul>
<hr>
<h3 id="méthode-segmentation-réseau">Méthode segmentation réseau</h3>
<ul>
<li>
<p><strong>FLSM</strong> (<em>Fixed Lenght Subnet Mask</em>)<br>
✔️ Tout les sous-réseaux partagent <mark>même masque et nbr d’IP</mark><br>
❌ Faille de sécurité<br>
❌ Gaspillage @IP non utilisées</p>
</li>
<li>
<p><strong>VLSM</strong> (<em>Variable Lenght Subnet Mask</em>)<br>
✔️ Chaque sous-réseau a un <mark>masque adapté</mark> au nbr d’IP nécessaire</p>
</li>
</ul>
<hr>
<h2 id="routage">Routage</h2>
<p>💡 Circulation de <strong>proche en proche</strong> : Un paquet est envoyé à la passerelle la plus proche, qui transfère à la passerelle suivante…</p>
<p>💡 <strong>Time To Live</strong></p>
<ul>
<li>Valeur par défaut modifiable</li>
<li>Décrementé à chaque passage dans un routeur</li>
<li>Si TTL = 0, destruction du paquet</li>
</ul>
<p>💡 <strong>Table de routage</strong></p>
<ul>
<li><mark>C</mark> @IP is directly connected *port = réseau connu par le routeur</li>
<li><mark>S</mark> @IP via @IP = transmission à un autre routeur</li>
<li><mark>S*</mark> 0.0.0.0/0 via @IP = route par défaut</li>
</ul>
<p>💡 <strong>Agrégation de routes</strong></p>
<ul>
<li>✔️ Table de routage plus petite</li>
<li>✔️ Routage + rapide</li>
<li>✔️ Regrouper un grand nbr de réseau</li>
</ul>
<p>▶️ Méthode :</p>
<ul>
<li>On a 3 réseaux : 192.168.<strong>1.0</strong>, 192.168.<strong>2.0</strong>, 192.168.<strong>3.0</strong></li>
<li>On les converti en <strong>binaire</strong> et regarde jusqu’où on retrouve un <strong>bit en commun</strong></li>
<li>192.168.0000 0<mark>0</mark>01.0<br>
192.168.0000 0<mark>0</mark>10.0<br>
192.168.0000 0<mark>0</mark>11.0</li>
<li>Le réseau agrégé sera : <strong>192.168.0.0 /22</strong></li>
</ul>
<p>💡 <strong>Encapsulation paquet / trame</strong></p>
<ul>
<li>Paquet IP : @IP DESTINATAIRE et @IP EMETTEUR</li>
<li>Trame Ethernet : <mark>Récréée</mark> à chaque réseau, @MAC TRANSMETTEUR (routeur) et @MAC PROCHAINE PASSERELLE</li>
</ul>
<p>🔴 Paquet IP encapsulé dans les <strong>Données Ethernet</strong> de la      trame Ethernet</p>
<hr>
<h3 id="routage-on-a-stick">Routage on-a-Stick</h3>
<p>💡 <strong>Création de sous-interfaces</strong></p>
<ul>
<li>Le routeur est connecté à un unique switch par une liaison trunk</li>
</ul>
<p>▶️ Commandes Cisco :</p>
<ol>
<li>
<p>Créer une sous-interface ( port.VLAN )<br>
📄 (config)# <mark><em>interface fa1/0.2</em></mark></p>
</li>
<li>
<p>Déclaration du VLAN sur la sous-interface<br>
📄 (config)# <mark><em>encapsulation dot1q 2</em></mark></p>
</li>
<li>
<p>Attribution d’une @IP ( passerelle )<br>
📄 (config)# <mark><em>#ip address @IP @Masque</em></mark></p>
</li>
<li>
<p>Allumage d’une sous-interface<br>
📄 (config)# <mark><em>no shutdown</em></mark></p>
</li>
</ol>
<hr>
<h3 id="communications-multicouches">Communications Multicouches</h3>
<p>💡 <strong>MLS (MultiLayer Switching)</strong></p>
<ul>
<li>Commutateur de niveau 2 capable de faire du routage (niveau 3)</li>
</ul>
<p>💡  <strong>SVI</strong> :  interface virtuelle sur laquelle chaque VLAN est identifié</p>
<ul>
<li>
<p>La SVI traite les paquets provenant de tous les <mark>ports physiques associés au VLAN</mark></p>
</li>
<li>
<p>La SVI est la <mark>passerelle</mark> par défaut du VLAN</p>
</li>
<li>
<p>✔️ + Rapide qu’un routeur on-a-Stick<br>
✔️ Economie d’un lien Switch - Routeur<br>
✔️ +++ Bande passante</p>
</li>
</ul>

