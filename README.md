# 🔐 Spring Security — TP Authentification & Autorisation par Rôles


## 🎯 Aperçu

Ce TP illustre les concepts fondamentaux de **Spring Security** à travers une application web simple qui :

- Protège des routes selon les rôles des utilisateurs
- Affiche une page de connexion personnalisée
- Redirige l'utilisateur vers son espace selon ses rôles après authentification
- Gère la déconnexion de façon sécurisée

---

## ✨ Fonctionnalités

| Fonctionnalité | Description |
|---|---|
| 🔑 **Authentification** | Page de login personnalisée avec nom d'utilisateur et mot de passe |
| 👤 **Espace Utilisateur** | Accessible aux rôles `USER` et `ADMIN` |
| 🛡️ **Espace Administrateur** | Accessible uniquement au rôle `ADMIN` |
| 🔀 **Redirection intelligente** | Après login, affichage des espaces disponibles selon le(s) rôle(s) |
| 🚪 **Déconnexion** | Session invalidée proprement via Spring Security |

---

## 📸 Captures d'écran

### 1. Page d'authentification

> Page de connexion personnalisée — saisie du nom d'utilisateur (`admin` ou `user`) et du mot de passe.

<img width="826" height="726" alt="authentification " src="https://github.com/user-attachments/assets/a39db47c-fab3-4d20-ab54-d26ae4391063" />


---

### 2. Page d'accueil après connexion

> Après une authentification réussie, l'utilisateur voit les espaces auxquels il a accès selon ses rôles.

<img width="722" height="752" alt="admin " src="https://github.com/user-attachments/assets/eb276601-f38d-4561-83f7-2c1f291a5f08" />


---

### 3. Espace Utilisateur

> Zone accessible aux rôles `USER` et `ADMIN` — affiche un badge **STANDARD ACCESS**.

<img width="715" height="637" alt="user " src="https://github.com/user-attachments/assets/fb743b72-923e-44f6-a01e-a7b35a6edb5b" />


---

## 🏗️ Architecture

```
Requête HTTP
     │
     ▼
┌─────────────────────┐
│   Security Filter   │  ◄── Vérifie l'authentification
│       Chain         │
└────────┬────────────┘
         │
    Authentifié ?
    ┌────┴────┐
   Non       Oui
    │         │
    ▼         ▼
 /login    Vérification
           des rôles
              │
    ┌─────────┴──────────┐
    ▼                    ▼
 ROLE_USER           ROLE_ADMIN
    │                    │
    ▼                    ▼
/user/home          /admin/home
                   + /user/home
```


## 📁 Structure du projet

```
src/
├── main/
│   ├── java/
│   │   └── com/example/security/
│   │       ├── config/
│   │       │   └── SecurityConfig.java       # Configuration Spring Security
│   │       ├── controller/
│   │       │   ├── HomeController.java        # Page d'accueil post-login
│   │       │   ├── UserController.java        # Espace utilisateur
│   │       │   └── AdminController.java       # Espace administrateur
│   │       └── SpringSecurityApplication.java
│   └── resources/
│       ├── templates/
│       │   ├── login.html                     # Page de connexion
│       │   ├── home.html                      # Redirection rôles
│       │   ├── user/home.html                 # Espace utilisateur
│       │   └── admin/home.html                # Espace administrateur
│       └── application.properties
└── test/
```

---

## 🛠️ Technologies utilisées

| Technologie | Rôle |
|---|---|
| **Spring Boot** | Framework principal |
| **Spring Security** | Authentification & Autorisation |
| **Thymeleaf** | Moteur de templates HTML |
| **Spring MVC** | Contrôleurs web |
| **Maven** | Gestion des dépendances |

