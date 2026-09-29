# BT4222-Group-9

## Dataset: JDsearch

This project uses the [JDsearch](https://github.com/rucliujn/JDsearch) dataset (~170K users, ~12.9M products, ~26.7M interactions). Paper: https://arxiv.org/pdf/2305.14810

The raw data (`user_behavior_data.txt`, `product_meta_data.txt`) is **not** included in this repo — it's too large for git (~5.7GB uncompressed). To run the notebooks yourself, get the data one of two ways:

### Option A: Run locally (e.g. VS Code)

1. Download `JDsearch.tar` from gdrive folder https://drive.google.com/file/d/1ppTZXnXsjkuxOEKcE3fwQbWA2MPcDKDL/view
2. Extract it into this same project folder:
   ```
   tar -xvf JDsearch.tar
   ```
   This creates a `JDsearch/` folder containing `user_behavior_data.txt` and `product_meta_data.txt` alongside the notebooks.
3. In the first two cells, comment out the `google.colab` import and the two Colab lines, and uncomment `BASE = Path("JDsearch")`.
4. Open and run the notebook in VS Code (or Jupyter).

### Option B: Run on Google Colab (default)

1. Put the extracted `user_behavior_data.txt` and `product_meta_data.txt` in `MyDrive/bt4222/JDsearch/` on your Google Drive. If you upload `JDsearch.tar` instead, extract it from a Colab cell first:
   ```
   !tar -xf /content/drive/MyDrive/bt4222/JDsearch.tar -C /content/drive/MyDrive/bt4222/
   ```
2. Open the notebook in Colab and run all cells. The first cells mount Drive and read the data from `/content/drive/MyDrive/bt4222/JDsearch/`.

## Notebooks

- `Feature_Dictionary.ipynb` — feature engineering and descriptive statistics over the JDsearch user behavior and product metadata logs.
