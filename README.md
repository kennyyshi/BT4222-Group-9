# BT4222-Group-9

## Dataset: JDsearch

This project uses the [JDsearch](https://github.com/rucliujn/JDsearch) dataset (~170K users, ~12.9M products, ~26.7M interactions). Paper: https://arxiv.org/pdf/2305.14810

The raw data (`user_behavior_data.txt`, `product_meta_data.txt`) is **not** included in this repo — it's too large for git (~5.7GB uncompressed). To run the notebooks yourself, get the data one of two ways:

### Option A: Run locally (e.g. VS Code)

1. Download `JDsearch.tar` from the JD Cloud Disk link in the [JDsearch README](https://github.com/rucliujn/JDsearch#obtain-the-data) (password: `zz4qza`; requires the JD mobile app to scan the QR code on the landing page).
2. Extract it into this same project folder:
   ```
   tar -xvf JDsearch.tar
   ```
   This creates a `JDsearch/` folder containing `user_behavior_data.txt` and `product_meta_data.txt` alongside the notebooks.
3. Open and run the notebook in VS Code (or Jupyter) — the data-loading cells expect the data at `./JDsearch/`.

### Option B: Run on Google Colab

1. Upload `JDsearch.tar` (or its extracted contents) to your Google Drive, e.g. `MyDrive/bt4222/JDsearch/`.
2. Open the notebook in Colab.
3. Uncomment the Colab data-loading cell (mounts Drive and points at `/content/drive/MyDrive/bt4222/JDsearch/`) and comment out/remove the local-path version before running.

## Notebooks

- `Feature_Dictionary.ipynb` — feature engineering and descriptive statistics over the JDsearch user behavior and product metadata logs.
