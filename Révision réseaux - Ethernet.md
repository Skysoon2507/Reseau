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

