Below is a sample **README** file for your **IPL Win Predictor** project. Feel free to modify any sections (like installation commands, project structure, or model details) to match your exact setup and preferences.

---

# IPL Win Predictor

This project is a **Streamlit** web application that predicts the winning probability of an IPL (Indian Premier League) cricket match based on live match situations. A machine learning model (Logistic Regression, optionally combined with other ensemble methods) is trained on historical IPL data to provide near real-time predictions.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Data Preparation & Modeling](#data-preparation--modeling)
- [Installation & Usage](#installation--usage)
- [How It Works](#how-it-works)
- [Model Performance](#model-performance)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Overview

The **IPL Win Predictor** allows users to select:
- The batting and bowling teams,
- The city where the match is being played,
- The current score, number of overs bowled, and wickets lost,
- The target score,

After entering these details, the app uses a pre-trained machine learning model to calculate and display the **winning probabilities** for both the batting team and the bowling team. Below is the screenshot of the app running on localhost:8501.
<img width="1728" alt="image" src="https://github.com/user-attachments/assets/b3fda20e-b336-439d-bfcd-e87c73abcdd6" />


## Features

1. **Easy-to-Use Interface**: Built using Streamlit, so you can simply run the app in a browser.
2. **Real-Time Predictions**: Get an immediate probability of winning based on the current match situation.
3. **Flexible Input**: Supports multiple IPL teams and various host cities.
4. **Reusable Pipeline**: The training pipeline is built in Jupyter Notebook (preprocessing, one-hot encoding, model training) and serialized (using Pickle) for quick inference.


## Data Preparation & Modeling

1. **Data Source**  
   - IPL match data (ball-by-ball or summarized) was collected from Kaggle or other cricket databases.

2. **Data Cleaning & Feature Engineering**  
   - Address missing values, handle categorical features (e.g., teams, cities), engineer new features like current run rate (CRR), required run rate (RRR), etc.

3. **Model Training**  
   - A `LogisticRegression` model (or `RandomForestClassifier` in some versions) is used to predict the probability that the **batting team** will win.
   - Key libraries:
     - `scikit-learn` for modeling and pipelines
     - `pandas` and `numpy` for data manipulation
     - `pickle` for model serialization

4. **Pipeline**  
   - **ColumnTransformer** + **OneHotEncoder** handles categorical features (`batting_team`, `bowling_team`, `city`).
   - The pipeline ensures that all transformations and modeling steps are chained together and can be reused for inference.

5. **Serialization**  
   - The trained model pipeline is saved to `pipe.pkl` using `pickle.dump` for easy loading in the Streamlit app.

## Installation & Usage

### Prerequisites
- **Python 3.7+** (Check with `python --version`)
- **pip** or **conda** for package management

### 1. Clone or Download this Repository

```bash
git clone https://github.com/your-username/ipl-win-predictor.git
cd ipl-win-predictor
```

### 2. Install Required Libraries

If you have a `requirements.txt`, install using:
```bash
pip install -r requirements.txt
```

Otherwise, you can manually install key packages:
```bash
pip install streamlit scikit-learn pandas numpy
```

### 3. Run the Streamlit App

```bash
streamlit run app.py
```

The terminal will display a URL (like `http://localhost:8501`). Open it in your web browser to view and interact with the app.

## How It Works

1. **User Inputs**:  
   The user selects or inputs:
   - Batting team & Bowling team (dropdown)
   - City/venue (dropdown)
   - Current score, overs completed, wickets fallen
   - Target score

2. **Feature Engineering on the Fly**:  
   - **Runs Left** = Target − Current Score  
   - **Balls Left** = 120 − (Overs × 6) (assuming a 20-over innings)  
   - **Wickets in Hand** = 10 − Wickets Fallen  
   - **Current Run Rate (CRR)** = Current Score / Overs  
   - **Required Run Rate (RRR)** = (Runs Left × 6) / Balls Left

3. **Model Prediction**:  
   - The input data is passed through the loaded `pipe.pkl` pipeline.
   - The model calculates **winning probability** for the batting team (and by extension, for the bowling side).

4. **Output**:  
   - Probability that the batting team will win.
   - Probability that the bowling team will win (1 − batting win probability).

## Model Performance

- Training Data Accuracy: `~79.66%` (as indicated by `accuracy_score(y_test, y_pred)`).
- Additional metrics like F1-score, confusion matrix, or cross-validation scores can be found in the accompanying Jupyter Notebook (`data_preprocessing.ipynb`).

## Contributing

1. Fork the repo.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes and commit (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Submit a Pull Request detailing your changes.

Feel free to open an issue if you discover a bug or have a feature request.

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## Contact

For questions, suggestions, or feedback, please reach out via:
- **Email**: your_email@example.com  
- **GitHub**: [YourGitHubProfile](https://github.com/your-username)

---

**Thank you for using the IPL Win Predictor!**  
If you find this project useful, consider giving a ⭐ on GitHub. Enjoy predicting match outcomes!
