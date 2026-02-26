# GeminiCLI Sentiment Analysis (Shadow Bridge)

**GeminiCLI Sentiment Analysis** (codenamed *Shadow Bridge*) is a high-performance integration layer designed to bridge the gap between real-time global financial intelligence and algorithmic trading platforms like MetaTrader 5 (MT5). By leveraging the **Gemini 2.0 Flash** model via the Gemini CLI, this script transforms raw, unstructured news data into actionable numerical sentiment vectors for automated decision-making.

## Key Features

- **Real-Time Sentinel**: Monitors curated RSS feeds (Yahoo Finance, MarketWatch, Investing.com, etc.) to ingest headlines as they break.
- **Intelligent Targeting**: Merges dynamic signals from HFT scanners with strategic focus lists, reducing noise by processing only relevant news.
- **AI-Driven Quantitative Analysis**: Uses Gemini 2.0 Flash to convert headlines into a sentiment score between -1.0 (Extreme Bearish) and 1.0 (Extreme Bullish).
- **Smoothed Data Vectors**: Employs Exponential Moving Average (EMA) smoothing to prevent "whipsaw" reactions in trading logic.
- **IPC Architecture**: Communicates with MT5 through file-based Inter-Process Communication, ensuring low-latency data availability for Expert Advisors (EAs).
- **Autonomous Maintenance**: Includes a "Hygiene Engine" that automatically archives historical data to keep the live feed lightweight.

## Technical Implementation: Data Isolation

A critical architectural feature of this implementation is the use of **isolated user data environments**. To ensure that concurrent runs of the script or different instances of the Gemini CLI do not collide, the script dynamically assigns and manages specific `user_data` folders (configured via the `GEMINI_CLI_HOME` environment variable). 

This approach allows for:
- **State Persistence**: Each script run maintains its own session history and configuration state independently.
- **Parallel Processing**: Multiple instances of the bridge can monitor different asset classes or strategies without cross-contamination.
- **Security & Integrity**: Prevents accidental leakage of context or state between different automated trading modules.

## Installation & Setup

1. Ensure the Gemini CLI is installed and authenticated.
2. Configure the `MT5_FILES_PATH` in `shadow_bridge.py` to point to your MetaTrader 5 Files directory.
3. Run the script:
   ```bash
   python shadow_bridge.py
   ```

## License
MIT License
