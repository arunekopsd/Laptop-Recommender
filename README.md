# Laptop Recommender

A Flask web app that recommends laptops based on what you'll use them for: gaming, business, creative work, studying and more. Pick a use case and it suggests similar laptops from a dataset of about 800 models, with images and prices. You can also look up a specific laptop by name.

Built as a 6th-semester mini-project (Team 10).

## How it works

1. **Data.** `Dataset/laptops.csv` has ~800 laptops with name, price, processor, RAM, OS, storage, rating, brand and an assigned use case.
2. **Feature tags.** For each laptop, the processor, RAM, OS and use case are combined into one text "tag", lowercased and stemmed with NLTK's Porter stemmer.
3. **Vectorizing.** The tags are turned into word-count vectors with scikit-learn's `CountVectorizer`.
4. **Similarity.** Cosine similarity is computed between every pair of laptops. The resulting matrix and the cleaned dataset are saved to `model/` as pickle files.
5. **Recommending.** The Flask app loads those files. When you pick a use case, it finds a laptop in that category and returns the most similar ones, skipping duplicates.

The full pipeline is in `Laptop Recommender.ipynb`.

### Use cases in the dataset

Gaming · Business/Professional · Home/Everyday use · Budget Friendly · Creative/Design · Student/Education · Multimedia/Entertainment · Ultra-portable

## Pages

| Route | What it does |
|---|---|
| `/` | Home page with a random selection of laptops |
| `/recommend` | Choose a use case, get recommendations |
| `/product` | Search for a laptop by name and see its details |
| `/about`, `/contact` | Info pages |

## Getting started

The saved model files were created with pandas 1.3.5, which needs **Python 3.9**. Newer pandas versions can't load them (see the note below).

```bash
git clone https://github.com/arunekopsd/Laptop-Recommender.git
cd Laptop-Recommender
python3.9 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

Then open http://127.0.0.1:5000.

**Using a newer Python?** Install `nltk` along with current pandas and scikit-learn, run the notebook top to bottom to regenerate `model/similarity.pkl` and `model/usecases_list.pkl`, then start the app.

## Project structure

```
app.py                      Flask app and recommendation function
Laptop Recommender.ipynb    data cleaning, feature tags, similarity model
Dataset/laptops.csv         laptop dataset
model/                      saved similarity matrix and dataset (pickle)
templates/                  HTML pages (Jinja2 + Bootstrap 5)
static/                     images and favicon
amazon.py                   Selenium scraper used to collect Amazon listings
scapdata/laptops.xlsx       output from the scraper
```

`amazon.py` was a data-collection experiment and isn't needed to run the app. It expects Chrome with ChromeDriver and has Windows paths hard-coded, so edit those before running it.

## Built with

Python · Flask · pandas · scikit-learn · NLTK · Bootstrap 5 · Selenium

## Team

1. [Ashwin Sivasankaran](https://github.com/ashwinsk24)
2. [Bimal Dev](https://github.com/Bimal41)
3. [Catherine Jose](https://github.com/cath0806)
4. [Farhan Naeem](https://github.com/arunekopsd)

Forked from [ashwinsk24/Laptop-Recommender](https://github.com/ashwinsk24/Laptop-Recommender).
