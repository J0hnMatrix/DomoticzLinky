# Plugin Linky pour Domoticz (Migration MyElectricalData)

Ceci est un plugin pour [Domoticz](https://domoticz.com), permettant de récupérer les données de consommation et de production d'électricité de vos compteurs Linky (comptes particuliers) en s'appuyant sur la passerelle communautaire gratuite **MyElectricalData**.

Ce plugin est une version mise à jour du plugin historique qui utilisait le proxy de Russandol (`russandol.pro`) aujourd'hui obsolète.

---

## Prérequis

1. **Compte MyElectricalData :**
   * Rendez-vous sur [myelectricaldata.fr](https://www.myelectricaldata.fr).
   * Connectez-vous avec vos identifiants Enedis pour valider le partage de données (consentement).
   * Activez impérativement la **collecte et l'enregistrement de la consommation horaire** dans votre espace Enedis (à renouveler chaque année).
   * Récupérez votre **clé d'accès (Token)** depuis votre tableau de bord MyElectricalData.

2. **Domoticz :**
   * Version minimale : **4.11070** (ou plus récente). Pour visualiser la production et les heures creuses, la version **4.11774** ou **2020.1** (ou plus récente) est requise.
   * Le framework Python 3 doit être installé et activé sur votre serveur Domoticz.

---

## Installation

Déplacez-vous dans le sous-répertoire `plugins` de votre installation Domoticz et clonez le dépôt :
```bash
cd domoticz/plugins
git clone https://github.com/J0hnMatrix/DomoticzLinky
```
*(Ou remplacez simplement le fichier `plugin.py` existant par la version mise à jour).*

Redémarrez Domoticz pour charger le plugin.

---

## Configuration

Ajoutez le matériel dans Domoticz depuis l'onglet **Configuration / Matériel** :

1. Choisissez le type de matériel **Linky**.
2. Remplissez les champs requis :
   * **Point de Livraison (PDL)** (champ *Identifiant / Username*) : Renseignez votre numéro de PDL à 14 chiffres. Vous pouvez en renseigner plusieurs en les séparant par des virgules ou des espaces.
   * **Token MyElectricalData** (champ *Mot de passe / Password*) : Collez la clé d'accès obtenue sur le site de MyElectricalData.
   * **Heures creuses** : Configurez vos plages d'heures creuses (ex: `22h30-06h30`), ou laissez vide pour désactiver.
   * **Consommation (affichage principal / secondaire)** : Choisissez le type de pic ou cumul à afficher sur votre tableau de bord.
3. Cliquez sur **Ajouter**.

> [!TIP]
> **Création automatique :** Les capteurs (tuiles de mesures) sont créés automatiquement dans Domoticz dès le démarrage du plugin. Vous n'avez plus besoin d'activer l'option système "Accepter de nouveaux périphériques".
>
> *(Note : Si les tuiles n'apparaissent pas directement dans l'onglet **Utility / Mesures**, pensez à vérifier dans **Configuration / Utilisateurs** que votre compte a bien l'autorisation d'afficher ces nouveaux périphériques).*

---

## Dépannage et Logs

### Le périphérique affiche "invalid!:" ou "0"
* À la création du matériel, les valeurs par défaut sont initialisées à `0` pour éviter d'afficher des erreurs. Les vraies données de consommation et de production seront récupérées lors de la première requête API réussie (le plugin interroge l'API régulièrement toutes les heures).

### Erreur de Token ou accès refusé
* Vérifiez dans les logs de Domoticz (**Configuration > Log**). Si le plugin indique que le token est expiré ou invalide, assurez-vous d'avoir correctement copié le Token depuis votre espace MyElectricalData et d'avoir validé le consentement Enedis.
* Les serveurs d'Enedis et de MyElectricalData sont parfois indisponibles la nuit, le plugin réessaiera automatiquement plus tard.

---

## Licence & Crédits

Ce projet est sous licence **AGPLv3**.

### Auteurs & Contributeurs originaux
* **Baptiste Candellier** - *Kindle Linky plugin* - [linkindle](https://github.com/outadoc/linkindle)
* **Asdepique777** - *Jeedom Linky plugin* - [jeedom_linky](https://github.com/Asdepique777/jeedom_linky)
* **epierre** - *Linky external script for Domoticz* - [domoticz_linky](https://github.com/empierre/domoticz_linky)
* **Guillaume Zin** - *Portage vers le plugin framework de Domoticz*
* **Frédéric Caillet** - *Hébergement et maintenance de l'ancien proxy Russandol*
* **MyElectricalData** - *Passerelle API communautaire*
