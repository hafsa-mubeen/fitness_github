# Fitness Instructor Generator

A Streamlit-based fitness assistant that creates personalized workout plans from a selected goal or a short natural-language prompt. The app predicts the user's fitness goal, recommends relevant exercises, shows exercise videos, runs live timers, and can optionally speak workout instructions using text-to-speech.

## Features

- Personalized workout generation for:
  - Weight loss
  - Muscle gain
  - Flexibility
  - Endurance
  - Core strength
  - Balance
- Natural-language goal prediction using a TF-IDF + LinearSVC machine learning model
- Exercise ranking with cosine similarity based on the user's preference text
- Built-in exercise metadata with sets, reps, duration, rest time, and descriptions
- Exercise videos for supported movements
- Live workout timers and progress bars
- Optional text-to-speech workout instructions
- Simple Streamlit interface
## Live Demo 


https://github.com/user-attachments/assets/6a577356-c82f-4124-a5bf-a84207c9efe7






## Demo Workflow

1. Choose a fitness goal from the radio buttons.
2. Optionally enter a workout preference, such as:

```text
20 minute home workout
stretching routine for flexibility
dumbbell workout for muscle gain
cardio session to burn fat
```

3. Click **Generate Workout**.
4. The app predicts or uses your goal, selects the best exercises, plays available videos, and runs timers for each set.

## Tech Stack

- Python
- Streamlit
- scikit-learn
- NLTK
- pyttsx3

## Project Structure

```text
fitness_github/
├── app.py                       # Streamlit app entry point
├── requirements.txt             # Python dependencies
├── assets/                      # Exercise video files
├── audio/
│   └── tts.py                   # Text-to-speech helper
├── data/
│   └── training_data.csv        # Labeled training examples for goal prediction
├── docs/
│   └── pipeline.md              # Detailed NLP/ML pipeline notes
├── nlp/
│   ├── entity_extractor.py      # Rule-based entity extraction
│   ├── exercise_metadata.py     # Exercise catalog
│   ├── intent_classifier.py     # Rule-based intent classifier
│   ├── ml_helper.py             # ML prediction wrapper with fallback
│   ├── ml_intent_model.py       # Model training and prediction
│   └── preprocess.py            # Text preprocessing helpers
└── workout_engine/
    └── generator.py             # Workout filtering and ranking logic
```

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/fitness_github.git
cd fitness_github
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the App

```bash
streamlit run app.py
```

Then open the local Streamlit URL shown in your terminal.

## Machine Learning Model

The app uses labeled examples from `data/training_data.csv` to train a fitness-goal classifier.

Supported labels:

- `weight_loss`
- `muscle_gain`
- `flexibility`
- `endurance`
- `core_strength`
- `balance`

The model is trained automatically the first time prediction is needed. If `data/training_data.csv` is updated, the app retrains the model so the latest examples are used.

You can also evaluate the model candidates manually:

```bash
python -m nlp.ml_intent_model --evaluate
```

## How Workout Generation Works

1. The Streamlit UI collects a selected goal and optional preference text.
2. If preference text is provided, the ML model predicts the most likely fitness goal.
3. The workout generator filters exercises from `nlp/exercise_metadata.py` by goal.
4. If preference text exists, matching exercises are ranked using TF-IDF and cosine similarity.
5. The top exercises are displayed with videos, timers, rest periods, and optional voice prompts.

## Exercise Videos

The app includes videos for exercises such as:

- Jumping Jacks
- Squats
- Lunges
- Push-ups
- Dumbbell Curls
- Plank
- Hamstring Stretch
- Neck Stretch
- Child Pose

If an exercise does not have a matching video file in `assets/`, the app still shows the exercise and timer.

## Notes

- Text-to-speech uses `pyttsx3`, which depends on local system voice support.
- Some NLP helper functions use NLTK resources such as stopwords and WordNet. If you use those helpers directly and resources are missing, install them with:

```python
import nltk
nltk.download("stopwords")
nltk.download("wordnet")
```

## License

This project is licensed under the MIT License.
