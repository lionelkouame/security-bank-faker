# 🏦 Security Bank Faker

> **Architecting the Unbreakable.** Une implémentation de référence du composant **Symfony Security** pour une plateforme Fintech B2B fictive.

[![Symfony 8.0](https://img.shields.io/badge/Symfony-8.0-black.svg?logo=symfony)](https://symfony.com)
[![PHP 8.4](https://img.shields.io/badge/PHP-8.4-777bb4.svg?logo=php)](https://php.net)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🎯 Objectifs du Projet
[cite_start]Ce projet sert de fil rouge pour explorer 100% des capacités du **SecurityBundle** de Symfony[cite: 6].
L'objectif est de simuler une banque en ligne exigeant des niveaux d'authentification variés et une gestion granulaire des permissions.

## 🛡️ Fonctionnalités de Sécurité Implémentées
- [ ] **User Management** :
- [ ] **Robust Hashing** : Utilisation de l'algorithme `auto` (Argon2id/Bcrypt).
- [ ] **Firewalls complexes** : Gestion de sessions et de tokens API.
- [ ] **Brute-force Protection** : Login Throttling intégré.
- [ ] **Voters Avancés** : Logique métier pour les virements bancaires.

## 🚀 Installation
```bash
composer install
docker-compose up -d
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
