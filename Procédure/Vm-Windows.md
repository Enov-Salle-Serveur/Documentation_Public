# Documentation : Configuration Réseau et Contextualisation de Windows Server 2022 sous OpenNebula

Cette documentation détaille les étapes pour ajouter et configurer correctement une carte réseau émulée pour une machine virtuelle Windows Server 2022 dans OpenNebula, ainsi que l'installation du package de contextualisation.

---

## Étape 1 : Configuration de la carte réseau dans OpenNebula (Sunstone)

Avant de démarrer la machine virtuelle, il est nécessaire de lui associer une carte réseau avec un profil de matériel que Windows peut reconnaître nativement.

1. Connectez-vous à l'interface **OpenNebula Sunstone**.
2. Éteignez la machine virtuelle si elle est en cours d'exécution (*Poweroff*).
3. Allez dans le menu **Templates** > **VMs** (ou directement dans la configuration de la VM éteinte) et cliquez sur **Update / Modifier**.
4. Rendez-vous dans l'onglet **Network** (Réseau).
5. Ajoutez ou modifiez la carte réseau existante en configurant les options suivantes :
   * **Virtual NIC Hardware Mode** : Sélectionnez `Emulated`.
   * **Hardware model to emulate** : Saisissez ou sélectionnez `e1000` (ce mode simule une carte Intel standard reconnue nativement par Windows Server 2022).

*Pensez à sauvegarder les modifications avant de démarrer la VM.*

> **[INSERER CAPTURE D'ÉCRAN : Interface OpenNebula montrant les champs 'Emulated' et 'e1000' configurés]**

---

## Étape 2 : Validation de la carte réseau sous Windows

1. Démarrez la machine virtuelle depuis OpenNebula et ouvrez la console VNC.
2. Connectez-vous à la session Windows avec les identifiants suivants :
   * **Utilisateur** : `Administrateur`
   * **Mot de passe** : `Scoubidou1&`

> **[INSERER CAPTURE D'ÉCRAN : Écran de connexion Windows ou Bureau Windows ouvert]**

3. Faites un clic droit sur le menu Démarrer et ouvrez le **Gestionnaire de périphériques** (*Device Manager*).
4. Déroulez la section **Cartes réseau** (*Network adapters*). La carte réseau émulée Intel (e1000) doit apparaître comme fonctionnelle et active, sans triangle jaune.

> **[INSERER CAPTURE D'ÉCRAN : Gestionnaire de périphériques Windows avec la carte réseau active]**

---

## Étape 3 : Installation d'OpenNebula Context pour Windows

Le package de contextualisation permet à Windows de récupérer automatiquement son adresse IP, sa passerelle, ses DNS et son nom d'hôte depuis OpenNebula à chaque démarrage.

1. Depuis la VM Windows, ouvrez le navigateur Internet et téléchargez le package officiel d'OpenNebula au format `.msi` :
   * URL officielle : [https://github.com/OpenNebula/addon-context-windows/releases](https://github.com/OpenNebula/addon-context-windows/releases)
2. Double-cliquez sur le fichier d'installation téléchargé (`one-context-7.X.X.msi`).
3. Suivez l'assistant d'installation en laissant toutes les options par défaut, puis cliquez sur **Install**.

> **[INSERER CAPTURE D'ÉCRAN : Assistant d'installation du package .msi OpenNebula Context]**

4. Une fois l'installation terminée, cliquez sur **Finish**. Un service Windows nommé `OneContext` est désormais actif en arrière-plan.

---

## Étape 4 : Préparation du Template final (Sysprep)

*Cette étape est indispensable si vous souhaitez transformer cette VM en modèle réutilisable par d'autres utilisateurs.*

1. Ouvrez la fenêtre "Exécuter" de Windows (Touches `Apt + R` ou `Démarrer + R`).
2. Saisissez `sysprep` et validez.
3. Dans le dossier qui s'ouvre, double-cliquez sur l'application **`sysprep.exe`**.
4. Configurez l'outil exactement comme suit :
   * **Action de nettoyage du système** : `Passer au mode OOBE (Out-of-Box Experience)`
   * **Option "Généraliser"** : **Cocher impérativement la case** (permet d'effacer les configurations réseau actuelles pour qu'OpenNebula génère une nouvelle IP propre au prochain démarrage).
   * **Options d'arrêt** : Sélectionner `Arrêter` (*Shutdown*).

> **[INSERER CAPTURE D'ÉCRAN : Fenêtre de l'outil Sysprep configurée avec 'OOBE', 'Généraliser' coché et 'Arrêter']**

5. Cliquez sur **OK**. Windows va nettoyer le système puis s'éteindre automatiquement.

La machine virtuelle est désormais prête à être transformée en Template OpenNebula. Pensez à cocher l'option **Network** dans l'onglet *Context* du template Sunstone pour que l'attribution automatique des adresses IP soit fonctionnelle !
