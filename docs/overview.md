# Food App — Project Overview

## Summary

**foodapp** is a .NET console application (targeting net10.0) that will evolve into a full-featured food management platform. The application aims to help users discover, plan, and track their meals while managing recipes, ingredients, and nutritional information in one place.

---

## Goals

- Provide an easy way to **browse and search recipes** by ingredient, cuisine, or dietary preference.
- Allow users to **plan weekly meals** and auto-generate shopping lists.
- Track **nutritional intake** (calories, macronutrients) over time.
- Support **personal recipe creation** and sharing within a community.

---

## Target Users

| Persona          | Description                                                       |
|------------------|-------------------------------------------------------------------|
| Home Cook        | Wants simple recipe discovery and shopping list generation.       |
| Diet-Conscious   | Tracks daily nutritional goals and macronutrient breakdowns.      |
| Meal Planner     | Plans an entire week's meals in advance for the household.        |
| Food Enthusiast  | Creates, saves, and shares their own recipes with others.         |

---

## High-Level Architecture (Planned)

```
foodapp/
├── Core/                 # Domain models, business logic
│   ├── Recipes/
│   ├── MealPlanner/
│   └── Nutrition/
├── Infrastructure/       # Data persistence, external API integrations
│   ├── Database/
│   └── ExternalApis/     # e.g., Spoonacular, Open Food Facts
├── Presentation/         # CLI / future API layer
└── Tests/                # Unit and integration tests
```

---

## Technology Stack

| Layer          | Technology                         |
|----------------|-------------------------------------|
| Language       | C# 13 / .NET 10                     |
| Data Store     | TBD (SQLite for local, PostgreSQL for hosted) |
| External APIs  | TBD (Open Food Facts, Spoonacular)  |
| Testing        | xUnit + FluentAssertions            |
| CI/CD          | GitHub Actions                      |

---

## Milestones

| # | Milestone                       | Status     |
|---|---------------------------------|------------|
| 1 | Project scaffolding & repo setup | ✅ Done    |
| 2 | Core domain models               | 🔲 Planned |
| 3 | Recipe CRUD (CLI)                | 🔲 Planned |
| 4 | Meal planner feature             | 🔲 Planned |
| 5 | Nutrition tracking               | 🔲 Planned |
| 6 | Community / sharing              | 🔲 Planned |

---

## Repository

- **GitHub:** https://github.com/mjakara87/foodapp
- **Branch strategy:** `main` (stable) → feature branches → PR

