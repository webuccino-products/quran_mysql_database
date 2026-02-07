# Quran Database (MySQL)

This repository provides a ready-to-import MySQL database for the Holy Quran:
- Arabic text both fully vocalized (with tashkeel/diacritics) and unvocalized (without vowel marks).
- English translations of meaning provided as separate SQL files that can be optionally imported to extend the database with selected translations.

## Project Overview

The aim is to help teams integrate the Holy Quran text into their infrastructure without spending time building the database layer. The project is MIT licensed, so it can be used in both commercial and non-commercial applications.

## Recognition

Resource files used to generate this database come from the `quran-layers` project by [BigProf](https://github.com/bigprof-software/quran-layers).  
Repository: [https://github.com/bigprof-software/quran-layers](https://github.com/bigprof-software/quran-layers)

## What’s Included (Current)

The main `quranDB.sql` file contains two core tables:

### `chapters` Table
Stores the Surah metadata:
- `id`: Surah number (1–114).
- `arabic_name`: Arabic Surah name (Unicode).
- `english_transliteration`: English transliteration of the Surah name.
- `english_translation`: English meaning/translation of the Surah name.

> **Note:** If imported successfully, this table should contain 114 records.

### `verses` Table
Stores each Ayah linked to its Surah:
- `id`: Auto-increment verse row ID.
- `chapter_id`: Surah number (FK → `chapters.id`).
- `verse_number`: Ayah number within the Surah (1..n).
- `arabic_text_tashkeel`: Arabic Ayah text with Tashkeel (diacritics).
- `arabic_text_plain`: Arabic Ayah text without Tashkeel.

Arabic is stored using `utf8mb4` to preserve full diacritics.

### Translation SQL Files (`translations/`)

Each optional translation is provided as a separate SQL file using this naming scheme:
`{Translation_name.sql}`

Each translation file creates a table with the following columns:
- `id`: Auto-increment row ID.
- `chapter_id`: Surah number (FK → `chapters.id`).
- `verse_number`: Ayah number within the Surah (1..n).
- `english_text`: English translation of the Meaning of the Ayah.

## Prerequisites


- MySQL server: https://www.mysql.com/
- MySQL client: https://www.phpmyadmin.net/ or https://www.heidisql.com/
> **Note:** If you’re working on a local machine, a stack such as XAMPP can install a MySQL server locally on your system, along with phpMyAdmin, the popular MySQL client.

## How to Use

1. Get the repository:
   - Clone: `git clone https://github.com/webuccinoco/quran_mysql_database.git`
   - Or download the repository: click the green **Code** button → **Download ZIP**, then extract the ZIP.
2. Create a database named **`QuranDB`** using your MySQL client (or let the import create it).
3. In your MySQL client (phpMyAdmin / MySQL Workbench / CLI), use **Import**.
4. Import this file only:
   - `quranDB.sql`

That file creates the database, tables, and inserts all data.

### Optional Translations

Translation SQL files are available in `translations/`. Import any single translation file (or all of them) after the main database is imported.

> **Note:** Some translations allow commercial use and others are limited to free/non-commercial use. Check the copyright/license for each translation online **before** importing.

| Translation ID | Title | Translator | Publishing Year | Description |
| --- | --- | --- | --- | --- |
| 1 | The Clear Quran | Dr. Mustafa Khattab | 2015 | Uses contemporary English to ensure clarity and accessibility for modern readers. |
| 2 | The Koran Interpreted | Arthur John Arberry | 1955 | His 1955 translation is highly regarded for its literary quality and attempt to mirror the cadence and rhythm of the original Arabic text. Arberry was a professor of Arabic at Cambridge University, not a practitioner of Islam. |

## Roadmap

- **Add More Translations** 
- **Add Transliteration** (Display Arabic to Latin transliteration for each verse)
- **Add navigation based on traditional Quran structure** (Juz' (Ajzaa - Parts), Hizb, Sajdah (Prostration verses))
- **Topics, Tags and Verse Linking** (Juz' (Ajzaa - Parts), Hizb, Sajdah (Prostration verses))
- **Cross-Verse Connections** 

