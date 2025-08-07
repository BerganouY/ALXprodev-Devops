# Pokémon API Automation Suite

## Table of Contents
- [Task 1: Basic API Request](#task-1-basic-api-request-apiautomation-0x00)
- [Task 2: Data Extraction](#task-2-data-extraction-data_extraction_automation-0x01)
- [Task 3: Batch Processing](#task-3-batch-processing-batchprocessing-0x02)
- [Task 4: Data Summary](#task-4-data-summary-summarydata-0x03)
- [Task 5: Parallel Fetching](#task-5-parallel-fetching-batchprocessing-0x04)
- [Requirements](#requirements)
- [Directory Structure](#directory-structure)
- [Error Handling](#error-handling)
- [License](#license)

---

## Task 1: Basic API Request (`apiAutomation-0x00`)

### Objective
Fetch Pikachu data from the Pokémon API and save to a JSON file.

### Features
- Makes a `GET` request to the PokéAPI
- Saves response to `data.json`
- Logs errors to `errors.txt`
- Handles HTTP failures gracefully

### Usage
```bash
./apiAutomation-0x00
```

**Sample Output**
```
Successfully retrieved Pikachu data and saved to data.json
```

---

## Task 2: Data Extraction (`data_extraction_automation-0x01`)

### Objective
Parse the JSON and extract key Pokémon stats.

### Features
- Extracts `name`, `height`, `weight`, and `type`
- Formats output string precisely
- Uses `jq`, `awk`, and `sed`
- Converts units (decimeters → meters, hectograms → kilograms)

### Usage
```bash
./data_extraction_automation-0x01
```

**Sample Output**
```
Pikachu is of type Electric, weighs 6kg, and is 0.4m tall.
```

---

## Task 3: Batch Processing (`batchProcessing-0x02`)

### Objective
Fetch data for multiple Pokémon.

### Features
- Processes: `Bulbasaur`, `Ivysaur`, `Venusaur`, `Charmander`, `Charmeleon`
- Saves each to separate JSON files
- Includes rate limiting (2 seconds between requests)
- Basic HTTP error handling

### Usage
```bash
./batchProcessing-0x02
```

**Sample Output**
```
Fetching data for bulbasaur...
Saved data to pokemon_data/bulbasaur.json ✅
Fetching data for ivysaur...
Saved data to pokemon_data/ivysaur.json ✅
```

---

## Task 4: Data Summary (`summaryData-0x03`)

### Objective
Generate a CSV report with average values.

### Features
- Processes all JSON files from the batch
- Creates a CSV report with headers
- Calculates average height and weight using `awk`
- Proper decimal formatting with `sed`

### Usage
```bash
./summaryData-0x03
```

**Sample Output**
```
Name,Height (m),Weight (kg)
Bulbasaur,0.7,6.9
Ivysaur,1.0,13.0
...

Average Height: 1.08 m
Average Weight: 29.48 kg
```

---

## Task 5: Parallel Fetching (`batchProcessing-0x04`)

### Objective
Optimized batch processing with parallelism.

### Features
- 3 concurrent requests
- PID-based background job tracking
- 3 retry attempts per Pokémon on failure
- Comprehensive error logging
- Handles rate limits and job cleanup

### Usage
```bash
./batchProcessing-0x04
```

**Sample Output**
```
Starting parallel fetch for 5 Pokémon...
[PID 1234] ✅ Success: bulbasaur
[PID 1235] 🔄 Retrying ivysaur (attempt 2/3)
[PID 1236] ✅ Success: venusaur
Parallel fetch complete. 4 succeeded, 1 failed.
```

---

## Requirements

```bash
# Ubuntu/Debian
sudo apt-get install curl jq awk sed

# macOS
brew install curl jq
```

---

## Directory Structure

```
Advanced_shell/
├── apiAutomation-0x00
├── data_extraction_automation-0x01
├── batchProcessing-0x02
├── summaryData-0x03
├── batchProcessing-0x04
└── pokemon_data/
    ├── *.json
    └── *.log
```

---

## Error Handling

- All scripts validate JSON responses
- The parallel fetch version includes exponential backoff
- Failed requests are clearly logged
- No partial or corrupted files are left on failure