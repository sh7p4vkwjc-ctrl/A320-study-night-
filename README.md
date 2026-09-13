# Athena A320/321 & ATPL Study App ✈️

A personal aviation revision app with a cockpit-at-night theme, tappable flashcards, interactive quizzes, and emoji-based confidence tracking. The app lives in one file: `index.html`.

This README describes the version updated on 13 September 2026: **1,184 flashcards, 1,184 quiz questions, and 20 populated topic sets**. Normal Procedure is a visible placeholder, not an additional question set.

## Getting started

1. Download `index.html` and open it in a browser that runs local HTML and JavaScript. A file preview may not run the interactive controls.
2. Choose **Flashcards** or **Quiz** on the home screen.
3. Select a topic from the compact menu. Both modes use the same labels and order.
4. Tap **VietJet OM** to reveal its two sections: **OM-A Chapter 8** and **OM-A Remaining Chapters**.

No installation, build step, or account is required for local study. Use the same browser and file location or website address to retain access to your saved progress.

## Topics and coverage

### A320 · Type Rating — 718 questions

The main menu follows the order of the supplied CAE Pelesys Athena course screenshot.

| Menu item | Questions |
| --- | ---: |
| Normal Procedure | Not added |
| Abnormal Procedure | 24 |
| Aircraft Systems – ATA 20 to 27 | 76 |
| Aircraft Systems – ATA 28 to 70 | 133 |
| Ops Specs – Performance – Limitation | 29 |
| Special Operations | 44 |
| Adverse Weather | 173 |
| VietJet OM | 239 |

VietJet OM contains **137 Chapter 8 questions** and **102 Remaining Chapters questions**, imported from the two separately supplied VietJet OM-A PDFs. The parent button shows their combined count; questions and progress remain separate within each section. These sections are not substitutes for Normal Procedure.

### ATPL · Aircraft & Principles — 129 questions

| Topic | Questions |
| --- | ---: |
| Aircraft General Knowledge | 39 |
| Principles of Flight | 19 |
| Powerplant | 28 |
| Electrical | 21 |
| Instrumentation | 22 |

### ATPL · Flight Operations — 337 questions

| Topic | Questions |
| --- | ---: |
| Air Law | 122 |
| Operational Procedures | 7 |
| Communication | 21 |
| Meteorology | 96 |
| Mass and Balance | 10 |
| ATPL Performance | 32 |
| Human Performance | 49 |

Counts represent imported questions, not complete coverage of every subject. Source question numbers are retained and may contain gaps.

## Flashcards

Tap a card to reveal or hide its answer. Tap an emoji to record your confidence without flipping the card:

| Emoji | Rating | Meaning |
| --- | --- | --- |
| 😵 | Again | Needs more revision |
| 🤔 | Almost | Partly remembered |
| 😎 | Got it | Confidently remembered |

Each question has one confidence rating. Choosing another emoji replaces it; tapping the selected emoji again clears it.

The flashcard toolbar provides:

- **Flashcards:** study the selected topic.
- **Info Summary ✨:** read the selected topic's question-and-answer revision notes.
- **Review Queue:** see rated cards across all topics, grouped into Again, Almost, and Got it.
- **Progress:** see rating counts and completion bars for each topic.
- **Reset ratings:** clear confidence ratings after confirmation. This does **not** clear quiz Right/Review results.

## Quiz

Choose a topic, answer the question, and move using **Previous** and **Next**.

- **Multiple choice:** tapping an answer checks it immediately and highlights the correct answer.
- **Multiple response:** select all applicable answers, then tap the check button. The selection must match the full correct set.
- **Matching:** use the dropdowns to match the items, then check your answers.

Correct attempts are recorded in **✓ Right**; incorrect attempts in **↻ Review**. The latest checked attempt determines that question's result. Revisiting a question lets you try it again.

The quiz filters show **All**, **Right**, **Review**, **😵 Again**, **🤔 Almost**, and **😎 Got it**, with counts for the currently selected topic or OM-A section.

Emoji confidence ratings are shared with flashcards. Quiz correctness is tracked separately: answering correctly does not automatically assign Got it, and choosing Again does not mark an answer wrong. You can rate confidence before or after answering.

## Saving progress

Progress is saved in the browser's `localStorage`:

| Storage key | Data |
| --- | --- |
| `a320-study-progress-v2` | Shared Again / Almost / Got it ratings |
| `athenaA320TextQuizV3` | Quiz Right / Review results |

Browser storage is not a backup. Clearing site data, using private browsing, changing browser/device, or changing the app's address can remove or isolate progress. Storage behavior for locally opened files varies by browser. Downloading a newer HTML file does not transfer progress to a different device.

There is currently no built-in progress export/import or quiz-results reset button.

## Offline use and optional sync

The question data, styling, study logic, and included source images are embedded in `index.html`. Local study does not require a question API or a sign-in.

The file still requests the Supabase SDK from an external CDN. With the shipped placeholder settings, cloud initialization is skipped and local study does not depend on that SDK. Sign-in and cloud sync require an internet connection and a configured backend.

There is **no service worker or guaranteed offline website cache**. Do not assume a hosted page will reopen offline just because you visited it once. Save a local copy and test it in your intended browser with the connection disabled before relying on it away from Wi-Fi.

The sign-in interface is present, but cloud sync is **not configured in this version**. To enable it, a maintainer must set the inline `window.SUPABASE_URL` and `window.SUPABASE_ANON_KEY` values in `index.html`, configure email authentication and redirect URLs, and provide a `progress` table with appropriate per-user Row Level Security. The sync code uses `user_id`, `card_key`, `rating`, and `updated_at`, with an upsert conflict target of `user_id,card_key`.

Cloud integration currently covers confidence ratings only, not quiz Right/Review results. No backend setup files are included with the single HTML app. Never place a service-role secret in this client-side file.

## Content and source images

Questions and answers were imported from the supplied Athena and ATPL source material. Relevant source diagrams are embedded where included, including the Meteorology SIGWX chart. The original PDFs are not needed to display those embedded images.

Transcription and the source answer keys can contain errors. This is a personal revision aid, not an official CAE, airline, or regulatory product, and not an operational reference. Check doubtful answers against the original source and current approved training or operating documentation.

## Maintaining the app

The HTML contains the inline CSS, flashcard markup, revision summaries, quiz dataset, and application scripts. `window.studyMenu` defines the shared menu order, display labels, Normal Procedure placeholder, and VietJet OM nesting.

Keep saved-progress identifiers stable when changing presentation:

- Flashcard keys use `<internal topic name>__<source question number>`.
- Quiz result keys use `<deck slug>__<source question number>`.
- `flashTopicByDeck` connects quiz questions to their shared flashcard ratings.

For example, the menu now displays **Ops Specs – Performance – Limitation**, but its internal topic remains `A320 Performance` and its quiz slug remains `performance`. Renaming those internal identifiers would disconnect existing saved progress.

When adding material, update the flashcards, Info Summary, quiz data, menu configuration, and topic mapping together. Only enable Normal Procedure once its actual questions are added. Recheck counts, answer keys, diagrams, topic selection, and confidence filters in both modes after changes.
