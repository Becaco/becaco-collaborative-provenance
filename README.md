
# Becaco Data Preparation for Collaborative Provenance Research

This repository provides tools, scripts, and guidelines for preparing data for collaborative and large-scale provenance research, with a focus on interoperability and reproducibility.

## Goals

- Demonstrate best practices for data cleaning and normalization
- Enable collaborative workflows for provenance data across institutions
- Support large-scale, cross-institutional research on provenance

# Guidelines for Integrating Your Data into the BECACO Knowledge Graph

The **BECACO Knowledge Graph** uses a Neo4j graph database to represent museum objects, their properties, and relationships such as ownership, materials, and archaeological periods.  
This document will guide you in preparing and uploading your data seamlessly.

---

## 📁 Data Format

- **Preferred formats**: Excel (.xlsx) or CSV (.csv)

---

## 🗓️ Step 1: Required Columns for Object Descriptions

| Column Name         | Description                                 | Required?     | Format / Notes                          |
|---------------------|---------------------------------------------|----------------|------------------------------------------|
| `ObjectID`          | Unique identifier for each object           | ✅ Yes         | Alphanumeric, must be unique             |
| `ObjectName`        | Name or title of the object                 | 🔶 Recommended | String                                   |
| `LocalId`           | Local identifier (e.g., museum inventory)   | 🔶 Recommended | String                                   |
| `Culture`           | Cultural attribution                        | Optional       | String                                   |
| `ArchaeologicalPeriod` | Time period or dating                   | Optional       | String                                   |
| `Materials`         | Materials used                              | Optional       | List of strings, separated by `;`   |
| `Techniques`        | Techniques or procedures applied            | Optional       | List of strings, separated by `;`  |
| `DimensionH`        | Height dimension                            | Optional       | Numeric or string                        |
| `DimensionL`        | Length dimension                            | Optional       | Numeric or string                        |
| `DimensionW`        | Width dimension                             | Optional       | Numeric or string                        |

---

## ✅ Data Preparation Tips

- Use **consistent and unique `ObjectID`s** to avoid conflicts.
- Separate multiple values (e.g., for `Materials` or `Techniques`) with **commas** or **semicolons**.
- Avoid empty rows or missing `ObjectID`s.
- For dimensions, **use numeric values** if available; leave blank if unknown.
- If a particular information is unavailable, it is preferable to **leave the field blank** rather than inserting placeholders (e.g., “N/A” or “Unknown”).

 ---


## 🗓️ Step 2: Provide Actor Information in Two Separate Sheets

To clearly distinguish between individuals and institutions, please provide actor information in **two separate files or sheets**:

- **Sheet 1 — Individuals (e.g., artists, collectors, archaeologists)**  
- **Sheet 2 — Institutions (e.g., museums, universities, foundations)**

---

### 👤 Sheet 1: Individuals

Use this structure to describe people involved in the object's history.

| Column Name        | Description                                                             | Required?     | Format / Notes                                         |
|--------------------|-------------------------------------------------------------------------|----------------|---------------------------------------------------------|
| `ActorID`          | Unique identifier for the person                                         | ✅ Yes         | Alphanumeric, must be unique                            |
| `Name in database` | Name as it appears in the original museum database                      | ✅ Yes         | String                                                  |
| `LastName`         | Last name                                                                | Recommended    | String                                                  |
| `FirstName`        | First name                                                               | Recommended    | String                                                  |
| `WikiData ID`      | Wikidata identifier                                                      | Optional       | Format: Q123456                                         |
| `Gender`            | Gender                                                                   | Optional       | e.g., male, female                             |
| `BirthDate`        | Date of birth                                                            | Optional       | Format: YYYY-MM-DD                                      |
| `DeathDate`        | Date of death                                                            | Optional       | Format: YYYY-MM-DD                                      |
| `Nationality`      | National or cultural affiliation                                         | Optional       | String                                                  |
| `Institution`      | Affiliated institution (if applicable)                                   | Optional       | String                                                  |
| `Occupation`       | Role or profession                                                       | Optional       | e.g., painter, curator, archaeologist                   |
| `Biography`        | Short biography                                                          | Optional       | Text                                                    |
| `Biography Source` | Source of the biography                                                  | Optional       | URL or reference                                        |
| `Notes`            | Additional notes                                                         | Optional       | Free text                                               |

---

### 🏛️ Sheet 2: Institutions

Use this structure for organizations such as museums, universities, foundations, etc.

| Column Name             | Description                                                       | Required?     | Format / Notes                                        |
|--------------------------|-------------------------------------------------------------------|----------------|--------------------------------------------------------|
| `ActorID`                | Unique identifier for the institution                             | ✅ Yes         | Alphanumeric                                           |
| `Name in database`       | Name as it appears in the original museum database                | ✅ Yes         | String                                                 |
| `Type of Institution`    | Nature of the institution (e.g., museum, university, foundation)   | Recommended    | String                                                 |
| `Institutional Status`   | Public, private, nonprofit, etc.                                   | Optional       | String                                                 |
| `Origin`                 | Country of origin                                                  | Optional       | e.g., USA, France                                      |
| `Place of activity`      | Geographic area of operation                                       | Optional       | e.g., Honduras                                         |
| `Years of activity`      | Time span of the institution's activity                            | Optional       | e.g., "19th–20th century"                              |
| `Remarks`                | Observations or comments                                           | Optional       | Free text                                              |
| `📖 Literature`          | References (books, articles, URLs)                                 | Optional       | e.g., citation with or without link                    |
| `🗄️ People from readings` | Individuals related to the institution via literature              | Optional       | List of names or links, separated by `;`               |

