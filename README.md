# Handwritten Digit Recognizer

This Streamlit application recognizes handwritten digits from a drawing canvas. It resizes the drawing to `28 x 28` pixels, applies the project preprocessing, and predicts a digit from `0` to `9` using the trained Histogram Gradient Boosting model.

## Clone the project

Install Git and Python 3.14, then replace the placeholder with the actual GitHub repository URL:

```bash
git clone https://github.com/<YOUR-USERNAME>/<YOUR-REPOSITORY>.git
cd <YOUR-REPOSITORY>
```

The cloned repository must contain `app/app.py`, `app/gbc_custom.pkl`, and `app/requirements.txt`. Do not copy the `.venv` folder from another computer; create a new environment locally.

## Setup on Windows

From PowerShell in the cloned repository:

```powershell
py -3.14 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r .\app\requirements.txt
```

## Setup on macOS or Linux

From a terminal in the cloned repository:

```bash
python3.14 -m venv .venv
./.venv/bin/python -m pip install --upgrade pip
./.venv/bin/python -m pip install -r ./app/requirements.txt
```

The dependency pins include Python 3.14-compatible wheels. The serialized model was created with scikit-learn 1.2.x, while the app uses scikit-learn 1.9.1 with a compatibility shim during model loading.

## Run the application

Windows PowerShell:

```powershell
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py
```

macOS or Linux:

```bash
./.venv/bin/python -m streamlit run ./app/app.py
```

Open the URL printed by Streamlit, normally `http://localhost:8501`. Stop the server with `Ctrl+C`.

Always launch Streamlit through `.venv`. Running `streamlit run` directly may use a global Python installation without the project dependencies.

## Alternative: Makefile

If `make` is installed:

```bash
cd app
make run
```

The direct virtual-environment commands are recommended on Windows because `make` is not installed by default.

## Using the app

1. Draw a digit on the canvas.
2. Review the displayed **Model Input** image.
3. Select **Predict**.
4. Read the predicted digit and probability chart.

The input is converted to grayscale and passed to the classifier as a `1 x 784` feature array.

## Project structure

| File or directory | Purpose |
| --- | --- |
| `app/app.py` | Streamlit interface, preprocessing, prediction, and probability chart. |
| `app/gbc_custom.pkl` | Trained Histogram Gradient Boosting classifier. |
| `app/requirements.txt` | Python dependencies for the app. |
| `app/Makefile` | Optional `make run` command. |
| `Images/` | Evaluation plots, confusion matrices, transformed examples, and sample images. |
| `*.ipynb` | Training, augmentation, evaluation, and prediction notebooks. |

## Troubleshooting

### `No module named cv2`

Install dependencies and run with the project interpreter:

```powershell
.\.venv\Scripts\python.exe -m pip install -r .\app\requirements.txt
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py
```

### `No such file or directory: 'gbc_custom.pkl'`

Run from the repository root using the command above and confirm that `app/gbc_custom.pkl` exists. The app resolves the model path relative to `app.py`.

### Port 8501 is already in use

```powershell
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py --server.port 8501
```

Then open `http://localhost:8501`.
