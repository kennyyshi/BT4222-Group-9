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
2. Open the notebook in Colab and run all cells. The first cells mount Drive and read the data from `/content/drive/MyDrive/bt4222/JDsearch/`. `step1a_history` and `step1b_query_item` read from `/content/drive/MyDrive/JDsearch/` instead: set `BASE` (step 1a) or `DATA_DIR` (step 1b) in their first code cells to your folder.

## Data sample

Every notebook starts from `user_subset.parquet` in the [`JDsearch`](https://drive.google.com/drive/folders/1BBowElqdtOscFCv-exMlE1IAEHMUxnmi) Drive folder: the sample built for the interim report and used unchanged since. It drops the 2,103 searches with no click, cart or purchase, keeps a random 50% of users stratified on whether they purchased (85,864 users, one final search each, every candidate kept), and splits users 70 / 15 / 15 into train, validation and test (60,104 / 12,880 / 12,880), also stratified on purchase. No user appears in two splits. Histories in this file are cut to the latest 200 actions; `step1a_history` restores the full histories from the raw data.

## Pipeline

Each step is one notebook in this folder, run in Colab with its outputs kept. Large data stays on Google Drive.

| Notebook | Step | Owner | Data on Drive |
|---|---|---|---|
| `step0_feature_dictionary.ipynb` | Interim feature dictionary | Kexun, Bing Yang | None |
| `step1a_history.ipynb` | History features | Caleb | [`step1a_history`](https://drive.google.com/drive/folders/1OK7Grk-kP4aB19SVr-DmW7lHcDNEA2vb) |
| `step1b_query_item.ipynb` | Query and item features | Gareth | [`step1b_query_item`](https://drive.google.com/drive/folders/146-fzpjCRpXjL-ZEmJ-AgBl1OMF8fIVf) |
| `step2a_metadata_preparation.ipynb` | Candidate metadata for the baselines | Bing Yang | [`step2_baselines`](https://drive.google.com/drive/folders/1Zza4LWA7XFlSmH1XbD1NEExwqIqE6Lgj) |
| `step2b_baseline_ncf_lstm_optimized.ipynb` | Baselines (popularity, BM25, LSTM-NCF) and their gaps | Bing Yang | [`step2_baselines`](https://drive.google.com/drive/folders/1Zza4LWA7XFlSmH1XbD1NEExwqIqE6Lgj) |
| `step3a_lambdarank.ipynb` | Learning-to-rank | Ning | [`step3a_lambdarank`](https://drive.google.com/drive/folders/1CRvRH_hctK9C6pgDFUfPrxxeZ_QsDpuM) |
| `step3a_lambdarank_seeds.ipynb` | LambdaRank refit with seeds 43 and 44 (the reported 0.406 ± 0.001) | Ning | [`step3a_lambdarank`](https://drive.google.com/drive/folders/1CRvRH_hctK9C6pgDFUfPrxxeZ_QsDpuM) |
| `step3b_attention.ipynb` | Attention model | Kexun | [`step3b_attention`](https://drive.google.com/drive/folders/1UBAXYCw2ZWm2lpeUl8DNwJGPgqO1aJPa) |
| `step4_diagnostics.ipynb` | Diagnostics | Bryan | [`step4_diagnostics`](https://drive.google.com/drive/folders/1VBLkzDiBVOQJ_gExfZUq_3XgB3jZmWz2) |

**Run order:** `step1a_history` and `step1b_query_item`, then `step2a_metadata_preparation`, `step2b_baseline_ncf_lstm_optimized` and `step3b_attention`, then `step3a_lambdarank` (it reads the popularity features exported by `step3b_attention`) and `step3a_lambdarank_seeds`, then `step4_diagnostics`. `step0_feature_dictionary` is interim analysis and nothing depends on it.
