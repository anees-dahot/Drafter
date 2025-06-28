# Gemini Project Instructions: Drafter

This document outlines the plan and instructions for building the "Drafter" Flutter application.

## Project Overview

Drafter is a Flutter application that allows users to generate draft articles using an AI service and save them to their mobile device for later use.

## Core Features

1.  **AI Article Generation:**
    *   Integrate with a generative AI API (e.g., Gemini) to create draft articles based on user prompts.
    *   Provide a user interface for inputting article topics or prompts.
    *   Display the generated article content.

2.  **Local Storage:**
    *   Implement a mechanism to save, view, edit, and delete drafted articles.
    *   Use a local storage solution like `shared_preferences` for simple key-value storage or `Hive` for a more structured NoSQL database approach. `Hive` is recommended for storing structured data like articles (e.g., title, content, date).

## Suggested Features

### MVP (Minimum Viable Product) Features:
*   **AI-Powered Drafting:** The core feature. Input a prompt, get a draft.
*   **Save, Edit, Delete Drafts:** Full CRUD (Create, Read, Update, Delete) functionality for the articles you save.
*   **Simple Local Storage:** Using `Hive` or `shared_preferences` to keep drafts on the device.
*   **Copy to Clipboard:** Easily copy the generated text to use in other applications.

### Advanced Features:
*   **Rich Text Editor:** Allow formatting of saved drafts (bold, italics, lists, headers).
*   **Categorization/Tags:** Organize drafts into folders or with tags for better management.
*   **Search Functionality:** Search saved drafts by title or content.
*   **Prompt History:** Save a history of prompts you've used for quick reuse.
*   **Customizable AI Settings:** Allow users to select different AI models, or adjust parameters like creativity/temperature.
*   **Export Options:** Export drafts to `.txt` or `.md` files.
*   **Cloud Sync:** Use a service like Firebase to sync drafts across multiple devices.
*   **Dark Mode:** A must-have for many users.

## Suggested Screens

1.  **Drafting Screen (Home Screen):**
    *   **Purpose:** The main screen for generating new articles.
    *   **Components:** A text field for the user's prompt, a "Generate" button, and an area to display the AI-generated result with "Save" and "Copy" buttons.

2.  **Saved Articles Screen:**
    *   **Purpose:** To browse and manage all saved drafts.
    *   **Components:** A list of all saved articles (showing title and maybe a date/snippet). Tapping an article would navigate to the `Article Detail Screen`. You could include a search bar here.

3.  **Article Detail/Editor Screen:**
    *   **Purpose:** To view and edit a saved draft.
    *   **Components:** Displays the full text of the article. An "Edit" button could transform the text view into a text field (or a rich text editor) to allow changes. A "Delete" button would also be here.

4.  **Settings Screen:**
    *   **Purpose:** For application settings and information.
    *   **Components:** Options for Dark Mode, managing AI settings (like API keys), and an "About" section.

## Suggested Project Structure

```
lib/
├───core/
│   ├───ai/
│   │   └───gemini_service.dart
│   └───storage/
│       └───hive_service.dart
├───features/
│   ├───drafting/
│   │   ├───bloc/
│   │   │   ├───draft_bloc.dart
│   │   │   ├───draft_event.dart
│   │   │   └───draft_state.dart
│   │   └───screens/
│   │   │   ├───draft_screen.dart    
│   │   └───widgets/
│   │       ├───draft_input_field.dart
│   │       └───generated_article_view.dart
│   └───saved_articles/
│       ├───bloc/
│       │   ├───saved_articles_bloc.dart
│       │   ├───saved_articles_event.dart
│       │   └───saved_articles_state.dart
│       └───screens/
│       │   ├───saved-articles_screen.dart   
│       └───widgets/
│           └───article_list_item.dart
├───models/
│   └───article.dart
└───main.dart
```

## Implementation Steps

1.  **Setup Dependencies:**
    *   Add the necessary packages to `pubspec.yaml`:
        *   `flutter_bloc` for state management.
        *   `dio` or `http` for making API calls to the AI service.
        *   `hive` and `hive_flutter` for local storage.
        *   `path_provider` to find the correct local path to store the Hive database.

2.  **AI Integration:**
    *   Create a service class (`GeminiService`) to handle communication with the AI API.
    *   Implement a BLoC (`DraftBloc`) to manage the state of the article generation process (e.g., loading, success, error).

3.  **Local Storage:**
    *   Create a service class (`HiveService`) to encapsulate all database operations (e.g., saving, retrieving, deleting articles).
    *   Define an `Article` model class with `HiveType` annotations.
    *   Initialize Hive in `main.dart`.

4.  **User Interface:**
    *   Create a home screen with a text input for the article prompt and a button to trigger generation.
    *   Display the generated article content.
    *   Add a "Save" button to store the article locally.
    *   Create a separate screen to list and view saved articles.
