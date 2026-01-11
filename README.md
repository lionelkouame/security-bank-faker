# 🏦 Security Bank Faker

> **Projet fil rouge pour une série d'article** Une implémentation de référence du composant **Symfony Security** pour une plateforme Fintech B2B fictive.

[![Symfony 8.0](https://img.shields.io/badge/Symfony-8.0-black.svg?logo=symfony)](https://symfony.com)
[![PHP 8.4](https://img.shields.io/badge/PHP-8.4-777bb4.svg?logo=php)](https://php.net)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🎯 Objectifs du Projet
Ce projet sert de fil rouge pour explorer 100% des capacités du **SecurityBundle** de Symfony
L'objectif est de simuler une banque en ligne exigeant des niveaux d'authentification variés et une gestion granulaire des permissions.

## Section : Les UserProviders
- [📚 Deep Dive : Les Cas d'Usage du "User Provider"](docs/spec.md)
- [providers..mermaid](docs/providers..mermaid)

## 🚀 Installation
```bash
composer install
docker-compose up -d
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
