# Food App — Use Cases

> This document describes the primary use cases for the foodapp platform. Each use case is described with actors, preconditions, main flow, and alternative flows.

---

## UC-01: Browse and Search Recipes

| Field         | Detail                                 |
|---------------|----------------------------------------|
| **Actor**     | Any user                               |
| **Goal**      | Find recipes that match criteria       |
| **Priority**  | High                                   |

**Preconditions**
- The application is running.
- At least one recipe exists in the data store (or an external API is reachable).

**Main Flow**
1. User opens the recipe search screen / command.
2. User enters a search term (ingredient, cuisine, dish name, or dietary tag).
3. System queries local data store and/or external API.
4. System returns a ranked list of matching recipes.
5. User selects a recipe to see full details (ingredients, steps, nutrition).

**Alternative Flows**
- *No results found:* System informs the user and suggests broadening the search.
- *External API unreachable:* System falls back to local data only and notifies the user.

---

## UC-02: Create a Personal Recipe

| Field         | Detail                                 |
|---------------|----------------------------------------|
| **Actor**     | Registered user                        |
| **Goal**      | Save a custom recipe for personal use  |
| **Priority**  | High                                   |

**Preconditions**
- User has an account (or local profile).

**Main Flow**
1. User selects "Create Recipe".
2. User enters recipe name, servings, preparation time, and cooking time.
3. User adds ingredients (name, quantity, unit).
4. User adds step-by-step instructions.
5. User optionally adds tags (cuisine, dietary labels, e.g. vegan, gluten-free).
6. System validates input and saves the recipe.
7. System confirms and displays the saved recipe.

**Alternative Flows**
- *Missing required fields:* System highlights errors and prompts correction.
- *Duplicate recipe name:* System warns and asks the user to rename or overwrite.

---

## UC-03: Plan Weekly Meals

| Field         | Detail                                         |
|---------------|------------------------------------------------|
| **Actor**     | Registered user                                |
| **Goal**      | Assign recipes to days of the week             |
| **Priority**  | High                                           |

**Preconditions**
- At least one recipe exists in the system.

**Main Flow**
1. User opens the Meal Planner for a target week.
2. User selects a day and meal slot (Breakfast / Lunch / Dinner / Snack).
3. User searches for or picks a recipe from the list.
4. System assigns the recipe to the slot and records the servings count.
5. User repeats for other days / meal slots.
6. User saves the weekly plan.

**Alternative Flows**
- *Recipe slots conflict with dietary restrictions on the profile:* System warns the user.
- *User clears a slot:* System removes the assignment and recalculates totals.

---

## UC-04: Generate Shopping List

| Field         | Detail                                         |
|---------------|------------------------------------------------|
| **Actor**     | Registered user                                |
| **Goal**      | Get a consolidated ingredient list for the week|
| **Priority**  | High                                           |

**Preconditions**
- A weekly meal plan exists (UC-03).

**Main Flow**
1. User requests a shopping list for the current or a selected week.
2. System aggregates ingredients across all planned meals.
3. System deduplicates and sums quantities for the same ingredient/unit.
4. System displays the consolidated shopping list, grouped by category (Produce, Dairy, Meat, etc.).
5. User optionally checks off items or exports the list.

**Alternative Flows**
- *No meal plan exists:* System prompts the user to create a plan first.
- *Export:* System outputs the list as plain text or CSV.

---

## UC-05: Track Daily Nutritional Intake

| Field         | Detail                                         |
|---------------|------------------------------------------------|
| **Actor**     | Registered user                                |
| **Goal**      | Log meals eaten and see nutritional summary    |
| **Priority**  | Medium                                         |

**Preconditions**
- Nutritional data is available for at least the consumed recipes.

**Main Flow**
1. User opens the Nutrition Log for the current day.
2. User adds a consumed meal (recipe + actual servings eaten).
3. System calculates calories, protein, carbohydrates, fat, and fibre for the entry.
4. System displays a running daily total and a comparison against the user's daily targets.
5. User can add, edit, or remove entries.

**Alternative Flows**
- *Nutritional data missing for an ingredient:* System flags the item and asks the user to enter it manually.
- *Daily target not set:* System displays raw totals only.

---

## UC-06: Share a Recipe

| Field         | Detail                                         |
|---------------|------------------------------------------------|
| **Actor**     | Registered user                                |
| **Goal**      | Make a personal recipe visible to the community|
| **Priority**  | Low                                            |

**Preconditions**
- User has at least one personal recipe.
- Community / sharing feature is enabled.

**Main Flow**
1. User navigates to their recipe and selects "Share".
2. System asks the user to confirm and choose a visibility level (Public / Friends).
3. System publishes the recipe under the user's profile.
4. Other users can discover, view, and save the shared recipe.

**Alternative Flows**
- *User unshares:* System reverts the recipe to private without deleting community saves.

---

## UC-07: Manage User Profile & Dietary Preferences

| Field         | Detail                                         |
|---------------|------------------------------------------------|
| **Actor**     | Registered user                                |
| **Goal**      | Configure personal dietary goals and restrictions |
| **Priority**  | Medium                                         |

**Main Flow**
1. User opens Profile Settings.
2. User sets daily calorie and macro targets.
3. User sets dietary restrictions (e.g., lactose-free, nut allergy, vegan).
4. System saves preferences and applies them as filters/warnings throughout the app.

---

*Document version: 1.0 — April 2026*

