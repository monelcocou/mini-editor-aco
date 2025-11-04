# 📝 MINI-EDITOR

Un éditeur de texte minimaliste développé en Java, mettant en œuvre les patterns de conception **Command** et **Memento** pour offrir des fonctionnalités d'édition avancées avec support d'annulation/rétablissement (Undo/Redo).

---

## 📋 À propos

**MINI-EDITOR** est un projet académique réalisé dans le cadre du cours **ACO (Analyse et Conception à Objets)** en Master 1 à l'ISTIC (Université de Rennes 1).

L'objectif est de concevoir et implémenter un éditeur de texte en suivant une approche incrémentale, en appliquant des principes de conception orientée objet et des design patterns reconnus.

---

## 🎯 Objectifs pédagogiques

- 🏗️ **Conception orientée objet** : Maîtriser la séparation des responsabilités et l'encapsulation
- 🎨 **Design Patterns** : Implémenter les patterns **Command** et **Memento**
- 🔄 **Développement itératif** : Suivre une approche en spirale avec versions successives
- 🧪 **Tests unitaires** : Assurer la qualité du code avec JUnit 5
- 📐 **Architecture logicielle** : Découpler l'interface utilisateur de la logique métier

---

## 🏗️ Architecture

Le projet suit une architecture en couches avec séparation claire des responsabilités :

```
┌─────────────────────────────┐
│   Interface Utilisateur     │ (Console/GUI)
│        (Invoker)            │
└──────────┬──────────────────┘
           │
           ↓
┌─────────────────────────────┐
│    Commandes (Command)      │ Cut, Copy, Paste, Insert, Delete
│   Pattern Command           │
└──────────┬──────────────────┘
           │
           ↓
┌─────────────────────────────┐
│   Engine (Receiver)         │ Logique métier d'édition
│   - buffer                  │
│   - clipboard               │
│   - selection               │
└─────────────────────────────┘
```

### Composants principaux

- **Engine** : Interface principale du moteur d'édition
- **EngineImpl** : Implémentation concrète gérant le buffer, le clipboard et la sélection
- **Selection** : Interface pour la gestion de la sélection de texte
- **SelectionImpl** : Implémentation concrète de la sélection
- **Command** : Pattern Command pour encapsuler les actions d'édition
- **Memento** : Pattern Memento pour sauvegarder/restaurer l'état

---

## 🌿 Organisation des branches Git

Le projet utilise une stratégie de branches pour séparer clairement les différentes versions :

```
main
 ├── v0  → Structure de base (squelette fourni)
 ├── v1  → Fonctionnalités de base
 ├── v2  → Enregistrement et rejeu
 └── v3  → Undo/Redo illimité
```

### Navigation entre les branches

```bash
# Voir toutes les branches
git branch -a

# Basculer vers une version spécifique
git checkout v1  # Pour la version 1
git checkout v2  # Pour la version 2
git checkout v3  # Pour la version 3
```

---

## 🚀 Versions

### 📦 V0 - Structure de base
**Branche :** `v0`

- Squelette fourni avec interfaces `Engine` et `Selection`
- Classes d'implémentation vides (`EngineImpl`, `SelectionImpl`)
- Tests unitaires de base

### ✏️ V1 - Fonctionnalités de base
**Branche :** `v1`

**Fonctionnalités :**
- ✅ Édition de texte (buffer)
- ✅ Gestion de la sélection
- ✅ Opérations : Cut, Copy, Paste, Insert, Delete
- ✅ Presse-papier (clipboard)

**Pattern utilisé :** Command (structure de base)

### 🎬 V2 - Enregistrement et rejeu
**Branche :** `v2`

**Nouvelles fonctionnalités :**
- 📼 Enregistrement des actions utilisateur
- ▶️ Rejeu des séquences d'actions (macros)

**Patterns utilisés :** 
- Command (pour encapsuler les actions)
- Memento (pour sauvegarder les paramètres des commandes)

### ⏮️ V3 - Undo/Redo illimité
**Branche :** `v3`

