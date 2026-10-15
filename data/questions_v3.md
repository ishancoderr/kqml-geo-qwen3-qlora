# Fine-tuning examples — questions_v3.yaml

347 questions, 1119 training examples. Generated — edit `questions_v3.yaml`, not this file.

Each step is one line of the JSONL: the model gets the linked system prompt plus **Model sees**, and is trained to reply with **Model must answer**.

# data

## d01 · DIRECT_LOOKUP

> What was the population of Hessen in 2019?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · fetch (answering Agent-1) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 5 | SQL · fetch (answering Agent-2) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What was the population of Hessen in 2019?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What was the population of Hessen in 2019?
```

**Model must answer**

```json
{
  "spatial": ["Hessen"],
  "temporal": [2019],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Hessen in [2019]",
  "entity_type": "state",
  "spatial": ["Hessen"],
  "temporal": [2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · fetch (answering Agent-1)

*this agent answering Agent-1's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-1 asks for population of Hessen in [2019]",
  "entity_type": "state",
  "spatial": ["Hessen"],
  "temporal": [2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 5 · SQL · fetch (answering Agent-2)

*this agent answering Agent-2's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-2 asks for population of Hessen in [2019]",
  "entity_type": "state",
  "spatial": ["Hessen"],
  "temporal": [2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d02 · DIRECT_LOOKUP

> How many people lived in Sachsen and Thüringen in 2022?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many people lived in Sachsen and Thüringen in 2022?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many people lived in Sachsen and Thüringen in 2022?
```

**Model must answer**

```json
{
  "spatial": ["Sachsen", "Thüringen"],
  "temporal": [2022],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Sachsen, Thüringen in [2022]",
  "entity_type": "state",
  "spatial": ["Sachsen", "Thüringen"],
  "temporal": [2022],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d03 · DIRECT_LOOKUP

> Show me the number of marriages in Niedersachsen from 2018 to 2021.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show me the number of marriages in Niedersachsen from 2018 to 2021.
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show me the number of marriages in Niedersachsen from 2018 to 2021.
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen"],
  "temporal": [2018, 2019, 2020, 2021],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Niedersachsen in [2018, 2019, 2020, 2021]",
  "entity_type": "state",
  "spatial": ["Niedersachsen"],
  "temporal": [2018, 2019, 2020, 2021],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d04 · DIRECT_LOOKUP

> Live births in Bremen and Saarland, 2020

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Live births in Bremen and Saarland, 2020
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Live births in Bremen and Saarland, 2020
```

**Model must answer**

```json
{
  "spatial": ["Bremen", "Saarland"],
  "temporal": [2020],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Bremen, Saarland in [2020]",
  "entity_type": "state",
  "spatial": ["Bremen", "Saarland"],
  "temporal": [2020],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Saarland']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Saarland']",
  "entity_type": "state",
  "spatial": ["Saarland"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d05 · DIRECT_LOOKUP

> Give me population, marriages and live births for Rheinland-Pfalz in 2023.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · fetch (answering Agent-1) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 5 | SQL · fetch (answering Agent-2) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me population, marriages and live births for Rheinland-Pfalz in 2023.
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me population, marriages and live births for Rheinland-Pfalz in 2023.
```

**Model must answer**

```json
{
  "spatial": ["Rheinland-Pfalz"],
  "temporal": [2023],
  "attributes": ["population", "marriages", "live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population, marriages, live_births of Rheinland-Pfalz in [2023]",
  "entity_type": "state",
  "spatial": ["Rheinland-Pfalz"],
  "temporal": [2023],
  "attributes": ["population", "marriages", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · fetch (answering Agent-1)

*this agent answering Agent-1's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-1 asks for population, marriages, live_births of Rheinland-Pfalz in [2023]",
  "entity_type": "state",
  "spatial": ["Rheinland-Pfalz"],
  "temporal": [2023],
  "attributes": ["population", "marriages", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 5 · SQL · fetch (answering Agent-2)

*this agent answering Agent-2's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-2 asks for population, marriages, live_births of Rheinland-Pfalz in [2023]",
  "entity_type": "state",
  "spatial": ["Rheinland-Pfalz"],
  "temporal": [2023],
  "attributes": ["population", "marriages", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d06 · DIRECT_LOOKUP

> How many babies were born in Mecklenburg-Vorpommern in 2017?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many babies were born in Mecklenburg-Vorpommern in 2017?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many babies were born in Mecklenburg-Vorpommern in 2017?
```

**Model must answer**

```json
{
  "spatial": ["Mecklenburg-Vorpommern"],
  "temporal": [2017],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Mecklenburg-Vorpommern in [2017]",
  "entity_type": "state",
  "spatial": ["Mecklenburg-Vorpommern"],
  "temporal": [2017],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d07 · DIRECT_LOOKUP

> Population of every German state in 2018

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of every German state in 2018
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of every German state in 2018
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2018],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2018]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"],
  "temporal": [2018],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d08 · DIRECT_LOOKUP

> Marriages in all federal states for 2022 and 2023

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Marriages in all federal states for 2022 and 2023
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Marriages in all federal states for 2022 and 2023
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2022, 2023],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2022, 2023]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"],
  "temporal": [2022, 2023],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Bremen', 'Saarland']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Bremen', 'Saarland']",
  "entity_type": "state",
  "spatial": ["Bremen", "Saarland"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d09 · DIRECT_LOOKUP

> Inhabitants of Baden-Wuerttemberg between 2015 and 2019

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Inhabitants of Baden-Württemberg between 2015 and 2019
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Inhabitants of Baden-Württemberg between 2015 and 2019
```

**Model must answer**

```json
{
  "spatial": ["Baden-Württemberg"],
  "temporal": [2015, 2016, 2017, 2018, 2019],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Baden-Württemberg in [2015, 2016, 2017, 2018, 2019]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg"],
  "temporal": [2015, 2016, 2017, 2018, 2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d10 · DIRECT_LOOKUP · validation

> How many residents did Brandenburg have in 2020?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many residents did Brandenburg have in 2020?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many residents did Brandenburg have in 2020?
```

**Model must answer**

```json
{
  "spatial": ["Brandenburg"],
  "temporal": [2020],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Brandenburg in [2020]",
  "entity_type": "state",
  "spatial": ["Brandenburg"],
  "temporal": [2020],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d11 · DIRECT_LOOKUP

> Number of marriages and births in Schleswig-Holstein in 2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Number of marriages and births in Schleswig-Holstein in 2016
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Number of marriages and births in Schleswig-Holstein in 2016
```

**Model must answer**

```json
{
  "spatial": ["Schleswig-Holstein"],
  "temporal": [2016],
  "attributes": ["marriages", "live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages, live_births of Schleswig-Holstein in [2016]",
  "entity_type": "state",
  "spatial": ["Schleswig-Holstein"],
  "temporal": [2016],
  "attributes": ["marriages", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d12 · DIRECT_LOOKUP

> Compare the population of Berlin, Hamburg and Bremen in 2020

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |
| 5 | SQL · fetch (answering Agent-1) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 6 | SQL · fetch (answering Agent-2) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Compare the population of Berlin, Hamburg and Bremen in 2020
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Compare the population of Berlin, Hamburg and Bremen in 2020
```

**Model must answer**

```json
{
  "spatial": ["Berlin", "Hamburg", "Bremen"],
  "temporal": [2020],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Berlin, Hamburg, Bremen in [2020]",
  "entity_type": "state",
  "spatial": ["Berlin", "Hamburg", "Bremen"],
  "temporal": [2020],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Bremen']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Bremen']",
  "entity_type": "state",
  "spatial": ["Bremen"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### 5 · SQL · fetch (answering Agent-1)

*this agent answering Agent-1's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-1 asks for population of Berlin, Hamburg, Bremen in [2020]",
  "entity_type": "state",
  "spatial": ["Berlin", "Hamburg", "Bremen"],
  "temporal": [2020],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 6 · SQL · fetch (answering Agent-2)

*this agent answering Agent-2's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-2 asks for population of Berlin, Hamburg, Bremen in [2020]",
  "entity_type": "state",
  "spatial": ["Berlin", "Hamburg", "Bremen"],
  "temporal": [2020],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d13 · DIRECT_LOOKUP

> nordrhein westfalen population 2024

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Nordrhein-Westfalen population 2024
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Nordrhein-Westfalen population 2024
```

**Model must answer**

```json
{
  "spatial": ["Nordrhein-Westfalen"],
  "temporal": [2024],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Nordrhein-Westfalen in [2024]",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen"],
  "temporal": [2024],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d14 · DIRECT_LOOKUP

> What were the live births in Sachsen-Anhalt in 2019 and 2021?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What were the live births in Sachsen-Anhalt in 2019 and 2021?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What were the live births in Sachsen-Anhalt in 2019 and 2021?
```

**Model must answer**

```json
{
  "spatial": ["Sachsen-Anhalt"],
  "temporal": [2019, 2021],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Sachsen-Anhalt in [2019, 2021]",
  "entity_type": "state",
  "spatial": ["Sachsen-Anhalt"],
  "temporal": [2019, 2021],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d15 · DIRECT_LOOKUP

> Population and marriages for Bayern and Baden-Württemberg, 2014-2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population and marriages for Bayern and Baden-Württemberg, 2014-2016
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population and marriages for Bayern and Baden-Württemberg, 2014-2016
```

**Model must answer**

```json
{
  "spatial": ["Bayern", "Baden-Württemberg"],
  "temporal": [2014, 2015, 2016],
  "attributes": ["population", "marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population, marriages of Bayern, Baden-Württemberg in [2014, 2015, 2016]",
  "entity_type": "state",
  "spatial": ["Bayern", "Baden-Württemberg"],
  "temporal": [2014, 2015, 2016],
  "attributes": ["population", "marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d16 · DIRECT_LOOKUP

> How many couples got married in Hessen in 2023?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many couples got married in Hessen in 2023?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many couples got married in Hessen in 2023?
```

**Model must answer**

```json
{
  "spatial": ["Hessen"],
  "temporal": [2023],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Hessen in [2023]",
  "entity_type": "state",
  "spatial": ["Hessen"],
  "temporal": [2023],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d17 · DIRECT_LOOKUP

> Tell me the population figures for Thüringen, Sachsen and Sachsen-Anhalt in 2020.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Tell me the population figures for Thüringen, Sachsen and Sachsen-Anhalt in 2020.
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Tell me the population figures for Thüringen, Sachsen and Sachsen-Anhalt in 2020.
```

**Model must answer**

```json
{
  "spatial": ["Thüringen", "Sachsen", "Sachsen-Anhalt"],
  "temporal": [2020],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Thüringen, Sachsen, Sachsen-Anhalt in [2020]",
  "entity_type": "state",
  "spatial": ["Thüringen", "Sachsen", "Sachsen-Anhalt"],
  "temporal": [2020],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Sachsen-Anhalt']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Sachsen-Anhalt']",
  "entity_type": "state",
  "spatial": ["Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d18 · DIRECT_LOOKUP

> Bavaria population in 2022

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Bavaria population in 2022
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Bavaria population in 2022
```

**Model must answer**

```json
{
  "spatial": ["Bayern"],
  "temporal": [2022],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Bayern in [2022]",
  "entity_type": "state",
  "spatial": ["Bayern"],
  "temporal": [2022],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d19 · DIRECT_LOOKUP

> How many marriages were registered in Lower Saxony in 2019?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many marriages were registered in Lower Saxony in 2019?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many marriages were registered in Lower Saxony in 2019?
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen"],
  "temporal": [2019],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Niedersachsen in [2019]",
  "entity_type": "state",
  "spatial": ["Niedersachsen"],
  "temporal": [2019],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d20 · DIRECT_LOOKUP · validation

> Live birth data for Hamburg and Schleswig-Holstein from 2021 to 2024

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · fetch (answering Agent-1) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 5 | SQL · fetch (answering Agent-2) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Live birth data for Hamburg and Schleswig-Holstein from 2021 to 2024
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Live birth data for Hamburg and Schleswig-Holstein from 2021 to 2024
```

**Model must answer**

```json
{
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "temporal": [2021, 2022, 2023, 2024],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Hamburg, Schleswig-Holstein in [2021, 2022, 2023, 2024]",
  "entity_type": "state",
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "temporal": [2021, 2022, 2023, 2024],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · fetch (answering Agent-1)

*this agent answering Agent-1's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-1 asks for live_births of Hamburg, Schleswig-Holstein in [2021, 2022, 2023, 2024]",
  "entity_type": "state",
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "temporal": [2021, 2022, 2023, 2024],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 5 · SQL · fetch (answering Agent-2)

*this agent answering Agent-2's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-2 asks for live_births of Hamburg, Schleswig-Holstein in [2021, 2022, 2023, 2024]",
  "entity_type": "state",
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "temporal": [2021, 2022, 2023, 2024],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d21 · DIRECT_LOOKUP

> What is the population of Sachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
What is the population of Sachsen?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What is the population of Sachsen?
```

**Model must answer**

```json
{
  "spatial": ["Sachsen"],
  "temporal": [],
  "attributes": ["population"],
  "entity_type": "state"
}
```

---

## d22 · DIRECT_LOOKUP

> Show marriage numbers for Bremen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Show marriage numbers for Bremen
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show marriage numbers for Bremen
```

**Model must answer**

```json
{
  "spatial": ["Bremen"],
  "temporal": [],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

---

## d23 · DIRECT_LOOKUP

> What was the population of Saarland in 1995?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What was the population of Saarland in 1995?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What was the population of Saarland in 1995?
```

**Model must answer**

```json
{
  "spatial": ["Saarland"],
  "temporal": [1995],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Saarland in [1995]",
  "entity_type": "state",
  "spatial": ["Saarland"],
  "temporal": [1995],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d24 · DIRECT_LOOKUP

> Live births in Hessen and Sachsen from 2010 to 2013

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Live births in Hessen and Sachsen from 2010 to 2013
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Live births in Hessen and Sachsen from 2010 to 2013
```

**Model must answer**

```json
{
  "spatial": ["Hessen", "Sachsen"],
  "temporal": [2010, 2011, 2012, 2013],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Hessen, Sachsen in [2010, 2011, 2012, 2013]",
  "entity_type": "state",
  "spatial": ["Hessen", "Sachsen"],
  "temporal": [2010, 2011, 2012, 2013],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d25 · DIRECT_LOOKUP

> Marriages in Brandenburg, Berlin and Hamburg in 2018

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Marriages in Brandenburg, Berlin and Hamburg in 2018
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Marriages in Brandenburg, Berlin and Hamburg in 2018
```

**Model must answer**

```json
{
  "spatial": ["Brandenburg", "Berlin", "Hamburg"],
  "temporal": [2018],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Brandenburg, Berlin, Hamburg in [2018]",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Berlin", "Hamburg"],
  "temporal": [2018],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Berlin', 'Hamburg']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Berlin', 'Hamburg']",
  "entity_type": "state",
  "spatial": ["Berlin", "Hamburg"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d26 · DIRECT_LOOKUP

> Population of all German states in 1990

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Population of all German states in 1990
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of all German states in 1990
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [1990],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [1990]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"],
  "temporal": [1990],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Baden-Württemberg', 'Bayern', 'Berlin', 'Bremen', 'Hamburg']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Baden-Württemberg', 'Bayern', 'Berlin', 'Bremen', 'Hamburg']",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Bremen", "Hamburg"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d27 · DIRECT_LOOKUP

> Number of inhabitants in Nordrhein-Westfalen between 2003 and 2006

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Number of inhabitants in Nordrhein-Westfalen between 2003 and 2006
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Number of inhabitants in Nordrhein-Westfalen between 2003 and 2006
```

**Model must answer**

```json
{
  "spatial": ["Nordrhein-Westfalen"],
  "temporal": [2003, 2004, 2005, 2006],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Nordrhein-Westfalen in [2003, 2004, 2005, 2006]",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen"],
  "temporal": [2003, 2004, 2005, 2006],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d28 · DIRECT_LOOKUP

> How many marriages were there in Thüringen in 2011 and 2013?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many marriages were there in Thüringen in 2011 and 2013?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many marriages were there in Thüringen in 2011 and 2013?
```

**Model must answer**

```json
{
  "spatial": ["Thüringen"],
  "temporal": [2011, 2013],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Thüringen in [2011, 2013]",
  "entity_type": "state",
  "spatial": ["Thüringen"],
  "temporal": [2011, 2013],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d29 · DIRECT_LOOKUP

> Give me the live births for Bavaria in 2009

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Give me the live births for Bavaria in 2009
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the live births for Bavaria in 2009
```

**Model must answer**

```json
{
  "spatial": ["Bayern"],
  "temporal": [2009],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Bayern in [2009]",
  "entity_type": "state",
  "spatial": ["Bayern"],
  "temporal": [2009],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Bayern']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Bayern']",
  "entity_type": "state",
  "spatial": ["Bayern"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d30 · DIRECT_LOOKUP · validation

> Population of Saxony-Anhalt in 2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of Saxony-Anhalt in 2016
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of Saxony-Anhalt in 2016
```

**Model must answer**

```json
{
  "spatial": ["Sachsen-Anhalt"],
  "temporal": [2016],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Sachsen-Anhalt in [2016]",
  "entity_type": "state",
  "spatial": ["Sachsen-Anhalt"],
  "temporal": [2016],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d31 · DIRECT_LOOKUP

> births and marriages in mecklenburg vorpommern 2002

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
births and marriages in Mecklenburg-Vorpommern 2002
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: births and marriages in Mecklenburg-Vorpommern 2002
```

**Model must answer**

```json
{
  "spatial": ["Mecklenburg-Vorpommern"],
  "temporal": [2002],
  "attributes": ["live_births", "marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births, marriages of Mecklenburg-Vorpommern in [2002]",
  "entity_type": "state",
  "spatial": ["Mecklenburg-Vorpommern"],
  "temporal": [2002],
  "attributes": ["live_births", "marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d32 · DIRECT_LOOKUP

> Population and live births for Niedersachsen and Bremen in 2007

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · fetch (answering Agent-1) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 5 | SQL · fetch (answering Agent-2) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population and live births for Niedersachsen and Bremen in 2007
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population and live births for Niedersachsen and Bremen in 2007
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen", "Bremen"],
  "temporal": [2007],
  "attributes": ["population", "live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population, live_births of Niedersachsen, Bremen in [2007]",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Bremen"],
  "temporal": [2007],
  "attributes": ["population", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · fetch (answering Agent-1)

*this agent answering Agent-1's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-1 asks for population, live_births of Niedersachsen, Bremen in [2007]",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Bremen"],
  "temporal": [2007],
  "attributes": ["population", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 5 · SQL · fetch (answering Agent-2)

*this agent answering Agent-2's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-2 asks for population, live_births of Niedersachsen, Bremen in [2007]",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Bremen"],
  "temporal": [2007],
  "attributes": ["population", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d33 · DIRECT_LOOKUP

> How many people lived in Schleswig-Holstein in 1999?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many people lived in Schleswig-Holstein in 1999?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many people lived in Schleswig-Holstein in 1999?
```

**Model must answer**

```json
{
  "spatial": ["Schleswig-Holstein"],
  "temporal": [1999],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Schleswig-Holstein in [1999]",
  "entity_type": "state",
  "spatial": ["Schleswig-Holstein"],
  "temporal": [1999],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d34 · DIRECT_LOOKUP

> Show marriages for every federal state in 2019

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show marriages for every federal state in 2019
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show marriages for every federal state in 2019
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2019],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2019]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"],
  "temporal": [2019],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d35 · DIRECT_LOOKUP

> Population of Rheinland-Pfalz from 1991 to 1994

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of Rheinland-Pfalz from 1991 to 1994
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of Rheinland-Pfalz from 1991 to 1994
```

**Model must answer**

```json
{
  "spatial": ["Rheinland-Pfalz"],
  "temporal": [1991, 1992, 1993, 1994],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Rheinland-Pfalz in [1991, 1992, 1993, 1994]",
  "entity_type": "state",
  "spatial": ["Rheinland-Pfalz"],
  "temporal": [1991, 1992, 1993, 1994],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d36 · DIRECT_LOOKUP

> Give me the population of Rheinland-Pfalz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Give me the population of Rheinland-Pfalz
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the population of Rheinland-Pfalz
```

**Model must answer**

```json
{
  "spatial": ["Rheinland-Pfalz"],
  "temporal": [],
  "attributes": ["population"],
  "entity_type": "state"
}
```

---

## d37 · DIRECT_LOOKUP

> Live births in Hamburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Live births in Hamburg?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Live births in Hamburg?
```

**Model must answer**

```json
{
  "spatial": ["Hamburg"],
  "temporal": [],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

---

## d38 · DIRECT_LOOKUP

> Marriage statistics for Brandenburg and Sachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Marriage statistics for Brandenburg and Sachsen
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Marriage statistics for Brandenburg and Sachsen
```

**Model must answer**

```json
{
  "spatial": ["Brandenburg", "Sachsen"],
  "temporal": [],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

---

## d39 · DIRECT_LOOKUP

> Population of Hesse in 2001

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of Hesse in 2001
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of Hesse in 2001
```

**Model must answer**

```json
{
  "spatial": ["Hessen"],
  "temporal": [2001],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Hessen in [2001]",
  "entity_type": "state",
  "spatial": ["Hessen"],
  "temporal": [2001],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d40 · DIRECT_LOOKUP · validation

> Give me population, marriages and live births for Saarland and Thüringen in 2004

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me population, marriages and live births for Saarland and Thüringen in 2004
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me population, marriages and live births for Saarland and Thüringen in 2004
```

**Model must answer**

```json
{
  "spatial": ["Saarland", "Thüringen"],
  "temporal": [2004],
  "attributes": ["population", "marriages", "live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population, marriages, live_births of Saarland, Thüringen in [2004]",
  "entity_type": "state",
  "spatial": ["Saarland", "Thüringen"],
  "temporal": [2004],
  "attributes": ["population", "marriages", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d41 · DIRECT_LOOKUP

> How many babies were born in Sachsen in 1996?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many babies were born in Sachsen in 1996?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many babies were born in Sachsen in 1996?
```

**Model must answer**

```json
{
  "spatial": ["Sachsen"],
  "temporal": [1996],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Sachsen in [1996]",
  "entity_type": "state",
  "spatial": ["Sachsen"],
  "temporal": [1996],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d42 · DIRECT_LOOKUP

> Marriages in Baden-Württemberg from 2016 to 2019

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |
| 5 | SQL · fetch (answering Agent-1) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 6 | SQL · fetch (answering Agent-2) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Marriages in Baden-Württemberg from 2016 to 2019
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Marriages in Baden-Württemberg from 2016 to 2019
```

**Model must answer**

```json
{
  "spatial": ["Baden-Württemberg"],
  "temporal": [2016, 2017, 2018, 2019],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Baden-Württemberg in [2016, 2017, 2018, 2019]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg"],
  "temporal": [2016, 2017, 2018, 2019],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Baden-Württemberg']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Baden-Württemberg']",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### 5 · SQL · fetch (answering Agent-1)

*this agent answering Agent-1's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-1 asks for marriages of Baden-Württemberg in [2016, 2017, 2018, 2019]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg"],
  "temporal": [2016, 2017, 2018, 2019],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 6 · SQL · fetch (answering Agent-2)

*this agent answering Agent-2's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-2 asks for marriages of Baden-Württemberg in [2016, 2017, 2018, 2019]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg"],
  "temporal": [2016, 2017, 2018, 2019],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d43 · DIRECT_LOOKUP

> nrw marriages 2010

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
nrw marriages 2010
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: nrw marriages 2010
```

**Model must answer**

```json
{
  "spatial": ["Nordrhein-Westfalen"],
  "temporal": [2010],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Nordrhein-Westfalen in [2010]",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen"],
  "temporal": [2010],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d44 · DIRECT_LOOKUP

> Population in Berlin in 1990 and 2000

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Population in Berlin in 1990 and 2000
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population in Berlin in 1990 and 2000
```

**Model must answer**

```json
{
  "spatial": ["Berlin"],
  "temporal": [1990, 2000],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Berlin in [1990, 2000]",
  "entity_type": "state",
  "spatial": ["Berlin"],
  "temporal": [1990, 2000],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Berlin']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Berlin']",
  "entity_type": "state",
  "spatial": ["Berlin"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d45 · DIRECT_LOOKUP

> Live births in Brandenburg, Mecklenburg-Vorpommern and Sachsen-Anhalt in 2015

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Live births in Brandenburg, Mecklenburg-Vorpommern and Sachsen-Anhalt in 2015
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Live births in Brandenburg, Mecklenburg-Vorpommern and Sachsen-Anhalt in 2015
```

**Model must answer**

```json
{
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern", "Sachsen-Anhalt"],
  "temporal": [2015],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Brandenburg, Mecklenburg-Vorpommern, Sachsen-Anhalt in [2015]",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern", "Sachsen-Anhalt"],
  "temporal": [2015],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d46 · DIRECT_LOOKUP

> How many residents did Niedersachsen have in 2012?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many residents did Niedersachsen have in 2012?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many residents did Niedersachsen have in 2012?
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen"],
  "temporal": [2012],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Niedersachsen in [2012]",
  "entity_type": "state",
  "spatial": ["Niedersachsen"],
  "temporal": [2012],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d47 · DIRECT_LOOKUP

> Marriages and live births in Hamburg and Schleswig-Holstein, 2005

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · DIRECT_LOOKUP → presence | [sql_DIRECT_LOOKUP_presence.txt](prompts/sql_DIRECT_LOOKUP_presence.txt) |

### 1 · Classify

**Model sees**

```text
Marriages and live births in Hamburg and Schleswig-Holstein, 2005
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Marriages and live births in Hamburg and Schleswig-Holstein, 2005
```

**Model must answer**

```json
{
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "temporal": [2005],
  "attributes": ["marriages", "live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages, live_births of Hamburg, Schleswig-Holstein in [2005]",
  "entity_type": "state",
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "temporal": [2005],
  "attributes": ["marriages", "live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · DIRECT_LOOKUP → presence

*runs only when the fetch found no rows for ['Hamburg']*

**Model sees**

```json
{
  "question": "Which of these state names have any row at all: ['Hamburg']",
  "entity_type": "state",
  "spatial": ["Hamburg"]
}
```

**Model must answer**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

---

## d48 · DIRECT_LOOKUP

> What were the population figures of Thüringen from 2017 to 2019?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What were the population figures of Thüringen from 2017 to 2019?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What were the population figures of Thüringen from 2017 to 2019?
```

**Model must answer**

```json
{
  "spatial": ["Thüringen"],
  "temporal": [2017, 2018, 2019],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Thüringen in [2017, 2018, 2019]",
  "entity_type": "state",
  "spatial": ["Thüringen"],
  "temporal": [2017, 2018, 2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d49 · DIRECT_LOOKUP

> Population of Nordrhein-Westfalen and Rheinland-Pfalz in 2013

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 4 | SQL · fetch (answering Agent-1) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |
| 5 | SQL · fetch (answering Agent-2) | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of Nordrhein-Westfalen and Rheinland-Pfalz in 2013
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of Nordrhein-Westfalen and Rheinland-Pfalz in 2013
```

**Model must answer**

```json
{
  "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"],
  "temporal": [2013],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Nordrhein-Westfalen, Rheinland-Pfalz in [2013]",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"],
  "temporal": [2013],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 4 · SQL · fetch (answering Agent-1)

*this agent answering Agent-1's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-1 asks for population of Nordrhein-Westfalen, Rheinland-Pfalz in [2013]",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"],
  "temporal": [2013],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### 5 · SQL · fetch (answering Agent-2)

*this agent answering Agent-2's :missing-slots ask*

**Model sees**

```json
{
  "question": "Agent-2 asks for population of Nordrhein-Westfalen, Rheinland-Pfalz in [2013]",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"],
  "temporal": [2013],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d50 · DIRECT_LOOKUP · validation

> Live births for all states in 2000

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Live births for all states in 2000
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Live births for all states in 2000
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2000],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2000]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"],
  "temporal": [2000],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d51 · DIRECT_LOOKUP

> Population of Hessen 2015-2015

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of Hessen 2015-2015
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of Hessen 2015-2015
```

**Model must answer**

```json
{
  "spatial": ["Hessen"],
  "temporal": [2015],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Hessen in [2015]",
  "entity_type": "state",
  "spatial": ["Hessen"],
  "temporal": [2015],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d52 · DIRECT_LOOKUP

> Live births in Sachsen from 2019 back to 2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Live births in Sachsen from 2019 back to 2016
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Live births in Sachsen from 2019 back to 2016
```

**Model must answer**

```json
{
  "spatial": ["Sachsen"],
  "temporal": [2016, 2017, 2018, 2019],
  "attributes": ["live_births"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Sachsen in [2016, 2017, 2018, 2019]",
  "entity_type": "state",
  "spatial": ["Sachsen"],
  "temporal": [2016, 2017, 2018, 2019],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d53 · DIRECT_LOOKUP

> Marriages in Brandenburg and brandenburg in 2010

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Marriages in Brandenburg and Brandenburg in 2010
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Marriages in Brandenburg and Brandenburg in 2010
```

**Model must answer**

```json
{
  "spatial": ["Brandenburg"],
  "temporal": [2010],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Brandenburg in [2010]",
  "entity_type": "state",
  "spatial": ["Brandenburg"],
  "temporal": [2010],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d54 · DIRECT_LOOKUP

> What were births, people and marriages in Saarland in 2003?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What were births, people and marriages in Saarland in 2003?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What were births, people and marriages in Saarland in 2003?
```

**Model must answer**

```json
{
  "spatial": ["Saarland"],
  "temporal": [2003],
  "attributes": ["live_births", "population", "marriages"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births, population, marriages of Saarland in [2003]",
  "entity_type": "state",
  "spatial": ["Saarland"],
  "temporal": [2003],
  "attributes": ["live_births", "population", "marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births, sd.population AS population, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d55 · DIRECT_LOOKUP

> POPULATION OF THUERINGEN IN 2014

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
POPULATION OF Thüringen IN 2014
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: POPULATION OF Thüringen IN 2014
```

**Model must answer**

```json
{
  "spatial": ["Thüringen"],
  "temporal": [2014],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Thüringen in [2014]",
  "entity_type": "state",
  "spatial": ["Thüringen"],
  "temporal": [2014],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d56 · DIRECT_LOOKUP

> population sachsen 2009 2011 2013

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
population Sachsen 2009 2011 2013
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: population Sachsen 2009 2011 2013
```

**Model must answer**

```json
{
  "spatial": ["Sachsen"],
  "temporal": [2009, 2011, 2013],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Sachsen in [2009, 2011, 2013]",
  "entity_type": "state",
  "spatial": ["Sachsen"],
  "temporal": [2009, 2011, 2013],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d57 · DIRECT_LOOKUP

> How many marriages did Hessen have?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
How many marriages did Hessen have?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many marriages did Hessen have?
```

**Model must answer**

```json
{
  "spatial": ["Hessen"],
  "temporal": [],
  "attributes": ["marriages"],
  "entity_type": "state"
}
```

---

## d58 · DIRECT_LOOKUP

> Give me data for Niedersachsen in 2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me data for Niedersachsen in 2016
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me data for Niedersachsen in 2016
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen"],
  "temporal": [2016],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Niedersachsen in [2016]",
  "entity_type": "state",
  "spatial": ["Niedersachsen"],
  "temporal": [2016],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d59 · DIRECT_LOOKUP

> Population of Mecklenburg-Vorpommern and Sachsen-Anhalt in 1990 and in 2019

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of Mecklenburg-Vorpommern and Sachsen-Anhalt in 1990 and in 2019
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of Mecklenburg-Vorpommern and Sachsen-Anhalt in 1990 and in 2019
```

**Model must answer**

```json
{
  "spatial": ["Mecklenburg-Vorpommern", "Sachsen-Anhalt"],
  "temporal": [1990, 2019],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Mecklenburg-Vorpommern, Sachsen-Anhalt in [1990, 2019]",
  "entity_type": "state",
  "spatial": ["Mecklenburg-Vorpommern", "Sachsen-Anhalt"],
  "temporal": [1990, 2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d60 · DIRECT_LOOKUP · validation

> How many people lived in Germany's federal states in 2011?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many people lived in Germany's federal states in 2011?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many people lived in Germany's federal states in 2011?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2011],
  "attributes": ["population"],
  "entity_type": "state"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2011]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"],
  "temporal": [2011],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d62 · DIRECT_LOOKUP

> What was the combined population of Sachsen and Sachsen-Anhalt in 2017?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What was the combined population of Sachsen and Sachsen-Anhalt in 2017?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What was the combined population of Sachsen and Sachsen-Anhalt in 2017?
```

**Model must answer**

```json
{
  "spatial": ["Sachsen", "Sachsen-Anhalt"],
  "temporal": [2017],
  "attributes": ["population"],
  "entity_type": "state",
  "aggregate": "sum"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Sachsen, Sachsen-Anhalt in [2017]",
  "entity_type": "state",
  "spatial": ["Sachsen", "Sachsen-Anhalt"],
  "temporal": [2017],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d63 · DIRECT_LOOKUP

> How many marriages were there in Hamburg and Bremen together in 2016?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
How many marriages were there in Hamburg and Bremen together in 2016?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: How many marriages were there in Hamburg and Bremen together in 2016?
```

**Model must answer**

```json
{
  "spatial": ["Hamburg", "Bremen"],
  "temporal": [2016],
  "attributes": ["marriages"],
  "entity_type": "state",
  "aggregate": "sum"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch marriages of Hamburg, Bremen in [2016]",
  "entity_type": "state",
  "spatial": ["Hamburg", "Bremen"],
  "temporal": [2016],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d64 · DIRECT_LOOKUP

> Total live births of Niedersachsen, Bremen and Hamburg from 2015 to 2017

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Total live births of Niedersachsen, Bremen and Hamburg from 2015 to 2017
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Total live births of Niedersachsen, Bremen and Hamburg from 2015 to 2017
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen", "Bremen", "Hamburg"],
  "temporal": [2015, 2016, 2017],
  "attributes": ["live_births"],
  "entity_type": "state",
  "aggregate": "sum"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch live_births of Niedersachsen, Bremen, Hamburg in [2015, 2016, 2017]",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Bremen", "Hamburg"],
  "temporal": [2015, 2016, 2017],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d66 · DIRECT_LOOKUP

> cumulative population of all german states in 2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
cumulative population of all german states in 2016
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: cumulative population of all german states in 2016
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2016],
  "attributes": ["population"],
  "entity_type": "state",
  "aggregate": "sum"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2016]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"],
  "temporal": [2016],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d67 · DIRECT_LOOKUP

> Population of Saarland plus Rheinland-Pfalz in 2018

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |
| 3 | SQL · DIRECT_LOOKUP → fetch | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Population of Saarland plus Rheinland-Pfalz in 2018
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Population of Saarland plus Rheinland-Pfalz in 2018
```

**Model must answer**

```json
{
  "spatial": ["Saarland", "Rheinland-Pfalz"],
  "temporal": [2018],
  "attributes": ["population"],
  "entity_type": "state",
  "aggregate": "sum"
}
```

### 3 · SQL · DIRECT_LOOKUP → fetch

**Model sees**

```json
{
  "question": "Fetch population of Saarland, Rheinland-Pfalz in [2018]",
  "entity_type": "state",
  "spatial": ["Saarland", "Rheinland-Pfalz"],
  "temporal": [2018],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## d68 · DIRECT_LOOKUP

> What is the combined population of Hessen and Bayern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_DIRECT_LOOKUP.txt](prompts/extract_DIRECT_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
What is the combined population of Hessen and Bayern?
```

**Model must answer**

```json
{"query_type": "DIRECT_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What is the combined population of Hessen and Bayern?
```

**Model must answer**

```json
{
  "spatial": ["Hessen", "Bayern"],
  "temporal": [],
  "attributes": ["population"],
  "entity_type": "state",
  "aggregate": "sum"
}
```

---

# geometry

## g01 · GEOMETRY_LOOKUP

> Show the boundary of Hessen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show the boundary of Hessen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show the boundary of Hessen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hessen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hessen']",
  "entity_type": "state",
  "spatial": ["Hessen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g02 · GEOMETRY_LOOKUP

> What is the shape of Thüringen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What is the shape of Thüringen?
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What is the shape of Thüringen?
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Thüringen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Thüringen']",
  "entity_type": "state",
  "spatial": ["Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g03 · GEOMETRY_LOOKUP

> Give me the geometry of Köln

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me the geometry of Cologne
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the geometry of Cologne
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Cologne", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Cologne']",
  "entity_type": "city",
  "spatial": ["Cologne"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g04 · GEOMETRY_LOOKUP

> Where is Leipzig located? Give me its coordinates.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Where is Leipzig located? Give me its coordinates.
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Where is Leipzig located? Give me its coordinates.
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Leipzig", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Leipzig']",
  "entity_type": "city",
  "spatial": ["Leipzig"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g05 · GEOMETRY_LOOKUP

> WKT for Niedersachsen and Bremen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
WKT for Niedersachsen and Bremen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: WKT for Niedersachsen and Bremen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Niedersachsen", "entity_type": "state"}, {"entity_name": "Bremen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bremen', 'Niedersachsen']",
  "entity_type": "state",
  "spatial": ["Bremen", "Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g06 · GEOMETRY_LOOKUP

> Show me the outline of Mecklenburg-Vorpommern

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show me the outline of Mecklenburg-Vorpommern
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show me the outline of Mecklenburg-Vorpommern
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Mecklenburg-Vorpommern", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Mecklenburg-Vorpommern']",
  "entity_type": "state",
  "spatial": ["Mecklenburg-Vorpommern"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g07 · GEOMETRY_LOOKUP

> What are the coordinates of Dresden and Erfurt?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What are the coordinates of Dresden and Erfurt?
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What are the coordinates of Dresden and Erfurt?
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Dresden", "entity_type": "city"}, {"entity_name": "Erfurt", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Dresden', 'Erfurt']",
  "entity_type": "city",
  "spatial": ["Dresden", "Erfurt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g08 · GEOMETRY_LOOKUP

> Geometry of the city of Hamburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Geometry of the city of Hamburg
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Geometry of the city of Hamburg
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hamburg", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Hamburg']",
  "entity_type": "city",
  "spatial": ["Hamburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g09 · GEOMETRY_LOOKUP

> Give me the polygons of Saarland and Rheinland-Pfalz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me the polygons of Saarland and Rheinland-Pfalz
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the polygons of Saarland and Rheinland-Pfalz
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Saarland", "entity_type": "state"}, {"entity_name": "Rheinland-Pfalz", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Rheinland-Pfalz', 'Saarland']",
  "entity_type": "state",
  "spatial": ["Rheinland-Pfalz", "Saarland"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g10 · GEOMETRY_LOOKUP · validation

> Point location of Stuttgart

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Point location of Stuttgart
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Point location of Stuttgart
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Stuttgart", "entity_type": "city"}]
}
```

---

## g11 · GEOMETRY_LOOKUP

> Boundaries of Brandenburg, Berlin and Sachsen-Anhalt

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Boundaries of Brandenburg, Berlin and Sachsen-Anhalt
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Boundaries of Brandenburg, Berlin and Sachsen-Anhalt
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Brandenburg", "entity_type": "state"}, {"entity_name": "Berlin", "entity_type": "state"}, {"entity_name": "Sachsen-Anhalt", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Berlin', 'Brandenburg', 'Sachsen-Anhalt']",
  "entity_type": "state",
  "spatial": ["Berlin", "Brandenburg", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g12 · GEOMETRY_LOOKUP

> Show the centroid of Frankfurt

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show the centroid of Frankfurt
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show the centroid of Frankfurt
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Frankfurt", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Frankfurt']",
  "entity_type": "city",
  "spatial": ["Frankfurt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g13 · GEOMETRY_LOOKUP

> geometry of muenchen and nuernberg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
geometry of Munich and Nuremberg
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: geometry of Munich and Nuremberg
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Munich", "entity_type": "city"}, {"entity_name": "Nuremberg", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Munich', 'Nuremberg']",
  "entity_type": "city",
  "spatial": ["Munich", "Nuremberg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g14 · GEOMETRY_LOOKUP

> Give me the shapes of Hessen and Kassel

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me the shapes of Hessen and Kassel
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the shapes of Hessen and Kassel
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hessen", "entity_type": "state"}, {"entity_name": "Kassel", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Kassel']",
  "entity_type": "city",
  "spatial": ["Kassel"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g15 · GEOMETRY_LOOKUP

> Map the border of Schleswig-Holstein

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Map the border of Schleswig-Holstein
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Map the border of Schleswig-Holstein
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Schleswig-Holstein", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Schleswig-Holstein']",
  "entity_type": "state",
  "spatial": ["Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g16 · GEOMETRY_LOOKUP

> What does the boundary of Baden-Württemberg look like as WKT?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
What does the boundary of Baden-Württemberg look like as WKT?
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What does the boundary of Baden-Württemberg look like as WKT?
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Baden-Württemberg", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Baden-Württemberg']",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g17 · GEOMETRY_LOOKUP

> Coordinates of Hannover, the city of Bremen and Kiel

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Coordinates of Hannover, the city of Bremen and Kiel
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Coordinates of Hannover, the city of Bremen and Kiel
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hannover", "entity_type": "city"}, {"entity_name": "Bremen", "entity_type": "city"}, {"entity_name": "Kiel", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bremen', 'Hannover', 'Kiel']",
  "entity_type": "city",
  "spatial": ["Bremen", "Hannover", "Kiel"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g18 · GEOMETRY_LOOKUP

> Return the geometry for Nordrhein-Westfalen, Düsseldorf and Dortmund

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Return the geometry for Nordrhein-Westfalen, Düsseldorf and Dortmund
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Return the geometry for Nordrhein-Westfalen, Düsseldorf and Dortmund
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Nordrhein-Westfalen", "entity_type": "state"}, {"entity_name": "Düsseldorf", "entity_type": "city"}, {"entity_name": "Dortmund", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Nordrhein-Westfalen']",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Dortmund', 'Düsseldorf']",
  "entity_type": "city",
  "spatial": ["Dortmund", "Düsseldorf"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g19 · GEOMETRY_LOOKUP

> Show shapes of Sachsen and Thüringen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show shapes of Sachsen and Thüringen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show shapes of Sachsen and Thüringen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Sachsen", "entity_type": "state"}, {"entity_name": "Thüringen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Sachsen', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Sachsen", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g20 · GEOMETRY_LOOKUP · validation

> Where exactly is Magdeburg? I need its point geometry.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Where exactly is Magdeburg? I need its point geometry.
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Where exactly is Magdeburg? I need its point geometry.
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Magdeburg", "entity_type": "city"}]
}
```

---

## g21 · GEOMETRY_LOOKUP

> Give me the boundary of Hesse

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Give me the boundary of Hesse
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the boundary of Hesse
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hessen", "entity_type": "state"}]
}
```

---

## g22 · GEOMETRY_LOOKUP

> Shape of Rostock and Potsdam

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Shape of Rostock and Potsdam
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Shape of Rostock and Potsdam
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Rostock", "entity_type": "city"}, {"entity_name": "Potsdam", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Potsdam', 'Rostock']",
  "entity_type": "city",
  "spatial": ["Potsdam", "Rostock"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g23 · GEOMETRY_LOOKUP

> Show the shapes of all federal states

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show the shapes of all federal states
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show the shapes of all federal states
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Baden-Württemberg", "entity_type": "state"}, {"entity_name": "Bayern", "entity_type": "state"}, {"entity_name": "Berlin", "entity_type": "state"}, {"entity_name": "Brandenburg", "entity_type": "state"}, {"entity_name": "Bremen", "entity_type": "state"}, {"entity_name": "Hamburg", "entity_type": "state"}, {"entity_name": "Hessen", "entity_type": "state"}, {"entity_name": "Mecklenburg-Vorpommern", "entity_type": "state"}, {"entity_name": "Niedersachsen", "entity_type": "state"}, {"entity_name": "Nordrhein-Westfalen", "entity_type": "state"}, {"entity_name": "Rheinland-Pfalz", "entity_type": "state"}, {"entity_name": "Saarland", "entity_type": "state"}, {"entity_name": "Sachsen", "entity_type": "state"}, {"entity_name": "Sachsen-Anhalt", "entity_type": "state"}, {"entity_name": "Schleswig-Holstein", "entity_type": "state"}, {"entity_name": "Thüringen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Baden-Württemberg', 'Bayern', 'Berlin', 'Brandenburg', 'Bremen', 'Hamburg', 'Hessen', 'Mecklenburg-Vorpommern', 'Niedersachsen', 'Nordrhein-Westfalen', 'Rheinland-Pfalz', 'Saarland', 'Sachsen', 'Sachsen-Anhalt', 'Schleswig-Holstein', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g24 · GEOMETRY_LOOKUP

> Boundary of Rheinland-Pfalz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Boundary of Rheinland-Pfalz
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Boundary of Rheinland-Pfalz
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Rheinland-Pfalz", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Rheinland-Pfalz']",
  "entity_type": "state",
  "spatial": ["Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g25 · GEOMETRY_LOOKUP

> Coordinates of Bamberg and Erlangen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Coordinates of Bamberg and Erlangen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Coordinates of Bamberg and Erlangen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Bamberg", "entity_type": "city"}, {"entity_name": "Erlangen", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bamberg', 'Erlangen']",
  "entity_type": "city",
  "spatial": ["Bamberg", "Erlangen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g26 · GEOMETRY_LOOKUP

> Give me the geometry of the city of Bremen and the state of Niedersachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me the geometry of the city of Bremen and the state of Niedersachsen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the geometry of the city of Bremen and the state of Niedersachsen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Bremen", "entity_type": "city"}, {"entity_name": "Niedersachsen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bremen']",
  "entity_type": "city",
  "spatial": ["Bremen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Niedersachsen']",
  "entity_type": "state",
  "spatial": ["Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g27 · GEOMETRY_LOOKUP

> WKT for Sachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
WKT for Sachsen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: WKT for Sachsen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Sachsen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Sachsen']",
  "entity_type": "state",
  "spatial": ["Sachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g28 · GEOMETRY_LOOKUP

> Where is Wiesbaden located?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Where is Wiesbaden located?
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Where is Wiesbaden located?
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Wiesbaden", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Wiesbaden']",
  "entity_type": "city",
  "spatial": ["Wiesbaden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g29 · GEOMETRY_LOOKUP

> Polygon of Baden-Württemberg and point of Karlsruhe

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Polygon of Baden-Württemberg and point of Karlsruhe
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Polygon of Baden-Württemberg and point of Karlsruhe
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Baden-Württemberg", "entity_type": "state"}, {"entity_name": "Karlsruhe", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Karlsruhe']",
  "entity_type": "city",
  "spatial": ["Karlsruhe"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g30 · GEOMETRY_LOOKUP · validation

> Shape of Lower Saxony

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Shape of Lower Saxony
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Shape of Lower Saxony
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Niedersachsen", "entity_type": "state"}]
}
```

---

## g31 · GEOMETRY_LOOKUP

> Geometries of Brandenburg, Sachsen and Thüringen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Geometries of Brandenburg, Sachsen and Thüringen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Geometries of Brandenburg, Sachsen and Thüringen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Brandenburg", "entity_type": "state"}, {"entity_name": "Sachsen", "entity_type": "state"}, {"entity_name": "Thüringen", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Sachsen', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Sachsen", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g32 · GEOMETRY_LOOKUP

> coordinates of koeln and duesseldorf

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
coordinates of Cologne and Düsseldorf
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: coordinates of Cologne and Düsseldorf
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Cologne", "entity_type": "city"}, {"entity_name": "Düsseldorf", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Cologne', 'Düsseldorf']",
  "entity_type": "city",
  "spatial": ["Cologne", "Düsseldorf"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g33 · GEOMETRY_LOOKUP

> Boundary polygons of Hamburg and Schleswig-Holstein

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Boundary polygons of Hamburg and Schleswig-Holstein
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Boundary polygons of Hamburg and Schleswig-Holstein
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hamburg", "entity_type": "state"}, {"entity_name": "Schleswig-Holstein", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hamburg', 'Schleswig-Holstein']",
  "entity_type": "state",
  "spatial": ["Hamburg", "Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g34 · GEOMETRY_LOOKUP

> Centroid of Stendal and Wernigerode

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Centroid of Stendal and Wernigerode
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Centroid of Stendal and Wernigerode
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Stendal", "entity_type": "city"}, {"entity_name": "Wernigerode", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Stendal', 'Wernigerode']",
  "entity_type": "city",
  "spatial": ["Stendal", "Wernigerode"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g35 · GEOMETRY_LOOKUP

> Outline of Saxony

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Outline of Saxony
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Outline of Saxony
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Sachsen", "entity_type": "state"}]
}
```

---

## g36 · GEOMETRY_LOOKUP

> Point locations of Freiburg im Breisgau and Konstanz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Point locations of Freiburg im Breisgau and Konstanz
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Point locations of Freiburg im Breisgau and Konstanz
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Freiburg im Breisgau", "entity_type": "city"}, {"entity_name": "Konstanz", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Freiburg im Breisgau', 'Konstanz']",
  "entity_type": "city",
  "spatial": ["Freiburg im Breisgau", "Konstanz"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g37 · GEOMETRY_LOOKUP

> Geometry of Cottbus and Eberswalde

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Geometry of Cottbus and Eberswalde
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Geometry of Cottbus and Eberswalde
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Cottbus", "entity_type": "city"}, {"entity_name": "Eberswalde", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Cottbus', 'Eberswalde']",
  "entity_type": "city",
  "spatial": ["Cottbus", "Eberswalde"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g38 · GEOMETRY_LOOKUP

> What does Schleswig-Holstein look like on a map? Give me its geometry.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
What does Schleswig-Holstein look like on a map? Give me its geometry.
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: What does Schleswig-Holstein look like on a map? Give me its geometry.
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Schleswig-Holstein", "entity_type": "state"}]
}
```

---

## g39 · GEOMETRY_LOOKUP

> Geometry of Kassel, Fulda and Marburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Geometry of Kassel, Fulda and Marburg
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Geometry of Kassel, Fulda and Marburg
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Kassel", "entity_type": "city"}, {"entity_name": "Fulda", "entity_type": "city"}, {"entity_name": "Marburg", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Fulda', 'Kassel', 'Marburg']",
  "entity_type": "city",
  "spatial": ["Fulda", "Kassel", "Marburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g40 · GEOMETRY_LOOKUP · validation

> WKT of Saarland and Saarlouis

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
WKT of Saarland and Saarlouis
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: WKT of Saarland and Saarlouis
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Saarland", "entity_type": "state"}, {"entity_name": "Saarlouis", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Saarlouis']",
  "entity_type": "city",
  "spatial": ["Saarlouis"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g41 · GEOMETRY_LOOKUP

> Show the boundaries of Bayern and Baden-Württemberg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Show the boundaries of Bayern and Baden-Württemberg
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Show the boundaries of Bayern and Baden-Württemberg
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Bayern", "entity_type": "state"}, {"entity_name": "Baden-Württemberg", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Baden-Württemberg', 'Bayern']",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g42 · GEOMETRY_LOOKUP

> Coordinates for Oldenburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Coordinates for Oldenburg
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Coordinates for Oldenburg
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Oldenburg", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Oldenburg']",
  "entity_type": "city",
  "spatial": ["Oldenburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g43 · GEOMETRY_LOOKUP

> Shape of the city of Hamburg and of Lübeck

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Shape of the city of Hamburg and of Lübeck
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Shape of the city of Hamburg and of Lübeck
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hamburg", "entity_type": "city"}, {"entity_name": "Lübeck", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Hamburg', 'Lübeck']",
  "entity_type": "city",
  "spatial": ["Hamburg", "Lübeck"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g44 · GEOMETRY_LOOKUP

> Give me the boundary of Thuringia

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
Give me the boundary of Thuringia
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the boundary of Thuringia
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Thüringen", "entity_type": "state"}]
}
```

---

## g45 · GEOMETRY_LOOKUP

> Geometries of Nordrhein-Westfalen, Hessen and Rheinland-Pfalz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Geometries of Nordrhein-Westfalen, Hessen and Rheinland-Pfalz
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Geometries of Nordrhein-Westfalen, Hessen and Rheinland-Pfalz
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Nordrhein-Westfalen", "entity_type": "state"}, {"entity_name": "Hessen", "entity_type": "state"}, {"entity_name": "Rheinland-Pfalz", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hessen', 'Nordrhein-Westfalen', 'Rheinland-Pfalz']",
  "entity_type": "state",
  "spatial": ["Hessen", "Nordrhein-Westfalen", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g46 · GEOMETRY_LOOKUP

> Give me the geometries of Hamburg the state and Hamburg the city

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Give me the geometries of Hamburg the state and Hamburg the city
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the geometries of Hamburg the state and Hamburg the city
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Hamburg", "entity_type": "state"}, {"entity_name": "Hamburg", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hamburg']",
  "entity_type": "state",
  "spatial": ["Hamburg"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g47 · GEOMETRY_LOOKUP

> shape of bremen city

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
shape of Bremen city
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: shape of Bremen city
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Bremen", "entity_type": "city"}]
}
```

---

## g48 · GEOMETRY_LOOKUP

> boundary of Berlin

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
boundary of Berlin
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: boundary of Berlin
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Berlin", "entity_type": "state"}]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Berlin']",
  "entity_type": "state",
  "spatial": ["Berlin"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## g49 · GEOMETRY_LOOKUP

> Coordinates of Essen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Coordinates of Essen
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: Coordinates of Essen
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Essen", "entity_type": "city"}]
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Essen']",
  "entity_type": "city",
  "spatial": ["Essen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

---

## g50 · GEOMETRY_LOOKUP · validation

> WKT for Frankfurt

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
WKT for Frankfurt
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: WKT for Frankfurt
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Frankfurt", "entity_type": "city"}]
}
```

---

## g51 · GEOMETRY_LOOKUP

> geometry of baden wuerttemberg and bayern

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_GEOMETRY_LOOKUP.txt](prompts/extract_GEOMETRY_LOOKUP.txt) |

### 1 · Classify

**Model sees**

```text
geometry of Baden-Württemberg and Bayern
```

**Model must answer**

```json
{"query_type": "GEOMETRY_LOOKUP"}
```

### 2 · Extract

**Model sees**

```text
Query: geometry of Baden-Württemberg and Bayern
```

**Model must answer**

```json
{
  "entities": [{"entity_name": "Baden-Württemberg", "entity_type": "state"}, {"entity_name": "Bayern", "entity_type": "state"}]
}
```

---

# operation

## o01 · SPATIAL_OPERATION

> Combine Hessen and Thüringen into one boundary

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Combine Hessen and Thüringen into one boundary
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Combine Hessen and Thüringen into one boundary
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Hessen", "Thüringen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hessen', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Hessen", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Hessen", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o02 · SPATIAL_OPERATION

> Merge Niedersachsen and Bremen into a single shape

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Merge Niedersachsen and Bremen into a single shape
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Niedersachsen and Bremen into a single shape
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Niedersachsen", "Bremen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Niedersachsen", "Bremen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o03 · SPATIAL_OPERATION

> What is the union of Rheinland-Pfalz and Saarland?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
What is the union of Rheinland-Pfalz and Saarland?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: What is the union of Rheinland-Pfalz and Saarland?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Rheinland-Pfalz", "Saarland"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Rheinland-Pfalz", "Saarland"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o04 · SPATIAL_OPERATION

> One combined area for Sachsen, Sachsen-Anhalt and Thüringen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
One combined area for Sachsen, Sachsen-Anhalt and Thüringen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: One combined area for Sachsen, Sachsen-Anhalt and Thüringen
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Sachsen", "Sachsen-Anhalt", "Thüringen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Sachsen', 'Sachsen-Anhalt', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Sachsen", "Sachsen-Anhalt", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Sachsen", "Sachsen-Anhalt", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o05 · SPATIAL_OPERATION

> Join Berlin and Brandenburg into one polygon

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Join Berlin and Brandenburg into one polygon
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Join Berlin and Brandenburg into one polygon
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Berlin", "Brandenburg"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Berlin', 'Brandenburg']",
  "entity_type": "state",
  "spatial": ["Berlin", "Brandenburg"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Berlin", "Brandenburg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o06 · SPATIAL_OPERATION

> What area do Hessen and Bayern have in common?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
What area do Hessen and Bayern have in common?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: What area do Hessen and Bayern have in common?
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Hessen", "Bayern"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bayern', 'Hessen']",
  "entity_type": "state",
  "spatial": ["Bayern", "Hessen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Hessen", "Bayern"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o07 · SPATIAL_OPERATION

> Intersection of Nordrhein-Westfalen and Niedersachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Intersection of Nordrhein-Westfalen and Niedersachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Intersection of Nordrhein-Westfalen and Niedersachsen
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Nordrhein-Westfalen", "Niedersachsen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Niedersachsen', 'Nordrhein-Westfalen']",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Nordrhein-Westfalen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Nordrhein-Westfalen", "Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o08 · SPATIAL_OPERATION

> Which region is shared by Brandenburg and Mecklenburg-Vorpommern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which region is shared by Brandenburg and Mecklenburg-Vorpommern?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which region is shared by Brandenburg and Mecklenburg-Vorpommern?
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Mecklenburg-Vorpommern']",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o09 · SPATIAL_OPERATION

> Overlap between Baden-Württemberg and Rheinland-Pfalz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Overlap between Baden-Württemberg and Rheinland-Pfalz
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Overlap between Baden-Württemberg and Rheinland-Pfalz
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Baden-Württemberg", "Rheinland-Pfalz"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Baden-Württemberg', 'Rheinland-Pfalz']",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Baden-Württemberg", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o10 · SPATIAL_OPERATION · validation

> Niedersachsen without Bremen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |

### 1 · Classify

**Model sees**

```text
Niedersachsen without Bremen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Niedersachsen without Bremen
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Niedersachsen", "Bremen"],
  "entity_type": "state",
  "distance_km": null
}
```

---

## o11 · SPATIAL_OPERATION

> Remove Hamburg from Schleswig-Holstein

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Remove Hamburg from Schleswig-Holstein
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Remove Hamburg from Schleswig-Holstein
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Schleswig-Holstein", "Hamburg"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Schleswig-Holstein", "Hamburg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o12 · SPATIAL_OPERATION

> Show Bayern minus Baden-Württemberg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Show Bayern minus Baden-Württemberg
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Show Bayern minus Baden-Württemberg
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Bayern", "Baden-Württemberg"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Bayern", "Baden-Württemberg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o13 · SPATIAL_OPERATION

> Hessen with Thüringen cut out

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Hessen with Thüringen cut out
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Hessen with Thüringen cut out
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Hessen", "Thüringen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Hessen", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o14 · SPATIAL_OPERATION

> What is left of Sachsen once Sachsen-Anhalt is taken away?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
What is left of Sachsen once Sachsen-Anhalt is taken away?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: What is left of Sachsen once Sachsen-Anhalt is taken away?
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Sachsen", "Sachsen-Anhalt"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Sachsen', 'Sachsen-Anhalt']",
  "entity_type": "state",
  "spatial": ["Sachsen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Sachsen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o15 · SPATIAL_OPERATION

> Areas in Hessen or Rheinland-Pfalz but not in both

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Areas in Hessen or Rheinland-Pfalz but not in both
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Areas in Hessen or Rheinland-Pfalz but not in both
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Hessen", "Rheinland-Pfalz"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hessen', 'Rheinland-Pfalz']",
  "entity_type": "state",
  "spatial": ["Hessen", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Hessen", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o16 · SPATIAL_OPERATION

> Symmetric difference of Thüringen and Sachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Symmetric difference of Thüringen and Sachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Symmetric difference of Thüringen and Sachsen
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Thüringen", "Sachsen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Thüringen", "Sachsen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o17 · SPATIAL_OPERATION

> Which parts belong to exactly one of Niedersachsen and Nordrhein-Westfalen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which parts belong to exactly one of Niedersachsen and Nordrhein-Westfalen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which parts belong to exactly one of Niedersachsen and Nordrhein-Westfalen?
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Niedersachsen", "Nordrhein-Westfalen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Niedersachsen", "Nordrhein-Westfalen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o18 · SPATIAL_OPERATION

> Give me the symmetric difference between Brandenburg and Sachsen-Anhalt

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Give me the symmetric difference between Brandenburg and Sachsen-Anhalt
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the symmetric difference between Brandenburg and Sachsen-Anhalt
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Brandenburg", "Sachsen-Anhalt"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Sachsen-Anhalt']",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Brandenburg", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o19 · SPATIAL_OPERATION

> Which of Hessen and Thüringen lie within 80 km of Frankfurt?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Hessen and Thüringen lie within 80 km of Frankfurt?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Hessen and Thüringen lie within 80 km of Frankfurt?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Frankfurt", "Hessen", "Thüringen"],
  "entity_type": "state",
  "distance_km": 80
}
```

### 3 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Hessen and Thüringen lie within 80 km of Frankfurt?",
  "operation": "BufferWithin",
  "spatial": ["Frankfurt", "Hessen", "Thüringen"],
  "distance_km": 80.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o20 · SPATIAL_OPERATION · validation

> Which of Sachsen and Brandenburg lie within 50 km of Leipzig?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Sachsen and Brandenburg lie within 50 km of Leipzig?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Sachsen and Brandenburg lie within 50 km of Leipzig?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Leipzig", "Sachsen", "Brandenburg"],
  "entity_type": "state",
  "distance_km": 50
}
```

### 3 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Sachsen and Brandenburg lie within 50 km of Leipzig?",
  "operation": "BufferWithin",
  "spatial": ["Leipzig", "Sachsen", "Brandenburg"],
  "distance_km": 50.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o21 · SPATIAL_OPERATION

> Of Bayern and Baden-Württemberg, which are within 120 km of Stuttgart?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Of Bayern and Baden-Württemberg, which are within 120 km of Stuttgart?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Of Bayern and Baden-Württemberg, which are within 120 km of Stuttgart?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Stuttgart", "Bayern", "Baden-Württemberg"],
  "entity_type": "state",
  "distance_km": 120
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Stuttgart']",
  "entity_type": "city",
  "spatial": ["Stuttgart"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Of Bayern and Baden-Württemberg, which are within 120 km of Stuttgart?",
  "operation": "BufferWithin",
  "spatial": ["Stuttgart", "Bayern", "Baden-Württemberg"],
  "distance_km": 120.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o22 · SPATIAL_OPERATION

> Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 5 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Rostock", "Mecklenburg-Vorpommern", "Schleswig-Holstein", "Brandenburg"],
  "entity_type": "state",
  "distance_km": 100
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Rostock']",
  "entity_type": "city",
  "spatial": ["Rostock"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Mecklenburg-Vorpommern', 'Schleswig-Holstein']",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern", "Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 5 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?",
  "operation": "BufferWithin",
  "spatial": ["Rostock", "Mecklenburg-Vorpommern", "Schleswig-Holstein", "Brandenburg"],
  "distance_km": 100.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o23 · SPATIAL_OPERATION

> Merge Bayern and Baden-Württemberg into one area

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Merge Bayern and Baden-Württemberg into one area
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Bayern and Baden-Württemberg into one area
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Bayern", "Baden-Württemberg"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Bayern", "Baden-Württemberg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o24 · SPATIAL_OPERATION

> Union of Niedersachsen, Bremen and Hamburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Union of Niedersachsen, Bremen and Hamburg
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Union of Niedersachsen, Bremen and Hamburg
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Niedersachsen", "Bremen", "Hamburg"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bremen', 'Hamburg', 'Niedersachsen']",
  "entity_type": "state",
  "spatial": ["Bremen", "Hamburg", "Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Niedersachsen", "Bremen", "Hamburg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o25 · SPATIAL_OPERATION

> Combine Sachsen and Brandenburg into a single shape

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Combine Sachsen and Brandenburg into a single shape
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Combine Sachsen and Brandenburg into a single shape
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Sachsen", "Brandenburg"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Sachsen']",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Sachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Sachsen", "Brandenburg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o26 · SPATIAL_OPERATION

> One shape for Rheinland-Pfalz and Nordrhein-Westfalen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
One shape for Rheinland-Pfalz and Nordrhein-Westfalen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: One shape for Rheinland-Pfalz and Nordrhein-Westfalen
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Rheinland-Pfalz", "Nordrhein-Westfalen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Nordrhein-Westfalen', 'Rheinland-Pfalz']",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Rheinland-Pfalz", "Nordrhein-Westfalen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o27 · SPATIAL_OPERATION

> Join Mecklenburg-Vorpommern and Schleswig-Holstein

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Join Mecklenburg-Vorpommern and Schleswig-Holstein
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Join Mecklenburg-Vorpommern and Schleswig-Holstein
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Mecklenburg-Vorpommern', 'Schleswig-Holstein']",
  "entity_type": "state",
  "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o28 · SPATIAL_OPERATION

> What area do Sachsen and Bayern have in common?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
What area do Sachsen and Bayern have in common?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: What area do Sachsen and Bayern have in common?
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Sachsen", "Bayern"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bayern', 'Sachsen']",
  "entity_type": "state",
  "spatial": ["Bayern", "Sachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Sachsen", "Bayern"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o29 · SPATIAL_OPERATION

> Intersection of Hessen and Rheinland-Pfalz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Intersection of Hessen and Rheinland-Pfalz
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Intersection of Hessen and Rheinland-Pfalz
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Hessen", "Rheinland-Pfalz"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Hessen", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o30 · SPATIAL_OPERATION · validation

> Shared area of Brandenburg and Berlin

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Shared area of Brandenburg and Berlin
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Shared area of Brandenburg and Berlin
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Brandenburg", "Berlin"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Brandenburg", "Berlin"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o31 · SPATIAL_OPERATION

> Overlap between Niedersachsen and Sachsen-Anhalt

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Overlap between Niedersachsen and Sachsen-Anhalt
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Overlap between Niedersachsen and Sachsen-Anhalt
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Niedersachsen", "Sachsen-Anhalt"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Niedersachsen', 'Sachsen-Anhalt']",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Niedersachsen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o32 · SPATIAL_OPERATION

> Show Nordrhein-Westfalen without Niedersachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Show Nordrhein-Westfalen without Niedersachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Show Nordrhein-Westfalen without Niedersachsen
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Nordrhein-Westfalen", "Niedersachsen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Nordrhein-Westfalen", "Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o33 · SPATIAL_OPERATION

> Remove Saarland from Rheinland-Pfalz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Remove Saarland from Rheinland-Pfalz
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Remove Saarland from Rheinland-Pfalz
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Rheinland-Pfalz", "Saarland"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Rheinland-Pfalz", "Saarland"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o34 · SPATIAL_OPERATION

> Thüringen with Sachsen cut away

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Thüringen with Sachsen cut away
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Thüringen with Sachsen cut away
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Thüringen", "Sachsen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Thüringen", "Sachsen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o35 · SPATIAL_OPERATION

> Subtract Hamburg from Niedersachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Subtract Hamburg from Niedersachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Subtract Hamburg from Niedersachsen
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Niedersachsen", "Hamburg"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hamburg', 'Niedersachsen']",
  "entity_type": "state",
  "spatial": ["Hamburg", "Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Niedersachsen", "Hamburg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o36 · SPATIAL_OPERATION

> What remains of Hessen after taking out Bayern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
What remains of Hessen after taking out Bayern?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: What remains of Hessen after taking out Bayern?
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Hessen", "Bayern"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Hessen", "Bayern"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o37 · SPATIAL_OPERATION

> Take Mecklenburg-Vorpommern away from Brandenburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Take Mecklenburg-Vorpommern away from Brandenburg
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Take Mecklenburg-Vorpommern away from Brandenburg
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o38 · SPATIAL_OPERATION

> Symmetric difference between Bayern and Thüringen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Symmetric difference between Bayern and Thüringen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Symmetric difference between Bayern and Thüringen
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Bayern", "Thüringen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bayern', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Bayern", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Bayern", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o39 · SPATIAL_OPERATION

> Areas that belong to Sachsen or Sachsen-Anhalt but not both

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Areas that belong to Sachsen or Sachsen-Anhalt but not both
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Areas that belong to Sachsen or Sachsen-Anhalt but not both
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Sachsen", "Sachsen-Anhalt"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Sachsen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o40 · SPATIAL_OPERATION · validation

> Which parts lie in exactly one of Hessen and Niedersachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which parts lie in exactly one of Hessen and Niedersachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which parts lie in exactly one of Hessen and Niedersachsen?
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Hessen", "Niedersachsen"],
  "entity_type": "state",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hessen', 'Niedersachsen']",
  "entity_type": "state",
  "spatial": ["Hessen", "Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Hessen", "Niedersachsen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o41 · SPATIAL_OPERATION

> Which of Niedersachsen and Sachsen-Anhalt lie within 60 km of Braunschweig?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Niedersachsen and Sachsen-Anhalt lie within 60 km of Braunschweig?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Niedersachsen and Sachsen-Anhalt lie within 60 km of Braunschweig?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Braunschweig", "Niedersachsen", "Sachsen-Anhalt"],
  "entity_type": "state",
  "distance_km": 60
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Braunschweig']",
  "entity_type": "city",
  "spatial": ["Braunschweig"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Niedersachsen and Sachsen-Anhalt lie within 60 km of Braunschweig?",
  "operation": "BufferWithin",
  "spatial": ["Braunschweig", "Niedersachsen", "Sachsen-Anhalt"],
  "distance_km": 60.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o42 · SPATIAL_OPERATION

> Which of Bayern and Sachsen are within 100 km of Nürnberg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Bayern and Sachsen are within 100 km of Nuremberg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Bayern and Sachsen are within 100 km of Nuremberg?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Nuremberg", "Bayern", "Sachsen"],
  "entity_type": "state",
  "distance_km": 100
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Nuremberg']",
  "entity_type": "city",
  "spatial": ["Nuremberg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Bayern and Sachsen are within 100 km of Nürnberg?",
  "operation": "BufferWithin",
  "spatial": ["Nuremberg", "Bayern", "Sachsen"],
  "distance_km": 100.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o43 · SPATIAL_OPERATION

> Of Hessen and Rheinland-Pfalz, which lie within 30 km of Mainz?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Of Hessen and Rheinland-Pfalz, which lie within 30 km of Mainz?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Of Hessen and Rheinland-Pfalz, which lie within 30 km of Mainz?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Mainz", "Hessen", "Rheinland-Pfalz"],
  "entity_type": "state",
  "distance_km": 30
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Mainz']",
  "entity_type": "city",
  "spatial": ["Mainz"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Of Hessen and Rheinland-Pfalz, which lie within 30 km of Mainz?",
  "operation": "BufferWithin",
  "spatial": ["Mainz", "Hessen", "Rheinland-Pfalz"],
  "distance_km": 30.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o44 · SPATIAL_OPERATION

> Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 5 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Bremerhaven", "Schleswig-Holstein", "Niedersachsen"],
  "entity_type": "state",
  "distance_km": 50
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bremerhaven']",
  "entity_type": "city",
  "spatial": ["Bremerhaven"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Niedersachsen', 'Schleswig-Holstein']",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 5 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?",
  "operation": "BufferWithin",
  "spatial": ["Bremerhaven", "Schleswig-Holstein", "Niedersachsen"],
  "distance_km": 50.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o45 · SPATIAL_OPERATION

> Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 5 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Erfurt", "Thüringen", "Hessen", "Bayern"],
  "entity_type": "state",
  "distance_km": 80
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Erfurt']",
  "entity_type": "city",
  "spatial": ["Erfurt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bayern', 'Hessen', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Bayern", "Hessen", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 5 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?",
  "operation": "BufferWithin",
  "spatial": ["Erfurt", "Thüringen", "Hessen", "Bayern"],
  "distance_km": 80.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o46 · SPATIAL_OPERATION

> Which of Brandenburg and Sachsen lie within 40 km of Cottbus?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Brandenburg and Sachsen lie within 40 km of Cottbus?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Brandenburg and Sachsen lie within 40 km of Cottbus?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Cottbus", "Brandenburg", "Sachsen"],
  "entity_type": "state",
  "distance_km": 40
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Cottbus']",
  "entity_type": "city",
  "spatial": ["Cottbus"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Brandenburg and Sachsen lie within 40 km of Cottbus?",
  "operation": "BufferWithin",
  "spatial": ["Cottbus", "Brandenburg", "Sachsen"],
  "distance_km": 40.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o47 · SPATIAL_OPERATION

> Which of Nordrhein-Westfalen and Rheinland-Pfalz are within 50 km of Köln?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Nordrhein-Westfalen and Rheinland-Pfalz are within 50 km of Cologne?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Nordrhein-Westfalen and Rheinland-Pfalz are within 50 km of Cologne?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Cologne", "Nordrhein-Westfalen", "Rheinland-Pfalz"],
  "entity_type": "state",
  "distance_km": 50
}
```

### 3 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Nordrhein-Westfalen and Rheinland-Pfalz are within 50 km of Köln?",
  "operation": "BufferWithin",
  "spatial": ["Cologne", "Nordrhein-Westfalen", "Rheinland-Pfalz"],
  "distance_km": 50.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o48 · SPATIAL_OPERATION

> Which of Baden-Württemberg and Rheinland-Pfalz lie within 25 km of Karlsruhe?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Baden-Württemberg and Rheinland-Pfalz lie within 25 km of Karlsruhe?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Baden-Württemberg and Rheinland-Pfalz lie within 25 km of Karlsruhe?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Karlsruhe", "Baden-Württemberg", "Rheinland-Pfalz"],
  "entity_type": "state",
  "distance_km": 25
}
```

### 3 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Baden-Württemberg and Rheinland-Pfalz lie within 25 km of Karlsruhe?",
  "operation": "BufferWithin",
  "spatial": ["Karlsruhe", "Baden-Württemberg", "Rheinland-Pfalz"],
  "distance_km": 25.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o49 · SPATIAL_OPERATION

> Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 5 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Magdeburg", "Sachsen-Anhalt", "Niedersachsen", "Brandenburg"],
  "entity_type": "state",
  "distance_km": 90
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Magdeburg']",
  "entity_type": "city",
  "spatial": ["Magdeburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Niedersachsen', 'Sachsen-Anhalt']",
  "entity_type": "state",
  "spatial": ["Brandenburg", "Niedersachsen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 5 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?",
  "operation": "BufferWithin",
  "spatial": ["Magdeburg", "Sachsen-Anhalt", "Niedersachsen", "Brandenburg"],
  "distance_km": 90.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o50 · SPATIAL_OPERATION · validation

> Which of Hessen and Nordrhein-Westfalen lie within 60 km of Siegen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → buffer_within | [sql_SPATIAL_OPERATION_buffer_within.txt](prompts/sql_SPATIAL_OPERATION_buffer_within.txt) |

### 1 · Classify

**Model sees**

```text
Which of Hessen and Nordrhein-Westfalen lie within 60 km of Siegen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which of Hessen and Nordrhein-Westfalen lie within 60 km of Siegen?
```

**Model must answer**

```json
{
  "operation": "BufferWithin",
  "spatial": ["Siegen", "Hessen", "Nordrhein-Westfalen"],
  "entity_type": "state",
  "distance_km": 60
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Siegen']",
  "entity_type": "city",
  "spatial": ["Siegen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → buffer_within

**Model sees**

```json
{
  "question": "Which of Hessen and Nordrhein-Westfalen lie within 60 km of Siegen?",
  "operation": "BufferWithin",
  "spatial": ["Siegen", "Hessen", "Nordrhein-Westfalen"],
  "distance_km": 60.0
}
```

**Model must answer**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

---

## o51 · SPATIAL_OPERATION

> Merge Bayern and Baden-Württemberg into one area and what cities are inside that area?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · cities inside the new shape | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Merge Bayern and Baden-Württemberg into one area and what cities are inside that area?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Bayern and Baden-Württemberg into one area and what cities are inside that area?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Bayern", "Baden-Württemberg"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · cities inside the new shape

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": []
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## o52 · SPATIAL_OPERATION

> Combine Hessen and Rheinland-Pfalz — which cities lie inside the combined area?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Combine Hessen and Rheinland-Pfalz— which cities lie inside the combined area?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Combine Hessen and Rheinland-Pfalz— which cities lie inside the combined area?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Hessen", "Rheinland-Pfalz"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Hessen", "Rheinland-Pfalz"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o53 · SPATIAL_OPERATION

> Which cities are inside the union of Sachsen-Anhalt and Brandenburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are inside the union of Sachsen-Anhalt and Brandenburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are inside the union of Sachsen-Anhalt and Brandenburg?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Sachsen-Anhalt", "Brandenburg"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Sachsen-Anhalt", "Brandenburg"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o54 · SPATIAL_OPERATION

> Join Niedersachsen and Bremen into one region and list all cities in it

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |

### 1 · Classify

**Model sees**

```text
Join Niedersachsen and Bremen into one region and list all cities in it
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Join Niedersachsen and Bremen into one region and list all cities in it
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Niedersachsen", "Bremen"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

---

## o55 · SPATIAL_OPERATION

> Merge Saxony and Thuringia. Which cities does the merged area contain?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Merge Saxony and Thuringia. Which cities does the merged area contain?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Saxony and Thuringia. Which cities does the merged area contain?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Sachsen", "Thüringen"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Sachsen", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o56 · SPATIAL_OPERATION

> List the cities inside the combined area of Schleswig-Holstein, Hamburg and Mecklenburg-Vorpommern

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
List the cities inside the combined area of Schleswig-Holstein, Hamburg and Mecklenburg-Vorpommern
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: List the cities inside the combined area of Schleswig-Holstein, Hamburg and Mecklenburg-Vorpommern
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Schleswig-Holstein", "Hamburg", "Mecklenburg-Vorpommern"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hamburg', 'Mecklenburg-Vorpommern', 'Schleswig-Holstein']",
  "entity_type": "state",
  "spatial": ["Hamburg", "Mecklenburg-Vorpommern", "Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Schleswig-Holstein", "Hamburg", "Mecklenburg-Vorpommern"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o57 · SPATIAL_OPERATION

> Which cities are in Berlin and Brandenburg together?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are in Berlin and Brandenburg together?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are in Berlin and Brandenburg together?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Berlin", "Brandenburg"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

---

## o58 · SPATIAL_OPERATION

> merge nordrhein westfalen and hessen, then show me the cities inside

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
merge Nordrhein-Westfalen and Hessen, then show me the cities inside
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: merge Nordrhein-Westfalen and Hessen, then show me the cities inside
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Nordrhein-Westfalen", "Hessen"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hessen', 'Nordrhein-Westfalen']",
  "entity_type": "state",
  "spatial": ["Hessen", "Nordrhein-Westfalen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Nordrhein-Westfalen", "Hessen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o59 · SPATIAL_OPERATION

> If you combine Thüringen and Sachsen-Anhalt, which cities are in that area?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
If you combine Thüringen and Sachsen-Anhalt, which cities are in that area?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: If you combine Thüringen and Sachsen-Anhalt, which cities are in that area?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Thüringen", "Sachsen-Anhalt"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Sachsen-Anhalt', 'Thüringen']",
  "entity_type": "state",
  "spatial": ["Sachsen-Anhalt", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Thüringen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o60 · SPATIAL_OPERATION · validation

> Which cities lie in the area shared by Hessen and Bayern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie in the area shared by Hessen and Bayern?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie in the area shared by Hessen and Bayern?
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Hessen", "Bayern"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

---

## o61 · SPATIAL_OPERATION

> Cities in the overlap of Niedersachsen and Nordrhein-Westfalen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Cities in the overlap of Niedersachsen and Nordrhein-Westfalen
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities in the overlap of Niedersachsen and Nordrhein-Westfalen
```

**Model must answer**

```json
{
  "operation": "Intersection",
  "spatial": ["Niedersachsen", "Nordrhein-Westfalen"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Intersection of these two shapes",
  "operation": "Intersection",
  "spatial": ["Niedersachsen", "Nordrhein-Westfalen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o62 · SPATIAL_OPERATION

> Which cities are in Niedersachsen once Bremen is removed?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are in Niedersachsen once Bremen is removed?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are in Niedersachsen once Bremen is removed?
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Niedersachsen", "Bremen"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Niedersachsen", "Bremen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o63 · SPATIAL_OPERATION

> List the cities of Schleswig-Holstein without Hamburg's area

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |

### 1 · Classify

**Model sees**

```text
List the cities of Schleswig-Holstein without Hamburg's area
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: List the cities of Schleswig-Holstein without Hamburg's area
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Schleswig-Holstein", "Hamburg"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

---

## o64 · SPATIAL_OPERATION

> Take Sachsen-Anhalt out of Niedersachsen and tell me which cities remain inside

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Take Sachsen-Anhalt out of Niedersachsen and tell me which cities remain inside
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Take Sachsen-Anhalt out of Niedersachsen and tell me which cities remain inside
```

**Model must answer**

```json
{
  "operation": "Difference",
  "spatial": ["Niedersachsen", "Sachsen-Anhalt"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Difference of these two shapes",
  "operation": "Difference",
  "spatial": ["Niedersachsen", "Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o65 · SPATIAL_OPERATION

> Which cities lie in exactly one of Rheinland-Pfalz and Hessen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie in exactly one of Rheinland-Pfalz and Hessen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie in exactly one of Rheinland-Pfalz and Hessen?
```

**Model must answer**

```json
{
  "operation": "SymDifference",
  "spatial": ["Rheinland-Pfalz", "Hessen"],
  "entity_type": "state",
  "distance_km": null,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "SymDifference of these two shapes",
  "operation": "SymDifference",
  "spatial": ["Rheinland-Pfalz", "Hessen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o66 · SPATIAL_OPERATION

> Combine the cities Dresden and Leipzig into one shape

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |

### 1 · Classify

**Model sees**

```text
Combine the cities Dresden and Leipzig into one shape
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Combine the cities Dresden and Leipzig into one shape
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Dresden", "Leipzig"],
  "entity_type": "city",
  "distance_km": null
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Dresden', 'Leipzig']",
  "entity_type": "city",
  "spatial": ["Dresden", "Leipzig"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Dresden", "Leipzig"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

---

## o67 · SPATIAL_OPERATION

> Merge Bayern and Baden-Württemberg and give me the total population of that area for 2018

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Merge Bayern and Baden-Württemberg and give me the total population of that area for 2018
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Bayern and Baden-Württemberg and give me the total population of that area for 2018
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Bayern", "Baden-Württemberg"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population"],
  "temporal": [2018]
}
```

### 3 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch population of Bayern, Baden-Württemberg in [2018]",
  "entity_type": "state",
  "spatial": ["Bayern", "Baden-Württemberg"],
  "temporal": [2018],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o68 · SPATIAL_OPERATION

> If you join Berlin and Brandenburg into one region, what is its population in 2019?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
If you join Berlin and Brandenburg into one region, what is its population in 2019?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: If you join Berlin and Brandenburg into one region, what is its population in 2019?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Berlin", "Brandenburg"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population"],
  "temporal": [2019]
}
```

### 3 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch population of Berlin, Brandenburg in [2019]",
  "entity_type": "state",
  "spatial": ["Berlin", "Brandenburg"],
  "temporal": [2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o69 · SPATIAL_OPERATION

> Merge Sachsen and Thüringen into one shape and give me their combined population for 2018

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Merge Sachsen and Thüringen into one shape and give me their combined population for 2018
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Sachsen and Thüringen into one shape and give me their combined population for 2018
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Sachsen", "Thüringen"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population"],
  "temporal": [2018]
}
```

### 3 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch population of Sachsen, Thüringen in [2018]",
  "entity_type": "state",
  "spatial": ["Sachsen", "Thüringen"],
  "temporal": [2018],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o70 · SPATIAL_OPERATION · validation

> Combine Hamburg and Schleswig-Holstein into one area: show the shape and the total live births in 2019

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |
| 4 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Combine Hamburg and Schleswig-Holstein into one area: show the shape and the total live births in 2019
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Combine Hamburg and Schleswig-Holstein into one area: show the shape and the total live births in 2019
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["live_births"],
  "temporal": [2019]
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Hamburg", "Schleswig-Holstein"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### 4 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch live_births of Hamburg, Schleswig-Holstein in [2019]",
  "entity_type": "state",
  "spatial": ["Hamburg", "Schleswig-Holstein"],
  "temporal": [2019],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o71 · SPATIAL_OPERATION

> Merge Niedersachsen and Bremen into one shape and give me its population in 2018

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Merge Niedersachsen and Bremen into one shape and give me its population in 2018
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Niedersachsen and Bremen into one shape and give me its population in 2018
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Niedersachsen", "Bremen"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population"],
  "temporal": [2018]
}
```

### 3 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch population of Niedersachsen, Bremen in [2018]",
  "entity_type": "state",
  "spatial": ["Niedersachsen", "Bremen"],
  "temporal": [2018],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o72 · SPATIAL_OPERATION

> Join Bayern and Thüringen into one area and tell me the total marriages there in 2017

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |
| 4 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Join Bayern and Thüringen into one area and tell me the total marriages there in 2017
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Join Bayern and Thüringen into one area and tell me the total marriages there in 2017
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Bayern", "Thüringen"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["marriages"],
  "temporal": [2017]
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Bayern", "Thüringen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### 4 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch marriages of Bayern, Thüringen in [2017]",
  "entity_type": "state",
  "spatial": ["Bayern", "Thüringen"],
  "temporal": [2017],
  "attributes": ["marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o73 · SPATIAL_OPERATION

> Combine Berlin, Brandenburg and Sachsen into one region: show it and the combined population for 2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |
| 5 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Combine Berlin, Brandenburg and Sachsen into one region: show it and the combined population for 2016
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Combine Berlin, Brandenburg and Sachsen into one region: show it and the combined population for 2016
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Berlin", "Brandenburg", "Sachsen"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population"],
  "temporal": [2016]
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Berlin', 'Brandenburg', 'Sachsen']",
  "entity_type": "state",
  "spatial": ["Berlin", "Brandenburg", "Sachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Berlin", "Brandenburg", "Sachsen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### 5 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch population of Berlin, Brandenburg, Sachsen in [2016]",
  "entity_type": "state",
  "spatial": ["Berlin", "Brandenburg", "Sachsen"],
  "temporal": [2016],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o74 · SPATIAL_OPERATION

> Create one area from Rheinland-Pfalz and Saarland and give me its live births from 2015 to 2017

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Create one area from Rheinland-Pfalz and Saarland and give me its live births from 2015 to 2017
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Create one area from Rheinland-Pfalz and Saarland and give me its live births from 2015 to 2017
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Rheinland-Pfalz", "Saarland"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["live_births"],
  "temporal": [2015, 2016, 2017]
}
```

### 3 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch live_births of Rheinland-Pfalz, Saarland in [2015, 2016, 2017]",
  "entity_type": "state",
  "spatial": ["Rheinland-Pfalz", "Saarland"],
  "temporal": [2015, 2016, 2017],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o75 · SPATIAL_OPERATION

> Merge Hessen and Nordrhein-Westfalen into one shape. What was its population in 2019?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |
| 4 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Merge Hessen and Nordrhein-Westfalen into one shape. What was its population in 2019?
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Hessen and Nordrhein-Westfalen into one shape. What was its population in 2019?
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Hessen", "Nordrhein-Westfalen"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population"],
  "temporal": [2019]
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Hessen", "Nordrhein-Westfalen"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### 4 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch population of Hessen, Nordrhein-Westfalen in [2019]",
  "entity_type": "state",
  "spatial": ["Hessen", "Nordrhein-Westfalen"],
  "temporal": [2019],
  "attributes": ["population"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o76 · SPATIAL_OPERATION

> Union of Baden-Württemberg and Bayern with the total live births in 2018

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · SPATIAL_OPERATION → compute | [sql_SPATIAL_OPERATION_compute.txt](prompts/sql_SPATIAL_OPERATION_compute.txt) |
| 4 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Union of Baden-Württemberg and Bayern with the total live births in 2018
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Union of Baden-Württemberg and Bayern with the total live births in 2018
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Baden-Württemberg", "Bayern"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["live_births"],
  "temporal": [2018]
}
```

### 3 · SQL · SPATIAL_OPERATION → compute

**Model sees**

```json
{
  "question": "Union of these two shapes",
  "operation": "Union",
  "spatial": ["Baden-Württemberg", "Bayern"]
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### 4 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch live_births of Baden-Württemberg, Bayern in [2018]",
  "entity_type": "state",
  "spatial": ["Baden-Württemberg", "Bayern"],
  "temporal": [2018],
  "attributes": ["live_births"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o77 · SPATIAL_OPERATION

> Merge Mecklenburg-Vorpommern and Schleswig-Holstein into one shape and give me the population and marriages for 2016

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |
| 3 | SQL · the merged area's data | [sql_DIRECT_LOOKUP_fetch.txt](prompts/sql_DIRECT_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Merge Mecklenburg-Vorpommern and Schleswig-Holstein into one shape and give me the population and marriages for 2016
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Merge Mecklenburg-Vorpommern and Schleswig-Holstein into one shape and give me the population and marriages for 2016
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population", "marriages"],
  "temporal": [2016]
}
```

### 3 · SQL · the merged area's data

**Model sees**

```json
{
  "question": "Fetch population, marriages of Mecklenburg-Vorpommern, Schleswig-Holstein in [2016]",
  "entity_type": "state",
  "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"],
  "temporal": [2016],
  "attributes": ["population", "marriages"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

---

## o78 · SPATIAL_OPERATION

> Join Sachsen-Anhalt and Thüringen into one area and give me its population

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_OPERATION.txt](prompts/extract_SPATIAL_OPERATION.txt) |

### 1 · Classify

**Model sees**

```text
Join Sachsen-Anhalt and Thüringen into one area and give me its population
```

**Model must answer**

```json
{"query_type": "SPATIAL_OPERATION"}
```

### 2 · Extract

**Model sees**

```text
Query: Join Sachsen-Anhalt and Thüringen into one area and give me its population
```

**Model must answer**

```json
{
  "operation": "Union",
  "spatial": ["Sachsen-Anhalt", "Thüringen"],
  "entity_type": "state",
  "distance_km": null,
  "attributes": ["population"],
  "temporal": []
}
```

---

# relationship

## r01 · SPATIAL_ADJACENCY

> Which states border Hessen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states border Hessen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states border Hessen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Hessen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Hessen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Hessen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r02 · SPATIAL_ADJACENCY

> Does Brandenburg share a border with Sachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Does Brandenburg share a border with Sachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Does Brandenburg share a border with Sachsen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Brandenburg", "refs": ["Sachsen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Sachsen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Sachsen"], "subject": "Brandenburg", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r03 · SPATIAL_ADJACENCY

> Is Saarland adjacent to Rheinland-Pfalz?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Saarland adjacent to Rheinland-Pfalz?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Saarland adjacent to Rheinland-Pfalz?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Saarland", "refs": ["Rheinland-Pfalz"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Rheinland-Pfalz?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Rheinland-Pfalz"], "subject": "Saarland", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r04 · SPATIAL_ADJACENCY

> Name the neighbours of Niedersachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Name the neighbours of Niedersachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Name the neighbours of Niedersachsen
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Niedersachsen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Niedersachsen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Niedersachsen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r05 · SPATIAL_ADJACENCY

> Which state touches both Bayern and Thüringen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which state touches both Bayern and Thüringen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which state touches both Bayern and Thüringen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Bayern", "Thüringen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Bayern, Thüringen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Bayern", "Thüringen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r06 · SPATIAL_ADJACENCY

> Do Hamburg and Bremen touch?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Do Hamburg and Bremen touch?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Do Hamburg and Bremen touch?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Hamburg", "refs": ["Bremen"], "distance_km": null}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bremen', 'Hamburg']",
  "entity_type": "state",
  "spatial": ["Bremen", "Hamburg"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Bremen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Bremen"], "subject": "Hamburg", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r07 · SPATIAL_ADJACENCY

> Which states share a border with Baden-Württemberg? Show their population in 2021.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states share a border with Baden-Württemberg? Show their population in 2021.
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states share a border with Baden-Württemberg? Show their population in 2021.
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2021],
  "attributes": ["population"],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Baden-Württemberg"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

*the data fetch for the resulting states follows; it is the DIRECT_LOOKUP fetch pattern and depends on the map, so not generated here*

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Baden-Württemberg?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Baden-Württemberg"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r08 · SPATIAL_ADJACENCY

> Neighbouring states of Mecklenburg-Vorpommern and their marriages from 2019 to 2020

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Neighbouring states of Mecklenburg-Vorpommern and their marriages from 2019 to 2020
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Neighbouring states of Mecklenburg-Vorpommern and their marriages from 2019 to 2020
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2019, 2020],
  "attributes": ["marriages"],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Mecklenburg-Vorpommern"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

*the data fetch for the resulting states follows; it is the DIRECT_LOOKUP fetch pattern and depends on the map, so not generated here*

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Mecklenburg-Vorpommern?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Mecklenburg-Vorpommern"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r09 · SPATIAL_DIRECTION

> Which states lie south of Niedersachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie south of Niedersachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie south of Niedersachsen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "south_of", "subject": null, "refs": ["Niedersachsen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie south of Niedersachsen?",
  "spatial_relationship": {"type": "south_of", "refs": ["Niedersachsen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r10 · SPATIAL_DIRECTION · validation

> Is Hamburg north of Hessen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Hamburg north of Hessen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Hamburg north of Hessen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "north_of", "subject": "Hamburg", "refs": ["Hessen"], "distance_km": null}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hamburg', 'Hessen']",
  "entity_type": "state",
  "spatial": ["Hamburg", "Hessen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie north of Hessen?",
  "spatial_relationship": {"type": "north_of", "refs": ["Hessen"], "subject": "Hamburg", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r11 · SPATIAL_DIRECTION

> States east of Nordrhein-Westfalen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States east of Nordrhein-Westfalen
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: States east of Nordrhein-Westfalen
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "east_of", "subject": null, "refs": ["Nordrhein-Westfalen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie east of Nordrhein-Westfalen?",
  "spatial_relationship": {"type": "east_of", "refs": ["Nordrhein-Westfalen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r12 · SPATIAL_DIRECTION

> Does Saarland lie west of Bayern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Does Saarland lie west of Bayern?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Does Saarland lie west of Bayern?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "west_of", "subject": "Saarland", "refs": ["Bayern"], "distance_km": null}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bayern', 'Saarland']",
  "entity_type": "state",
  "spatial": ["Bayern", "Saarland"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie west of Bayern?",
  "spatial_relationship": {"type": "west_of", "refs": ["Bayern"], "subject": "Saarland", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r13 · SPATIAL_DIRECTION

> Which federal states are located north of Thüringen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which federal states are located north of Thüringen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which federal states are located north of Thüringen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "north_of", "subject": null, "refs": ["Thüringen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie north of Thüringen?",
  "spatial_relationship": {"type": "north_of", "refs": ["Thüringen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r14 · SPATIAL_DIRECTION

> Is Sachsen east of Hessen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Sachsen east of Hessen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Sachsen east of Hessen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "east_of", "subject": "Sachsen", "refs": ["Hessen"], "distance_km": null}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Hessen', 'Sachsen']",
  "entity_type": "state",
  "spatial": ["Hessen", "Sachsen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie east of Hessen?",
  "spatial_relationship": {"type": "east_of", "refs": ["Hessen"], "subject": "Sachsen", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r15 · SPATIAL_DIRECTION

> States west of Sachsen-Anhalt with their live births in 2022

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States west of Sachsen-Anhalt with their live births in 2022
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: States west of Sachsen-Anhalt with their live births in 2022
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2022],
  "attributes": ["live_births"],
  "spatial_relationship": {"type": "west_of", "subject": null, "refs": ["Sachsen-Anhalt"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

*the data fetch for the resulting states follows; it is the DIRECT_LOOKUP fetch pattern and depends on the map, so not generated here*

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie west of Sachsen-Anhalt?",
  "spatial_relationship": {"type": "west_of", "refs": ["Sachsen-Anhalt"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r16 · SPATIAL_DIRECTION

> Which states are south of Brandenburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are south of Brandenburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are south of Brandenburg?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "south_of", "subject": null, "refs": ["Brandenburg"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie south of Brandenburg?",
  "spatial_relationship": {"type": "south_of", "refs": ["Brandenburg"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r17 · SPATIAL_DISTANCE

> Which states are within 150 km of Frankfurt?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are within 150 km of Frankfurt?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are within 150 km of Frankfurt?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Frankfurt"], "distance_km": 150}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 150 km of Frankfurt?",
  "spatial_relationship": {"type": "distance", "refs": ["Frankfurt"], "subject": null, "distance_km": 150}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r18 · SPATIAL_DISTANCE

> Is Thüringen within 50 km of Leipzig?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Thüringen within 50 km of Leipzig?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Thüringen within 50 km of Leipzig?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": "Thüringen", "refs": ["Leipzig"], "distance_km": 50}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 50 km of Leipzig?",
  "spatial_relationship": {"type": "distance", "refs": ["Leipzig"], "subject": "Thüringen", "distance_km": 50}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r19 · SPATIAL_DISTANCE

> States within 200 km of Berlin

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States within 200 km of Berlin
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: States within 200 km of Berlin
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Berlin"], "distance_km": 200}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 200 km of Berlin?",
  "spatial_relationship": {"type": "distance", "refs": ["Berlin"], "subject": null, "distance_km": 200}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r20 · SPATIAL_DISTANCE · validation

> Which states lie within 80 km of Stuttgart?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie within 80 km of Stuttgart?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie within 80 km of Stuttgart?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Stuttgart"], "distance_km": 80}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 80 km of Stuttgart?",
  "spatial_relationship": {"type": "distance", "refs": ["Stuttgart"], "subject": null, "distance_km": 80}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r21 · SPATIAL_DISTANCE

> Is Bremen within 100 km of Hannover?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Bremen within 100 km of Hannover?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Bremen within 100 km of Hannover?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": "Bremen", "refs": ["Hannover"], "distance_km": 100}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bremen']",
  "entity_type": "state",
  "spatial": ["Bremen"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Hannover']",
  "entity_type": "city",
  "spatial": ["Hannover"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 5 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 100 km of Hannover?",
  "spatial_relationship": {"type": "distance", "refs": ["Hannover"], "subject": "Bremen", "distance_km": 100}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r22 · SPATIAL_DISTANCE

> States within 120 km of Köln and their population in 2020

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States within 120 km of Cologne and their population in 2020
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: States within 120 km of Cologne and their population in 2020
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2020],
  "attributes": ["population"],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Cologne"], "distance_km": 120}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

*the data fetch for the resulting states follows; it is the DIRECT_LOOKUP fetch pattern and depends on the map, so not generated here*

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 120 km of Cologne?",
  "spatial_relationship": {"type": "distance", "refs": ["Cologne"], "subject": null, "distance_km": 120}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r23 · SPATIAL_ADJACENCY

> Which states border Sachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states border Sachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states border Sachsen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Sachsen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Sachsen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Sachsen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r24 · SPATIAL_ADJACENCY

> Does Thüringen share a border with Hessen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Does Thüringen share a border with Hessen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Does Thüringen share a border with Hessen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Thüringen", "refs": ["Hessen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Hessen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Hessen"], "subject": "Thüringen", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r25 · SPATIAL_ADJACENCY

> Is Hamburg adjacent to Niedersachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Hamburg adjacent to Niedersachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Hamburg adjacent to Niedersachsen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Hamburg", "refs": ["Niedersachsen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Niedersachsen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Niedersachsen"], "subject": "Hamburg", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r26 · SPATIAL_ADJACENCY

> Neighbours of Schleswig-Holstein

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Neighbours of Schleswig-Holstein
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Neighbours of Schleswig-Holstein
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Schleswig-Holstein"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Schleswig-Holstein?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Schleswig-Holstein"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r27 · SPATIAL_ADJACENCY

> Which states touch both Hessen and Bayern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states touch both Hessen and Bayern?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states touch both Hessen and Bayern?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Hessen", "Bayern"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Hessen, Bayern?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Hessen", "Bayern"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r28 · SPATIAL_ADJACENCY

> Do Saarland and Nordrhein-Westfalen share a border?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Do Saarland and Nordrhein-Westfalen share a border?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Do Saarland and Nordrhein-Westfalen share a border?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Saarland", "refs": ["Nordrhein-Westfalen"], "distance_km": null}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Nordrhein-Westfalen', 'Saarland']",
  "entity_type": "state",
  "spatial": ["Nordrhein-Westfalen", "Saarland"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Nordrhein-Westfalen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Nordrhein-Westfalen"], "subject": "Saarland", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r29 · SPATIAL_ADJACENCY

> Which states border Hessen? Give me their marriages in 2016.

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |

### 1 · Classify

**Model sees**

```text
Which states border Hessen? Give me their marriages in 2016.
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states border Hessen? Give me their marriages in 2016.
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2016],
  "attributes": ["marriages"],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Hessen"], "distance_km": null}
}
```

---

## r30 · SPATIAL_ADJACENCY · validation

> Neighbouring states of Lower Saxony

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |

### 1 · Classify

**Model sees**

```text
Neighbouring states of Lower Saxony
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Neighbouring states of Lower Saxony
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Niedersachsen"], "distance_km": null}
}
```

---

## r31 · SPATIAL_ADJACENCY

> Is Rheinland-Pfalz adjacent to Baden-Württemberg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Rheinland-Pfalz adjacent to Baden-Württemberg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Rheinland-Pfalz adjacent to Baden-Württemberg?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Rheinland-Pfalz", "refs": ["Baden-Württemberg"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Baden-Württemberg?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Baden-Württemberg"], "subject": "Rheinland-Pfalz", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r32 · SPATIAL_DIRECTION

> Which states lie north of Sachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie north of Sachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie north of Sachsen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "north_of", "subject": null, "refs": ["Sachsen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie north of Sachsen?",
  "spatial_relationship": {"type": "north_of", "refs": ["Sachsen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r33 · SPATIAL_DIRECTION

> Is Niedersachsen north of Nordrhein-Westfalen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Niedersachsen north of Nordrhein-Westfalen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Niedersachsen north of Nordrhein-Westfalen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "north_of", "subject": "Niedersachsen", "refs": ["Nordrhein-Westfalen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie north of Nordrhein-Westfalen?",
  "spatial_relationship": {"type": "north_of", "refs": ["Nordrhein-Westfalen"], "subject": "Niedersachsen", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r34 · SPATIAL_DIRECTION

> States west of Thüringen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States west of Thüringen
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: States west of Thüringen
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "west_of", "subject": null, "refs": ["Thüringen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie west of Thüringen?",
  "spatial_relationship": {"type": "west_of", "refs": ["Thüringen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r35 · SPATIAL_DIRECTION

> Does Bayern lie east of Baden-Württemberg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Does Bayern lie east of Baden-Württemberg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Does Bayern lie east of Baden-Württemberg?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "east_of", "subject": "Bayern", "refs": ["Baden-Württemberg"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie east of Baden-Württemberg?",
  "spatial_relationship": {"type": "east_of", "refs": ["Baden-Württemberg"], "subject": "Bayern", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r36 · SPATIAL_DIRECTION

> Which states are south of Mecklenburg-Vorpommern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are south of Mecklenburg-Vorpommern?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are south of Mecklenburg-Vorpommern?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "south_of", "subject": null, "refs": ["Mecklenburg-Vorpommern"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie south of Mecklenburg-Vorpommern?",
  "spatial_relationship": {"type": "south_of", "refs": ["Mecklenburg-Vorpommern"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r37 · SPATIAL_DIRECTION

> Is Hessen west of Thüringen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Hessen west of Thüringen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Hessen west of Thüringen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "west_of", "subject": "Hessen", "refs": ["Thüringen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie west of Thüringen?",
  "spatial_relationship": {"type": "west_of", "refs": ["Thüringen"], "subject": "Hessen", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r38 · SPATIAL_DIRECTION

> States south of Schleswig-Holstein with their live births in 2010

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States south of Schleswig-Holstein with their live births in 2010
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: States south of Schleswig-Holstein with their live births in 2010
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2010],
  "attributes": ["live_births"],
  "spatial_relationship": {"type": "south_of", "subject": null, "refs": ["Schleswig-Holstein"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

*the data fetch for the resulting states follows; it is the DIRECT_LOOKUP fetch pattern and depends on the map, so not generated here*

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie south of Schleswig-Holstein?",
  "spatial_relationship": {"type": "south_of", "refs": ["Schleswig-Holstein"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r39 · SPATIAL_DIRECTION

> Which states lie east of Rheinland-Pfalz?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie east of Rheinland-Pfalz?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie east of Rheinland-Pfalz?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "east_of", "subject": null, "refs": ["Rheinland-Pfalz"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie east of Rheinland-Pfalz?",
  "spatial_relationship": {"type": "east_of", "refs": ["Rheinland-Pfalz"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r40 · SPATIAL_DIRECTION · validation

> Is Sachsen-Anhalt north of Thüringen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Sachsen-Anhalt north of Thüringen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Sachsen-Anhalt north of Thüringen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "north_of", "subject": "Sachsen-Anhalt", "refs": ["Thüringen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie north of Thüringen?",
  "spatial_relationship": {"type": "north_of", "refs": ["Thüringen"], "subject": "Sachsen-Anhalt", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r41 · SPATIAL_DIRECTION

> Which states are west of Brandenburg, and what was their population in 2005?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are west of Brandenburg, and what was their population in 2005?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are west of Brandenburg, and what was their population in 2005?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2005],
  "attributes": ["population"],
  "spatial_relationship": {"type": "west_of", "subject": null, "refs": ["Brandenburg"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

*the data fetch for the resulting states follows; it is the DIRECT_LOOKUP fetch pattern and depends on the map, so not generated here*

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie west of Brandenburg?",
  "spatial_relationship": {"type": "west_of", "refs": ["Brandenburg"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r42 · SPATIAL_DISTANCE

> Which states are within 100 km of Braunschweig?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are within 100 km of Braunschweig?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are within 100 km of Braunschweig?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Braunschweig"], "distance_km": 100}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 100 km of Braunschweig?",
  "spatial_relationship": {"type": "distance", "refs": ["Braunschweig"], "subject": null, "distance_km": 100}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r43 · SPATIAL_DISTANCE

> Is Bayern within 60 km of Erfurt?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Bayern within 60 km of Erfurt?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Bayern within 60 km of Erfurt?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": "Bayern", "refs": ["Erfurt"], "distance_km": 60}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Bayern']",
  "entity_type": "state",
  "spatial": ["Bayern"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 60 km of Erfurt?",
  "spatial_relationship": {"type": "distance", "refs": ["Erfurt"], "subject": "Bayern", "distance_km": 60}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r44 · SPATIAL_DISTANCE

> States within 75 km of Bremen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States within 75 km of Bremen
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: States within 75 km of Bremen
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Bremen"], "distance_km": 75}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 75 km of Bremen?",
  "spatial_relationship": {"type": "distance", "refs": ["Bremen"], "subject": null, "distance_km": 75}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r45 · SPATIAL_DISTANCE

> Which states lie within 50 km of Mainz?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie within 50 km of Mainz?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie within 50 km of Mainz?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Mainz"], "distance_km": 50}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 50 km of Mainz?",
  "spatial_relationship": {"type": "distance", "refs": ["Mainz"], "subject": null, "distance_km": 50}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r46 · SPATIAL_DISTANCE

> Is Sachsen-Anhalt within 30 km of Leipzig?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Sachsen-Anhalt within 30 km of Leipzig?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Sachsen-Anhalt within 30 km of Leipzig?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": "Sachsen-Anhalt", "refs": ["Leipzig"], "distance_km": 30}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Sachsen-Anhalt']",
  "entity_type": "state",
  "spatial": ["Sachsen-Anhalt"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 30 km of Leipzig?",
  "spatial_relationship": {"type": "distance", "refs": ["Leipzig"], "subject": "Sachsen-Anhalt", "distance_km": 30}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r47 · SPATIAL_DISTANCE

> Which states are within 120 km of Hannover?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are within 120 km of Hannover?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are within 120 km of Hannover?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Hannover"], "distance_km": 120}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 120 km of Hannover?",
  "spatial_relationship": {"type": "distance", "refs": ["Hannover"], "subject": null, "distance_km": 120}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r48 · SPATIAL_DISTANCE

> Is Saarland within 80 km of Karlsruhe?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Saarland within 80 km of Karlsruhe?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Saarland within 80 km of Karlsruhe?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": "Saarland", "refs": ["Karlsruhe"], "distance_km": 80}
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Saarland']",
  "entity_type": "state",
  "spatial": ["Saarland"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 80 km of Karlsruhe?",
  "spatial_relationship": {"type": "distance", "refs": ["Karlsruhe"], "subject": "Saarland", "distance_km": 80}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r49 · SPATIAL_DISTANCE

> Which states lie within 90 km of Nürnberg, with their population in 2014?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie within 90 km of Nuremberg, with their population in 2014?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie within 90 km of Nuremberg, with their population in 2014?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [2014],
  "attributes": ["population"],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Nuremberg"], "distance_km": 90}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

*the data fetch for the resulting states follows; it is the DIRECT_LOOKUP fetch pattern and depends on the map, so not generated here*

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 90 km of Nuremberg?",
  "spatial_relationship": {"type": "distance", "refs": ["Nuremberg"], "subject": null, "distance_km": 90}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r50 · SPATIAL_DISTANCE · validation

> States within 40 km of Koblenz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States within 40 km of Koblenz
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: States within 40 km of Koblenz
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Koblenz"], "distance_km": 40}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 40 km of Koblenz?",
  "spatial_relationship": {"type": "distance", "refs": ["Koblenz"], "subject": null, "distance_km": 40}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r51 · SPATIAL_ADJACENCY

> Which states border Berlin?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states border Berlin?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states border Berlin?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Berlin"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Berlin?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Berlin"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r52 · SPATIAL_ADJACENCY

> Does Bremen border Niedersachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Does Bremen border Niedersachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Does Bremen border Niedersachsen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": "Bremen", "refs": ["Niedersachsen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Niedersachsen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Niedersachsen"], "subject": "Bremen", "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r53 · SPATIAL_ADJACENCY

> Which states border both Berlin and Hessen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_ADJACENCY.txt](prompts/extract_SPATIAL_ADJACENCY.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states border both Berlin and Hessen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_ADJACENCY"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states border both Berlin and Hessen?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "adjacency", "subject": null, "refs": ["Berlin", "Hessen"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states border Berlin, Hessen?",
  "spatial_relationship": {"type": "adjacency", "refs": ["Berlin", "Hessen"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

---

## r54 · SPATIAL_DIRECTION

> Which states are south of Bayern?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are south of Bayern?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are south of Bayern?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "south_of", "subject": null, "refs": ["Bayern"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie south of Bayern?",
  "spatial_relationship": {"type": "south_of", "refs": ["Bayern"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r55 · SPATIAL_DIRECTION

> Which states lie north of Schleswig-Holstein?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DIRECTION.txt](prompts/extract_SPATIAL_DIRECTION.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie north of Schleswig-Holstein?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DIRECTION"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie north of Schleswig-Holstein?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "north_of", "subject": null, "refs": ["Schleswig-Holstein"], "distance_km": null}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie north of Schleswig-Holstein?",
  "spatial_relationship": {"type": "north_of", "refs": ["Schleswig-Holstein"], "subject": null, "distance_km": null}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

---

## r56 · SPATIAL_DISTANCE

> Which states are within 50 km of Berlin?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are within 50 km of Berlin?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are within 50 km of Berlin?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Berlin"], "distance_km": 50}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 50 km of Berlin?",
  "spatial_relationship": {"type": "distance", "refs": ["Berlin"], "subject": null, "distance_km": 50}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r57 · SPATIAL_DISTANCE

> Which states lie within 10 km of Hamburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states lie within 10 km of Hamburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states lie within 10 km of Hamburg?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": null, "refs": ["Hamburg"], "distance_km": 10}
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 10 km of Hamburg?",
  "spatial_relationship": {"type": "distance", "refs": ["Hamburg"], "subject": null, "distance_km": 10}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r58 · SPATIAL_DISTANCE

> Is Saarland within 500 km of Kiel?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Is Saarland within 500 km of Kiel?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Is Saarland within 500 km of Kiel?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "subject": "Saarland", "refs": ["Kiel"], "distance_km": 500}
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Kiel']",
  "entity_type": "city",
  "spatial": ["Kiel"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 500 km of Kiel?",
  "spatial_relationship": {"type": "distance", "refs": ["Kiel"], "subject": "Saarland", "distance_km": 500}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r59 · SPATIAL_DISTANCE

> Which states are at most 50 km from Fulda?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
Which states are at most 50 km from Fulda?
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: Which states are at most 50 km from Fulda?
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "refs": ["Fulda"], "distance_km": 50}
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Fulda']",
  "entity_type": "city",
  "spatial": ["Fulda"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 50 km of Fulda?",
  "spatial_relationship": {"type": "distance", "refs": ["Fulda"], "subject": null, "distance_km": 50}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

## r60 · SPATIAL_DISTANCE · validation

> States no more than 25 km away from Ulm

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_DISTANCE.txt](prompts/extract_SPATIAL_DISTANCE.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP → compute | [sql_SPATIAL_RELATIONSHIP_compute.txt](prompts/sql_SPATIAL_RELATIONSHIP_compute.txt) |

### 1 · Classify

**Model sees**

```text
States no more than 25 km away from Ulm
```

**Model must answer**

```json
{"query_type": "SPATIAL_DISTANCE"}
```

### 2 · Extract

**Model sees**

```text
Query: States no more than 25 km away from Ulm
```

**Model must answer**

```json
{
  "spatial": "all",
  "temporal": [],
  "attributes": [],
  "spatial_relationship": {"type": "distance", "refs": ["Ulm"], "distance_km": 25}
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Ulm']",
  "entity_type": "city",
  "spatial": ["Ulm"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP → compute

**Model sees**

```json
{
  "question": "Which of the candidate federal states lie within 25 km of Ulm?",
  "spatial_relationship": {"type": "distance", "refs": ["Ulm"], "subject": null, "distance_km": 25}
}
```

**Model must answer**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

---

# delegation

## b01 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 30 km of Leipzig?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 5 | SQL · within (answering Agent-1) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 6 | SQL · within (answering Agent-2) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 30 km of Leipzig?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 30 km of Leipzig?
```

**Model must answer**

```json
{
  "spatial": ["Leipzig"],
  "operations": ["Buffer", "Within"],
  "distance_km": 30,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 30 km of Leipzig?",
  "spatial": ["Leipzig"],
  "distance_km": 30.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Leipzig"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 5 · SQL · within (answering Agent-1)

*this agent testing its own cities for Agent-1's delegated zone*

**Model sees**

```json
{
  "question": "Agent-1 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Leipzig"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 6 · SQL · within (answering Agent-2)

*this agent testing its own cities for Agent-2's delegated zone*

**Model sees**

```json
{
  "question": "Agent-2 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Leipzig"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b02 · SPATIAL_RELATIONSHIP_BUFFER

> List all cities within 100 km of Frankfurt

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
List all cities within 100 km of Frankfurt
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: List all cities within 100 km of Frankfurt
```

**Model must answer**

```json
{
  "spatial": ["Frankfurt"],
  "operations": ["Buffer", "Within"],
  "distance_km": 100,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "List all cities within 100 km of Frankfurt",
  "spatial": ["Frankfurt"],
  "distance_km": 100.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Frankfurt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b03 · SPATIAL_RELATIONSHIP_BUFFER

> What cities are near Hannover, within 75 km?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
What cities are near Hannover, within 75 km?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: What cities are near Hannover, within 75 km?
```

**Model must answer**

```json
{
  "spatial": ["Hannover"],
  "operations": ["Buffer", "Within"],
  "distance_km": 75,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "What cities are near Hannover, within 75 km?",
  "spatial": ["Hannover"],
  "distance_km": 75.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Hannover"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b04 · SPATIAL_RELATIONSHIP_BUFFER

> Cities within 40 km of Köln

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Cities within 40 km of Cologne
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities within 40 km of Cologne
```

**Model must answer**

```json
{
  "spatial": ["Cologne"],
  "operations": ["Buffer", "Within"],
  "distance_km": 40,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Cities within 40 km of Köln",
  "spatial": ["Cologne"],
  "distance_km": 40.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Cologne"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b05 · SPATIAL_RELATIONSHIP_BUFFER

> Which towns lie within 60 km of Dresden?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 6 | SQL · within (answering Agent-1) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 7 | SQL · within (answering Agent-2) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which towns lie within 60 km of Dresden?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which towns lie within 60 km of Dresden?
```

**Model must answer**

```json
{
  "spatial": ["Dresden"],
  "operations": ["Buffer", "Within"],
  "distance_km": 60,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Dresden']",
  "entity_type": "city",
  "spatial": ["Dresden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which towns lie within 60 km of Dresden?",
  "spatial": ["Dresden"],
  "distance_km": 60.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Dresden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 6 · SQL · within (answering Agent-1)

*this agent testing its own cities for Agent-1's delegated zone*

**Model sees**

```json
{
  "question": "Agent-1 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Dresden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 7 · SQL · within (answering Agent-2)

*this agent testing its own cities for Agent-2's delegated zone*

**Model sees**

```json
{
  "question": "Agent-2 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Dresden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b06 · SPATIAL_RELATIONSHIP_BUFFER

> Find every city in a 120 km radius around Berlin

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Find every city in a 120 km radius around Berlin
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Find every city in a 120 km radius around Berlin
```

**Model must answer**

```json
{
  "spatial": ["Berlin"],
  "operations": ["Buffer", "Within"],
  "distance_km": 120,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Find every city in a 120 km radius around Berlin",
  "spatial": ["Berlin"],
  "distance_km": 120.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b07 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 25 km of Düsseldorf?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 25 km of Düsseldorf?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 25 km of Düsseldorf?
```

**Model must answer**

```json
{
  "spatial": ["Düsseldorf"],
  "operations": ["Buffer", "Within"],
  "distance_km": 25,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Düsseldorf']",
  "entity_type": "city",
  "spatial": ["Düsseldorf"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 25 km of Düsseldorf?",
  "spatial": ["Düsseldorf"],
  "distance_km": 25.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Düsseldorf"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b08 · SPATIAL_RELATIONSHIP_BUFFER

> Show the cities close to Stuttgart

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Show the cities close to Stuttgart
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Show the cities close to Stuttgart
```

**Model must answer**

```json
{
  "spatial": ["Stuttgart"],
  "operations": ["Buffer", "Within"],
  "distance_km": 100,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Show the cities close to Stuttgart",
  "spatial": ["Stuttgart"],
  "distance_km": 100.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Stuttgart"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b09 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities can be found within 200 km of Hamburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Which cities can be found within 200 km of Hamburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities can be found within 200 km of Hamburg?
```

**Model must answer**

```json
{
  "spatial": ["Hamburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 200,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities can be found within 200 km of Hamburg?",
  "spatial": ["Hamburg"],
  "distance_km": 200.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b10 · SPATIAL_RELATIONSHIP_BUFFER · validation

> Cities in a 90 km radius of Nürnberg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 5 | SQL · within (answering Agent-1) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 6 | SQL · within (answering Agent-2) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Cities in a 90 km radius of Nuremberg
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities in a 90 km radius of Nuremberg
```

**Model must answer**

```json
{
  "spatial": ["Nuremberg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 90,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Cities in a 90 km radius of Nürnberg",
  "spatial": ["Nuremberg"],
  "distance_km": 90.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Nuremberg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 5 · SQL · within (answering Agent-1)

*this agent testing its own cities for Agent-1's delegated zone*

**Model sees**

```json
{
  "question": "Agent-1 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Nuremberg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 6 · SQL · within (answering Agent-2)

*this agent testing its own cities for Agent-2's delegated zone*

**Model sees**

```json
{
  "question": "Agent-2 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Nuremberg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b11 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are less than 70 km from Kassel?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are less than 70 km from Kassel?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are less than 70 km from Kassel?
```

**Model must answer**

```json
{
  "spatial": ["Kassel"],
  "operations": ["Buffer", "Within"],
  "distance_km": 70,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are less than 70 km from Kassel?",
  "spatial": ["Kassel"],
  "distance_km": 70.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Kassel"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b12 · SPATIAL_RELATIONSHIP_BUFFER

> Name the cities within 150 km of München

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Name the cities within 150 km of Munich
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Name the cities within 150 km of Munich
```

**Model must answer**

```json
{
  "spatial": ["Munich"],
  "operations": ["Buffer", "Within"],
  "distance_km": 150,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Munich']",
  "entity_type": "city",
  "spatial": ["Munich"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Name the cities within 150 km of München",
  "spatial": ["Munich"],
  "distance_km": 150.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Munich"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b13 · SPATIAL_RELATIONSHIP_BUFFER

> Are there any cities within 35 km of Bremen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Are there any cities within 35 km of Bremen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Are there any cities within 35 km of Bremen?
```

**Model must answer**

```json
{
  "spatial": ["Bremen"],
  "operations": ["Buffer", "Within"],
  "distance_km": 35,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Are there any cities within 35 km of Bremen?",
  "spatial": ["Bremen"],
  "distance_km": 35.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b14 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities lie within 80 km of Erfurt?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 80 km of Erfurt?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie within 80 km of Erfurt?
```

**Model must answer**

```json
{
  "spatial": ["Erfurt"],
  "operations": ["Buffer", "Within"],
  "distance_km": 80,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities lie within 80 km of Erfurt?",
  "spatial": ["Erfurt"],
  "distance_km": 80.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Erfurt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b15 · SPATIAL_RELATIONSHIP_BUFFER

> cities within 45km of Mainz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
cities within 45km of Mainz
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: cities within 45km of Mainz
```

**Model must answer**

```json
{
  "spatial": ["Mainz"],
  "operations": ["Buffer", "Within"],
  "distance_km": 45,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "cities within 45km of Mainz",
  "spatial": ["Mainz"],
  "distance_km": 45.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Mainz"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b16 · SPATIAL_RELATIONSHIP_BUFFER

> What cities are located within 100 kilometres of Kiel?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
What cities are located within 100 kilometres of Kiel?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: What cities are located within 100 kilometres of Kiel?
```

**Model must answer**

```json
{
  "spatial": ["Kiel"],
  "operations": ["Buffer", "Within"],
  "distance_km": 100,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "What cities are located within 100 kilometres of Kiel?",
  "spatial": ["Kiel"],
  "distance_km": 100.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Kiel"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b17 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 55 km of Magdeburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 55 km of Magdeburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 55 km of Magdeburg?
```

**Model must answer**

```json
{
  "spatial": ["Magdeburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 55,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 55 km of Magdeburg?",
  "spatial": ["Magdeburg"],
  "distance_km": 55.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Magdeburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b18 · SPATIAL_RELATIONSHIP_BUFFER

> Give me all cities within 65 km of Rostock

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Give me all cities within 65 km of Rostock
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me all cities within 65 km of Rostock
```

**Model must answer**

```json
{
  "spatial": ["Rostock"],
  "operations": ["Buffer", "Within"],
  "distance_km": 65,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Give me all cities within 65 km of Rostock",
  "spatial": ["Rostock"],
  "distance_km": 65.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Rostock"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b19 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities lie within 110 km of Freiburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 110 km of Freiburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie within 110 km of Freiburg?
```

**Model must answer**

```json
{
  "spatial": ["Freiburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 110,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Freiburg']",
  "entity_type": "city",
  "spatial": ["Freiburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities lie within 110 km of Freiburg?",
  "spatial": ["Freiburg"],
  "distance_km": 110.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Freiburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b20 · SPATIAL_RELATIONSHIP_BUFFER · validation

> Cities that are at most 50 km away from Bonn

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Cities that are at most 50 km away from Bonn
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities that are at most 50 km away from Bonn
```

**Model must answer**

```json
{
  "spatial": ["Bonn"],
  "operations": ["Buffer", "Within"],
  "distance_km": 50,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bonn']",
  "entity_type": "city",
  "spatial": ["Bonn"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Cities that are at most 50 km away from Bonn",
  "spatial": ["Bonn"],
  "distance_km": 50.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Bonn"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b21 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities surround Augsburg within 40 km?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities surround Augsburg within 40 km?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities surround Augsburg within 40 km?
```

**Model must answer**

```json
{
  "spatial": ["Augsburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 40,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Augsburg']",
  "entity_type": "city",
  "spatial": ["Augsburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities surround Augsburg within 40 km?",
  "spatial": ["Augsburg"],
  "distance_km": 40.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Augsburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b22 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 85 km of Münster?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 85 km of Münster?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 85 km of Münster?
```

**Model must answer**

```json
{
  "spatial": ["Münster"],
  "operations": ["Buffer", "Within"],
  "distance_km": 85,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Münster']",
  "entity_type": "city",
  "spatial": ["Münster"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 85 km of Münster?",
  "spatial": ["Münster"],
  "distance_km": 85.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Münster"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b23 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 30 km of Wiesbaden?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 5 | SQL · within (answering Agent-1) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 6 | SQL · within (answering Agent-2) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 30 km of Wiesbaden?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 30 km of Wiesbaden?
```

**Model must answer**

```json
{
  "spatial": ["Wiesbaden"],
  "operations": ["Buffer", "Within"],
  "distance_km": 30,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 30 km of Wiesbaden?",
  "spatial": ["Wiesbaden"],
  "distance_km": 30.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Wiesbaden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 5 · SQL · within (answering Agent-1)

*this agent testing its own cities for Agent-1's delegated zone*

**Model sees**

```json
{
  "question": "Agent-1 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Wiesbaden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 6 · SQL · within (answering Agent-2)

*this agent testing its own cities for Agent-2's delegated zone*

**Model sees**

```json
{
  "question": "Agent-2 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Wiesbaden"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b24 · SPATIAL_RELATIONSHIP_BUFFER

> List all cities within 50 km of Karlsruhe

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
List all cities within 50 km of Karlsruhe
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: List all cities within 50 km of Karlsruhe
```

**Model must answer**

```json
{
  "spatial": ["Karlsruhe"],
  "operations": ["Buffer", "Within"],
  "distance_km": 50,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "List all cities within 50 km of Karlsruhe",
  "spatial": ["Karlsruhe"],
  "distance_km": 50.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Karlsruhe"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b25 · SPATIAL_RELATIONSHIP_BUFFER

> What cities lie near Koblenz, within 40 km?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
What cities lie near Koblenz, within 40 km?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: What cities lie near Koblenz, within 40 km?
```

**Model must answer**

```json
{
  "spatial": ["Koblenz"],
  "operations": ["Buffer", "Within"],
  "distance_km": 40,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Koblenz']",
  "entity_type": "city",
  "spatial": ["Koblenz"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "What cities lie near Koblenz, within 40 km?",
  "spatial": ["Koblenz"],
  "distance_km": 40.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Koblenz"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b26 · SPATIAL_RELATIONSHIP_BUFFER

> Cities within 70 km of Braunschweig

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Cities within 70 km of Braunschweig
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities within 70 km of Braunschweig
```

**Model must answer**

```json
{
  "spatial": ["Braunschweig"],
  "operations": ["Buffer", "Within"],
  "distance_km": 70,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Cities within 70 km of Braunschweig",
  "spatial": ["Braunschweig"],
  "distance_km": 70.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Braunschweig"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b27 · SPATIAL_RELATIONSHIP_BUFFER

> Which towns are within 35 km of Oldenburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which towns are within 35 km of Oldenburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which towns are within 35 km of Oldenburg?
```

**Model must answer**

```json
{
  "spatial": ["Oldenburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 35,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which towns are within 35 km of Oldenburg?",
  "spatial": ["Oldenburg"],
  "distance_km": 35.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Oldenburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b28 · SPATIAL_RELATIONSHIP_BUFFER

> Find every city in a 60 km radius of Ingolstadt

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Find every city in a 60 km radius of Ingolstadt
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Find every city in a 60 km radius of Ingolstadt
```

**Model must answer**

```json
{
  "spatial": ["Ingolstadt"],
  "operations": ["Buffer", "Within"],
  "distance_km": 60,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Ingolstadt']",
  "entity_type": "city",
  "spatial": ["Ingolstadt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Find every city in a 60 km radius of Ingolstadt",
  "spatial": ["Ingolstadt"],
  "distance_km": 60.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Ingolstadt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b29 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are close to Bamberg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are close to Bamberg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are close to Bamberg?
```

**Model must answer**

```json
{
  "spatial": ["Bamberg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 100,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bamberg']",
  "entity_type": "city",
  "spatial": ["Bamberg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are close to Bamberg?",
  "spatial": ["Bamberg"],
  "distance_km": 100.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Bamberg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b30 · SPATIAL_RELATIONSHIP_BUFFER · validation

> Cities that are at most 45 km from Siegen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 5 | SQL · within (answering Agent-1) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 6 | SQL · within (answering Agent-2) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Cities that are at most 45 km from Siegen
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities that are at most 45 km from Siegen
```

**Model must answer**

```json
{
  "spatial": ["Siegen"],
  "operations": ["Buffer", "Within"],
  "distance_km": 45,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Cities that are at most 45 km from Siegen",
  "spatial": ["Siegen"],
  "distance_km": 45.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Siegen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 5 · SQL · within (answering Agent-1)

*this agent testing its own cities for Agent-1's delegated zone*

**Model sees**

```json
{
  "question": "Agent-1 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Siegen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 6 · SQL · within (answering Agent-2)

*this agent testing its own cities for Agent-2's delegated zone*

**Model sees**

```json
{
  "question": "Agent-2 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": ["Siegen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b31 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities lie within 20 km of Fulda?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 20 km of Fulda?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie within 20 km of Fulda?
```

**Model must answer**

```json
{
  "spatial": ["Fulda"],
  "operations": ["Buffer", "Within"],
  "distance_km": 20,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities lie within 20 km of Fulda?",
  "spatial": ["Fulda"],
  "distance_km": 20.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Fulda"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b32 · SPATIAL_RELATIONSHIP_BUFFER

> Show the cities within 25 km of Gießen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Show the cities within 25 km of Gießen
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Show the cities within 25 km of Gießen
```

**Model must answer**

```json
{
  "spatial": ["Gießen"],
  "operations": ["Buffer", "Within"],
  "distance_km": 25,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Gießen']",
  "entity_type": "city",
  "spatial": ["Gießen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Show the cities within 25 km of Gießen",
  "spatial": ["Gießen"],
  "distance_km": 25.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Gießen"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b33 · SPATIAL_RELATIONSHIP_BUFFER

> What cities are within 30 kilometres of Darmstadt?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
What cities are within 30 kilometres of Darmstadt?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: What cities are within 30 kilometres of Darmstadt?
```

**Model must answer**

```json
{
  "spatial": ["Darmstadt"],
  "operations": ["Buffer", "Within"],
  "distance_km": 30,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Darmstadt']",
  "entity_type": "city",
  "spatial": ["Darmstadt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "What cities are within 30 kilometres of Darmstadt?",
  "spatial": ["Darmstadt"],
  "distance_km": 30.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Darmstadt"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b34 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are less than 80 km from Cottbus?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are less than 80 km from Cottbus?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are less than 80 km from Cottbus?
```

**Model must answer**

```json
{
  "spatial": ["Cottbus"],
  "operations": ["Buffer", "Within"],
  "distance_km": 80,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are less than 80 km from Cottbus?",
  "spatial": ["Cottbus"],
  "distance_km": 80.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Cottbus"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b35 · SPATIAL_RELATIONSHIP_BUFFER

> cities within 50km of gera

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
cities within 50km of gera
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: cities within 50km of gera
```

**Model must answer**

```json
{
  "spatial": ["Gera"],
  "operations": ["Buffer", "Within"],
  "distance_km": 50,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Gera']",
  "entity_type": "city",
  "spatial": ["Gera"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "cities within 50km of gera",
  "spatial": ["Gera"],
  "distance_km": 50.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Gera"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b36 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities surround Weimar within 40 km?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities surround Weimar within 40 km?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities surround Weimar within 40 km?
```

**Model must answer**

```json
{
  "spatial": ["Weimar"],
  "operations": ["Buffer", "Within"],
  "distance_km": 40,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Weimar']",
  "entity_type": "city",
  "spatial": ["Weimar"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities surround Weimar within 40 km?",
  "spatial": ["Weimar"],
  "distance_km": 40.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Weimar"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b37 · SPATIAL_RELATIONSHIP_BUFFER

> Name the cities within 90 km of Wolfsburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Name the cities within 90 km of Wolfsburg
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Name the cities within 90 km of Wolfsburg
```

**Model must answer**

```json
{
  "spatial": ["Wolfsburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 90,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Wolfsburg']",
  "entity_type": "city",
  "spatial": ["Wolfsburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Name the cities within 90 km of Wolfsburg",
  "spatial": ["Wolfsburg"],
  "distance_km": 90.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Wolfsburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b38 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities lie within 65 km of Flensburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 65 km of Flensburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie within 65 km of Flensburg?
```

**Model must answer**

```json
{
  "spatial": ["Flensburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 65,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Flensburg']",
  "entity_type": "city",
  "spatial": ["Flensburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities lie within 65 km of Flensburg?",
  "spatial": ["Flensburg"],
  "distance_km": 65.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Flensburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b39 · SPATIAL_RELATIONSHIP_BUFFER

> Cities near Stralsund

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Cities near Stralsund
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities near Stralsund
```

**Model must answer**

```json
{
  "spatial": ["Stralsund"],
  "operations": ["Buffer", "Within"],
  "distance_km": 100,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Stralsund']",
  "entity_type": "city",
  "spatial": ["Stralsund"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Cities near Stralsund",
  "spatial": ["Stralsund"],
  "distance_km": 100.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Stralsund"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b40 · SPATIAL_RELATIONSHIP_BUFFER · validation

> Which cities are within 55 km of Görlitz?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 55 km of Görlitz?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 55 km of Görlitz?
```

**Model must answer**

```json
{
  "spatial": ["Görlitz"],
  "operations": ["Buffer", "Within"],
  "distance_km": 55,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Görlitz']",
  "entity_type": "city",
  "spatial": ["Görlitz"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 55 km of Görlitz?",
  "spatial": ["Görlitz"],
  "distance_km": 55.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Görlitz"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b41 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 5 km of Bochum?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 5 km of Bochum?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 5 km of Bochum?
```

**Model must answer**

```json
{
  "spatial": ["Bochum"],
  "operations": ["Buffer", "Within"],
  "distance_km": 5,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bochum']",
  "entity_type": "city",
  "spatial": ["Bochum"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 5 km of Bochum?",
  "spatial": ["Bochum"],
  "distance_km": 5.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Bochum"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b42 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities lie within 300 km of Kassel?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 300 km of Kassel?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie within 300 km of Kassel?
```

**Model must answer**

```json
{
  "spatial": ["Kassel"],
  "operations": ["Buffer", "Within"],
  "distance_km": 300,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities lie within 300 km of Kassel?",
  "spatial": ["Kassel"],
  "distance_km": 300.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b43 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 20 km of München?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 20 km of Munich?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 20 km of Munich?
```

**Model must answer**

```json
{
  "spatial": ["Munich"],
  "operations": ["Buffer", "Within"],
  "distance_km": 20,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 20 km of München?",
  "spatial": ["Munich"],
  "distance_km": 20.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b44 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 40 km of the city of Hamburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 40 km of the city of Hamburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 40 km of the city of Hamburg?
```

**Model must answer**

```json
{
  "spatial": ["Hamburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 40,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 40 km of the city of Hamburg?",
  "spatial": ["Hamburg"],
  "distance_km": 40.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b45 · SPATIAL_RELATIONSHIP_BUFFER

> cities within 12.5 km of Mainz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
cities within 12.5 km of Mainz
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: cities within 12.5 km of Mainz
```

**Model must answer**

```json
{
  "spatial": ["Mainz"],
  "operations": ["Buffer", "Within"],
  "distance_km": 12.5,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "cities within 12.5 km of Mainz",
  "spatial": ["Mainz"],
  "distance_km": 12.5
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b46 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are within 25 km of Aschaffenburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are within 25 km of Aschaffenburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are within 25 km of Aschaffenburg?
```

**Model must answer**

```json
{
  "spatial": ["Aschaffenburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 25,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Aschaffenburg']",
  "entity_type": "city",
  "spatial": ["Aschaffenburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are within 25 km of Aschaffenburg?",
  "spatial": ["Aschaffenburg"],
  "distance_km": 25.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Aschaffenburg"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b47 · SPATIAL_RELATIONSHIP_BUFFER

> Give me the cities within Hessen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · within (answering Agent-1) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |
| 4 | SQL · within (answering Agent-2) | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Give me the cities within Hessen
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Give me the cities within Hessen
```

**Model must answer**

```json
{
  "spatial": ["Hessen"],
  "operations": ["Buffer", "Within"],
  "distance_km": 0,
  "target_entity": "city"
}
```

### 3 · SQL · within (answering Agent-1)

*this agent testing its own cities for Agent-1's delegated zone*

**Model sees**

```json
{
  "question": "Agent-1 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": []
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### 4 · SQL · within (answering Agent-2)

*this agent testing its own cities for Agent-2's delegated zone*

**Model sees**

```json
{
  "question": "Agent-2 asks which of our cities lie inside this zone",
  "target_entity": "city",
  "exclude": []
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b48 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are located in Bavaria?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are located in Bavaria?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are located in Bavaria?
```

**Model must answer**

```json
{
  "spatial": ["Bayern"],
  "operations": ["Buffer", "Within"],
  "distance_km": 0,
  "target_entity": "city"
}
```

---

## b49 · SPATIAL_RELATIONSHIP_BUFFER

> List all cities inside Sachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |

### 1 · Classify

**Model sees**

```text
List all cities inside Sachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: List all cities inside Sachsen
```

**Model must answer**

```json
{
  "spatial": ["Sachsen"],
  "operations": ["Buffer", "Within"],
  "distance_km": 0,
  "target_entity": "city"
}
```

---

## b50 · SPATIAL_RELATIONSHIP_BUFFER · validation

> what cities are in niedersachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |

### 1 · Classify

**Model sees**

```text
what cities are in Niedersachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: what cities are in Niedersachsen
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen"],
  "operations": ["Buffer", "Within"],
  "distance_km": 0,
  "target_entity": "city"
}
```

---

## b51 · SPATIAL_RELATIONSHIP_BUFFER

> Show me every city that lies within the Saarland

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |

### 1 · Classify

**Model sees**

```text
Show me every city that lies within the Saarland
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Show me every city that lies within the Saarland
```

**Model must answer**

```json
{
  "spatial": ["Saarland"],
  "operations": ["Buffer", "Within"],
  "distance_km": 0,
  "target_entity": "city"
}
```

---

## b52 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities does Brandenburg contain?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (state) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |

### 1 · Classify

**Model sees**

```text
Which cities does Brandenburg contain?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities does Brandenburg contain?
```

**Model must answer**

```json
{
  "spatial": ["Brandenburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 0,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (state)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these state names: ['Brandenburg']",
  "entity_type": "state",
  "spatial": ["Brandenburg"]
}
```

**Model must answer**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

---

## b53 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are in the state of Hamburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are in the state of Hamburg?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are in the state of Hamburg?
```

**Model must answer**

```json
{
  "spatial": ["Hamburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 0,
  "target_entity": "city"
}
```

---

## b54 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities lie within 25 km of Schleswig-Holstein?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 25 km of Schleswig-Holstein?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie within 25 km of Schleswig-Holstein?
```

**Model must answer**

```json
{
  "spatial": ["Schleswig-Holstein"],
  "operations": ["Buffer", "Within"],
  "distance_km": 25,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities lie within 25 km of Schleswig-Holstein?",
  "spatial": ["Schleswig-Holstein"],
  "distance_km": 25.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b55 · SPATIAL_RELATIONSHIP_BUFFER

> What are the cities north of Hessen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |

### 1 · Classify

**Model sees**

```text
What are the cities north of Hessen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: What are the cities north of Hessen?
```

**Model must answer**

```json
{
  "spatial": ["Hessen"],
  "operations": ["Buffer", "Within"],
  "distance_km": null,
  "target_entity": "city",
  "direction": "north_of"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "What are the cities north of Hessen?",
  "spatial": ["Hessen"],
  "direction": "north_of",
  "radius_km": 1000.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

---

## b56 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities lie south of Thüringen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie south of Thüringen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie south of Thüringen?
```

**Model must answer**

```json
{
  "spatial": ["Thüringen"],
  "operations": ["Buffer", "Within"],
  "distance_km": null,
  "target_entity": "city",
  "direction": "south_of"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "Which cities lie south of Thüringen?",
  "spatial": ["Thüringen"],
  "direction": "south_of",
  "radius_km": 1000.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

---

## b57 · SPATIAL_RELATIONSHIP_BUFFER

> List the cities east of Niedersachsen

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |

### 1 · Classify

**Model sees**

```text
List the cities east of Niedersachsen
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: List the cities east of Niedersachsen
```

**Model must answer**

```json
{
  "spatial": ["Niedersachsen"],
  "operations": ["Buffer", "Within"],
  "distance_km": null,
  "target_entity": "city",
  "direction": "east_of"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "List the cities east of Niedersachsen",
  "spatial": ["Niedersachsen"],
  "direction": "east_of",
  "radius_km": 1000.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

---

## b58 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are west of Sachsen?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are west of Sachsen?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are west of Sachsen?
```

**Model must answer**

```json
{
  "spatial": ["Sachsen"],
  "operations": ["Buffer", "Within"],
  "distance_km": null,
  "target_entity": "city",
  "direction": "west_of"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "Which cities are west of Sachsen?",
  "spatial": ["Sachsen"],
  "direction": "west_of",
  "radius_km": 1000.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

---

## b59 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are east of Dortmund?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are east of Dortmund?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are east of Dortmund?
```

**Model must answer**

```json
{
  "spatial": ["Dortmund"],
  "operations": ["Buffer", "Within"],
  "distance_km": null,
  "target_entity": "city",
  "direction": "east_of"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Dortmund']",
  "entity_type": "city",
  "spatial": ["Dortmund"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "Which cities are east of Dortmund?",
  "spatial": ["Dortmund"],
  "direction": "east_of",
  "radius_km": 1000.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Dortmund"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b60 · SPATIAL_RELATIONSHIP_BUFFER · validation

> Which cities lie within 50 km north of Frankfurt am Main?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 50 km north of Frankfurt am Main?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities lie within 50 km north of Frankfurt am Main?
```

**Model must answer**

```json
{
  "spatial": ["Frankfurt am Main"],
  "operations": ["Buffer", "Within"],
  "distance_km": 50,
  "target_entity": "city",
  "direction": "north_of"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Frankfurt am Main']",
  "entity_type": "city",
  "spatial": ["Frankfurt am Main"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "Which cities lie within 50 km north of Frankfurt am Main?",
  "spatial": ["Frankfurt am Main"],
  "direction": "north_of",
  "radius_km": 50.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Frankfurt am Main"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b61 · SPATIAL_RELATIONSHIP_BUFFER

> cities to the south of Hamburg within 30 km

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |

### 1 · Classify

**Model sees**

```text
cities to the south of Hamburg within 30 km
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: cities to the south of Hamburg within 30 km
```

**Model must answer**

```json
{
  "spatial": ["Hamburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 30,
  "target_entity": "city",
  "direction": "south_of"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "cities to the south of Hamburg within 30 km",
  "spatial": ["Hamburg"],
  "direction": "south_of",
  "radius_km": 30.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

---

## b62 · SPATIAL_RELATIONSHIP_BUFFER

> Which towns lie west of Bavaria?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → sector | [sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_sector.txt) |

### 1 · Classify

**Model sees**

```text
Which towns lie west of Bavaria?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which towns lie west of Bavaria?
```

**Model must answer**

```json
{
  "spatial": ["Bayern"],
  "operations": ["Buffer", "Within"],
  "distance_km": null,
  "target_entity": "city",
  "direction": "west_of"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → sector

**Model sees**

```json
{
  "question": "Which towns lie west of Bavaria?",
  "spatial": ["Bayern"],
  "direction": "west_of",
  "radius_km": 1000.0
}
```

**Model must answer**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

---

## b63 · SPATIAL_RELATIONSHIP_BUFFER

> Cities that are at most 30 km from Bielefeld

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · shape fetch (city) | [sql_GEOMETRY_LOOKUP_fetch.txt](prompts/sql_GEOMETRY_LOOKUP_fetch.txt) |
| 4 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |
| 5 | SQL · SPATIAL_RELATIONSHIP_BUFFER → within | [sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_within.txt) |

### 1 · Classify

**Model sees**

```text
Cities that are at most 30 km from Bielefeld
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Cities that are at most 30 km from Bielefeld
```

**Model must answer**

```json
{
  "spatial": ["Bielefeld"],
  "operations": ["Buffer", "Within"],
  "distance_km": 30,
  "target_entity": "city"
}
```

### 3 · SQL · shape fetch (city)

**Model sees**

```json
{
  "question": "Fetch the stored shapes of these city names: ['Bielefeld']",
  "entity_type": "city",
  "spatial": ["Bielefeld"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### 4 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Cities that are at most 30 km from Bielefeld",
  "spatial": ["Bielefeld"],
  "distance_km": 30.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### 5 · SQL · SPATIAL_RELATIONSHIP_BUFFER → within

**Model sees**

```json
{
  "question": "Which of our cities lie inside this zone?",
  "target_entity": "city",
  "exclude": ["Bielefeld"]
}
```

**Model must answer**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

---

## b64 · SPATIAL_RELATIONSHIP_BUFFER

> Which cities are no more than 20 km away from Kiel?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Which cities are no more than 20 km away from Kiel?
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Which cities are no more than 20 km away from Kiel?
```

**Model must answer**

```json
{
  "spatial": ["Kiel"],
  "operations": ["Buffer", "Within"],
  "distance_km": 20,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Which cities are no more than 20 km away from Kiel?",
  "spatial": ["Kiel"],
  "distance_km": 20.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b65 · SPATIAL_RELATIONSHIP_BUFFER

> cities at most 60 km from Augsburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
cities at most 60 km from Augsburg
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: cities at most 60 km from Augsburg
```

**Model must answer**

```json
{
  "spatial": ["Augsburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 60,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "cities at most 60 km from Augsburg",
  "spatial": ["Augsburg"],
  "distance_km": 60.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b66 · SPATIAL_RELATIONSHIP_BUFFER

> Show the cities at most 15 km away from Mainz

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Show the cities at most 15 km away from Mainz
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Show the cities at most 15 km away from Mainz
```

**Model must answer**

```json
{
  "spatial": ["Mainz"],
  "operations": ["Buffer", "Within"],
  "distance_km": 15,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Show the cities at most 15 km away from Mainz",
  "spatial": ["Mainz"],
  "distance_km": 15.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

## b67 · SPATIAL_RELATIONSHIP_BUFFER

> Name every city no further than 40 km from Magdeburg

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |
| 2 | Extract | [extract_SPATIAL_RELATIONSHIP_BUFFER.txt](prompts/extract_SPATIAL_RELATIONSHIP_BUFFER.txt) |
| 3 | SQL · SPATIAL_RELATIONSHIP_BUFFER → zone | [sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt](prompts/sql_SPATIAL_RELATIONSHIP_BUFFER_zone.txt) |

### 1 · Classify

**Model sees**

```text
Name every city no further than 40 km from Magdeburg
```

**Model must answer**

```json
{"query_type": "SPATIAL_RELATIONSHIP_BUFFER"}
```

### 2 · Extract

**Model sees**

```text
Query: Name every city no further than 40 km from Magdeburg
```

**Model must answer**

```json
{
  "spatial": ["Magdeburg"],
  "operations": ["Buffer", "Within"],
  "distance_km": 40,
  "target_entity": "city"
}
```

### 3 · SQL · SPATIAL_RELATIONSHIP_BUFFER → zone

**Model sees**

```json
{
  "question": "Name every city no further than 40 km from Magdeburg",
  "spatial": ["Magdeburg"],
  "distance_km": 40.0
}
```

**Model must answer**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

---

# unrelated

## u01 · UNRELATED

> What is the capital of Italy?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
What is the capital of Italy?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u02 · UNRELATED

> How do I cook pasta?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
How do I cook pasta?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u03 · UNRELATED

> What was the population of Vienna in 2021?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
What was the population of Vienna in 2021?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u04 · UNRELATED

> Translate 'good morning' into Spanish

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Translate 'good morning' into Spanish
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u05 · UNRELATED

> Who is the current chancellor of Germany?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Who is the current chancellor of Germany?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u06 · UNRELATED

> Show me the weather forecast for tomorrow

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Show me the weather forecast for tomorrow
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u07 · UNRELATED

> How many people live in London?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
How many people live in London?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u08 · UNRELATED

> Write a short poem about rivers

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Write a short poem about rivers
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u09 · UNRELATED

> What is 25 times 4?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
What is 25 times 4?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u10 · UNRELATED · validation

> Which Swiss cantons border France?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Which Swiss cantons border France?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u11 · UNRELATED

> Which cities lie within 30 km of Salzburg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 30 km of Salzburg?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u12 · UNRELATED

> What is the population of Tyrol?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
What is the population of Tyrol?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u13 · UNRELATED

> Show me the boundary of Lombardy

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Show me the boundary of Lombardy
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u14 · UNRELATED

> Do France and Spain share a border?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Do France and Spain share a border?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u15 · UNRELATED

> Merge Belgium and the Netherlands into one shape

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Merge Belgium and the Netherlands into one shape
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u16 · UNRELATED

> How many marriages were there in Switzerland in 2015?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
How many marriages were there in Switzerland in 2015?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u17 · UNRELATED

> What's a good name for a cat?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
What's a good name for a cat?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u18 · UNRELATED

> Summarise the plot of Hamlet

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Summarise the plot of Hamlet
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u19 · UNRELATED

> What is the speed of light?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
What is the speed of light?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u20 · UNRELATED · validation

> Which language is spoken in Brazil?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Which language is spoken in Brazil?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u21 · UNRELATED

> Which cities lie within 20 km of Strasbourg?

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Which cities lie within 20 km of Strasbourg?
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u22 · UNRELATED

> Merge Austria and Switzerland into one shape

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Merge Austria and Switzerland into one shape
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u23 · UNRELATED

> Population of Salzburg in 2019

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Population of Salzburg in 2019
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u24 · UNRELATED

> hello

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
hello
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---

## u25 · UNRELATED

> Thanks, that's all for today

| # | Call | System prompt |
|---|---|---|
| 1 | Classify | [classify.txt](prompts/classify.txt) |

### 1 · Classify

**Model sees**

```text
Thanks, that's all for today
```

**Model must answer**

```json
{"query_type": "UNRELATED"}
```

---
