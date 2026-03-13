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

## ⚙️ Fonctionnement de la réparation automatique

Dès le démarrage, le logiciel effectue une vérification de la connexion internet pour déterminer s'il peut effectuer la réparation en ligne. Si aucune connexion n'est détectée, il vous proposera de passer par un **fichier ISO**. 

Le logiciel s'occupe de monter l'ISO tout seul et utilise automatiquement le chemin nécessaire pour effectuer la réparation hors ligne. Le processus se déroule en plusieurs étapes clés :

1. **Vérification du disque (CHKDSK) :** Lancement d'un CHKDSK en lecture seule. Si des erreurs sont détectées, une fenêtre propose d'effectuer un `CHKDSK /R /F` (nécessite un redémarrage).
2. **Analyse de l'image (DISM ScanHealth) :** Exécution de la commande pour détecter d'éventuelles corruptions de l'image système.
3. **Réparation de l'image (DISM RestoreHealth) :** Réparation des fichiers via Windows Update ou l'ISO sélectionné.
4. **Vérification de l'intégrité (SFC Scannow) :** Vérification et réparation des fichiers système en s'appuyant sur l'image saine.
5. **Nettoyage final :** Nettoyage du magasin de composants **WinSxS** (`StartComponentCleanup`) pour supprimer les versions obsolètes.

À la fin du processus, un rapport complet s'affiche avec le temps écoulé et une recommandation de redémarrage.

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
