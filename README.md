# Plateforme Énov - Guide de Configuration Global

Bienvenue sur le dépôt de documentation de la plateforme **Énov**. Ce projet regroupe l'ensemble des guides et procédures nécessaires pour configurer votre environnement et déployer vos ressources.

<p align="center">
  <img src="img/Logo_Enov_Main.png" alt="Logo Énov" width="300"/>
</p>

---

## 📚 Liste des Procédures Disponibles

Pour démarrer sur la plateforme, veuillez suivre les guides dans l'ordre suivant :

1. 👤 [Création de Compte](Procédure/Create_Account.md)  
   *Guide pour s'inscrire sur la plateforme avec vos identifiants institutionnels.*

2. 🔑 [Configuration du VPN NetBird](Procédure/SetupVPN.md)  
   *Étapes de connexion et d'installation du client VPN pour accéder au réseau privé.*

3. 🔒 [Ajout d'une Clé SSH](Procédure/Nebula_Add_SSH_Key.md)  
   *Étape obligatoire pour associer votre clé publique à votre compte avant de déployer des ressources.*

4. 🖥️ [Création d'une Machine Virtuelle](Procédure/Create_VM.md)  
   *Procédure pas à pas pour déployer et configurer votre VM sur OpenNebula.*

5. 💣​ [Création d'une Machine Windows](Procédure/VM-Windows.md) 

---  

## 🌐 Configurations Spécifiques : Utilisation d'un LAN Personnel

Si vous déployez des architectures avancées nécessitant l'isolation de vos machines via votre propre réseau privé virtuel, un dossier technique indépendant est à votre disposition :

* 🔌 [Configuration des Interfaces et du MTU pour LAN Personnel](Procédure/Setup-interface-for-LAN.md)  
  *Guide complet pour configurer le MTU à 1450 sur vos machines (Linux Ubuntu, Rocky, Windows) et vos pare-feux (PfSense, Fortigate), afin d'éviter les blocages de requêtes HTTP/HTTPS sur les réseaux encapsulés (VXLAN).*

> ⚠️ **Attention :** Les documentations du dossier LAN Personnel s'appliquent uniquement si vous configurez un réseau privé dédié. Ne modifiez pas ces paramètres sur les réseaux publics et mutualisés standards d'Enov.

---  
## 📈 Évolutions futures
*De nouvelles procédures et documentations techniques seront ajoutées à ce dossier au fur et à mesure des évolutions de la plateforme Énov.*
