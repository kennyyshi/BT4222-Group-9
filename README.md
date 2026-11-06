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

## Repository structure

Each step has its own folder, with its notebook, small outputs, links to its large data and its key findings.

| Folder | Step | Owner | Notebook |
|---|---|---|---|
| [`step1a_history/`](step1a_history/) | History features | Caleb | `step1a_history.ipynb` |
| [`step1b_query_item/`](step1b_query_item/) | Query and item features | Gareth | `step1b_query_item.ipynb` |
| [`step2_baselines/`](step2_baselines/) | Baselines and gaps | Bing Yang | `step2_baselines.ipynb` |
| [`step3a_lambdarank/`](step3a_lambdarank/) | Learning-to-rank | Ning | `step3a_lambdarank.ipynb` |
| [`step3b_attention/`](step3b_attention/) | Attention model | Kexun | `step3b_attention.ipynb` |
| [`step4_diagnostics/`](step4_diagnostics/) | Diagnostics | Bryan | `step4_diagnostics.ipynb` |

**Run order:** `step1a_history` and `step1b_query_item`, then `step2_baselines` and `step3b_attention`, then `step3a_lambdarank` (it reads the popularity features exported by `step3b_attention`), then `step4_diagnostics`.

### Uploading your work

1. Open your step's folder on GitHub, then choose **Add file > Upload files**.
2. Upload your notebook with its outputs, plus any small `.csv` and `.png` files.
3. Commit directly to `main`. Only change your own folder, so uploads don't clash.

**File sizes:** GitHub's web upload takes files up to 25 MB, and GitHub rejects anything over 100 MB. Keep larger files, including `.parquet` files, on Google Drive, and add a link to the table in your folder's `README.md`. Check that the link opens for anyone with it, because the course requires the data to be reachable from this repository.

## Notebooks

- `Feature_Dictionary.ipynb` — feature engineering and descriptive statistics over the JDsearch user behavior and product metadata logs.
