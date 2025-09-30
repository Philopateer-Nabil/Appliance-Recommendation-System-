# Appliance Recommendation System  Appliance Recommendation System

## 📝 Overview

This project implements a collaborative filtering recommendation system to suggest home appliances to users. Using a dataset of user interactions and appliance metadata, it leverages the **Singular Value Decomposition (SVD)** algorithm to predict user ratings for items they have not yet interacted with. The model's performance is optimized through hyperparameter tuning using `GridSearchCV`.

The final output is a function that generates personalized, top-N recommendations for any given user in the dataset.

---

## ✨ Features

-   **Exploratory Data Analysis (EDA):** In-depth analysis of user interaction patterns, rating distributions, and appliance popularity.
-   **Collaborative Filtering Model:** Built using the `surprise` library, a popular Python scikit for recommendation systems.
-   **SVD Algorithm:** Employs Singular Value Decomposition, a powerful matrix factorization technique for uncovering latent factors in user-item interactions.
-   **Hyperparameter Tuning:** Uses `GridSearchCV` to systematically find the optimal parameters for the SVD model, improving its predictive accuracy.
-   **Model Evaluation:** Assesses the model's performance using standard metrics like Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE).
-   **Personalized Recommendations:** A function to generate a ranked list of appliance recommendations for a specific user, excluding items they have already seen.

---

## 📊 Datasets

The system is trained on two datasets:

1.  `appliances.csv`: Contains metadata about the appliances.
    * `appliance_id`: Unique identifier for each appliance.
    * `name`: The name and model of the appliance.
    * `category`, `brand`, `price_range`, `features`: Descriptive attributes.
    * `base_avg_rating`: A pre-existing average rating.

2.  `interactions.csv`: Contains user interaction data.
    * `user_id`: Unique identifier for each user.
    * `appliance_id`: The identifier of the appliance the user interacted with.
    * `interaction_type`: The type of interaction (e.g., `view`, `rating`, `purchase`).
    * `rating`: The rating given by the user (scale 1-5).
    * `timestamp`: The time of the interaction.

---

## 🛠️ Methodology

The project follows these key steps:

1.  **Data Loading & Exploration:** The datasets are loaded, and a thorough EDA is conducted to understand data sparsity, distributions, and user behavior.
2.  **Data Preparation:** The interaction data is loaded into a `surprise` Dataset format, which is optimized for training recommendation models.
3.  **Model Training & Tuning:**
    * The data is split into an 80% training set and a 20% test set.
    * `GridSearchCV` is used on the SVD algorithm to find the best hyperparameters (`n_factors`, `n_epochs`, `lr_all`, `reg_all`) through 3-fold cross-validation.
4.  **Evaluation:**
    * The best SVD model from the grid search is trained on the designated training set.
    * The model's accuracy is evaluated on the test set, achieving a final **RMSE of 1.2118** and **MAE of 0.9934**.
5.  **Recommendation Generation:** A prediction function uses the trained model to estimate ratings for all appliances a user hasn't interacted with and returns the top-rated items as recommendations.

---

## 🚀 Technologies Used

-   Python
-   Pandas
-   NumPy
-   Matplotlib & Seaborn (for data visualization)
-   **Surprise** (for building and analyzing recommender systems)
-   Jupyter Notebook

---

## ⚙️ How to Run

1.  **Clone the repository:**
    
2.  **Install the required libraries:**
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-surprise
    ```

3.  **Ensure the datasets (`appliances.csv` and `interactions.csv`) are in the root directory of the project.**

4.  **Launch Jupyter Notebook and open `Appliance Recommendation System.ipynb`:**
    ```bash
    jupyter notebook "Appliance Recommendation System.ipynb"
    ```

5.  **Run the cells sequentially to see the analysis, model training, and final recommendations.**

---

## 💡 Example Output

Here is a sample of recommendations generated for user `U0509`:

| appliance_id | name                                | category          | brand   |   predicted_rating |
| :----------- | :---------------------------------- | :---------------- | :------ | -----------------: |
| AP0021       | Maytag Dishwasher Model Eco3090     | Dishwasher        | Maytag  |           3.574219 |
| AP0169       | Haier Robot Vacuum Model X778       | Robot Vacuum      | Haier   |           3.527358 |
| AP0149       | Haier Microwave Model Max7481       | Microwave         | Haier   |           3.519006 |
| AP0130       | Kenmore Air Conditioner Model X9731 | Air Conditioner   | Kenmore |           3.499149 |
| AP0060       | Bosch Toaster Model Pro721          | Toaster           | Bosch   |           3.478604 |
