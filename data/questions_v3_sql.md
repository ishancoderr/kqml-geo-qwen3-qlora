# SQL examples to review — questions_v3.yaml

Every SQL example of `questions_v3.yaml`, grouped by SQL step. Generated — edit `questions_v3.yaml` (questions) or `finetune/reference_sql.py` (the correct SQL), not this file.

**Input** is what the SQL step is given (it never sees the user's question itself); **Correct SQL** is what the model is trained to write. `:name` placeholders are bound by the agent when the statement runs.

| SQL step | examples | different correct SQL |
|---|---|---|
| DIRECT_LOOKUP · fetch | 84 | 9 |
| DIRECT_LOOKUP · presence | 10 | 1 |
| GEOMETRY_LOOKUP · fetch | 118 | 2 |
| SPATIAL_OPERATION · buffer_within | 14 | 1 |
| SPATIAL_OPERATION · compute | 51 | 4 |
| SPATIAL_RELATIONSHIP · compute | 58 | 3 |
| SPATIAL_RELATIONSHIP_BUFFER · sector | 8 | 1 |
| SPATIAL_RELATIONSHIP_BUFFER · within | 55 | 1 |
| SPATIAL_RELATIONSHIP_BUFFER · zone | 52 | 1 |

## DIRECT_LOOKUP · fetch

### d01 — What was the population of Hessen in 2019?

**Input**

```json
{"question": "Fetch population of Hessen in [2019]", "entity_type": "state", "spatial": ["Hessen"], "temporal": [2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d01 — What was the population of Hessen in 2019?

**Input**

```json
{"question": "Agent-1 asks for population of Hessen in [2019]", "entity_type": "state", "spatial": ["Hessen"], "temporal": [2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d01 — What was the population of Hessen in 2019?

**Input**

```json
{"question": "Agent-2 asks for population of Hessen in [2019]", "entity_type": "state", "spatial": ["Hessen"], "temporal": [2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d02 — How many people lived in Sachsen and Thüringen in 2022?

**Input**

```json
{"question": "Fetch population of Sachsen, Thüringen in [2022]", "entity_type": "state", "spatial": ["Sachsen", "Thüringen"], "temporal": [2022], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d03 — Show me the number of marriages in Niedersachsen from 2018 to 2021.

**Input**

```json
{"question": "Fetch marriages of Niedersachsen in [2018, 2019, 2020, 2021]", "entity_type": "state", "spatial": ["Niedersachsen"], "temporal": [2018, 2019, 2020, 2021], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d04 — Live births in Bremen and Saarland, 2020

**Input**

```json
{"question": "Fetch live_births of Bremen, Saarland in [2020]", "entity_type": "state", "spatial": ["Bremen", "Saarland"], "temporal": [2020], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d05 — Give me population, marriages and live births for Rheinland-Pfalz in 2023.

**Input**

```json
{"question": "Fetch population, marriages, live_births of Rheinland-Pfalz in [2023]", "entity_type": "state", "spatial": ["Rheinland-Pfalz"], "temporal": [2023], "attributes": ["population", "marriages", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d05 — Give me population, marriages and live births for Rheinland-Pfalz in 2023.

**Input**

```json
{"question": "Agent-1 asks for population, marriages, live_births of Rheinland-Pfalz in [2023]", "entity_type": "state", "spatial": ["Rheinland-Pfalz"], "temporal": [2023], "attributes": ["population", "marriages", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d05 — Give me population, marriages and live births for Rheinland-Pfalz in 2023.

**Input**

```json
{"question": "Agent-2 asks for population, marriages, live_births of Rheinland-Pfalz in [2023]", "entity_type": "state", "spatial": ["Rheinland-Pfalz"], "temporal": [2023], "attributes": ["population", "marriages", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d06 — How many babies were born in Mecklenburg-Vorpommern in 2017?

**Input**

```json
{"question": "Fetch live_births of Mecklenburg-Vorpommern in [2017]", "entity_type": "state", "spatial": ["Mecklenburg-Vorpommern"], "temporal": [2017], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d07 — Population of every German state in 2018

**Input**

```json
{"question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2018]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"], "temporal": [2018], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d08 — Marriages in all federal states for 2022 and 2023

**Input**

```json
{"question": "Fetch marriages of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2022, 2023]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"], "temporal": [2022, 2023], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d09 — Inhabitants of Baden-Wuerttemberg between 2015 and 2019

**Input**

```json
{"question": "Fetch population of Baden-Württemberg in [2015, 2016, 2017, 2018, 2019]", "entity_type": "state", "spatial": ["Baden-Württemberg"], "temporal": [2015, 2016, 2017, 2018, 2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d10 · validation — How many residents did Brandenburg have in 2020?

**Input**

```json
{"question": "Fetch population of Brandenburg in [2020]", "entity_type": "state", "spatial": ["Brandenburg"], "temporal": [2020], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d11 — Number of marriages and births in Schleswig-Holstein in 2016

**Input**

```json
{"question": "Fetch marriages, live_births of Schleswig-Holstein in [2016]", "entity_type": "state", "spatial": ["Schleswig-Holstein"], "temporal": [2016], "attributes": ["marriages", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d12 — Compare the population of Berlin, Hamburg and Bremen in 2020

**Input**

```json
{"question": "Fetch population of Berlin, Hamburg, Bremen in [2020]", "entity_type": "state", "spatial": ["Berlin", "Hamburg", "Bremen"], "temporal": [2020], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d12 — Compare the population of Berlin, Hamburg and Bremen in 2020

**Input**

```json
{"question": "Agent-1 asks for population of Berlin, Hamburg, Bremen in [2020]", "entity_type": "state", "spatial": ["Berlin", "Hamburg", "Bremen"], "temporal": [2020], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d12 — Compare the population of Berlin, Hamburg and Bremen in 2020

**Input**

```json
{"question": "Agent-2 asks for population of Berlin, Hamburg, Bremen in [2020]", "entity_type": "state", "spatial": ["Berlin", "Hamburg", "Bremen"], "temporal": [2020], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d13 — nordrhein westfalen population 2024

**Input**

```json
{"question": "Fetch population of Nordrhein-Westfalen in [2024]", "entity_type": "state", "spatial": ["Nordrhein-Westfalen"], "temporal": [2024], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d14 — What were the live births in Sachsen-Anhalt in 2019 and 2021?

**Input**

```json
{"question": "Fetch live_births of Sachsen-Anhalt in [2019, 2021]", "entity_type": "state", "spatial": ["Sachsen-Anhalt"], "temporal": [2019, 2021], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d15 — Population and marriages for Bayern and Baden-Württemberg, 2014-2016

**Input**

```json
{"question": "Fetch population, marriages of Bayern, Baden-Württemberg in [2014, 2015, 2016]", "entity_type": "state", "spatial": ["Bayern", "Baden-Württemberg"], "temporal": [2014, 2015, 2016], "attributes": ["population", "marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d16 — How many couples got married in Hessen in 2023?

**Input**

```json
{"question": "Fetch marriages of Hessen in [2023]", "entity_type": "state", "spatial": ["Hessen"], "temporal": [2023], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d17 — Tell me the population figures for Thüringen, Sachsen and Sachsen-Anhalt in 2020.

**Input**

```json
{"question": "Fetch population of Thüringen, Sachsen, Sachsen-Anhalt in [2020]", "entity_type": "state", "spatial": ["Thüringen", "Sachsen", "Sachsen-Anhalt"], "temporal": [2020], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d18 — Bavaria population in 2022

**Input**

```json
{"question": "Fetch population of Bayern in [2022]", "entity_type": "state", "spatial": ["Bayern"], "temporal": [2022], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d19 — How many marriages were registered in Lower Saxony in 2019?

**Input**

```json
{"question": "Fetch marriages of Niedersachsen in [2019]", "entity_type": "state", "spatial": ["Niedersachsen"], "temporal": [2019], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d20 · validation — Live birth data for Hamburg and Schleswig-Holstein from 2021 to 2024

**Input**

```json
{"question": "Fetch live_births of Hamburg, Schleswig-Holstein in [2021, 2022, 2023, 2024]", "entity_type": "state", "spatial": ["Hamburg", "Schleswig-Holstein"], "temporal": [2021, 2022, 2023, 2024], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d20 · validation — Live birth data for Hamburg and Schleswig-Holstein from 2021 to 2024

**Input**

```json
{"question": "Agent-1 asks for live_births of Hamburg, Schleswig-Holstein in [2021, 2022, 2023, 2024]", "entity_type": "state", "spatial": ["Hamburg", "Schleswig-Holstein"], "temporal": [2021, 2022, 2023, 2024], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d20 · validation — Live birth data for Hamburg and Schleswig-Holstein from 2021 to 2024

**Input**

```json
{"question": "Agent-2 asks for live_births of Hamburg, Schleswig-Holstein in [2021, 2022, 2023, 2024]", "entity_type": "state", "spatial": ["Hamburg", "Schleswig-Holstein"], "temporal": [2021, 2022, 2023, 2024], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d23 — What was the population of Saarland in 1995?

**Input**

```json
{"question": "Fetch population of Saarland in [1995]", "entity_type": "state", "spatial": ["Saarland"], "temporal": [1995], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d24 — Live births in Hessen and Sachsen from 2010 to 2013

**Input**

```json
{"question": "Fetch live_births of Hessen, Sachsen in [2010, 2011, 2012, 2013]", "entity_type": "state", "spatial": ["Hessen", "Sachsen"], "temporal": [2010, 2011, 2012, 2013], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d25 — Marriages in Brandenburg, Berlin and Hamburg in 2018

**Input**

```json
{"question": "Fetch marriages of Brandenburg, Berlin, Hamburg in [2018]", "entity_type": "state", "spatial": ["Brandenburg", "Berlin", "Hamburg"], "temporal": [2018], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d26 — Population of all German states in 1990

**Input**

```json
{"question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [1990]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"], "temporal": [1990], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d27 — Number of inhabitants in Nordrhein-Westfalen between 2003 and 2006

**Input**

```json
{"question": "Fetch population of Nordrhein-Westfalen in [2003, 2004, 2005, 2006]", "entity_type": "state", "spatial": ["Nordrhein-Westfalen"], "temporal": [2003, 2004, 2005, 2006], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d28 — How many marriages were there in Thüringen in 2011 and 2013?

**Input**

```json
{"question": "Fetch marriages of Thüringen in [2011, 2013]", "entity_type": "state", "spatial": ["Thüringen"], "temporal": [2011, 2013], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d29 — Give me the live births for Bavaria in 2009

**Input**

```json
{"question": "Fetch live_births of Bayern in [2009]", "entity_type": "state", "spatial": ["Bayern"], "temporal": [2009], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d30 · validation — Population of Saxony-Anhalt in 2016

**Input**

```json
{"question": "Fetch population of Sachsen-Anhalt in [2016]", "entity_type": "state", "spatial": ["Sachsen-Anhalt"], "temporal": [2016], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d31 — births and marriages in mecklenburg vorpommern 2002

**Input**

```json
{"question": "Fetch live_births, marriages of Mecklenburg-Vorpommern in [2002]", "entity_type": "state", "spatial": ["Mecklenburg-Vorpommern"], "temporal": [2002], "attributes": ["live_births", "marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d32 — Population and live births for Niedersachsen and Bremen in 2007

**Input**

```json
{"question": "Fetch population, live_births of Niedersachsen, Bremen in [2007]", "entity_type": "state", "spatial": ["Niedersachsen", "Bremen"], "temporal": [2007], "attributes": ["population", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d32 — Population and live births for Niedersachsen and Bremen in 2007

**Input**

```json
{"question": "Agent-1 asks for population, live_births of Niedersachsen, Bremen in [2007]", "entity_type": "state", "spatial": ["Niedersachsen", "Bremen"], "temporal": [2007], "attributes": ["population", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d32 — Population and live births for Niedersachsen and Bremen in 2007

**Input**

```json
{"question": "Agent-2 asks for population, live_births of Niedersachsen, Bremen in [2007]", "entity_type": "state", "spatial": ["Niedersachsen", "Bremen"], "temporal": [2007], "attributes": ["population", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d33 — How many people lived in Schleswig-Holstein in 1999?

**Input**

```json
{"question": "Fetch population of Schleswig-Holstein in [1999]", "entity_type": "state", "spatial": ["Schleswig-Holstein"], "temporal": [1999], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d34 — Show marriages for every federal state in 2019

**Input**

```json
{"question": "Fetch marriages of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2019]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"], "temporal": [2019], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d35 — Population of Rheinland-Pfalz from 1991 to 1994

**Input**

```json
{"question": "Fetch population of Rheinland-Pfalz in [1991, 1992, 1993, 1994]", "entity_type": "state", "spatial": ["Rheinland-Pfalz"], "temporal": [1991, 1992, 1993, 1994], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d39 — Population of Hesse in 2001

**Input**

```json
{"question": "Fetch population of Hessen in [2001]", "entity_type": "state", "spatial": ["Hessen"], "temporal": [2001], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d40 · validation — Give me population, marriages and live births for Saarland and Thüringen in 2004

**Input**

```json
{"question": "Fetch population, marriages, live_births of Saarland, Thüringen in [2004]", "entity_type": "state", "spatial": ["Saarland", "Thüringen"], "temporal": [2004], "attributes": ["population", "marriages", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d41 — How many babies were born in Sachsen in 1996?

**Input**

```json
{"question": "Fetch live_births of Sachsen in [1996]", "entity_type": "state", "spatial": ["Sachsen"], "temporal": [1996], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d42 — Marriages in Baden-Württemberg from 2016 to 2019

**Input**

```json
{"question": "Fetch marriages of Baden-Württemberg in [2016, 2017, 2018, 2019]", "entity_type": "state", "spatial": ["Baden-Württemberg"], "temporal": [2016, 2017, 2018, 2019], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d42 — Marriages in Baden-Württemberg from 2016 to 2019

**Input**

```json
{"question": "Agent-1 asks for marriages of Baden-Württemberg in [2016, 2017, 2018, 2019]", "entity_type": "state", "spatial": ["Baden-Württemberg"], "temporal": [2016, 2017, 2018, 2019], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d42 — Marriages in Baden-Württemberg from 2016 to 2019

**Input**

```json
{"question": "Agent-2 asks for marriages of Baden-Württemberg in [2016, 2017, 2018, 2019]", "entity_type": "state", "spatial": ["Baden-Württemberg"], "temporal": [2016, 2017, 2018, 2019], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d43 — nrw marriages 2010

**Input**

```json
{"question": "Fetch marriages of Nordrhein-Westfalen in [2010]", "entity_type": "state", "spatial": ["Nordrhein-Westfalen"], "temporal": [2010], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d44 — Population in Berlin in 1990 and 2000

**Input**

```json
{"question": "Fetch population of Berlin in [1990, 2000]", "entity_type": "state", "spatial": ["Berlin"], "temporal": [1990, 2000], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d45 — Live births in Brandenburg, Mecklenburg-Vorpommern and Sachsen-Anhalt in 2015

**Input**

```json
{"question": "Fetch live_births of Brandenburg, Mecklenburg-Vorpommern, Sachsen-Anhalt in [2015]", "entity_type": "state", "spatial": ["Brandenburg", "Mecklenburg-Vorpommern", "Sachsen-Anhalt"], "temporal": [2015], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d46 — How many residents did Niedersachsen have in 2012?

**Input**

```json
{"question": "Fetch population of Niedersachsen in [2012]", "entity_type": "state", "spatial": ["Niedersachsen"], "temporal": [2012], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d47 — Marriages and live births in Hamburg and Schleswig-Holstein, 2005

**Input**

```json
{"question": "Fetch marriages, live_births of Hamburg, Schleswig-Holstein in [2005]", "entity_type": "state", "spatial": ["Hamburg", "Schleswig-Holstein"], "temporal": [2005], "attributes": ["marriages", "live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d48 — What were the population figures of Thüringen from 2017 to 2019?

**Input**

```json
{"question": "Fetch population of Thüringen in [2017, 2018, 2019]", "entity_type": "state", "spatial": ["Thüringen"], "temporal": [2017, 2018, 2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d49 — Population of Nordrhein-Westfalen and Rheinland-Pfalz in 2013

**Input**

```json
{"question": "Fetch population of Nordrhein-Westfalen, Rheinland-Pfalz in [2013]", "entity_type": "state", "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"], "temporal": [2013], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d49 — Population of Nordrhein-Westfalen and Rheinland-Pfalz in 2013

**Input**

```json
{"question": "Agent-1 asks for population of Nordrhein-Westfalen, Rheinland-Pfalz in [2013]", "entity_type": "state", "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"], "temporal": [2013], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d49 — Population of Nordrhein-Westfalen and Rheinland-Pfalz in 2013

**Input**

```json
{"question": "Agent-2 asks for population of Nordrhein-Westfalen, Rheinland-Pfalz in [2013]", "entity_type": "state", "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"], "temporal": [2013], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d50 · validation — Live births for all states in 2000

**Input**

```json
{"question": "Fetch live_births of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2000]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"], "temporal": [2000], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d51 — Population of Hessen 2015-2015

**Input**

```json
{"question": "Fetch population of Hessen in [2015]", "entity_type": "state", "spatial": ["Hessen"], "temporal": [2015], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d52 — Live births in Sachsen from 2019 back to 2016

**Input**

```json
{"question": "Fetch live_births of Sachsen in [2016, 2017, 2018, 2019]", "entity_type": "state", "spatial": ["Sachsen"], "temporal": [2016, 2017, 2018, 2019], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d53 — Marriages in Brandenburg and brandenburg in 2010

**Input**

```json
{"question": "Fetch marriages of Brandenburg in [2010]", "entity_type": "state", "spatial": ["Brandenburg"], "temporal": [2010], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d54 — What were births, people and marriages in Saarland in 2003?

**Input**

```json
{"question": "Fetch live_births, population, marriages of Saarland in [2003]", "entity_type": "state", "spatial": ["Saarland"], "temporal": [2003], "attributes": ["live_births", "population", "marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births, sd.population AS population, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d55 — POPULATION OF THUERINGEN IN 2014

**Input**

```json
{"question": "Fetch population of Thüringen in [2014]", "entity_type": "state", "spatial": ["Thüringen"], "temporal": [2014], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d56 — population sachsen 2009 2011 2013

**Input**

```json
{"question": "Fetch population of Sachsen in [2009, 2011, 2013]", "entity_type": "state", "spatial": ["Sachsen"], "temporal": [2009, 2011, 2013], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d58 — Give me data for Niedersachsen in 2016

**Input**

```json
{"question": "Fetch population of Niedersachsen in [2016]", "entity_type": "state", "spatial": ["Niedersachsen"], "temporal": [2016], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d59 — Population of Mecklenburg-Vorpommern and Sachsen-Anhalt in 1990 and in 2019

**Input**

```json
{"question": "Fetch population of Mecklenburg-Vorpommern, Sachsen-Anhalt in [1990, 2019]", "entity_type": "state", "spatial": ["Mecklenburg-Vorpommern", "Sachsen-Anhalt"], "temporal": [1990, 2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d60 · validation — How many people lived in Germany's federal states in 2011?

**Input**

```json
{"question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2011]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"], "temporal": [2011], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d62 — What was the combined population of Sachsen and Sachsen-Anhalt in 2017?

**Input**

```json
{"question": "Fetch population of Sachsen, Sachsen-Anhalt in [2017]", "entity_type": "state", "spatial": ["Sachsen", "Sachsen-Anhalt"], "temporal": [2017], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d63 — How many marriages were there in Hamburg and Bremen together in 2016?

**Input**

```json
{"question": "Fetch marriages of Hamburg, Bremen in [2016]", "entity_type": "state", "spatial": ["Hamburg", "Bremen"], "temporal": [2016], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d64 — Total live births of Niedersachsen, Bremen and Hamburg from 2015 to 2017

**Input**

```json
{"question": "Fetch live_births of Niedersachsen, Bremen, Hamburg in [2015, 2016, 2017]", "entity_type": "state", "spatial": ["Niedersachsen", "Bremen", "Hamburg"], "temporal": [2015, 2016, 2017], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d66 — cumulative population of all german states in 2016

**Input**

```json
{"question": "Fetch population of Baden-Württemberg, Bayern, Berlin, Brandenburg, Bremen, Hamburg, Hessen, Mecklenburg-Vorpommern, Niedersachsen, Nordrhein-Westfalen, Rheinland-Pfalz, Saarland, Sachsen, Sachsen-Anhalt, Schleswig-Holstein, Thüringen in [2016]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"], "temporal": [2016], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### d67 — Population of Saarland plus Rheinland-Pfalz in 2018

**Input**

```json
{"question": "Fetch population of Saarland, Rheinland-Pfalz in [2018]", "entity_type": "state", "spatial": ["Saarland", "Rheinland-Pfalz"], "temporal": [2018], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o67 — Merge Bayern and Baden-Württemberg and give me the total population of that area for 2018

**Input**

```json
{"question": "Fetch population of Bayern, Baden-Württemberg in [2018]", "entity_type": "state", "spatial": ["Bayern", "Baden-Württemberg"], "temporal": [2018], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o68 — If you join Berlin and Brandenburg into one region, what is its population in 2019?

**Input**

```json
{"question": "Fetch population of Berlin, Brandenburg in [2019]", "entity_type": "state", "spatial": ["Berlin", "Brandenburg"], "temporal": [2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o69 — Merge Sachsen and Thüringen into one shape and give me their combined population for 2018

**Input**

```json
{"question": "Fetch population of Sachsen, Thüringen in [2018]", "entity_type": "state", "spatial": ["Sachsen", "Thüringen"], "temporal": [2018], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o70 · validation — Combine Hamburg and Schleswig-Holstein into one area: show the shape and the total live births in 2019

**Input**

```json
{"question": "Fetch live_births of Hamburg, Schleswig-Holstein in [2019]", "entity_type": "state", "spatial": ["Hamburg", "Schleswig-Holstein"], "temporal": [2019], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o71 — Merge Niedersachsen and Bremen into one shape and give me its population in 2018

**Input**

```json
{"question": "Fetch population of Niedersachsen, Bremen in [2018]", "entity_type": "state", "spatial": ["Niedersachsen", "Bremen"], "temporal": [2018], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o72 — Join Bayern and Thüringen into one area and tell me the total marriages there in 2017

**Input**

```json
{"question": "Fetch marriages of Bayern, Thüringen in [2017]", "entity_type": "state", "spatial": ["Bayern", "Thüringen"], "temporal": [2017], "attributes": ["marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o73 — Combine Berlin, Brandenburg and Sachsen into one region: show it and the combined population for 2016

**Input**

```json
{"question": "Fetch population of Berlin, Brandenburg, Sachsen in [2016]", "entity_type": "state", "spatial": ["Berlin", "Brandenburg", "Sachsen"], "temporal": [2016], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o74 — Create one area from Rheinland-Pfalz and Saarland and give me its live births from 2015 to 2017

**Input**

```json
{"question": "Fetch live_births of Rheinland-Pfalz, Saarland in [2015, 2016, 2017]", "entity_type": "state", "spatial": ["Rheinland-Pfalz", "Saarland"], "temporal": [2015, 2016, 2017], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o75 — Merge Hessen and Nordrhein-Westfalen into one shape. What was its population in 2019?

**Input**

```json
{"question": "Fetch population of Hessen, Nordrhein-Westfalen in [2019]", "entity_type": "state", "spatial": ["Hessen", "Nordrhein-Westfalen"], "temporal": [2019], "attributes": ["population"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o76 — Union of Baden-Württemberg and Bayern with the total live births in 2018

**Input**

```json
{"question": "Fetch live_births of Baden-Württemberg, Bayern in [2018]", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern"], "temporal": [2018], "attributes": ["live_births"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.live_births AS live_births FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```

### o77 — Merge Mecklenburg-Vorpommern and Schleswig-Holstein into one shape and give me the population and marriages for 2016

**Input**

```json
{"question": "Fetch population, marriages of Mecklenburg-Vorpommern, Schleswig-Holstein in [2016]", "entity_type": "state", "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"], "temporal": [2016], "attributes": ["population", "marriages"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, sd.stat_year AS year, sd.population AS population, sd.marriages AS marriages FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names) AND sd.stat_year = ANY(:years) ORDER BY s.state_name, sd.stat_year
```


## DIRECT_LOOKUP · presence

### d04 — Live births in Bremen and Saarland, 2020

**Input**

```json
{"question": "Which of these state names have any row at all: ['Saarland']", "entity_type": "state", "spatial": ["Saarland"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d08 — Marriages in all federal states for 2022 and 2023

**Input**

```json
{"question": "Which of these state names have any row at all: ['Bremen', 'Saarland']", "entity_type": "state", "spatial": ["Bremen", "Saarland"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d12 — Compare the population of Berlin, Hamburg and Bremen in 2020

**Input**

```json
{"question": "Which of these state names have any row at all: ['Bremen']", "entity_type": "state", "spatial": ["Bremen"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d17 — Tell me the population figures for Thüringen, Sachsen and Sachsen-Anhalt in 2020.

**Input**

```json
{"question": "Which of these state names have any row at all: ['Sachsen-Anhalt']", "entity_type": "state", "spatial": ["Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d25 — Marriages in Brandenburg, Berlin and Hamburg in 2018

**Input**

```json
{"question": "Which of these state names have any row at all: ['Berlin', 'Hamburg']", "entity_type": "state", "spatial": ["Berlin", "Hamburg"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d26 — Population of all German states in 1990

**Input**

```json
{"question": "Which of these state names have any row at all: ['Baden-Württemberg', 'Bayern', 'Berlin', 'Bremen', 'Hamburg']", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Bremen", "Hamburg"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d29 — Give me the live births for Bavaria in 2009

**Input**

```json
{"question": "Which of these state names have any row at all: ['Bayern']", "entity_type": "state", "spatial": ["Bayern"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d42 — Marriages in Baden-Württemberg from 2016 to 2019

**Input**

```json
{"question": "Which of these state names have any row at all: ['Baden-Württemberg']", "entity_type": "state", "spatial": ["Baden-Württemberg"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d44 — Population in Berlin in 1990 and 2000

**Input**

```json
{"question": "Which of these state names have any row at all: ['Berlin']", "entity_type": "state", "spatial": ["Berlin"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```

### d47 — Marriages and live births in Hamburg and Schleswig-Holstein, 2005

**Input**

```json
{"question": "Which of these state names have any row at all: ['Hamburg']", "entity_type": "state", "spatial": ["Hamburg"]}
```

**Correct SQL**

```sql
SELECT DISTINCT s.state_name AS entity_name FROM state_demographics sd JOIN states s ON s.state_id = sd.state_id WHERE s.state_name = ANY(:names)
```


## GEOMETRY_LOOKUP · fetch

### g01 — Show the boundary of Hessen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hessen']", "entity_type": "state", "spatial": ["Hessen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g02 — What is the shape of Thüringen?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Thüringen']", "entity_type": "state", "spatial": ["Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g03 — Give me the geometry of Köln

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Cologne']", "entity_type": "city", "spatial": ["Cologne"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g04 — Where is Leipzig located? Give me its coordinates.

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Leipzig']", "entity_type": "city", "spatial": ["Leipzig"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g05 — WKT for Niedersachsen and Bremen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bremen', 'Niedersachsen']", "entity_type": "state", "spatial": ["Bremen", "Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g06 — Show me the outline of Mecklenburg-Vorpommern

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Mecklenburg-Vorpommern']", "entity_type": "state", "spatial": ["Mecklenburg-Vorpommern"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g07 — What are the coordinates of Dresden and Erfurt?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Dresden', 'Erfurt']", "entity_type": "city", "spatial": ["Dresden", "Erfurt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g08 — Geometry of the city of Hamburg

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Hamburg']", "entity_type": "city", "spatial": ["Hamburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g09 — Give me the polygons of Saarland and Rheinland-Pfalz

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Rheinland-Pfalz', 'Saarland']", "entity_type": "state", "spatial": ["Rheinland-Pfalz", "Saarland"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g11 — Boundaries of Brandenburg, Berlin and Sachsen-Anhalt

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Berlin', 'Brandenburg', 'Sachsen-Anhalt']", "entity_type": "state", "spatial": ["Berlin", "Brandenburg", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g12 — Show the centroid of Frankfurt

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Frankfurt']", "entity_type": "city", "spatial": ["Frankfurt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g13 — geometry of muenchen and nuernberg

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Munich', 'Nuremberg']", "entity_type": "city", "spatial": ["Munich", "Nuremberg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g14 — Give me the shapes of Hessen and Kassel

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Kassel']", "entity_type": "city", "spatial": ["Kassel"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g15 — Map the border of Schleswig-Holstein

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Schleswig-Holstein']", "entity_type": "state", "spatial": ["Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g16 — What does the boundary of Baden-Württemberg look like as WKT?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Baden-Württemberg']", "entity_type": "state", "spatial": ["Baden-Württemberg"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g17 — Coordinates of Hannover, the city of Bremen and Kiel

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bremen', 'Hannover', 'Kiel']", "entity_type": "city", "spatial": ["Bremen", "Hannover", "Kiel"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g18 — Return the geometry for Nordrhein-Westfalen, Düsseldorf and Dortmund

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Nordrhein-Westfalen']", "entity_type": "state", "spatial": ["Nordrhein-Westfalen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g18 — Return the geometry for Nordrhein-Westfalen, Düsseldorf and Dortmund

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Dortmund', 'Düsseldorf']", "entity_type": "city", "spatial": ["Dortmund", "Düsseldorf"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g19 — Show shapes of Sachsen and Thüringen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Sachsen', 'Thüringen']", "entity_type": "state", "spatial": ["Sachsen", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g22 — Shape of Rostock and Potsdam

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Potsdam', 'Rostock']", "entity_type": "city", "spatial": ["Potsdam", "Rostock"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g23 — Show the shapes of all federal states

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Baden-Württemberg', 'Bayern', 'Berlin', 'Brandenburg', 'Bremen', 'Hamburg', 'Hessen', 'Mecklenburg-Vorpommern', 'Niedersachsen', 'Nordrhein-Westfalen', 'Rheinland-Pfalz', 'Saarland', 'Sachsen', 'Sachsen-Anhalt', 'Schleswig-Holstein', 'Thüringen']", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern", "Berlin", "Brandenburg", "Bremen", "Hamburg", "Hessen", "Mecklenburg-Vorpommern", "Niedersachsen", "Nordrhein-Westfalen", "Rheinland-Pfalz", "Saarland", "Sachsen", "Sachsen-Anhalt", "Schleswig-Holstein", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g24 — Boundary of Rheinland-Pfalz

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Rheinland-Pfalz']", "entity_type": "state", "spatial": ["Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g25 — Coordinates of Bamberg and Erlangen

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bamberg', 'Erlangen']", "entity_type": "city", "spatial": ["Bamberg", "Erlangen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g26 — Give me the geometry of the city of Bremen and the state of Niedersachsen

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bremen']", "entity_type": "city", "spatial": ["Bremen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g26 — Give me the geometry of the city of Bremen and the state of Niedersachsen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Niedersachsen']", "entity_type": "state", "spatial": ["Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g27 — WKT for Sachsen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Sachsen']", "entity_type": "state", "spatial": ["Sachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g28 — Where is Wiesbaden located?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Wiesbaden']", "entity_type": "city", "spatial": ["Wiesbaden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g29 — Polygon of Baden-Württemberg and point of Karlsruhe

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Karlsruhe']", "entity_type": "city", "spatial": ["Karlsruhe"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g31 — Geometries of Brandenburg, Sachsen and Thüringen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Sachsen', 'Thüringen']", "entity_type": "state", "spatial": ["Brandenburg", "Sachsen", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g32 — coordinates of koeln and duesseldorf

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Cologne', 'Düsseldorf']", "entity_type": "city", "spatial": ["Cologne", "Düsseldorf"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g33 — Boundary polygons of Hamburg and Schleswig-Holstein

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hamburg', 'Schleswig-Holstein']", "entity_type": "state", "spatial": ["Hamburg", "Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g34 — Centroid of Stendal and Wernigerode

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Stendal', 'Wernigerode']", "entity_type": "city", "spatial": ["Stendal", "Wernigerode"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g36 — Point locations of Freiburg im Breisgau and Konstanz

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Freiburg im Breisgau', 'Konstanz']", "entity_type": "city", "spatial": ["Freiburg im Breisgau", "Konstanz"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g37 — Geometry of Cottbus and Eberswalde

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Cottbus', 'Eberswalde']", "entity_type": "city", "spatial": ["Cottbus", "Eberswalde"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g39 — Geometry of Kassel, Fulda and Marburg

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Fulda', 'Kassel', 'Marburg']", "entity_type": "city", "spatial": ["Fulda", "Kassel", "Marburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g40 · validation — WKT of Saarland and Saarlouis

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Saarlouis']", "entity_type": "city", "spatial": ["Saarlouis"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g41 — Show the boundaries of Bayern and Baden-Württemberg

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Baden-Württemberg', 'Bayern']", "entity_type": "state", "spatial": ["Baden-Württemberg", "Bayern"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g42 — Coordinates for Oldenburg

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Oldenburg']", "entity_type": "city", "spatial": ["Oldenburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g43 — Shape of the city of Hamburg and of Lübeck

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Hamburg', 'Lübeck']", "entity_type": "city", "spatial": ["Hamburg", "Lübeck"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### g45 — Geometries of Nordrhein-Westfalen, Hessen and Rheinland-Pfalz

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hessen', 'Nordrhein-Westfalen', 'Rheinland-Pfalz']", "entity_type": "state", "spatial": ["Hessen", "Nordrhein-Westfalen", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g46 — Give me the geometries of Hamburg the state and Hamburg the city

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hamburg']", "entity_type": "state", "spatial": ["Hamburg"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g48 — boundary of Berlin

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Berlin']", "entity_type": "state", "spatial": ["Berlin"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### g49 — Coordinates of Essen

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Essen']", "entity_type": "city", "spatial": ["Essen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o01 — Combine Hessen and Thüringen into one boundary

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hessen', 'Thüringen']", "entity_type": "state", "spatial": ["Hessen", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o04 — One combined area for Sachsen, Sachsen-Anhalt and Thüringen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Sachsen', 'Sachsen-Anhalt', 'Thüringen']", "entity_type": "state", "spatial": ["Sachsen", "Sachsen-Anhalt", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o05 — Join Berlin and Brandenburg into one polygon

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Berlin', 'Brandenburg']", "entity_type": "state", "spatial": ["Berlin", "Brandenburg"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o06 — What area do Hessen and Bayern have in common?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bayern', 'Hessen']", "entity_type": "state", "spatial": ["Bayern", "Hessen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o07 — Intersection of Nordrhein-Westfalen and Niedersachsen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Niedersachsen', 'Nordrhein-Westfalen']", "entity_type": "state", "spatial": ["Niedersachsen", "Nordrhein-Westfalen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o08 — Which region is shared by Brandenburg and Mecklenburg-Vorpommern?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Mecklenburg-Vorpommern']", "entity_type": "state", "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o09 — Overlap between Baden-Württemberg and Rheinland-Pfalz

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Baden-Württemberg', 'Rheinland-Pfalz']", "entity_type": "state", "spatial": ["Baden-Württemberg", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o14 — What is left of Sachsen once Sachsen-Anhalt is taken away?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Sachsen', 'Sachsen-Anhalt']", "entity_type": "state", "spatial": ["Sachsen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o15 — Areas in Hessen or Rheinland-Pfalz but not in both

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hessen', 'Rheinland-Pfalz']", "entity_type": "state", "spatial": ["Hessen", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o18 — Give me the symmetric difference between Brandenburg and Sachsen-Anhalt

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Sachsen-Anhalt']", "entity_type": "state", "spatial": ["Brandenburg", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o21 — Of Bayern and Baden-Württemberg, which are within 120 km of Stuttgart?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Stuttgart']", "entity_type": "city", "spatial": ["Stuttgart"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o22 — Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Rostock']", "entity_type": "city", "spatial": ["Rostock"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o22 — Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Mecklenburg-Vorpommern', 'Schleswig-Holstein']", "entity_type": "state", "spatial": ["Brandenburg", "Mecklenburg-Vorpommern", "Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o24 — Union of Niedersachsen, Bremen and Hamburg

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bremen', 'Hamburg', 'Niedersachsen']", "entity_type": "state", "spatial": ["Bremen", "Hamburg", "Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o25 — Combine Sachsen and Brandenburg into a single shape

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Sachsen']", "entity_type": "state", "spatial": ["Brandenburg", "Sachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o26 — One shape for Rheinland-Pfalz and Nordrhein-Westfalen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Nordrhein-Westfalen', 'Rheinland-Pfalz']", "entity_type": "state", "spatial": ["Nordrhein-Westfalen", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o27 — Join Mecklenburg-Vorpommern and Schleswig-Holstein

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Mecklenburg-Vorpommern', 'Schleswig-Holstein']", "entity_type": "state", "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o28 — What area do Sachsen and Bayern have in common?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bayern', 'Sachsen']", "entity_type": "state", "spatial": ["Bayern", "Sachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o31 — Overlap between Niedersachsen and Sachsen-Anhalt

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Niedersachsen', 'Sachsen-Anhalt']", "entity_type": "state", "spatial": ["Niedersachsen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o35 — Subtract Hamburg from Niedersachsen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hamburg', 'Niedersachsen']", "entity_type": "state", "spatial": ["Hamburg", "Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o38 — Symmetric difference between Bayern and Thüringen

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bayern', 'Thüringen']", "entity_type": "state", "spatial": ["Bayern", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o40 · validation — Which parts lie in exactly one of Hessen and Niedersachsen?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hessen', 'Niedersachsen']", "entity_type": "state", "spatial": ["Hessen", "Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o41 — Which of Niedersachsen and Sachsen-Anhalt lie within 60 km of Braunschweig?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Braunschweig']", "entity_type": "city", "spatial": ["Braunschweig"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o42 — Which of Bayern and Sachsen are within 100 km of Nürnberg?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Nuremberg']", "entity_type": "city", "spatial": ["Nuremberg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o43 — Of Hessen and Rheinland-Pfalz, which lie within 30 km of Mainz?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Mainz']", "entity_type": "city", "spatial": ["Mainz"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o44 — Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bremerhaven']", "entity_type": "city", "spatial": ["Bremerhaven"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o44 — Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Niedersachsen', 'Schleswig-Holstein']", "entity_type": "state", "spatial": ["Niedersachsen", "Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o45 — Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Erfurt']", "entity_type": "city", "spatial": ["Erfurt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o45 — Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bayern', 'Hessen', 'Thüringen']", "entity_type": "state", "spatial": ["Bayern", "Hessen", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o46 — Which of Brandenburg and Sachsen lie within 40 km of Cottbus?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Cottbus']", "entity_type": "city", "spatial": ["Cottbus"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o49 — Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Magdeburg']", "entity_type": "city", "spatial": ["Magdeburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o49 — Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Brandenburg', 'Niedersachsen', 'Sachsen-Anhalt']", "entity_type": "state", "spatial": ["Brandenburg", "Niedersachsen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o50 · validation — Which of Hessen and Nordrhein-Westfalen lie within 60 km of Siegen?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Siegen']", "entity_type": "city", "spatial": ["Siegen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o56 — List the cities inside the combined area of Schleswig-Holstein, Hamburg and Mecklenburg-Vorpommern

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hamburg', 'Mecklenburg-Vorpommern', 'Schleswig-Holstein']", "entity_type": "state", "spatial": ["Hamburg", "Mecklenburg-Vorpommern", "Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o58 — merge nordrhein westfalen and hessen, then show me the cities inside

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hessen', 'Nordrhein-Westfalen']", "entity_type": "state", "spatial": ["Hessen", "Nordrhein-Westfalen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o59 — If you combine Thüringen and Sachsen-Anhalt, which cities are in that area?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Sachsen-Anhalt', 'Thüringen']", "entity_type": "state", "spatial": ["Sachsen-Anhalt", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### o66 — Combine the cities Dresden and Leipzig into one shape

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Dresden', 'Leipzig']", "entity_type": "city", "spatial": ["Dresden", "Leipzig"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### o73 — Combine Berlin, Brandenburg and Sachsen into one region: show it and the combined population for 2016

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Berlin', 'Brandenburg', 'Sachsen']", "entity_type": "state", "spatial": ["Berlin", "Brandenburg", "Sachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r06 — Do Hamburg and Bremen touch?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bremen', 'Hamburg']", "entity_type": "state", "spatial": ["Bremen", "Hamburg"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r10 · validation — Is Hamburg north of Hessen?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hamburg', 'Hessen']", "entity_type": "state", "spatial": ["Hamburg", "Hessen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r12 — Does Saarland lie west of Bayern?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bayern', 'Saarland']", "entity_type": "state", "spatial": ["Bayern", "Saarland"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r14 — Is Sachsen east of Hessen?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Hessen', 'Sachsen']", "entity_type": "state", "spatial": ["Hessen", "Sachsen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r21 — Is Bremen within 100 km of Hannover?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bremen']", "entity_type": "state", "spatial": ["Bremen"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r21 — Is Bremen within 100 km of Hannover?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Hannover']", "entity_type": "city", "spatial": ["Hannover"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### r28 — Do Saarland and Nordrhein-Westfalen share a border?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Nordrhein-Westfalen', 'Saarland']", "entity_type": "state", "spatial": ["Nordrhein-Westfalen", "Saarland"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r43 — Is Bayern within 60 km of Erfurt?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Bayern']", "entity_type": "state", "spatial": ["Bayern"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r46 — Is Sachsen-Anhalt within 30 km of Leipzig?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Sachsen-Anhalt']", "entity_type": "state", "spatial": ["Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r48 — Is Saarland within 80 km of Karlsruhe?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Saarland']", "entity_type": "state", "spatial": ["Saarland"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### r58 — Is Saarland within 500 km of Kiel?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Kiel']", "entity_type": "city", "spatial": ["Kiel"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### r59 — Which states are at most 50 km from Fulda?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Fulda']", "entity_type": "city", "spatial": ["Fulda"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### r60 · validation — States no more than 25 km away from Ulm

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Ulm']", "entity_type": "city", "spatial": ["Ulm"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b05 — Which towns lie within 60 km of Dresden?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Dresden']", "entity_type": "city", "spatial": ["Dresden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b07 — Which cities are within 25 km of Düsseldorf?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Düsseldorf']", "entity_type": "city", "spatial": ["Düsseldorf"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b12 — Name the cities within 150 km of München

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Munich']", "entity_type": "city", "spatial": ["Munich"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b19 — Which cities lie within 110 km of Freiburg?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Freiburg']", "entity_type": "city", "spatial": ["Freiburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b20 · validation — Cities that are at most 50 km away from Bonn

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bonn']", "entity_type": "city", "spatial": ["Bonn"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b21 — Which cities surround Augsburg within 40 km?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Augsburg']", "entity_type": "city", "spatial": ["Augsburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b22 — Which cities are within 85 km of Münster?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Münster']", "entity_type": "city", "spatial": ["Münster"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b25 — What cities lie near Koblenz, within 40 km?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Koblenz']", "entity_type": "city", "spatial": ["Koblenz"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b28 — Find every city in a 60 km radius of Ingolstadt

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Ingolstadt']", "entity_type": "city", "spatial": ["Ingolstadt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b29 — Which cities are close to Bamberg?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bamberg']", "entity_type": "city", "spatial": ["Bamberg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b32 — Show the cities within 25 km of Gießen

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Gießen']", "entity_type": "city", "spatial": ["Gießen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b33 — What cities are within 30 kilometres of Darmstadt?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Darmstadt']", "entity_type": "city", "spatial": ["Darmstadt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b35 — cities within 50km of gera

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Gera']", "entity_type": "city", "spatial": ["Gera"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b36 — Which cities surround Weimar within 40 km?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Weimar']", "entity_type": "city", "spatial": ["Weimar"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b37 — Name the cities within 90 km of Wolfsburg

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Wolfsburg']", "entity_type": "city", "spatial": ["Wolfsburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b38 — Which cities lie within 65 km of Flensburg?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Flensburg']", "entity_type": "city", "spatial": ["Flensburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b39 — Cities near Stralsund

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Stralsund']", "entity_type": "city", "spatial": ["Stralsund"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b40 · validation — Which cities are within 55 km of Görlitz?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Görlitz']", "entity_type": "city", "spatial": ["Görlitz"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b41 — Which cities are within 5 km of Bochum?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bochum']", "entity_type": "city", "spatial": ["Bochum"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b46 — Which cities are within 25 km of Aschaffenburg?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Aschaffenburg']", "entity_type": "city", "spatial": ["Aschaffenburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b52 — Which cities does Brandenburg contain?

**Input**

```json
{"question": "Fetch the stored shapes of these state names: ['Brandenburg']", "entity_type": "state", "spatial": ["Brandenburg"]}
```

**Correct SQL**

```sql
SELECT s.state_name AS entity_name, ST_AsText(s.geo_shape) AS wkt, ST_SRID(s.geo_shape) AS srid FROM states s WHERE s.state_name = ANY(:names)
```

### b59 — Which cities are east of Dortmund?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Dortmund']", "entity_type": "city", "spatial": ["Dortmund"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b60 · validation — Which cities lie within 50 km north of Frankfurt am Main?

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Frankfurt am Main']", "entity_type": "city", "spatial": ["Frankfurt am Main"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```

### b63 — Cities that are at most 30 km from Bielefeld

**Input**

```json
{"question": "Fetch the stored shapes of these city names: ['Bielefeld']", "entity_type": "city", "spatial": ["Bielefeld"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE c.city_name = ANY(:names)
```


## SPATIAL_OPERATION · buffer_within

### o19 — Which of Hessen and Thüringen lie within 80 km of Frankfurt?

**Input**

```json
{"question": "Which of Hessen and Thüringen lie within 80 km of Frankfurt?", "operation": "BufferWithin", "spatial": ["Frankfurt", "Hessen", "Thüringen"], "distance_km": 80.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o20 · validation — Which of Sachsen and Brandenburg lie within 50 km of Leipzig?

**Input**

```json
{"question": "Which of Sachsen and Brandenburg lie within 50 km of Leipzig?", "operation": "BufferWithin", "spatial": ["Leipzig", "Sachsen", "Brandenburg"], "distance_km": 50.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o21 — Of Bayern and Baden-Württemberg, which are within 120 km of Stuttgart?

**Input**

```json
{"question": "Of Bayern and Baden-Württemberg, which are within 120 km of Stuttgart?", "operation": "BufferWithin", "spatial": ["Stuttgart", "Bayern", "Baden-Württemberg"], "distance_km": 120.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o22 — Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?

**Input**

```json
{"question": "Which of Mecklenburg-Vorpommern, Schleswig-Holstein and Brandenburg lie within 100 km of Rostock?", "operation": "BufferWithin", "spatial": ["Rostock", "Mecklenburg-Vorpommern", "Schleswig-Holstein", "Brandenburg"], "distance_km": 100.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o41 — Which of Niedersachsen and Sachsen-Anhalt lie within 60 km of Braunschweig?

**Input**

```json
{"question": "Which of Niedersachsen and Sachsen-Anhalt lie within 60 km of Braunschweig?", "operation": "BufferWithin", "spatial": ["Braunschweig", "Niedersachsen", "Sachsen-Anhalt"], "distance_km": 60.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o42 — Which of Bayern and Sachsen are within 100 km of Nürnberg?

**Input**

```json
{"question": "Which of Bayern and Sachsen are within 100 km of Nürnberg?", "operation": "BufferWithin", "spatial": ["Nuremberg", "Bayern", "Sachsen"], "distance_km": 100.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o43 — Of Hessen and Rheinland-Pfalz, which lie within 30 km of Mainz?

**Input**

```json
{"question": "Of Hessen and Rheinland-Pfalz, which lie within 30 km of Mainz?", "operation": "BufferWithin", "spatial": ["Mainz", "Hessen", "Rheinland-Pfalz"], "distance_km": 30.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o44 — Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?

**Input**

```json
{"question": "Which of Schleswig-Holstein and Niedersachsen lie within 50 km of Bremerhaven?", "operation": "BufferWithin", "spatial": ["Bremerhaven", "Schleswig-Holstein", "Niedersachsen"], "distance_km": 50.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o45 — Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?

**Input**

```json
{"question": "Which of Thüringen, Hessen and Bayern lie within 80 km of Erfurt?", "operation": "BufferWithin", "spatial": ["Erfurt", "Thüringen", "Hessen", "Bayern"], "distance_km": 80.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o46 — Which of Brandenburg and Sachsen lie within 40 km of Cottbus?

**Input**

```json
{"question": "Which of Brandenburg and Sachsen lie within 40 km of Cottbus?", "operation": "BufferWithin", "spatial": ["Cottbus", "Brandenburg", "Sachsen"], "distance_km": 40.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o47 — Which of Nordrhein-Westfalen and Rheinland-Pfalz are within 50 km of Köln?

**Input**

```json
{"question": "Which of Nordrhein-Westfalen and Rheinland-Pfalz are within 50 km of Köln?", "operation": "BufferWithin", "spatial": ["Cologne", "Nordrhein-Westfalen", "Rheinland-Pfalz"], "distance_km": 50.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o48 — Which of Baden-Württemberg and Rheinland-Pfalz lie within 25 km of Karlsruhe?

**Input**

```json
{"question": "Which of Baden-Württemberg and Rheinland-Pfalz lie within 25 km of Karlsruhe?", "operation": "BufferWithin", "spatial": ["Karlsruhe", "Baden-Württemberg", "Rheinland-Pfalz"], "distance_km": 25.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o49 — Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?

**Input**

```json
{"question": "Which of Sachsen-Anhalt, Niedersachsen and Brandenburg lie within 90 km of Magdeburg?", "operation": "BufferWithin", "spatial": ["Magdeburg", "Sachsen-Anhalt", "Niedersachsen", "Brandenburg"], "distance_km": 90.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```

### o50 · validation — Which of Hessen and Nordrhein-Westfalen lie within 60 km of Siegen?

**Input**

```json
{"question": "Which of Hessen and Nordrhein-Westfalen lie within 60 km of Siegen?", "operation": "BufferWithin", "spatial": ["Siegen", "Hessen", "Nordrhein-Westfalen"], "distance_km": 60.0}
```

**Correct SQL**

```sql
WITH targets(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), zone(g) AS (SELECT ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) SELECT targets.entity_name AS entity_name, CASE WHEN targets.shape IS NULL THEN -1 WHEN ST_Intersects(targets.shape, zone.g) THEN 1 ELSE 0 END AS meets_zone FROM targets, zone
```


## SPATIAL_OPERATION · compute

### o01 — Combine Hessen and Thüringen into one boundary

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Hessen", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o02 — Merge Niedersachsen and Bremen into a single shape

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Niedersachsen", "Bremen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o03 — What is the union of Rheinland-Pfalz and Saarland?

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Rheinland-Pfalz", "Saarland"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o04 — One combined area for Sachsen, Sachsen-Anhalt and Thüringen

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Sachsen", "Sachsen-Anhalt", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o05 — Join Berlin and Brandenburg into one polygon

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Berlin", "Brandenburg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o06 — What area do Hessen and Bayern have in common?

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Hessen", "Bayern"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o07 — Intersection of Nordrhein-Westfalen and Niedersachsen

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Nordrhein-Westfalen", "Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o08 — Which region is shared by Brandenburg and Mecklenburg-Vorpommern?

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o09 — Overlap between Baden-Württemberg and Rheinland-Pfalz

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Baden-Württemberg", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o11 — Remove Hamburg from Schleswig-Holstein

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Schleswig-Holstein", "Hamburg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o12 — Show Bayern minus Baden-Württemberg

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Bayern", "Baden-Württemberg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o13 — Hessen with Thüringen cut out

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Hessen", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o14 — What is left of Sachsen once Sachsen-Anhalt is taken away?

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Sachsen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o15 — Areas in Hessen or Rheinland-Pfalz but not in both

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Hessen", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o16 — Symmetric difference of Thüringen and Sachsen

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Thüringen", "Sachsen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o17 — Which parts belong to exactly one of Niedersachsen and Nordrhein-Westfalen?

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Niedersachsen", "Nordrhein-Westfalen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o18 — Give me the symmetric difference between Brandenburg and Sachsen-Anhalt

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Brandenburg", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o23 — Merge Bayern and Baden-Württemberg into one area

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Bayern", "Baden-Württemberg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o24 — Union of Niedersachsen, Bremen and Hamburg

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Niedersachsen", "Bremen", "Hamburg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o25 — Combine Sachsen and Brandenburg into a single shape

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Sachsen", "Brandenburg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o26 — One shape for Rheinland-Pfalz and Nordrhein-Westfalen

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Rheinland-Pfalz", "Nordrhein-Westfalen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o27 — Join Mecklenburg-Vorpommern and Schleswig-Holstein

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Mecklenburg-Vorpommern", "Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o28 — What area do Sachsen and Bayern have in common?

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Sachsen", "Bayern"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o29 — Intersection of Hessen and Rheinland-Pfalz

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Hessen", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o30 · validation — Shared area of Brandenburg and Berlin

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Brandenburg", "Berlin"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o31 — Overlap between Niedersachsen and Sachsen-Anhalt

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Niedersachsen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o32 — Show Nordrhein-Westfalen without Niedersachsen

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Nordrhein-Westfalen", "Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o33 — Remove Saarland from Rheinland-Pfalz

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Rheinland-Pfalz", "Saarland"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o34 — Thüringen with Sachsen cut away

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Thüringen", "Sachsen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o35 — Subtract Hamburg from Niedersachsen

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Niedersachsen", "Hamburg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o36 — What remains of Hessen after taking out Bayern?

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Hessen", "Bayern"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o37 — Take Mecklenburg-Vorpommern away from Brandenburg

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Brandenburg", "Mecklenburg-Vorpommern"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o38 — Symmetric difference between Bayern and Thüringen

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Bayern", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o39 — Areas that belong to Sachsen or Sachsen-Anhalt but not both

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Sachsen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o40 · validation — Which parts lie in exactly one of Hessen and Niedersachsen?

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Hessen", "Niedersachsen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o52 — Combine Hessen and Rheinland-Pfalz — which cities lie inside the combined area?

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Hessen", "Rheinland-Pfalz"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o53 — Which cities are inside the union of Sachsen-Anhalt and Brandenburg?

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Sachsen-Anhalt", "Brandenburg"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o55 — Merge Saxony and Thuringia. Which cities does the merged area contain?

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Sachsen", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o56 — List the cities inside the combined area of Schleswig-Holstein, Hamburg and Mecklenburg-Vorpommern

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Schleswig-Holstein", "Hamburg", "Mecklenburg-Vorpommern"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o58 — merge nordrhein westfalen and hessen, then show me the cities inside

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Nordrhein-Westfalen", "Hessen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o59 — If you combine Thüringen and Sachsen-Anhalt, which cities are in that area?

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Thüringen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o61 — Cities in the overlap of Niedersachsen and Nordrhein-Westfalen

**Input**

```json
{"question": "Intersection of these two shapes", "operation": "Intersection", "spatial": ["Niedersachsen", "Nordrhein-Westfalen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Intersection(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o62 — Which cities are in Niedersachsen once Bremen is removed?

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Niedersachsen", "Bremen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o64 — Take Sachsen-Anhalt out of Niedersachsen and tell me which cities remain inside

**Input**

```json
{"question": "Difference of these two shapes", "operation": "Difference", "spatial": ["Niedersachsen", "Sachsen-Anhalt"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Difference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o65 — Which cities lie in exactly one of Rheinland-Pfalz and Hessen?

**Input**

```json
{"question": "SymDifference of these two shapes", "operation": "SymDifference", "spatial": ["Rheinland-Pfalz", "Hessen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_SymDifference(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o66 — Combine the cities Dresden and Leipzig into one shape

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Dresden", "Leipzig"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o70 · validation — Combine Hamburg and Schleswig-Holstein into one area: show the shape and the total live births in 2019

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Hamburg", "Schleswig-Holstein"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o72 — Join Bayern and Thüringen into one area and tell me the total marriages there in 2017

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Bayern", "Thüringen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o73 — Combine Berlin, Brandenburg and Sachsen into one region: show it and the combined population for 2016

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Berlin", "Brandenburg", "Sachsen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o75 — Merge Hessen and Nordrhein-Westfalen into one shape. What was its population in 2019?

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Hessen", "Nordrhein-Westfalen"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```

### o76 — Union of Baden-Württemberg and Bayern with the total live births in 2018

**Input**

```json
{"question": "Union of these two shapes", "operation": "Union", "spatial": ["Baden-Württemberg", "Bayern"]}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Union(ST_GeomFromText(:wkt_a, :srid_a), ST_GeomFromText(:wkt_b, :srid_b))) AS wkt
```


## SPATIAL_RELATIONSHIP · compute

### r01 — Which states border Hessen?

**Input**

```json
{"question": "Which of the candidate federal states border Hessen?", "spatial_relationship": {"type": "adjacency", "refs": ["Hessen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r02 — Does Brandenburg share a border with Sachsen?

**Input**

```json
{"question": "Which of the candidate federal states border Sachsen?", "spatial_relationship": {"type": "adjacency", "refs": ["Sachsen"], "subject": "Brandenburg", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r03 — Is Saarland adjacent to Rheinland-Pfalz?

**Input**

```json
{"question": "Which of the candidate federal states border Rheinland-Pfalz?", "spatial_relationship": {"type": "adjacency", "refs": ["Rheinland-Pfalz"], "subject": "Saarland", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r04 — Name the neighbours of Niedersachsen

**Input**

```json
{"question": "Which of the candidate federal states border Niedersachsen?", "spatial_relationship": {"type": "adjacency", "refs": ["Niedersachsen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r05 — Which state touches both Bayern and Thüringen?

**Input**

```json
{"question": "Which of the candidate federal states border Bayern, Thüringen?", "spatial_relationship": {"type": "adjacency", "refs": ["Bayern", "Thüringen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r06 — Do Hamburg and Bremen touch?

**Input**

```json
{"question": "Which of the candidate federal states border Bremen?", "spatial_relationship": {"type": "adjacency", "refs": ["Bremen"], "subject": "Hamburg", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r07 — Which states share a border with Baden-Württemberg? Show their population in 2021.

**Input**

```json
{"question": "Which of the candidate federal states border Baden-Württemberg?", "spatial_relationship": {"type": "adjacency", "refs": ["Baden-Württemberg"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r08 — Neighbouring states of Mecklenburg-Vorpommern and their marriages from 2019 to 2020

**Input**

```json
{"question": "Which of the candidate federal states border Mecklenburg-Vorpommern?", "spatial_relationship": {"type": "adjacency", "refs": ["Mecklenburg-Vorpommern"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r09 — Which states lie south of Niedersachsen?

**Input**

```json
{"question": "Which of the candidate federal states lie south of Niedersachsen?", "spatial_relationship": {"type": "south_of", "refs": ["Niedersachsen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r10 · validation — Is Hamburg north of Hessen?

**Input**

```json
{"question": "Which of the candidate federal states lie north of Hessen?", "spatial_relationship": {"type": "north_of", "refs": ["Hessen"], "subject": "Hamburg", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r11 — States east of Nordrhein-Westfalen

**Input**

```json
{"question": "Which of the candidate federal states lie east of Nordrhein-Westfalen?", "spatial_relationship": {"type": "east_of", "refs": ["Nordrhein-Westfalen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r12 — Does Saarland lie west of Bayern?

**Input**

```json
{"question": "Which of the candidate federal states lie west of Bayern?", "spatial_relationship": {"type": "west_of", "refs": ["Bayern"], "subject": "Saarland", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r13 — Which federal states are located north of Thüringen?

**Input**

```json
{"question": "Which of the candidate federal states lie north of Thüringen?", "spatial_relationship": {"type": "north_of", "refs": ["Thüringen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r14 — Is Sachsen east of Hessen?

**Input**

```json
{"question": "Which of the candidate federal states lie east of Hessen?", "spatial_relationship": {"type": "east_of", "refs": ["Hessen"], "subject": "Sachsen", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r15 — States west of Sachsen-Anhalt with their live births in 2022

**Input**

```json
{"question": "Which of the candidate federal states lie west of Sachsen-Anhalt?", "spatial_relationship": {"type": "west_of", "refs": ["Sachsen-Anhalt"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r16 — Which states are south of Brandenburg?

**Input**

```json
{"question": "Which of the candidate federal states lie south of Brandenburg?", "spatial_relationship": {"type": "south_of", "refs": ["Brandenburg"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r17 — Which states are within 150 km of Frankfurt?

**Input**

```json
{"question": "Which of the candidate federal states lie within 150 km of Frankfurt?", "spatial_relationship": {"type": "distance", "refs": ["Frankfurt"], "subject": null, "distance_km": 150}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r18 — Is Thüringen within 50 km of Leipzig?

**Input**

```json
{"question": "Which of the candidate federal states lie within 50 km of Leipzig?", "spatial_relationship": {"type": "distance", "refs": ["Leipzig"], "subject": "Thüringen", "distance_km": 50}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r19 — States within 200 km of Berlin

**Input**

```json
{"question": "Which of the candidate federal states lie within 200 km of Berlin?", "spatial_relationship": {"type": "distance", "refs": ["Berlin"], "subject": null, "distance_km": 200}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r20 · validation — Which states lie within 80 km of Stuttgart?

**Input**

```json
{"question": "Which of the candidate federal states lie within 80 km of Stuttgart?", "spatial_relationship": {"type": "distance", "refs": ["Stuttgart"], "subject": null, "distance_km": 80}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r21 — Is Bremen within 100 km of Hannover?

**Input**

```json
{"question": "Which of the candidate federal states lie within 100 km of Hannover?", "spatial_relationship": {"type": "distance", "refs": ["Hannover"], "subject": "Bremen", "distance_km": 100}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r22 — States within 120 km of Köln and their population in 2020

**Input**

```json
{"question": "Which of the candidate federal states lie within 120 km of Cologne?", "spatial_relationship": {"type": "distance", "refs": ["Cologne"], "subject": null, "distance_km": 120}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r23 — Which states border Sachsen?

**Input**

```json
{"question": "Which of the candidate federal states border Sachsen?", "spatial_relationship": {"type": "adjacency", "refs": ["Sachsen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r24 — Does Thüringen share a border with Hessen?

**Input**

```json
{"question": "Which of the candidate federal states border Hessen?", "spatial_relationship": {"type": "adjacency", "refs": ["Hessen"], "subject": "Thüringen", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r25 — Is Hamburg adjacent to Niedersachsen?

**Input**

```json
{"question": "Which of the candidate federal states border Niedersachsen?", "spatial_relationship": {"type": "adjacency", "refs": ["Niedersachsen"], "subject": "Hamburg", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r26 — Neighbours of Schleswig-Holstein

**Input**

```json
{"question": "Which of the candidate federal states border Schleswig-Holstein?", "spatial_relationship": {"type": "adjacency", "refs": ["Schleswig-Holstein"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r27 — Which states touch both Hessen and Bayern?

**Input**

```json
{"question": "Which of the candidate federal states border Hessen, Bayern?", "spatial_relationship": {"type": "adjacency", "refs": ["Hessen", "Bayern"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r28 — Do Saarland and Nordrhein-Westfalen share a border?

**Input**

```json
{"question": "Which of the candidate federal states border Nordrhein-Westfalen?", "spatial_relationship": {"type": "adjacency", "refs": ["Nordrhein-Westfalen"], "subject": "Saarland", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r31 — Is Rheinland-Pfalz adjacent to Baden-Württemberg?

**Input**

```json
{"question": "Which of the candidate federal states border Baden-Württemberg?", "spatial_relationship": {"type": "adjacency", "refs": ["Baden-Württemberg"], "subject": "Rheinland-Pfalz", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r32 — Which states lie north of Sachsen?

**Input**

```json
{"question": "Which of the candidate federal states lie north of Sachsen?", "spatial_relationship": {"type": "north_of", "refs": ["Sachsen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r33 — Is Niedersachsen north of Nordrhein-Westfalen?

**Input**

```json
{"question": "Which of the candidate federal states lie north of Nordrhein-Westfalen?", "spatial_relationship": {"type": "north_of", "refs": ["Nordrhein-Westfalen"], "subject": "Niedersachsen", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r34 — States west of Thüringen

**Input**

```json
{"question": "Which of the candidate federal states lie west of Thüringen?", "spatial_relationship": {"type": "west_of", "refs": ["Thüringen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r35 — Does Bayern lie east of Baden-Württemberg?

**Input**

```json
{"question": "Which of the candidate federal states lie east of Baden-Württemberg?", "spatial_relationship": {"type": "east_of", "refs": ["Baden-Württemberg"], "subject": "Bayern", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r36 — Which states are south of Mecklenburg-Vorpommern?

**Input**

```json
{"question": "Which of the candidate federal states lie south of Mecklenburg-Vorpommern?", "spatial_relationship": {"type": "south_of", "refs": ["Mecklenburg-Vorpommern"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r37 — Is Hessen west of Thüringen?

**Input**

```json
{"question": "Which of the candidate federal states lie west of Thüringen?", "spatial_relationship": {"type": "west_of", "refs": ["Thüringen"], "subject": "Hessen", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r38 — States south of Schleswig-Holstein with their live births in 2010

**Input**

```json
{"question": "Which of the candidate federal states lie south of Schleswig-Holstein?", "spatial_relationship": {"type": "south_of", "refs": ["Schleswig-Holstein"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r39 — Which states lie east of Rheinland-Pfalz?

**Input**

```json
{"question": "Which of the candidate federal states lie east of Rheinland-Pfalz?", "spatial_relationship": {"type": "east_of", "refs": ["Rheinland-Pfalz"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r40 · validation — Is Sachsen-Anhalt north of Thüringen?

**Input**

```json
{"question": "Which of the candidate federal states lie north of Thüringen?", "spatial_relationship": {"type": "north_of", "refs": ["Thüringen"], "subject": "Sachsen-Anhalt", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r41 — Which states are west of Brandenburg, and what was their population in 2005?

**Input**

```json
{"question": "Which of the candidate federal states lie west of Brandenburg?", "spatial_relationship": {"type": "west_of", "refs": ["Brandenburg"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r42 — Which states are within 100 km of Braunschweig?

**Input**

```json
{"question": "Which of the candidate federal states lie within 100 km of Braunschweig?", "spatial_relationship": {"type": "distance", "refs": ["Braunschweig"], "subject": null, "distance_km": 100}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r43 — Is Bayern within 60 km of Erfurt?

**Input**

```json
{"question": "Which of the candidate federal states lie within 60 km of Erfurt?", "spatial_relationship": {"type": "distance", "refs": ["Erfurt"], "subject": "Bayern", "distance_km": 60}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r44 — States within 75 km of Bremen

**Input**

```json
{"question": "Which of the candidate federal states lie within 75 km of Bremen?", "spatial_relationship": {"type": "distance", "refs": ["Bremen"], "subject": null, "distance_km": 75}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r45 — Which states lie within 50 km of Mainz?

**Input**

```json
{"question": "Which of the candidate federal states lie within 50 km of Mainz?", "spatial_relationship": {"type": "distance", "refs": ["Mainz"], "subject": null, "distance_km": 50}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r46 — Is Sachsen-Anhalt within 30 km of Leipzig?

**Input**

```json
{"question": "Which of the candidate federal states lie within 30 km of Leipzig?", "spatial_relationship": {"type": "distance", "refs": ["Leipzig"], "subject": "Sachsen-Anhalt", "distance_km": 30}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r47 — Which states are within 120 km of Hannover?

**Input**

```json
{"question": "Which of the candidate federal states lie within 120 km of Hannover?", "spatial_relationship": {"type": "distance", "refs": ["Hannover"], "subject": null, "distance_km": 120}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r48 — Is Saarland within 80 km of Karlsruhe?

**Input**

```json
{"question": "Which of the candidate federal states lie within 80 km of Karlsruhe?", "spatial_relationship": {"type": "distance", "refs": ["Karlsruhe"], "subject": "Saarland", "distance_km": 80}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r49 — Which states lie within 90 km of Nürnberg, with their population in 2014?

**Input**

```json
{"question": "Which of the candidate federal states lie within 90 km of Nuremberg?", "spatial_relationship": {"type": "distance", "refs": ["Nuremberg"], "subject": null, "distance_km": 90}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r50 · validation — States within 40 km of Koblenz

**Input**

```json
{"question": "Which of the candidate federal states lie within 40 km of Koblenz?", "spatial_relationship": {"type": "distance", "refs": ["Koblenz"], "subject": null, "distance_km": 40}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r51 — Which states border Berlin?

**Input**

```json
{"question": "Which of the candidate federal states border Berlin?", "spatial_relationship": {"type": "adjacency", "refs": ["Berlin"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r52 — Does Bremen border Niedersachsen?

**Input**

```json
{"question": "Which of the candidate federal states border Niedersachsen?", "spatial_relationship": {"type": "adjacency", "refs": ["Niedersachsen"], "subject": "Bremen", "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r53 — Which states border both Berlin and Hessen?

**Input**

```json
{"question": "Which of the candidate federal states border Berlin, Hessen?", "spatial_relationship": {"type": "adjacency", "refs": ["Berlin", "Hessen"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_Intersects(cand.shape, ref.shape) AND NOT ST_Equals(cand.shape, ref.shape)
```

### r54 — Which states are south of Bayern?

**Input**

```json
{"question": "Which of the candidate federal states lie south of Bayern?", "spatial_relationship": {"type": "south_of", "refs": ["Bayern"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r55 — Which states lie north of Schleswig-Holstein?

**Input**

```json
{"question": "Which of the candidate federal states lie north of Schleswig-Holstein?", "spatial_relationship": {"type": "north_of", "refs": ["Schleswig-Holstein"], "subject": null, "distance_km": null}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearing(entity_name, az) AS (SELECT cand.entity_name, degrees(ST_Azimuth(ST_Centroid(ref.shape), ST_Centroid(cand.shape))) FROM cand, ref WHERE cand.entity_name <> :ref) SELECT bearing.entity_name AS entity_name FROM bearing WHERE bearing.az BETWEEN :az_start AND :az_end OR bearing.az + 360 BETWEEN :az_start AND :az_end ORDER BY bearing.az
```

### r56 — Which states are within 50 km of Berlin?

**Input**

```json
{"question": "Which of the candidate federal states lie within 50 km of Berlin?", "spatial_relationship": {"type": "distance", "refs": ["Berlin"], "subject": null, "distance_km": 50}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r57 — Which states lie within 10 km of Hamburg?

**Input**

```json
{"question": "Which of the candidate federal states lie within 10 km of Hamburg?", "spatial_relationship": {"type": "distance", "refs": ["Hamburg"], "subject": null, "distance_km": 10}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r58 — Is Saarland within 500 km of Kiel?

**Input**

```json
{"question": "Which of the candidate federal states lie within 500 km of Kiel?", "spatial_relationship": {"type": "distance", "refs": ["Kiel"], "subject": "Saarland", "distance_km": 500}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r59 — Which states are at most 50 km from Fulda?

**Input**

```json
{"question": "Which of the candidate federal states lie within 50 km of Fulda?", "spatial_relationship": {"type": "distance", "refs": ["Fulda"], "subject": null, "distance_km": 50}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```

### r60 · validation — States no more than 25 km away from Ulm

**Input**

```json
{"question": "Which of the candidate federal states lie within 25 km of Ulm?", "spatial_relationship": {"type": "distance", "refs": ["Ulm"], "subject": null, "distance_km": 25}}
```

**Correct SQL**

```sql
WITH cand(entity_name, shape) AS (SELECT n, ST_GeomFromText(w, :cand_srid) FROM unnest(CAST(:names AS text[]), CAST(:wkts AS text[])) AS t(n, w)), ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)) SELECT cand.entity_name AS entity_name FROM cand, ref WHERE cand.entity_name <> :ref AND ST_DWithin(cand.shape::geography, ref.shape::geography, :dist_m) ORDER BY ST_Distance(cand.shape::geography, ref.shape::geography)
```


## SPATIAL_RELATIONSHIP_BUFFER · sector

### b55 — What are the cities north of Hessen?

**Input**

```json
{"question": "What are the cities north of Hessen?", "spatial": ["Hessen"], "direction": "north_of", "radius_km": 1000.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### b56 — Which cities lie south of Thüringen?

**Input**

```json
{"question": "Which cities lie south of Thüringen?", "spatial": ["Thüringen"], "direction": "south_of", "radius_km": 1000.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### b57 — List the cities east of Niedersachsen

**Input**

```json
{"question": "List the cities east of Niedersachsen", "spatial": ["Niedersachsen"], "direction": "east_of", "radius_km": 1000.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### b58 — Which cities are west of Sachsen?

**Input**

```json
{"question": "Which cities are west of Sachsen?", "spatial": ["Sachsen"], "direction": "west_of", "radius_km": 1000.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### b59 — Which cities are east of Dortmund?

**Input**

```json
{"question": "Which cities are east of Dortmund?", "spatial": ["Dortmund"], "direction": "east_of", "radius_km": 1000.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### b60 · validation — Which cities lie within 50 km north of Frankfurt am Main?

**Input**

```json
{"question": "Which cities lie within 50 km north of Frankfurt am Main?", "spatial": ["Frankfurt am Main"], "direction": "north_of", "radius_km": 50.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### b61 — cities to the south of Hamburg within 30 km

**Input**

```json
{"question": "cities to the south of Hamburg within 30 km", "spatial": ["Hamburg"], "direction": "south_of", "radius_km": 30.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```

### b62 — Which towns lie west of Bavaria?

**Input**

```json
{"question": "Which towns lie west of Bavaria?", "spatial": ["Bayern"], "direction": "west_of", "radius_km": 1000.0}
```

**Correct SQL**

```sql
WITH ref(shape) AS (SELECT ST_GeomFromText(:ref_wkt, :ref_srid)), bearings(a) AS (SELECT generate_series(CAST(:az_start AS int), CAST(:az_end AS int), 5)), arc(a, pt) AS (SELECT bearings.a, ST_Project(ST_Centroid(ref.shape)::geography, :radius_m, radians(bearings.a))::geometry FROM ref, bearings) SELECT ST_AsText(ST_Difference(ST_MakePolygon(ST_AddPoint(ST_AddPoint(ST_MakeLine(array_agg(arc.pt ORDER BY arc.a)), ST_Centroid(ref.shape), 0), ST_Centroid(ref.shape))), ref.shape)) AS wkt, :ref_srid AS srid FROM arc, ref GROUP BY ref.shape
```


## SPATIAL_RELATIONSHIP_BUFFER · within

### o51 — Merge Bayern and Baden-Württemberg into one area and what cities are inside that area?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": []}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b01 — Which cities are within 30 km of Leipzig?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Leipzig"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b01 — Which cities are within 30 km of Leipzig?

**Input**

```json
{"question": "Agent-1 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Leipzig"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b01 — Which cities are within 30 km of Leipzig?

**Input**

```json
{"question": "Agent-2 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Leipzig"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b02 — List all cities within 100 km of Frankfurt

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Frankfurt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b03 — What cities are near Hannover, within 75 km?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Hannover"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b04 — Cities within 40 km of Köln

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Cologne"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b05 — Which towns lie within 60 km of Dresden?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Dresden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b05 — Which towns lie within 60 km of Dresden?

**Input**

```json
{"question": "Agent-1 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Dresden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b05 — Which towns lie within 60 km of Dresden?

**Input**

```json
{"question": "Agent-2 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Dresden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b07 — Which cities are within 25 km of Düsseldorf?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Düsseldorf"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b08 — Show the cities close to Stuttgart

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Stuttgart"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b10 · validation — Cities in a 90 km radius of Nürnberg

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Nuremberg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b10 · validation — Cities in a 90 km radius of Nürnberg

**Input**

```json
{"question": "Agent-1 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Nuremberg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b10 · validation — Cities in a 90 km radius of Nürnberg

**Input**

```json
{"question": "Agent-2 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Nuremberg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b11 — Which cities are less than 70 km from Kassel?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Kassel"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b12 — Name the cities within 150 km of München

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Munich"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b14 — Which cities lie within 80 km of Erfurt?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Erfurt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b15 — cities within 45km of Mainz

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Mainz"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b16 — What cities are located within 100 kilometres of Kiel?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Kiel"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b17 — Which cities are within 55 km of Magdeburg?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Magdeburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b18 — Give me all cities within 65 km of Rostock

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Rostock"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b19 — Which cities lie within 110 km of Freiburg?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Freiburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b20 · validation — Cities that are at most 50 km away from Bonn

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Bonn"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b21 — Which cities surround Augsburg within 40 km?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Augsburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b22 — Which cities are within 85 km of Münster?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Münster"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b23 — Which cities are within 30 km of Wiesbaden?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Wiesbaden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b23 — Which cities are within 30 km of Wiesbaden?

**Input**

```json
{"question": "Agent-1 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Wiesbaden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b23 — Which cities are within 30 km of Wiesbaden?

**Input**

```json
{"question": "Agent-2 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Wiesbaden"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b24 — List all cities within 50 km of Karlsruhe

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Karlsruhe"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b25 — What cities lie near Koblenz, within 40 km?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Koblenz"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b26 — Cities within 70 km of Braunschweig

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Braunschweig"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b27 — Which towns are within 35 km of Oldenburg?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Oldenburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b28 — Find every city in a 60 km radius of Ingolstadt

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Ingolstadt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b29 — Which cities are close to Bamberg?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Bamberg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b30 · validation — Cities that are at most 45 km from Siegen

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Siegen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b30 · validation — Cities that are at most 45 km from Siegen

**Input**

```json
{"question": "Agent-1 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Siegen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b30 · validation — Cities that are at most 45 km from Siegen

**Input**

```json
{"question": "Agent-2 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": ["Siegen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b31 — Which cities lie within 20 km of Fulda?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Fulda"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b32 — Show the cities within 25 km of Gießen

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Gießen"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b33 — What cities are within 30 kilometres of Darmstadt?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Darmstadt"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b34 — Which cities are less than 80 km from Cottbus?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Cottbus"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b35 — cities within 50km of gera

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Gera"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b36 — Which cities surround Weimar within 40 km?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Weimar"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b37 — Name the cities within 90 km of Wolfsburg

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Wolfsburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b38 — Which cities lie within 65 km of Flensburg?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Flensburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b39 — Cities near Stralsund

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Stralsund"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b40 · validation — Which cities are within 55 km of Görlitz?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Görlitz"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b41 — Which cities are within 5 km of Bochum?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Bochum"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b46 — Which cities are within 25 km of Aschaffenburg?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Aschaffenburg"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b47 — Give me the cities within Hessen

**Input**

```json
{"question": "Agent-1 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": []}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b47 — Give me the cities within Hessen

**Input**

```json
{"question": "Agent-2 asks which of our cities lie inside this zone", "target_entity": "city", "exclude": []}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b59 — Which cities are east of Dortmund?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Dortmund"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b60 · validation — Which cities lie within 50 km north of Frankfurt am Main?

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Frankfurt am Main"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```

### b63 — Cities that are at most 30 km from Bielefeld

**Input**

```json
{"question": "Which of our cities lie inside this zone?", "target_entity": "city", "exclude": ["Bielefeld"]}
```

**Correct SQL**

```sql
SELECT c.city_name AS entity_name, ST_AsText(c.centroid) AS wkt, ST_SRID(c.centroid) AS srid FROM cities c WHERE ST_Within(c.centroid, ST_GeomFromText(:zone_wkt, :zone_srid)) AND NOT (c.city_name = ANY(:exclude))
```


## SPATIAL_RELATIONSHIP_BUFFER · zone

### b01 — Which cities are within 30 km of Leipzig?

**Input**

```json
{"question": "Which cities are within 30 km of Leipzig?", "spatial": ["Leipzig"], "distance_km": 30.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b02 — List all cities within 100 km of Frankfurt

**Input**

```json
{"question": "List all cities within 100 km of Frankfurt", "spatial": ["Frankfurt"], "distance_km": 100.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b03 — What cities are near Hannover, within 75 km?

**Input**

```json
{"question": "What cities are near Hannover, within 75 km?", "spatial": ["Hannover"], "distance_km": 75.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b04 — Cities within 40 km of Köln

**Input**

```json
{"question": "Cities within 40 km of Köln", "spatial": ["Cologne"], "distance_km": 40.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b05 — Which towns lie within 60 km of Dresden?

**Input**

```json
{"question": "Which towns lie within 60 km of Dresden?", "spatial": ["Dresden"], "distance_km": 60.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b06 — Find every city in a 120 km radius around Berlin

**Input**

```json
{"question": "Find every city in a 120 km radius around Berlin", "spatial": ["Berlin"], "distance_km": 120.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b07 — Which cities are within 25 km of Düsseldorf?

**Input**

```json
{"question": "Which cities are within 25 km of Düsseldorf?", "spatial": ["Düsseldorf"], "distance_km": 25.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b08 — Show the cities close to Stuttgart

**Input**

```json
{"question": "Show the cities close to Stuttgart", "spatial": ["Stuttgart"], "distance_km": 100.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b09 — Which cities can be found within 200 km of Hamburg?

**Input**

```json
{"question": "Which cities can be found within 200 km of Hamburg?", "spatial": ["Hamburg"], "distance_km": 200.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b10 · validation — Cities in a 90 km radius of Nürnberg

**Input**

```json
{"question": "Cities in a 90 km radius of Nürnberg", "spatial": ["Nuremberg"], "distance_km": 90.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b11 — Which cities are less than 70 km from Kassel?

**Input**

```json
{"question": "Which cities are less than 70 km from Kassel?", "spatial": ["Kassel"], "distance_km": 70.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b12 — Name the cities within 150 km of München

**Input**

```json
{"question": "Name the cities within 150 km of München", "spatial": ["Munich"], "distance_km": 150.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b13 — Are there any cities within 35 km of Bremen?

**Input**

```json
{"question": "Are there any cities within 35 km of Bremen?", "spatial": ["Bremen"], "distance_km": 35.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b14 — Which cities lie within 80 km of Erfurt?

**Input**

```json
{"question": "Which cities lie within 80 km of Erfurt?", "spatial": ["Erfurt"], "distance_km": 80.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b15 — cities within 45km of Mainz

**Input**

```json
{"question": "cities within 45km of Mainz", "spatial": ["Mainz"], "distance_km": 45.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b16 — What cities are located within 100 kilometres of Kiel?

**Input**

```json
{"question": "What cities are located within 100 kilometres of Kiel?", "spatial": ["Kiel"], "distance_km": 100.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b17 — Which cities are within 55 km of Magdeburg?

**Input**

```json
{"question": "Which cities are within 55 km of Magdeburg?", "spatial": ["Magdeburg"], "distance_km": 55.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b18 — Give me all cities within 65 km of Rostock

**Input**

```json
{"question": "Give me all cities within 65 km of Rostock", "spatial": ["Rostock"], "distance_km": 65.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b19 — Which cities lie within 110 km of Freiburg?

**Input**

```json
{"question": "Which cities lie within 110 km of Freiburg?", "spatial": ["Freiburg"], "distance_km": 110.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b20 · validation — Cities that are at most 50 km away from Bonn

**Input**

```json
{"question": "Cities that are at most 50 km away from Bonn", "spatial": ["Bonn"], "distance_km": 50.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b21 — Which cities surround Augsburg within 40 km?

**Input**

```json
{"question": "Which cities surround Augsburg within 40 km?", "spatial": ["Augsburg"], "distance_km": 40.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b22 — Which cities are within 85 km of Münster?

**Input**

```json
{"question": "Which cities are within 85 km of Münster?", "spatial": ["Münster"], "distance_km": 85.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b23 — Which cities are within 30 km of Wiesbaden?

**Input**

```json
{"question": "Which cities are within 30 km of Wiesbaden?", "spatial": ["Wiesbaden"], "distance_km": 30.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b24 — List all cities within 50 km of Karlsruhe

**Input**

```json
{"question": "List all cities within 50 km of Karlsruhe", "spatial": ["Karlsruhe"], "distance_km": 50.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b25 — What cities lie near Koblenz, within 40 km?

**Input**

```json
{"question": "What cities lie near Koblenz, within 40 km?", "spatial": ["Koblenz"], "distance_km": 40.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b26 — Cities within 70 km of Braunschweig

**Input**

```json
{"question": "Cities within 70 km of Braunschweig", "spatial": ["Braunschweig"], "distance_km": 70.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b27 — Which towns are within 35 km of Oldenburg?

**Input**

```json
{"question": "Which towns are within 35 km of Oldenburg?", "spatial": ["Oldenburg"], "distance_km": 35.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b28 — Find every city in a 60 km radius of Ingolstadt

**Input**

```json
{"question": "Find every city in a 60 km radius of Ingolstadt", "spatial": ["Ingolstadt"], "distance_km": 60.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b29 — Which cities are close to Bamberg?

**Input**

```json
{"question": "Which cities are close to Bamberg?", "spatial": ["Bamberg"], "distance_km": 100.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b30 · validation — Cities that are at most 45 km from Siegen

**Input**

```json
{"question": "Cities that are at most 45 km from Siegen", "spatial": ["Siegen"], "distance_km": 45.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b31 — Which cities lie within 20 km of Fulda?

**Input**

```json
{"question": "Which cities lie within 20 km of Fulda?", "spatial": ["Fulda"], "distance_km": 20.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b32 — Show the cities within 25 km of Gießen

**Input**

```json
{"question": "Show the cities within 25 km of Gießen", "spatial": ["Gießen"], "distance_km": 25.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b33 — What cities are within 30 kilometres of Darmstadt?

**Input**

```json
{"question": "What cities are within 30 kilometres of Darmstadt?", "spatial": ["Darmstadt"], "distance_km": 30.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b34 — Which cities are less than 80 km from Cottbus?

**Input**

```json
{"question": "Which cities are less than 80 km from Cottbus?", "spatial": ["Cottbus"], "distance_km": 80.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b35 — cities within 50km of gera

**Input**

```json
{"question": "cities within 50km of gera", "spatial": ["Gera"], "distance_km": 50.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b36 — Which cities surround Weimar within 40 km?

**Input**

```json
{"question": "Which cities surround Weimar within 40 km?", "spatial": ["Weimar"], "distance_km": 40.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b37 — Name the cities within 90 km of Wolfsburg

**Input**

```json
{"question": "Name the cities within 90 km of Wolfsburg", "spatial": ["Wolfsburg"], "distance_km": 90.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b38 — Which cities lie within 65 km of Flensburg?

**Input**

```json
{"question": "Which cities lie within 65 km of Flensburg?", "spatial": ["Flensburg"], "distance_km": 65.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b39 — Cities near Stralsund

**Input**

```json
{"question": "Cities near Stralsund", "spatial": ["Stralsund"], "distance_km": 100.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b40 · validation — Which cities are within 55 km of Görlitz?

**Input**

```json
{"question": "Which cities are within 55 km of Görlitz?", "spatial": ["Görlitz"], "distance_km": 55.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b41 — Which cities are within 5 km of Bochum?

**Input**

```json
{"question": "Which cities are within 5 km of Bochum?", "spatial": ["Bochum"], "distance_km": 5.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b42 — Which cities lie within 300 km of Kassel?

**Input**

```json
{"question": "Which cities lie within 300 km of Kassel?", "spatial": ["Kassel"], "distance_km": 300.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b43 — Which cities are within 20 km of München?

**Input**

```json
{"question": "Which cities are within 20 km of München?", "spatial": ["Munich"], "distance_km": 20.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b44 — Which cities are within 40 km of the city of Hamburg?

**Input**

```json
{"question": "Which cities are within 40 km of the city of Hamburg?", "spatial": ["Hamburg"], "distance_km": 40.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b45 — cities within 12.5 km of Mainz

**Input**

```json
{"question": "cities within 12.5 km of Mainz", "spatial": ["Mainz"], "distance_km": 12.5}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b46 — Which cities are within 25 km of Aschaffenburg?

**Input**

```json
{"question": "Which cities are within 25 km of Aschaffenburg?", "spatial": ["Aschaffenburg"], "distance_km": 25.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b54 — Which cities lie within 25 km of Schleswig-Holstein?

**Input**

```json
{"question": "Which cities lie within 25 km of Schleswig-Holstein?", "spatial": ["Schleswig-Holstein"], "distance_km": 25.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b63 — Cities that are at most 30 km from Bielefeld

**Input**

```json
{"question": "Cities that are at most 30 km from Bielefeld", "spatial": ["Bielefeld"], "distance_km": 30.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b64 — Which cities are no more than 20 km away from Kiel?

**Input**

```json
{"question": "Which cities are no more than 20 km away from Kiel?", "spatial": ["Kiel"], "distance_km": 20.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b65 — cities at most 60 km from Augsburg

**Input**

```json
{"question": "cities at most 60 km from Augsburg", "spatial": ["Augsburg"], "distance_km": 60.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b66 — Show the cities at most 15 km away from Mainz

**Input**

```json
{"question": "Show the cities at most 15 km away from Mainz", "spatial": ["Mainz"], "distance_km": 15.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```

### b67 — Name every city no further than 40 km from Magdeburg

**Input**

```json
{"question": "Name every city no further than 40 km from Magdeburg", "spatial": ["Magdeburg"], "distance_km": 40.0}
```

**Correct SQL**

```sql
SELECT ST_AsText(ST_Buffer(ST_GeomFromText(:ref_wkt, :ref_srid)::geography, :dist_m)::geometry) AS wkt, :ref_srid AS srid
```
