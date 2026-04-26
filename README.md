# 📱 Rapport d'analyse statique – UnCrackable-Level1.apk

---

## 🧾 Informations générales

- **Date d'analyse :** 26 avril 2026  
- **Analyste :** Mounir Merghich  
- **APK analysé :** UnCrackable-Level1.apk  
- **Version :** 1.0 (estimée)  
- **Provenance :** OWASP MSTG Crackme  
- **Outils utilisés :** JADX GUI, dex2jar, JD-GUI  

---

## 📌 Résumé exécutif

Cette analyse statique a révélé **5 vulnérabilités potentielles** dans l'application.

Les principales préoccupations concernent :
- 🔴 Secrets codés en dur dans le code
- 🔴 Vérification de sécurité côté client
- 🟠 Mécanismes anti-debug faibles

**Niveau de risque global : 🔴 Élevé**

### ✅ Actions prioritaires

1. Supprimer les secrets du code source  
2. Implémenter une validation côté serveur  
3. Renforcer les protections anti-tampering  

---

## 🔍 Analyse de l'APK

### 📂 Structure interne

- `AndroidManifest.xml`
- `classes.dex`
- `resources/`
- `res/values/strings.xml`

📸 **Screenshot – Structure APK :**  
<img width="519" height="1173" alt="Screenshot 2026-04-26 194228" src="https://github.com/user-attachments/assets/7347eae5-ca89-488d-bae0-e673e771d913" />


---

### 📜 Analyse du AndroidManifest.xml

- Package : `sg.vantagepoint.uncrackable1`
- Version : 1.0
- Permissions : (aucune critique)

🔎 Points importants :
- Pas de configuration critique visible
- Pas de `debuggable=true`

📸 **Screenshot – AndroidManifest :**  

| Image 1 | Image 2 | Image 3 | Image 4 |
|--------|--------|--------|--------|
| <img width="1982" height="1237" alt="Screenshot 2026-04-26 193918" src="https://github.com/user-attachments/assets/380f1b18-102c-4a15-b9aa-8739d8021ec4" /> | <img width="2185" height="986" alt="Screenshot 2026-04-26 194547" src="https://github.com/user-attachments/assets/82e64ac4-c2ce-426a-b2f8-48daf990c473" /> | <img width="2191" height="986" alt="Screenshot 2026-04-26 194619" src="https://github.com/user-attachments/assets/6fd043db-bd65-4b20-b3c1-6b44b327f0fc" /> | <img width="2186" height="976" alt="Screenshot 2026-04-26 194647" src="https://github.com/user-attachments/assets/4e7c1e90-7f09-4855-9919-ac709a8122d9" /> |

---

## 🔎 Recherche de chaînes sensibles

| Valeur trouvée | Emplacement | Sévérité | Description |
|----------------|------------|----------|------------|
| This is the correct secret | MainActivity | 🔴 Élevée | Secret exposé en clair |
| AES/ECB/PKCS7Padding | sg.vantagepoint.a.a | 🟠 Moyenne | Utilisation d’un chiffrement faible |
| Debug checks | Classes internes | 🟠 Moyenne | Détection debug contournable |

📸 **Screenshot – Recherche dans JADX :**  


---

## ⚠️ Constats détaillés

---

### 🔴 Constat #1 : Secret codé en dur

- **Sévérité :** Élevée  

**Description :**  
Le secret est directement présent dans le code.

**Localisation :**  
`MainActivity`

**Impact :**  
Bypass total de la sécurité.

**Remédiation :**  
- Ne pas stocker de secrets en clair  
- Utiliser Keystore Android  
- Déporter la logique côté serveur  

📸 **Screenshot :**  
<img width="2186" height="976" alt="Screenshot 2026-04-26 194647" src="https://github.com/user-attachments/assets/42b8afe7-b3e2-4e16-85cc-3f877b3c07de" />


---

### 🔴 Constat #2 : Validation côté client

- **Sévérité :** Élevée  

**Description :**  
La vérification est faite localement.

**Impact :**  
Facilement contournable via reverse engineering.

**Remédiation :**  
- Validation côté serveur  
- Authentification sécurisée  

📸 **Screenshot :**  
<img width="2191" height="986" alt="Screenshot 2026-04-26 194619" src="https://github.com/user-attachments/assets/ac0177b4-3160-4103-ab3f-e54adf66624c" />


---

### 🟠 Constat #3 : Protection anti-debug faible

- **Sévérité :** Moyenne  

**Description :**  
Détection root/debug présente mais faible.

**Impact :**  
Bypass possible par un attaquant.

**Remédiation :**  
- Obfuscation avancée  
- Anti-tampering  


---

### 🟠 Constat #4 : Données sensibles dans les ressources

- **Sévérité :** Moyenne  

**Description :**  
Informations visibles dans `strings.xml`.

**Impact :**  
Fuite d’informations.

**Remédiation :**  
- Ne pas stocker de données sensibles  
- Chiffrement si nécessaire  

📸 **Screenshot :**  
<img width="2189" height="983" alt="Screenshot 2026-04-26 194508" src="https://github.com/user-attachments/assets/e6ac2a43-5eae-4633-a784-cd987645bfe1" />


---

### 🟠 Constat #5 : Absence d’obfuscation

- **Sévérité :** Moyenne  

**Description :**  
Code lisible après décompilation.

**Impact :**  
Reverse engineering facilité.

**Remédiation :**  
- Utiliser ProGuard / R8  


---

## 🔄 Comparaison JADX vs JD-GUI

| Critère | JADX | JD-GUI |
|--------|------|--------|
| Structure Android | ✔️ | ❌ |
| Lisibilité | ✔️✔️ | ✔️ |
| Ressources XML | ✔️ | ❌ |
| Kotlin | ✔️ | ❌ |


---

## 📎 Annexes

### Permissions
- INTERNET (si présent)

### Composants exportés
- Aucun composant critique identifié

---

## 🧹 Nettoyage

- Données sensibles supprimées  
- Analyse conforme au cadre pédagogique  

---

## ✅ Deliverables

- ✔ Rapport complet  
- ✔ Vulnérabilités identifiées  
- ✔ Remédiations proposées  
- ✔ Screenshots à ajouter  

---

## 🧠 Conclusion

L’application est volontairement vulnérable et illustre :

- Mauvaise gestion des secrets  
- Mauvaise architecture de sécurité  
- Faible résistance au reverse engineering  

---
