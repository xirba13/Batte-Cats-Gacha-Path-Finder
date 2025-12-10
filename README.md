# Battle-Cats-Gacha-Path-Finder

A Python tool, made with Gemini's help, that calculates the optimal rolling path to obtain specific target units in The Battle Cats using seed tracking data. It uses multiprocessing to efficiently explore possibilities across multiple banners, handling track switching and guaranteed draws.


## 🚀 Features

* **Multi-Banner Support:** Analyzes multiple banners simultaneously to find the best route.
* **Track Switching Logic:** Accounts for track switches caused by guaranteed 11-draws or duplicate rares.
* **Resource Optimization:** Prioritizes paths that use fewer resources (Rare Tickets and Cat Food).
* **Configurable Limits:** Allows you to limit the number of rolls on specific banners (e.g., limiting a Legend Ticket banner to 1 action).
* **Multiprocessing:** Utilizes CPU cores to search for solutions faster.


## 📋 Prerequisites

* Python 3.x
* No external libraries required.


## ⚙️ Setup & Usage

### 1. Get Your Data
1. Go to [bc.godfat.org](https://bc.godfat.org) and load your seed.
2. Select the banners you want to analyze.
3. Inspect the page source or the table elements. Copy the raw `<table>...</table>` HTML content for the banners you want to track.
4. Delete the example data and paste your copied HTML into the file named **`data.txt`** in the same directory as the script.

### 2. Configure the Script
Open the Python script (`tracker_no_threads.py` or `tracker_threads_optimized.py`) and modify the **Configuration** section at the top:

* **Target Units:** Update the `TARGET_UBERS` set.
    * *Note:* You must use the **EXACT** names as they appear on the godfat website.
    ```python
    TARGET_UBERS = {
        "EVA Unit-01",
        "Kasli the Scourge",
        "Phonoa",
        # ... add your targets here
    }
    ```

* **Banner Limits (Optional):** If you want to restrict how many times the script can pull from a specific banner (useful for Platinum/Legend tickets), edit `BANNER_LIMITS`. The index is 0-based (0 is the first table in `data.txt`).
    ```python
    BANNER_LIMITS = {
        3: 1  # Limits the 4th banner in data.txt to exactly 1 action
    }
    ```

* **Performance Tuning:**
    * **Low-End PCs:** If your computer has limited resources or the script freezes, **lower** the values of `MAX_SEARCH_STEPS` (e.g., to 5000) and `MAX_SOLUTIONS_PER_WORKER` or use `tracker_no_threads.py`.
    * **High-End PCs:** If you have a powerful CPU, you can **increase** these values to calculate deeper paths and find more complex solutions.

### 3. Run the Script
Execute the script via terminal:

```bash
python tracker_no_threads.py
```

or if you used the multithreaded option:

```bash
python tracker_threads_optimized.py
```


## ⚠️ Disclaimer & Warning

**This tool is experimental and NOT fully tested.** While the logic simulates the tracking mechanics, edge cases (especially involving complex track switches with duplicate rares) might differ slightly from the game.

**🔴 CRITICAL:**
Always **manually cross-reference** the path calculated by this tool with the [Godfat Seed Tracker](https://bc.godfat.org) website before spending any in-game resources (Cat Food or Tickets). 

* **Do not follow the instructions blindly.**
* The author is not responsible for any wasted resources due to calculation errors.