**Nouvelles fonctionnalités :**
- ⏪ Annulation illimitée (Undo)
- ⏩ Rétablissement illimité (Redo)
- 📚 Historique complet des modifications

**Patterns utilisés :** 
- Command (avec méthode `undo()`)
- Memento (pour sauvegarder l'état de l'éditeur)
- Caretaker (UndoManager)

---

## 🛠️ Technologies

- **Langage** : Java 8+
- **Tests** : JUnit 5
- **Build** : Maven / Gradle
- **VCS** : Git / GitHub

---

## 📦 Installation et exécution

### Prérequis

- Java JDK 8 ou supérieur
- Maven ou Gradle (selon la configuration du projet)
- Git

### Cloner le projet

```bash
git clone https://github.com/monelcocou/mini-editor-aco.git
cd mini-editor-aco
```

### Basculer vers une version

```bash
# Par exemple, pour la V1
git checkout v1
```

### Compiler et exécuter

```bash
# Avec Maven
mvn clean compile
mvn test

# Avec Gradle
./gradlew build
./gradlew test
```

---

## 🧪 Tests

Le projet inclut des tests unitaires pour chaque version.

```bash
# Exécuter tous les tests
mvn test

# Exécuter un test spécifique
mvn test -Dtest=EngineTest
```

Les tests couvrent :
- ✅ Opérations de base (cut, copy, paste, insert, delete)
- ✅ Gestion de la sélection
- ✅ Enregistrement et rejeu (V2)
- ✅ Undo/Redo (V3)

---

## 📚 Patterns de conception utilisés

### 🎯 Pattern Command

**Problème résolu :** Découpler l'invocation d'une action de son exécution.

**Bénéfices :**
- Encapsulation des requêtes dans des objets
- Support d'annulation (undo)
- Enregistrement et rejeu d'actions
- File d'attente de commandes

**Application dans le projet :**
- `CutCommand`, `CopyCommand`, `PasteCommand`, `InsertCommand`, `DeleteCommand`
- `Recorder` pour enregistrer les actions
- `UndoManager` pour gérer l'historique

### 💾 Pattern Memento

**Problème résolu :** Sauvegarder et restaurer l'état d'un objet sans violer son encapsulation.

**Bénéfices :**
- Sauvegarde de l'état interne
- Restauration à un état précédent
- Encapsulation préservée

**Application dans le projet :**
- `EngineMemento` pour sauvegarder l'état de l'éditeur
- `InsertMemento` pour sauvegarder les paramètres des commandes
- Support d'Undo/Redo

---

## 📖 Documentation

### Structure du code

```
src/
├── main/
│   └── java/
│       └── fr/istic/aco/editor/
│           ├── Engine.java
│           ├── EngineImpl.java
│           ├── Selection.java
│           ├── SelectionImpl.java
│           └── commands/
│               ├── Command.java
│               ├── CutCommand.java
│               ├── CopyCommand.java
│               └── ...
└── test/
    └── java/
        └── fr/istic/aco/editor/
            └── EngineTest.java
```

### Diagrammes UML

Les diagrammes de classes et de séquence sont disponibles dans le dossier `/docs` pour chaque version.

---

## 🎓 Contexte académique

**Cours :** ACO - Analyse et Conception à Objets  
**Formation :** Master 1 Informatique  
**Établissement :** ISTIC - Université de Rennes 1  
**Année :** 2024-2025

### Objectifs du cours

Ce projet illustre les concepts suivants :
- Principes SOLID
- Design Patterns (GoF)
- Architecture en couches
- Tests unitaires
- Développement itératif

---

## 👤 Auteur

**Monel Cocou GAFFAN**

Master 1 ACO - ISTIC, Université de Rennes 1

---

## 📄 Licence

Ce projet est développé dans un cadre académique.

---

## 🙏 Remerciements

- Professeurs du cours ACO de l'ISTIC
- Auteurs des patterns de conception (Gang of Four)
- Communauté Java et JUnit

---

## 📞 Contact

Pour toute question concernant ce projet académique, n'hésitez pas à ouvrir une issue sur GitHub.

---

*Projet réalisé avec ❤️ dans le cadre du Master ACO à l'ISTIC*
