# TP2 – GitHub Actions  
**Auteur : Alouani Youssef**   
**Encadrant : Pr. KOUISSI Mohamed**

---

## 🎯 Objectif du TP

Ce TP a pour objectif de mettre en place un pipeline d’intégration continue (CI) à l’aide de **GitHub Actions** pour automatiser :

- La compilation d’un projet Android.
- L’exécution des tests unitaires.
- L’automatisation du workflow de développement.
- L’analyse des résultats via l’onglet *Actions* sur GitHub.

Ce travail permet de comprendre les fondements du CI/CD et l’importance de l’automatisation dans les projets logiciels modernes.

---

## 📁 Structure du dépôt

TP2-AlouaniYoussef/
│── app/ → Projet Android (code source)
│── .github/workflows/ → Workflows GitHub Actions
│ └── android-ci.yml → Pipeline CI
│── images/ → Captures d’écran du TP
│── README.md → Documentation principale
│── REPORT.md → Rapport détaillé du TP

yaml
Copy code

---

## ⚙️ Mise en place du Pipeline GitHub Actions

Le fichier `android-ci.yml` permet :

1. Le checkout du code depuis GitHub.
2. L’installation du **JDK 17** (requis par Android Gradle Plugin 8.8.2).
3. L’autorisation d’exécution pour `gradlew`.
4. La compilation du projet via :

   ```bash
   ./gradlew assembleDebug
L’exécution des tests unitaires :

bash
Copy code
./gradlew test
L’affichage des logs et résultats dans GitHub Actions.

🛠️ Code complet du Workflow (android-ci.yml)
yaml
Copy code
name: Android CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Grant execute permission for gradlew
        run: chmod +x ./gradlew

      - name: Build debug APK
        run: ./gradlew assembleDebug --no-daemon

      - name: Run unit tests
        run: ./gradlew test --no-daemon
📸 Captures d’écran du TP

<img width="1087" height="676" alt="1" src="https://github.com/user-attachments/assets/f929d92b-f2a0-4f99-931c-d9ecc15c73ce" /> <img width="983" height="350" alt="1-2" src="https://github.com/user-attachments/assets/14e9508d-12af-4e62-b12b-1148069d9824" />

<img width="902" height="641" alt="2" src="https://github.com/user-attachments/assets/cfe7cf8f-a637-414d-8643-9d9e2db1d3da" />

<img width="1151" height="587" alt="3" src="https://github.com/user-attachments/assets/7ab4ea04-8bac-4e6b-b51e-90669b7b24bf" /> <img width="929" height="637" alt="3-1" src="https://github.com/user-attachments/assets/230f1bb4-aa70-40a1-9782-18e52119b5bb" />

<img width="427" height="700" alt="4" src="https://github.com/user-attachments/assets/1e1b9b54-5cdd-4530-94fc-614c34a74daa" />

<img width="1034" height="789" alt="5" src="https://github.com/user-attachments/assets/7eb68a14-4118-4517-8821-321fde606287" /> <img width="1088" height="677" alt="5-1" src="https://github.com/user-attachments/assets/3045ac14-eb16-45ed-9a98-17cec3ed07ac" />
6. Résultats des Jobs GitHub Actions
<img width="1556" height="559" alt="6" src="https://github.com/user-attachments/assets/56477fa2-d39b-472e-bac1-9007baac9258" />
7. Validation finale
<img width="1150" height="703" alt="7" src="https://github.com/user-attachments/assets/17a52641-f636-4d16-8917-9b0916a6cec9" />
