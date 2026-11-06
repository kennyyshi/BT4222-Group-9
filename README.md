# BT4222-Group-9

Personalised reranking of JD.com search results: for each search, we reorder JD's candidate list so that the products users click, cart and buy rise to the top.
We compare LambdaRank on engineered features (test NDCG@10 0.406) with an attention model over users' past actions (0.399), against 0.328 for popularity alone.

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

## Pipeline

Each step is one notebook in this folder, run in Colab with its outputs kept. Large data stays on Google Drive.

| Notebook | Step | Owner | Data on Drive |
|---|---|---|---|
| `step0_sampling.ipynb` | Sampling and train / validation / test split | Ning | [`JDsearch`](https://drive.google.com/drive/folders/1BBowElqdtOscFCv-exMlE1IAEHMUxnmi) (`user_subset.parquet`) |
| `step0_feature_dictionary.ipynb` | Interim feature dictionary | Kexun, Bing Yang | None |
| `step1a_history.ipynb` | History features | Caleb | [`step1a_history`](https://drive.google.com/drive/folders/1OK7Grk-kP4aB19SVr-DmW7lHcDNEA2vb) |
| `step1b_query_item.ipynb` | Query and item features | Gareth | [`step1b_query_item`](https://drive.google.com/drive/folders/146-fzpjCRpXjL-ZEmJ-AgBl1OMF8fIVf) |
| `step2_baselines.ipynb` | Baselines and gaps | Bing Yang | [`step3_baselines`](https://drive.google.com/drive/folders/1VcEMbTilI6iVz22T9kcAhMT9M3BFMWKx) |
| `step3a_lambdarank.ipynb` | Learning-to-rank | Ning | [`step3a_lambdarank`](https://drive.google.com/drive/folders/1CRvRH_hctK9C6pgDFUfPrxxeZ_QsDpuM) |
| `step3b_attention.ipynb` | Attention model | Kexun | [`step3b_attention`](https://drive.google.com/drive/folders/1UBAXYCw2ZWm2lpeUl8DNwJGPgqO1aJPa) |
| `step4_diagnostics.ipynb` | Diagnostics | Bryan | To be added |

**Run order:** `step0_sampling`, then `step1a_history` and `step1b_query_item`, then `step2_baselines` and `step3b_attention`, then `step3a_lambdarank` (it reads the popularity features exported by `step3b_attention`), then `step4_diagnostics`. `step0_feature_dictionary` is interim analysis and nothing depends on it.
