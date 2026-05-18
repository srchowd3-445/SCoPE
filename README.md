# `methodv2` Standalone Bundle

This folder is a self-contained copy of the `FD-NL2SQL/methodv2` pipeline with
the code and local data dependencies needed to run it outside the parent
`FD-NL2SQL` repository.

## Included

- `methodv2/`
  The runnable pipeline scripts and prompt templates.
- `data/`
  The copied SQLite database, annotated CSVs, and exported
  `table_question_ground_truths_full` question set.
- `utils.py`
- `question_table_exports.py`
- `eval_run_baselines_v2.py`
- `eval_run_baselines_v3.py`
- `eval_run_baselines_derived.py`

## Notes

- The main runners now resolve dataset and run paths relative to this folder.
- The copied manifest was rewritten to use local question paths under
  `data/table_question_ground_truths_full/questions/`.
- Some model defaults still point to shared local snapshots under `/mnt/shared`.
  If those are unavailable on another machine, pass the relevant
  `--model_path` / `--*_model_path` arguments explicitly.
- Optional Python extras for embedding, richer evaluation, and local vLLM
  generation are listed in `requirements-optional.txt`.

## Example

```bash
python3 methodv2/run_question_table_copy_llm_naive.py \
  --manifest_csv data/table_question_ground_truths_full/manifest.csv \
  --annotated_csv 'data/cat3_query_sql_llm(2)_with_key_matches.csv' \
  --db_path data/database.db \
  --api_base http://127.0.0.1:8000/v1 \
  --api_key EMPTY \
  --model_name Qwen3-30B-A3B-Instruct-2507 \
  --run_name question_table_copy_llm_naive_local \
  --limit 10
```

## GitHub Pages

A project page is scaffolded in `docs/`:

- `docs/index.html`
- `docs/styles.css`

Deployment is automated with `.github/workflows/pages.yml`.

After pushing to GitHub:

1. Open repository `Settings` -> `Pages`
2. Under `Build and deployment`, set `Source` to `GitHub Actions`
3. Push to `main` (or `master`) to trigger deployment

The site will publish at:

`https://<your-username>.github.io/<repo-name>/`
