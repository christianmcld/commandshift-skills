# Inventory Agent

Voice-to-spreadsheet inventory management for retail and restaurant operations. Paste a voice note transcript describing stock counts, and this skill converts it into clean, structured CSV data with categorization, confidence scoring, and low-stock alerts.

## What It Does

- Parses natural, messy voice transcripts ("uh we got like 24 cases of Coke, maybe 30 Diet Coke")
- Extracts item-quantity pairs with unit detection
- Standardizes item names for consistency across counts
- Auto-categorizes items (Beverages, Produce, Dairy, Protein, Dry Goods, etc.)
- Compares against previous inventory to flag stock changes
- Generates CSV files, Google Sheets updates, or terminal summaries
- Produces alert reports for out-of-stock and low-stock items

## Install

```bash
cp -r ~/content-engine/skills/inventory-agent ~/.claude/skills/inventory-agent
```

## Usage

### Basic Count

```
/skill inventory-agent

Here's my walk-in cooler count from this morning:
"24 cases Coke, about 30 Diet Coke, Sprite is low maybe 8 cases,
we're completely out of Sprite Zero, got 15 cases of water,
uh Dr Pepper maybe 12 no wait 14 cases"
```

### With Previous Inventory Comparison

```
/skill inventory-agent

Previous inventory: ~/inventory/inventory_2026-03-18.csv

New count for the bar:
"Bud Light 6 cases, Miller Lite 4, we're out of PBR,
IPA has about 10 cases, house red wine 8 bottles,
house white 12 bottles, prosecco 3 bottles"
```

### Google Sheets Output

```
/skill inventory-agent — output to Google Sheets

Dry storage count: "flour 3 bags, sugar 5 bags, rice 2 bags
the pasta we got maybe 40 boxes, canned tomatoes about 24 cans,
olive oil is low like 4 bottles"
```

## Example Output

CSV file (`~/inventory/inventory_2026-03-25.csv`):

```csv
Item,Quantity,Unit,Category,Location,Confidence,Delta,Notes,Timestamp
Coca-Cola,24,cases,Beverages,Walk-in Cooler,exact,,,2026-03-25T14:30:00
Diet Coke,30,cases,Beverages,Walk-in Cooler,estimated,,said 'about',2026-03-25T14:30:00
Sprite,8,cases,Beverages,Walk-in Cooler,estimated,,said 'maybe',2026-03-25T14:30:00
Sprite Zero,0,cases,Beverages,Walk-in Cooler,exact,,OUT OF STOCK,2026-03-25T14:30:00
```

Plus a terminal summary with stock alerts.

## Requirements

- Claude Code CLI
- For CSV output: write access to `~/inventory/` (or user-specified path)
- For Google Sheets: Google Sheets MCP server configured
- Voice transcription must be done externally (Apple Voice Memos, Otter.ai, Whisper, etc.) — this skill processes the transcript text, not raw audio