---

### 📌 Notes

- Use **two separate sheets**: one for individuals and one for institutions.
- Each actor (person or institution) must have a **unique `ActorID`**.
- `Name in database` should match exactly the spelling used in the original source or museum database.
- Leave fields blank if the information is unknown.

---

## 🗓️ Step 3: Provide Event Information (Acquisitions, Collections, Legacies, etc.)

To represent the historical trajectory of museum objects, please fill in an Excel sheet structured as follows:

### 📄 Excel Sheet: `Events.xlsx`

| Column Name     | Description                                                                 | Required? | Format / Notes                                                        |
|------------------|------------------------------------------------------------------------------|-----------|------------------------------------------------------------------------|
| `Event_ID`       | Unique identifier for the event                                              | ✅ Yes    | Format: Alphanumeric (e.g., `MudecEV169`)                             |
| `EventType`      | Type of the event                                                            | ✅ Yes    | Examples: Acquisition, Legacy, Collection, Donation, etc.             |
| `Dates`          | Date(s) associated with the event                                            | ✅ Yes    | One or more years (e.g., `1934` or `1966;1970`). Add `?` for uncertain dates. |
| `Place`          | Location(s) where the event occurred                                         | Optional | One or more places (e.g., `Rome;Naples`). Add `?` for uncertain places. |
| `SourceActors`   | Identifier(s) of the actor(s) transferring the object(s)                     | Optional | Actor IDs (e.g., `MudecA20`), separated by commas if multiple         |
| `TargetActors`   | Identifier(s) of the receiving actor(s) or institution(s)                   | Optional | e.g., `Mudec Museum`                                                  |
| `ObjectIDs`      | Object identifier(s) involved in the event                                   | ✅ Yes    | `ObjectID`s separated by commas (e.g., `Mudec1;Mudec2`)               |

---



---

### 📌 Notes

- Each row represents one historical event.
- Use **commas (`,`)** to separate multiple entries in `ObjectIDs`, `SourceActors`, or `Dates`.
- Use **semicolons (`;`)** to separate multiple places.
- Leave `Place`, `SourceActors`, or `TargetActors` blank if unknown or not applicable.

---

### 📊 Example 

| Event_ID   | EventType   | Dates       | Place        | SourceActors | TargetActors  | ObjectIDs       |
|------------|-------------|-------------|--------------|---------------|----------------|------------------|
| MudecEV169 | Acquisition | 1934        |              | MudecA20      | Mudec Museum   | Mudec1;Mudec2    |
| MudecEV170 | Acquisition | 1865        |              | MudecA21      | Mudec Museum   | Mudec3           |
| MudecEV171 | Legacy      | 1988?,1987? |              | MudecA44      | Mudec Museum   | Mudec3           |
| MudecEV172 | Legacy      | 1966,1970   | Rome?;Milan  | MudecA21      | Mudec Museum   | Mudec2           |
| MudecEV173 | Collection  | 500?,600?   | Copán?       | MudecA22      |                | Mudec1           |

---

### 🧑‍💼 How to Fill in `SourceActors` and `TargetActors`?

The actors involved in an event depend on the **EventType**. You should refer to the table below to know whether to use only `SourceActors`, only `TargetActors`, or both.

| EventType           | CIDOC Class(es)     | `SourceActors` Required? | `TargetActors` Required? | Notes                                                                 |
|---------------------|---------------------|---------------------------|---------------------------|-----------------------------------------------------------------------|
| Creation            | E12_Production      | ✅ Yes                    | ❌ No                    | The creator (artist, maker, etc.) is the source                      |
| Own Creation        | E12_Production      | ✅ Yes                    | ❌ No                    | Same as above, but annotated as "Own Creation"                       |
| Collection          | E12_Production      | ✅ Yes                    | ❌ No                    | Source is the institution or person who assembled the collection     |
| Acquisition         | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source is the previous owner, target is the acquirer                 |
| Purchase            | E96_Purchase        | ✅ Yes                    | ✅ Yes                   | Source = seller, target = buyer                                      |
| Donation            | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = donor, target = recipient                                   |
| Exchange            | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = exchanger, target = recipient                                |
| Legacy              | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = deceased person or estate, target = inheritor               |
| Donation/Legacy     | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = donor, target = recipient                                       |
| Purchase/Legacy     | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = seller, target = buyer                                       |
| Seizure             | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = original owner, target = seizing institution                |
| Excavation          | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = Archaeologist , target = recipient                          |
| Loan                | E8_Acquisition      | ✅ Yes                    | ✅ Yes                   | Source = lender, target = borrower                                   |
| Previous Collection | E8_Acquisition      | ✅ Yes                    | ❌ No                    | Source = previous collector                                          |

---



### ✅ Tips

- Always use **actor identifiers (`ActorID`)** already defined in your `Individuals` or `Institutions` sheet.
- If only one actor is involved (e.g., Creation), fill only `SourceActors`.
- If multiple actors are involved, separate them with `;`: `MudecA20;MudecA44`










## ❓ Expressing Uncertainty

You can indicate uncertainty in your data using the `?` symbol:

- **Dates**: Add `?` to approximate years → `500?,600?`
- **Places**: Add `?` to places you're unsure about → `Honduras?;Copán`
- **Actors**: Add `?` to Actors you're unsure about → `MudecA21?`

This will be reflected in the knowledge graph as probabilistic information (Place, Actor...) or imprecise time spans.



