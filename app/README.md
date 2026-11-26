# Handwritten Digit Recognizer

This directory contains a Streamlit application that recognizes handwritten digits from a drawing canvas. The app resizes the drawing to `28 x 28` pixels, applies the project's custom preprocessing, and predicts a digit from `0` to `9` using a trained Histogram Gradient Boosting classifier.

## Run the application on Windows

The project already includes a virtual environment at the repository root. From PowerShell, run:

```powershell
cd "C:\Users\anmol\Downloads\Digit classification"
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py
```

Open the URL printed by Streamlit, normally:

```text
http://localhost:8501
```

Stop the server with `Ctrl+C`.

Always launch Streamlit through `.venv\Scripts\python.exe`. Running `streamlit run` directly can use a different global Python installation that does not contain the project dependencies.

## Fresh environment setup

The versions in `requirements.txt` target the older scikit-learn model and are best installed with Python 3.12 or an earlier supported Python version:

```powershell
cd "C:\Users\anmol\Downloads\Digit classification"
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r .\app\requirements.txt
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py
```

If the existing project `.venv` is already working, do not recreate it; use the run command above.

## Project files

| File or directory | Purpose |
| --- | --- |
| `app.py` | Streamlit user interface, preprocessing, prediction, and probability chart. |
| `gbc_custom.pkl` | Serialized Histogram Gradient Boosting classifier trained on the custom-transformed dataset. |
| `requirements.txt` | Python dependency list for the application. |
| `Makefile` | Defines the `run` command for environments that provide `make`. |
| `../Images/` | Evaluation plots, confusion matrices, transformed examples, and sample images. |
| `../*.ipynb` | Training, augmentation, evaluation, and prediction notebooks. |

## Using the app

1. Draw a digit on the canvas.
2. Review the displayed `Model Input` image.
3. Select **Predict**.
4. Read the predicted digit and probability chart.

The canvas is converted to grayscale, resized to `28 x 28`, and transformed so the classifier receives the same feature shape used during training: `1 x 784`.

## Compatibility notes

- The model was serialized with scikit-learn 1.2.x. `app.py` initializes the missing `_preprocessor` attribute when the model is loaded by a newer scikit-learn version.
- The model path is resolved relative to `app.py`, so the app can be launched from the repository root without a `gbc_custom.pkl` file-not-found error.
- Altair is pinned to `5.3.0` because newer Altair releases use Python typing features that fail in the project's Python 3.14 environment.

## Troubleshooting

### `No module named cv2`

The app was started with global Python. Use:

```powershell
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py
```

### `No such file or directory: 'gbc_custom.pkl'`

Use the command above from the repository root. The current app resolves the model path automatically relative to `app.py`.

### Port 8501 is already in use

Start the app on another port:

```powershell
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py --server.port 8502
```
