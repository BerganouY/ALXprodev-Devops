# Pokémon API Automation

A shell script that automates fetching Pokémon data from the [PokéAPI](https://pokeapi.co/) and saves the response to a JSON file.

## Description

This project contains a Bash script that:
1. Makes an API request to fetch data for Pikachu
2. Saves the successful response to `data.json`
3. Logs any errors to `errors.txt`

## Prerequisites

- `curl` (usually pre-installed on Linux/macOS)
- `jq` (lightweight command-line JSON processor)

To install `jq` on:
- **Ubuntu/Debian**: `sudo apt-get install jq`
- **macOS**: `brew install jq`

## Usage

1. Clone the repository or download the script:
   ```bash
   git clone https://github.com/your-username/ALXprodev-Devops.git
   cd ALXprodev-Devops/Advanced_shell/apiAutomation-0x00