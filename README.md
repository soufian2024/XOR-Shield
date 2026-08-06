# XOR-Shield 🔐✨

### 🔍 Quick View with Arabic
أداة ويب محلية وخفيفة الوزن مصممة لتشفير وفك تشفير الملفات (مثل الصور ومقاطع الفيديو) مباشرة داخل المتصفح دون الحاجة لخادم خارجي. يعتمد المشروع على خوارزمية XOR التناظرية، حيث يتم معالجة الملفات على شكل مصفوفات بايتات وعمل قناع رقمي باستخدام مفتاح سري يدخله المستخدم. يتميز المشروع بدعم المعاينة الفورية للملف الأصلي والملف المشفر، مع شريط تقدم مرئي لمعالجة الملفات الكبيرة على أجزاء دون تجميد المتصفح.

---

<br>

<!-- Badges conçus avec du code SVG natif intégré pour éviter les images cassées -->
<div align="left">
  <!-- Badge HTML5 -->
  <span style="display: inline-block; background: #E34F26; color: white; border-radius: 4px; padding: 4px 8px; font-family: sans-serif; font-size: 11px; font-weight: bold; margin-right: 5px;">
    <svg width="12" height="12" viewBox="0 0 24 24" fill="#FFFFFF" style="vertical-align: middle; margin-right: 4px;"><path d="M1.5 0h21l-1.9 21.15L12 24l-8.6-2.85L1.5 0zm17 5H6.4l.35 4h11.4l-.4 4.5-4.75 1.6-4.75-1.6-.3-3.2H4.8l.5 5.6 6.7 2.2 6.7-2.2L19.5 5z"/></svg>HTML5
  </span>
  <!-- Badge JavaScript -->
  <span style="display: inline-block; background: #F7DF1E; color: #000000; border-radius: 4px; padding: 4px 8px; font-family: sans-serif; font-size: 11px; font-weight: bold; margin-right: 5px;">
    <svg width="12" height="12" viewBox="0 0 24 24" fill="#000000" style="vertical-align: middle; margin-right: 4px;"><path d="M0 0h24v24H0z" fill="#F7DF1E"/><path d="M11.64 17.65c0 1.64-.98 2.54-2.6 2.54-1.34 0-2.22-.65-2.58-1.57h1.72c.22.48.6.76 1.04.76.54 0 .9-.28.9-.96v-6.3h1.52v6.53zm5.42 1.4c.54 0 1-.22 1.25-.66h.04l.08.54h1.34v-5.2c0-1.78-1.12-2.54-2.86-2.54-1.5 0-2.54.67-2.92 1.7h1.54c.26-.52.7-.82 1.3-.82.84 0 1.34.42 1.34 1.4v.68c-.46-.26-1.1-.44-1.84-.44-1.7 0-2.73.88-2.73 2.26 0 1.33.92 2.08 2.25 2.08zm.36-1.18c-.64 0-1.1-.28-1.1-.86 0-.6.5-.9 1.2-.9.56 0 1.04.14 1.34.34v.58c0 .5-.47.84-1.4.84z"/></svg>JavaScript
  </span>
  <!-- Badge Crypto / Cipher -->
  <span style="display: inline-block; background: #24292e; color: white; border-radius: 4px; padding: 4px 8px; font-family: sans-serif; font-size: 11px; font-weight: bold;">
    <svg width="12" height="12" viewBox="0 0 24 24" fill="#28a745" style="vertical-align: middle; margin-right: 4px;"><path d="M12 1L3 5v6c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V5l-9-4zm0 6c1.66 0 3 1.34 3 3v2h1v5H8v-5h1v-2c0-1.66 1.34-3 3-3zm-1.5 5h3v-2c0-.83-.67-1.5-1.5-1.5s-1.5.67-1.5 1.5v2z"/></svg>XOR Cipher
  </span>
</div>

---

## 📝 Description du Projet

**XOR-Shield** est une application web monopage (SPA) minimaliste et ultra-rapide permettant de chiffrer et déchiffrer des fichiers multimédias directement depuis votre navigateur. 

Le chiffrement par **OU exclusif (XOR)** étant un algorithme symétrique, le même mot de passe saisie applique le masque binaire pour verrouiller le fichier, et effectue l'opération inverse pour le restaurer. L'application traite l'intégralité des données côté client (`Client-Side`) sous forme de tableaux d'octets (`Uint8Array`), garantissant une confidentialité totale puisqu'aucun élément n'est envoyé vers un serveur externe.

---

## 🛡️ Fonctionnalités Principales & Points Forts

- **Chiffrement Symétrique Instantané :** Traitement binaire rapide via l'opérateur bit à bit `^` (XOR) appliqué sur chaque octet du fichier.
- **Gestion Asynchrone par Blocs (Chunking) :** Découpage intelligent des gros fichiers en morceaux de `1 Mo` traités via `setTimeout`. Cette approche évite de saturer ou de figer l'interface graphique (UI Thread) du navigateur pendant l'exécution.
- **Barre de Progression Dynamique :** Suivi visuel fluide du pourcentage d'avancement de la tâche en temps réel.
- **Prévisualisation Média Intégrée :** Utilisation des objets `Blob` de JavaScript pour générer des flux temporaires permettant de comparer l'aperçu du fichier original et du fichier chiffré (compatible images et vidéos).
- **Téléchargement Automatique Sécurisé :** Génération instantanée d'un lien de téléchargement automatique pour récupérer le fichier modifié, préfixé par `output_`.

---

## ⚠️ Limitations Techniques & Cryptographiques

> **Note de sécurité :** Ce projet possède une portée principalement éducative et démonstrative. **Il ne doit pas être utilisé pour sécuriser des données d'infrastructure critiques.**

1. **Vulnérabilité aux attaques par analyse de fréquence :** Si la clé choisie est plus courte que le fichier traité, elle se répète de manière cyclique (`i % keyBytes.length`). Un attaquant expérimenté peut casser ce chiffrement en étudiant les répétitions statistiques du fichier de sortie.
2. **Consommation de la mémoire vive (RAM) :** La méthode `FileReader.readAsArrayBuffer()` charge l'intégralité du document en mémoire vive. Le traitement simultané de fichiers de plusieurs gigaoctets peut provoquer un crash de l'onglet du navigateur.

---

## 🎮 Comment l'utiliser

1. Enregistrez le code source fourni dans un fichier nommé `index.html`.
2. Ouvrez ce fichier avec n'importe quel navigateur moderne (Chrome, Firefox, Brave, Edge).
3. Cliquez sur **"Choisir un fichier"** pour importer une image ou une vidéo.
4. Saisissez votre mot de passe secret dans le champ **"Enter key"**.
5. Cliquez sur **Encrypt/Decrypt** :
   - La barre de progression s'active, l'aperçu dynamique se charge, puis le téléchargement du fichier protégé démarre automatiquement.
   - **Pour restaurer le fichier :** Importez simplement le fichier généré (`output_...`) dans l'application et soumettez-le à nouveau avec **exactement le même mot de passe**.
