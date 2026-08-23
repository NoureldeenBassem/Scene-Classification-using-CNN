# Scene Classification with a CNN

Six class image classifier for natural scenes (**buildings, forest, glacier, mountain, sea, street**),
trained on the [Intel Image Classification](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)
dataset and deployed as a Streamlit app.

**93.0% accuracy** and **0.932 macro F1** on 3000 held out test photos.

**▶️ Try it live:** https://scene-classification-using-cnn-2f5pzdhy2it8yqsbfdwchl.streamlit.app/

**Author:** Eng. Noureldin Bassem Mohamed

## The problem

A stock photography platform tags every uploaded photo by hand and the backlog keeps growing.
The model tags the photo automatically so only the ones it is unsure about reach a human reviewer.

## What is in here

| file | what it is |
| --- | --- |
| `scene-classification.ipynb` | the full notebook: EDA, preprocessing, training, evaluation, write up |
| `app.py` | the Streamlit app, loads the trained model and predicts on an uploaded photo |
| `scene_model.keras` | the trained model saved from the notebook |
| `class_names.json` | class order and input size, so the app matches the training setup |
| `requirements.txt` | what the app needs to run |

## Approach

Transfer learning on **MobileNetV2** in TensorFlow / Keras, trained in two stages:

1. **Model A** - backbone frozen, only the classifier head trained (`lr=1e-3`).
2. **Model B** - the last block of the backbone unfrozen and fine-tuned (`lr=1e-5`), BatchNorm kept frozen.

20% of the training folder is held out for validation, and the `seg_test` folder is only touched at
the very end, so the reported test numbers are clean.

| model | accuracy | balanced accuracy | macro F1 |
| --- | --- | --- | --- |
| A (frozen) | 0.913 | 0.915 | 0.915 |
| **B (fine-tuned)** | **0.930** | **0.933** | **0.932** |

## The interesting result

The errors are not spread evenly. **114 of the 210 mistakes are glacier vs mountain**, in both
directions, more than half of everything the model gets wrong. Glacier has the lowest recall (0.834)
and mountain the lowest precision (0.851), which is the same problem seen from two sides. Buildings vs
street is a distant second. Forest is nearly perfect at 0.993 F1.

Because of that, the app reports a confidence with every prediction. At a 0.70 confidence threshold the
model tags 92% of photos by itself at 96% accuracy, so the review team only opens the hard ones.

## Running the app locally

```bash
pip install -r requirements.txt
streamlit run app.py
```

## Reproducing the notebook

The notebook was run on Kaggle (TensorFlow 2.20, Keras 3.13) with the Intel Image Classification
dataset attached and a GPU. Point `data_dir` at wherever the dataset lives, then Restart & Run All.
Both training stages together take under 10 minutes.
