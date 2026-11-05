# LLM Analysis of SEC 8-K Filings (CAP5619 Assignment 2)

Extracts newly announced products from S&P 500 8-K filings using a local LLM (Ollama) and writes a structured CSV.

## Run
1. Install [Ollama](https://ollama.com) and run `ollama pull llama3.1`
2. `pip install -r requirements.txt`
3. Open `8k_product_extraction.ipynb`, set `USER_AGENT` (your name + email, required by SEC), run all cells.

## Output
- `new_products_8k.csv` - company_name, stock_name, filing_time, new_product, product_description
- `new_products_8k.txt` - same data, pipe-separated
- `llm_raw_responses.jsonl` - raw LLM answers (audit trail)

## Method
Ticker -> CIK (SEC `company_tickers.json`) -> 8-K Atom feed -> 8-K body + EX-99 press release -> keyword-window passage filter -> Ollama NER-style JSON prompt (temperature 0) -> validation (180-char cap, empty/"None" rows dropped, de-duplication) -> CSV.
