# Entity Relationship Diagram

Reference the Creating an Entity Relationship Diagram final project guide in the course portal for more information about how to complete this deliverable.

## Create the List of Tables

Our database consists of 4 main entity tables and 1 junction table designed to support full CRUD operations, onboarding data persistence, and application logic:
*   **`users`:** Stores unique user profiles and the 5-step onboarding configuration attributes.
*   **`workout_logs`:** Tracks individual, historical user workout sessions to feed the Workout History UI.
*   **`accountability_groups`:** Tracks the metadata for distinct, user-created physical accountability circles.
*   **`group_members`:** The many-to-many junction table bridging users and their respective accountability groups.
*   **`exercises`:** A standalone global directory used as a master reference library for workouts.

## Add the Entity Relationship Diagram

![Momentum Entity Relationship Diagram](../images/momentum_erd.png)

### Table Structures

#### 1. users
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `user_id` | integer | primary key |
| `username` | text | unique display name of the user |
| `email` | text | unique email address used for identification |
| `fitness_goal` | text | primary objective from onboarding (e.g., 'Build Muscle') |
| `experience_level` | text | training background from onboarding (e.g., 'Intermediate') |
| `preferred_location` | text | choice of training facility environment (e.g., 'At the Gym') |
| `equipment_available`| text | comma-separated list or array of user fitness gear |
| `weekly_commitment` | integer | number of days per week the user commits to train |

#### 2. workout_logs
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `log_id` | integer | primary key |
| `user_id` | integer | foreign key pointing to users.user_id |
| `workout_name` | text | name of the logged session (e.g., 'Upper Body Strength') |
| `logged_date` | date | the calendar date the training session took place |
| `duration_minutes` | integer | total length of the session in minutes |
| `status` | text | categorical tracking status ('Completed' or 'Skipped') |

#### 3. accountability_groups
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `group_id` | integer | primary key |
| `group_name` | text | unique title of the accountability group circle |
| `description` | text | short bio explaining the purpose or target of the group |
| `created_by_user_id`| integer | foreign key pointing to users.user_id (group owner) |
| `current_streak` | integer | cumulative daily consecutive tracking streak metric |

#### 4. group_members (Many-to-Many Junction Table)
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `group_id` | integer | foreign key pointing to accountability_groups.group_id |
| `user_id` | integer | foreign key pointing to users.user_id |
| `joined_at` | timestamp | timestamp when the user joined the accountability squad |
| `is_admin` | boolean | flag identifying if the user has administrative privileges |
| `daily_status` | text | explicit daily checking status identifier ('Done' or 'Pending') |

#### 5. exercises (Standalone Table)
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `exercise_id` | integer | primary key |
| `exercise_name` | text | name of the physical exercise (e.g., 'Squat') |
| `target_muscle` | text | core anatomical muscle targeted by the movement |
| `equipment_needed` | text | primary mechanical equipment required to execute the lift |
