---


---

<h1 id="ethernet">ETHERNET</h1>
<h2 id="technologies-lan">TECHNOLOGIES LAN</h2>
<p>🔴 Norme Ethernet  : <strong>IEEE 802.2 et .3</strong></p>
<p>💡 Sous-couche <strong>LLC</strong></p>
<ul>
<li>Logical Link Control</li>
<li>Lien entre les couches <strong>supérieur</strong> (logicielles) et <strong>inférieur</strong> (matérielles)</li>
<li>Extrait les données de la couche <strong>réseau</strong></li>
</ul>
<p>💡 Sous-couche <strong>MAC</strong></p>
<ul>
<li>Media Access Control</li>
<li>Gestion des échanges au niveau <strong>matériel</strong></li>
<li><strong>Encapsulation de données</strong> : délimitations des trames, adressage, detection erreurs</li>
</ul>
<hr>
<p>💡 <strong>Trame Ethernet</strong></p>
<ul>
<li>
<p><strong>Préambule</strong></p>
</li>
<li>
<p><strong>@MAC Destination :</strong> L’adresse MAC de la trame est comparé à celle du périphérique. Si les deux correspondent, le périphérique accepte la trame. Différents types existent :<br>
▶️ Mono-diffusion<br>
▶️ Multi-diffusion<br>
▶️ Diffusion (utilisé par ARP pour 1ere communication)</p>
</li>
<li>
<p><strong>@MAC Source :</strong> Carte réseau / interface à l’originie de la trame -&gt; adresse monodiffusion</p>
</li>
<li>
<p><strong>EtherType :</strong> Protocole de la couche supérieur encapsulé dans la trame Ethernet. Les plus fréquentes :<br>
▶️ <strong>IPV4</strong> = 0x800<br>
▶️ <strong>IPV6</strong> = 0x86DD<br>
▶️ <strong>ARP</strong> = 0x806</p>
</li>
<li>
<p><strong>Données :</strong> données encapsulées de la couche supérieur (<strong>paquet réseau</strong>). La longueur minimale de la trame est de 64 bits. Si un paquet plus petit est encapsulé, on utilise des <strong>bits de remplissage</strong> pour atteindre cette taille minimale.</p>
</li>
<li>
<p><strong>FCS :</strong> Permet de détecter les erreurs d’intégrité d’une trame. Pour cela, il effectue un <strong>Contrôle de redondance cyclique</strong> (CRC)</p>
</li>
</ul>
<hr>
<p>💡 <strong>Adresse MAC :</strong></p>
<ul>
<li>Composé de <strong>12 nombres hexadec</strong></li>
<li>⭐️ Stockée dans la <strong>ROM</strong> de la <strong>carte réseau</strong></li>
<li>Utilisé comme adresse <strong>source</strong></li>
</ul>
<p>💡 <strong>Types de trames</strong></p>
<ul>
<li>▶️Unicast : @MAC dest @MAC source</li>
<li>▶️Broadcast : <strong>@FF-FF-FF-FF-FF</strong> @MAC source</li>
</ul>
<hr>
<h3 id="protocole-arp">Protocole ARP</h3>
<p>💡 Résolution d’une adresse <strong>IP</strong> en adresse <strong>MAC</strong></p>
<ul>
<li>Recherche en <strong>broadcast</strong> sur LE réseau (protocole de couche 2, pas 3)</li>
<li>Réponse en <strong>unicast</strong></li>
<li>Table de mappage <strong>IP/MAC</strong></li>
</ul>
<p>⭐️🔴 Si le protocole ARP traverse un routeur, le routeur <strong>supprime l’entête Ethernet de @MAC SOURCE de la trame et le remplace par son @MAC</strong></p>
<hr>
<h2 id="commutateur">COMMUTATEUR</h2>
<h3 id="architecture-dun-switch">Architecture d’un switch</h3>
<p>💡 Architecture matérielle d’un switch :</p>
<ul>
<li>Mémoire <strong>ROM</strong> (non-volatile)</li>
<li>Mémoire <strong>Flash</strong> (rapide)</li>
<li>Mémoire <strong>RAM</strong> (volatile)</li>
<li>Mémoire <strong>NVRAM</strong> (RAM non-volatile)</li>
<li>Interface <strong>console</strong> (config filaire du Switch)</li>
<li>Système de contrôle <strong>ASIC</strong> (gère la commutation et la rapidité)</li>
<li>Alimentation / CPU / Interfaces réseaux</li>
</ul>
<p>💡 Etapes <strong>démarrage Switch</strong></p>
<ol>
<li>Exécution du <strong>POST</strong> (<em>Power-On Self Test</em>) -&gt; vérifie que tout les composants fonctionne bien</li>
<li>Chargement du <strong>programme d’amorçage</strong> (ROMMon -&gt; <em>ROM Monitor)</em></li>
<li>Localisation de <strong>l’IOS</strong> et chargement dans la <strong>RAM</strong></li>
<li>Localisation du <strong>fichier de conf</strong></li>
</ol>
<hr>
<h3 id="securisation-contre-mac-flooding">Securisation contre MAC Flooding</h3>
<p>💡 Sécurisation d’une interface :</p>
<ul>
<li>
<p><code>switchport port-security maximum m</code><br>
▶️ Limite à m le nombre d’adresses MAC qui <strong>peuvent être apprises via cette interface</strong></p>
</li>
<li>
<p><code>switchport port-security mac-address AAAA.AAAA.AAAA</code><br>
▶️ Autorisation <strong>statique</strong> de l’adresse MAC <em>AAAA.AAAA.AAAA</em></p>
</li>
</ul>
<p>💡 Réactions d’un Switch si violation de la sécurité MAC</p>
<ul>
<li>
<p><code>switchport port-security violation protect/restrict/shutdown</code></p>
</li>
<li>
<p><strong>Protect</strong> : les trames provenant d’une @MAC inconnue sont <strong>bloquées</strong></p>
</li>
<li>
<p><strong>Restrict :</strong> envoi d’une <em>alerte SNMP</em> et incrémentation du <strong>compteur de violation</strong></p>
</li>
<li>
<p><strong>Shutdown</strong> (défaut) : <strong>Désactivation</strong> de l’interface et mise en état <code>« err-disabled »</code></p>
</li>
</ul>
<hr>
<h3 id="spanning-tree-protocol-stp">Spanning Tree Protocol (STP)</h3>
<p>💡 Etapes de mises en place :</p>
<ol>
<li>
<p>Election du <strong>commutateur racine</strong> (Root Bridge)<br>
▶️ Identifiant <em>BID le plus petit</em><br>
▶️ <em>Valeur de priorité</em> paramétrable + numéro de <em>VLAN</em> + <em>adresse MAC</em> du switch + numéro de port</p>
</li>
<li>
<p>Calcul du <strong>chemin</strong> de <strong>coût le plus faible</strong> vers chaque équipement depuis ce pont racine</p>
</li>
</ol>
<p>💡  Coût / débit standard :</p>
<ul>
<li>Ethernet : <strong>10 Mbits / 100</strong></li>
<li>FastEthernet : <strong>100 Mbits / 19</strong></li>
<li>Gigabit-Ethernet : <strong>1 Gbits / 4</strong></li>
<li>Ten-Gigabit-Ethernet : <strong>10 Gbits / 2</strong></li>
</ul>

