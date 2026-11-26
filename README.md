# Handwritten Digit Recognizer

This project is a Streamlit application for recognizing handwritten digits. Draw a digit on the canvas and the app will resize it to `28 x 28` pixels, apply the project preprocessing, and predict a digit from `0` to `9` using the trained Histogram Gradient Boosting model.

## Clone the project from GitHub

Install Git and Python 3.11 on the new computer, then run:

```bash
git clone https://github.com/<YOUR-USERNAME>/<YOUR-REPOSITORY>.git
cd <YOUR-REPOSITORY>
```

Replace `<YOUR-USERNAME>/<YOUR-REPOSITORY>` with the actual GitHub repository path. The cloned project must contain these files:

```text
app/
  app.py
  gbc_custom.pkl
  requirements.txt
```

Do not copy the `.venv` folder from another computer. Create a new environment on each system.

## Setup on Windows

Open PowerShell in the cloned repository and run:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r .\app\requirements.txt
```

## Setup on macOS or Linux

Open a terminal in the cloned repository and run:

```bash
python3.11 -m venv .venv
./.venv/bin/python -m pip install --upgrade pip
./.venv/bin/python -m pip install -r ./app/requirements.txt
```

Python 3.11 is recommended because the serialized model and the pinned dependencies were created for the older scikit-learn stack. Python 3.13 or 3.14 can require different package versions.

## Run the application

From the repository root, use the virtual-environment interpreter directly.

Windows PowerShell:

```powershell
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py
```

macOS or Linux:

```bash
./.venv/bin/python -m streamlit run ./app/app.py
```

Streamlit will print a local URL. Open:

```text
http://localhost:8501
```

Stop the server with `Ctrl+C`.

Always run Streamlit through `.venv`. Running `streamlit run` by itself may use a global Python installation that does not have `cv2`, Streamlit, or the other project dependencies installed.

## Alternative: use the Makefile

If `make` is installed:

```bash
cd app
make run
```

The direct virtual-environment commands above are recommended on Windows because `make` is not installed by default.

## How to use the app

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
| `app/requirements.txt` | Dependencies required by the app. |
| `app/Makefile` | Optional `make run` command. |
| `Images/` | Evaluation plots, confusion matrices, transformed examples, and sample images. |
| `*.ipynb` | Training, augmentation, evaluation, and prediction notebooks. |

## Compatibility notes

- The model was serialized with scikit-learn 1.2.x. `app.py` initializes the missing `_preprocessor` attribute when the model is loaded by a newer scikit-learn version.
- The model path is resolved relative to `app.py`, so the app can be launched from the repository root.
- Altair is pinned to `5.3.0` for compatibility with the current application environment.

## Troubleshooting

### `No module named cv2`

The app was started with the wrong Python interpreter. Reinstall dependencies and run through `.venv`:

```powershell
.\.venv\Scripts\python.exe -m pip install -r .\app\requirements.txt
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py
```

### `No such file or directory: 'gbc_custom.pkl'`

Run the application from the repository root using the command above. Confirm that `app/gbc_custom.pkl` exists in the cloned project.

### Port 8501 is already in use

Run on another port:

```powershell
.\.venv\Scripts\python.exe -m streamlit run .\app\app.py --server.port 8502
```

Then open `http://localhost:8502`.
