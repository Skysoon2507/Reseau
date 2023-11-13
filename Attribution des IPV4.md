---


---

<h1 id="attribution-des-adresses-ipv4">Attribution des adresses IPV4</h1>
<p>💡 Les paquets provenant d’une IP privé ne peuvent pas communiquer à travers des routeurs publics, ils suppriment directement le paquet</p>
<h2 id="network-address-translation-nat">Network Address Translation (NAT)</h2>
<ul>
<li>C’est la traduction d’une <strong>IP privée en adresse publique</strong> lors du passage du <mark>routeur</mark> entre le <strong>réseau privé et internet</strong></li>
</ul>
<h3 id="nat-statique">Nat Statique</h3>
<ul>
<li>
<p>Associer <strong>UNE</strong> adresse <em>privé</em> vers <strong>UNE</strong> adresse <em>publique</em></p>
</li>
<li>
<p>Etapes de configurations :</p>
<ol>
<li>
<p>Configurer l’<strong>interface interne</strong> du routeur (vres le réseau privé)  avec <code>(config-if)# ip nat inside</code></p>
</li>
<li>
<p>Configurer de même l’<strong>interface externe</strong> (internet) avec <code>(config-if)#ip nat outside</code></p>
</li>
<li>
<p>Saisir les <strong>règles de traduction</strong> pour chaque IP privé avec <code>(config)#ip nat inside source static IPprivée IPpublique</code></p>
</li>
<li>
<p>Afficher la table NAT : <code>#show ip nat translations</code></p>
</li>
</ol>
</li>
</ul>
<hr>
<h3 id="nat-dynamique">Nat Dynamique</h3>
<ul>
<li>Pour définir le pool d’IP NAT, on peut faire la commande suivante : <code>ip nat pool add-public 7.7.7.7 7.7.7.7 netmask 255.255.255.0</code>
<ul>
<li>On retrouve les champs suivants :</li>
</ul>
</li>
</ul>

<table>
<thead>
<tr>
<th>ip nat pool add-public</th>
<th></th>
</tr>
</thead>
<tbody></tbody>
</table><ul>
<li>
<p>Pour configurer une access-list, on inverse le masque pour décider ce qui sera affecter :</p>
<ul>
<li><code>access-list 1 permit 192.168.1.0 0.0.0.255</code></li>
<li><code>access-list 1 permit 192.168.1.0 0.0.0.255</code></li>
<li><code>access-list 1 permit 172.16.0.1 0.0.255.255</code></li>
</ul>
</li>
<li>
<p>Pour voir les règles d’access-list : <code>sh ip access-list</code></p>
</li>
<li>
<p>Pour lier la pool au NAT : <code>ip nat inside source list 1 pool add-public</code></p>
</li>
</ul>
<h3 id="pat">PAT</h3>
<ul>
<li>Pour activer le PAT sur un routeur qui a déjà le <strong>NAT dynamique activé</strong>, on rajoute <mark>overload</mark> à la fin de commande suivante : <code>ip nat inside source list 1 pool add-public overload</code></li>
<li>Même chose mais avec un range d’IP NAT dynamique, on doit changer le <em>pool</em> par l’interface de sortie pour économiser une IP publique : <code>ip nat inside source list 1 interface fa0/0 overload</code></li>
</ul>

