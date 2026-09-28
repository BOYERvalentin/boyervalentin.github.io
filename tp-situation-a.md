# Remplacement d'un switch d'étage saturé

[← Retour au portfolio](tp-camille.html)

*PME de métallurgie, 45 postes, site principal — mars 2026 — option SISR*

## Contexte

Le site principal compte 45 postes, dont 12 dans l'atelier, reliés à un switch d'étage installé en 2016. Les postes de l'atelier servent aux plans de fabrication et à la saisie des temps.

## Problématique

Depuis trois semaines, les 12 postes de l'atelier subissaient des coupures réseau de quelques secondes, plusieurs fois par jour. La sauvegarde du serveur de fichiers, lancée à 12 h, durait 42 minutes au lieu des 6 minutes habituelles et terminait parfois en erreur.

## Démarche

J'ai d'abord relevé les débits depuis un poste de l'atelier : 8 Mo/s en copie vers le serveur, contre 74 Mo/s depuis un poste du bureau. Trois hypothèses : le câblage, la carte réseau des postes, le switch.

J'ai écarté le câblage : les liens ont été certifiés en 2023 et un test au testeur de câble sur trois prises n'a rien montré. J'ai écarté la carte réseau : le problème touchait les 12 postes, pas un seul.

Restait le switch, un modèle 16 ports à 100 Mb/s dont les compteurs affichaient des erreurs de collision. Je l'ai remplacé par un switch administrable gigabit prêté par le fournisseur, pour valider l'hypothèse avant tout achat.

## Outils mobilisés

- Switch administrable 16 ports gigabit (modèle de prêt, puis modèle acheté)
- Testeur de câble RJ45
- Wireshark 4.2 pour observer les retransmissions
- GLPI 10.0 pour le suivi du ticket et la mise à jour de l'inventaire

## Précautions prises

J'ai sauvegardé la configuration de l'ancien switch, étiqueté les 16 câbles avant de les débrancher, et programmé l'intervention entre 12 h 30 et 13 h 15, hors production. J'ai prévenu le chef d'atelier la veille.

## Résultats

Le débit de copie est passé de 8 Mo/s à 74 Mo/s. La sauvegarde est redescendue à 6 minutes. Aucune coupure signalée dans les trois semaines qui ont suivi. L'inventaire GLPI a été mis à jour le jour même.

## Bilan personnel

J'ai perdu deux jours à suspecter le câblage alors que les compteurs d'erreurs du switch donnaient la réponse dès le premier relevé. La prochaine fois, je commencerai par interroger les équipements réseau en SNMP avant de tester les liens un par un.

---

**Compétences mobilisées** : gérer le patrimoine informatique ; répondre aux incidents et aux demandes d'assistance.

# Situation B

## Contexte

Le 28 septembre 2026, j’ai été sollicité pour un poste du bureau d’études, un Dell OptiPlex 7090 Tower. Depuis environ quinze jours, il redémarrait tout seul trois ou quatre fois par jour. L’utilisateur perdait son travail à chaque redémarrage.

## Problème constaté

J’ai consulté l’Observateur d’événements et relevé des erreurs Kernel-Power 41. Elles indiquaient des arrêts inattendus, sans suffire à identifier leur cause.

## Pistes examinées

J’ai d’abord envisagé un problème logiciel et installé les mises à jour de Windows. Comme les redémarrages ont continué, cette piste n’a pas été confirmée. J’ai ensuite testé la mémoire vive avec MemTest pendant une nuit : le test a signalé 0 erreur, ce qui m’a conduit à écarter la RAM.

## Inspection du matériel

Avant d’ouvrir le poste, je l’ai éteint, débranché du secteur et attendu quelques minutes. J’ai constaté que l’alimentation était très poussiéreuse et que son ventilateur faisait un bruit inhabituel.

## Mesure et diagnostic

J’ai mesuré la consommation avec une prise wattmétrique. Le poste atteignait 310 W en pointe, alors que l’alimentation était donnée pour 350 W. Cette marge réduite, associée à l’état de l’alimentation, m’a fait suspecter qu’elle était en cause.

## Intervention et résultats

J’ai remplacé l’alimentation par un modèle de 550 W et nettoyé le poste. Depuis l’intervention, aucun redémarrage intempestif n’a été constaté pendant un mois.

## Bilan

C’était la première panne matérielle que j’identifiais seul, et j’étais content d’avoir trouvé l’origine du problème. Pour une prochaine panne de ce type, je vérifierai l’alimentation plus tôt, après les premiers contrôles.

