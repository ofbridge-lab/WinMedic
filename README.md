# WinMedic

**WinMedic** est un outil de réparation automatisée pour Windows conçu pour simplifier au maximum la restauration du système. 
Contrairement à des outils comme *DISM GUI* qui sont des interfaces manuelles, WinMedic orchestre intelligemment les commandes de réparation dans l'ordre logique pour garantir un résultat optimal.

##  Dans quels cas utiliser WinMedic

Le spectre d'utilisation est large. Vous devriez envisager de lancer l'outil si vous rencontrez :
* **Lenteur extrême au démarrage** (fond d'écran figé plusieurs minutes).
* **Comportements erratiques** (Menu Démarrer ou barre des tâches gelés).
* **Erreurs de mise à jour** (Windows Update bloqué).
* **Écrans bleus (BSOD)** répétés.
* **Fichiers système manquants** (.dll introuvables).
* **Maintenance préventive** après une désinfection virale.

---

#### ⚙️ Fonctionnement de la réparation automatique
Dès le démarrage, le logiciel effectue une vérification de la connexion internet pour déterminer s'il peut effectuer la réparation en ligne. Si aucune connexion n'est détectée, il vous proposera de passer par un fichier ISO. Vous avez également la possibilité de choisir manuellement l'option ISO dès le départ. Une fois l'ISO sélectionné, le logiciel s'occupe de le monter tout seul et utilise automatiquement le chemin nécessaire pour effectuer la réparation hors ligne.

Le processus se déroule en plusieurs étapes clés :

* **Vérification du disque (CHKDSK) :** L'outil lance d'abord un CHKDSK en lecture seule. Si des erreurs sont détectées, une fenêtre vous demandera si vous souhaitez effectuer un CHKDSK /R /F. Cette action nécessite un redémarrage. Une fois la réparation du disque terminée au reboot, vous pourrez relancer l'application pour poursuivre le processus. (Ignorer cette étape est déconseillé pour une réussite optimale).
* **Analyse de l'image (DISM ScanHealth) :** Le logiciel exécute ensuite la commande DISM /Online /Cleanup-Image /ScanHealth pour détecter d'éventuelles corruptions de l'image système.
* **Réparation de l'image (DISM RestoreHealth) :** Si une erreur est détectée, la commande RestoreHealth est lancée pour réparer les fichiers corrompus en téléchargeant des fichiers sains via Windows Update (ou via l'ISO sélectionné).
* **Vérification de l'intégrité (SFC Scannow) :** Une fois l'image système réparée, le logiciel lance SFC /scannow pour vérifier et réparer les fichiers système en s'appuyant sur l'image désormais saine.
* **Nettoyage final :** Pour terminer, la commande DISM /Online /Cleanup-Image /StartComponentCleanup nettoie le magasin de composants WinSxS en supprimant les versions obsolètes des mises à jour.

À la fin du processus, un rapport s'affiche pour indiquer si tout s'est bien passé ainsi que le temps écoulé. Une fenêtre vous recommandera alors de redémarrer le PC.
---

## 🛠️ Outils individuels pour les experts

Pour les utilisateurs avancés, l'onglet **"Outils individuels"** permet de lancer chaque commande de manière isolée :

| Commande | Rôle et Action |
| :--- | :--- |
| **CHKDSK** | Vérifie l'intégrité du système de fichiers (lecture seule). |
| **CHKDSK /R /F** | Corrige les erreurs disque et secteurs défectueux (reboot requis). |
| **DISM /ScanHealth** | Analyse approfondie de l'image système sans correction. |
| **DISM /RestoreHealth** | Répare l'image Windows via Windows Update ou source locale. |
| **DISM /AnalyzeComponentStore** | Estime l'espace disque récupérable dans WinSxS. |
| **DISM /StartComponentCleanup** | Libère de l'espace en supprimant les composants obsolètes. |
| **SFC /scannow** | Vérifie et répare les fichiers système corrompus. |

---

---
*WinMedic - Redonner vie à un Windows capricieux en quelques clics.*
