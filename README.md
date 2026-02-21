# Quran Database (MySQL) – Structured Quran Text Dataset for Developers

![License](https://img.shields.io/badge/License-MIT-green)
![Database](https://img.shields.io/badge/Database-MySQL-orange)
![Encoding](https://img.shields.io/badge/Encoding-UTF8MB4-blue)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)


This repository provides a **ready-to-import MySQL database containing the text of the Holy Quran** for developers who need a reliable, structured Quran dataset.

The database includes:

- Arabic Quran text **with Tashkeel (diacritics)**  
- Arabic Quran text **without Tashkeel (plain)**  
- Optional English translations of meaning (separate SQL files)

This project allows teams to integrate Quran data into websites, mobile apps, research tools, and educational platforms **without building the database layer from scratch**.

---

## 🔹 Official Project

Repository: https://github.com/webuccinoco/quran_mysql_database  

⚠️ This is the official repository of this dataset.

---

## 📑 Table of Contents

- [Project Overview](#project-overview)
- [Recognition](#recognition)
- [What’s Included](#whats-included)
  - [chapters Table](#chapters-table)
  - [verses Table](#verses-table)
  - [Translation SQL Files](#translation-sql-files-translations)
- [Database Encoding](#database-encoding)
- [Prerequisites](#prerequisites)
- [How to Use](#how-to-use)
- [Optional Translations](#optional-translations)
- [Roadmap](#roadmap)
- [License](#license)
- [Ownership](#ownership)

---

## Project Overview

The aim of this project is to help teams integrate the Holy Quran text into their infrastructure quickly and consistently.

The project is released under the **MIT License**, allowing usage in both commercial and non-commercial applications.

---

## Recognition

The `arabic_text_tashkeel` and `transliteration` data used in this project are sourced from the [Quran JSON API](https://quran-json-api.vercel.app/). We extend our gratitude to the developers of this API for providing accurate and accessible Quranic data.

Resource files used to generate the plain arabic text (The unvocalized without vowel marks) from the `quran-layers` project by [BigProf](https://github.com/bigprof-software/quran-layers).  
Repository: [https://github.com/bigprof-software/quran-layers](https://github.com/bigprof-software/quran-layers)

## What’s Included (Current)

The main `quranDB.sql` file contains two core tables:

### chapters Table

Stores Surah metadata:

- `id` – Surah number (1–114)  
- `arabic_name` – Arabic Surah name (Unicode)  
- `english_transliteration` – English transliteration of the Surah name  
- `english_translation` – English meaning of the Surah name  

> Expected rows: **114**

---

### verses Table

Stores each Ayah linked to its Surah:
- `id`: Unique identifier for each verse.
- `chapter_id`: Surah number (FK → `chapters.id`).
- `verse_number`: Ayah number within the Surah (1..n).
- `arabic_text_tashkeel`: Fully diacriticized Arabic text.
- `arabic_text_plain`: Simplified Arabic text without diacritics.
- `transliteration`: Romanized representation of the Arabic text.

Arabic is stored using `utf8mb4` to preserve full diacritics.

### Translation SQL Files (`translations/`)

Each translation is provided as a separate SQL file.

Naming pattern:

```
translations/{translation_name}.sql
```

Each translation table contains:

- `id` – Auto-increment row ID  
- `chapter_id` – Surah number  
- `verse_number` – Ayah number  
- `english_text` – Translation of meaning  

Translations are optional and can be imported independently.

---

## Database Encoding

All Arabic text is stored using:

```
utf8mb4
```

This ensures correct preservation of Arabic characters and diacritics.

---

## Prerequisites

- MySQL Server  
  https://www.mysql.com/

- MySQL Client  
  - https://www.phpmyadmin.net/  
  - https://www.heidisql.com/  
  - https://www.mysql.com/products/workbench/

> Tip: Local stacks such as **XAMPP**, **WAMP**, or **MAMP** include MySQL and phpMyAdmin.

---

## How to Use

1. Clone or download the repository:

```
git clone https://github.com/webuccinoco/quran_mysql_database.git
```

or

Download ZIP → Extract

2. Create a database (optional)

The file `quranDB.sql` is designed to **create the database automatically** during import (in the next step) using the name:

```
QuranDB
```

If you are fine with this default behavior, you can **skip this step** and move directly to **Step 3 (Import)**.

---

### If you prefer to create the database manually

Create a database named:

```
QuranDB
```

Using the following charset and collation (recommended for Arabic Quran text):

```sql
CREATE DATABASE QuranDB
CHARACTER SET utf8mb4
COLLATE utf8mb4_0900_as_cs;
```

> **Why this matters**  
> - `utf8mb4` fully supports Arabic characters and Quranic diacritics (Tashkeel).  
> - `utf8mb4_0900_as_cs` is accent-sensitive and case-sensitive, ensuring exact storage and matching of Quran text.

If your MySQL version is **older than 8.0**, you may use:

```sql
CREATE DATABASE QuranDB
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_cs;
```

---

### Using a different database name

If you want to use a different database name than `QuranDB`, open the file:

```
quranDB.sql
```

and replace all occurrences of:

```
QuranDB
```

with your preferred database name **before importing**.

3. Import:

```
quranDB.sql
```

This file will only create the DB if it dose not exist then creates tables and inserts all data in it.

---

## Optional Translations

After importing the main database, you may import any translation file from:

```
translations/
```

> ⚠️ Important  
> Some translations permit commercial use while others are limited to non-commercial usage.  
> Always verify the license of each translation before using it in commercial projects.

### Important Note on UTF-8 Encoding

When using translations, ensure that your HTML page includes the following tag inside the `<head>` section:

```html
<meta charset="UTF-8">
```

This is crucial because some translations contain special Unicode characters, such as macrons and angled quotation marks. Without UTF-8 encoding, these characters may be stored or displayed using HTML entities instead of their proper readable form.

#### Comparison Example

Correct (UTF-8 – Recommended for storage and display):

```
Alif-Lām-Mīm.
You ‹alone› we worship and You ‹alone› we ask for help.
```

Example of Entity-Encoded Version (may appear if UTF-8 is not properly used):

```
Alif-L&amacr;m-M&imacr;m.
You &lsaquo;alone&rsaquo; we worship and You &lsaquo;alone&rsaquo; we ask for help.
```

To ensure translations are stored in clean UTF-8 format (human-readable form), configure your database and web pages to use UTF-8 encoding. HTML entities should not be required when the page is properly configured with UTF-8.

---

### Included Translation Metadata

| ID | Title | Translator | Year | Description |
|----|------|------------|------|-------------|
| 1 | The Clear Quran | Dr. Mustafa Khattab | 2015 | Contemporary English translation focused on clarity and accessibility. |
| 2 | The Koran Interpreted | Arthur John Arberry | 1955 | Literary English translation aiming to reflect rhythm and style of Arabic. |

---



## Change Log
### Version v1.2.0
- Updated `arabic_text_tashkeel` values to use the authoritative source mentioned above.
- Added a new `transliteration` column to the `verses` table.
- Populated transliteration values for all verses using the same source.

### Version v1.1.0
- Adding 2 traslations.

### Version v1.0.0
- Adding the Arabic Text
