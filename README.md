
# Movie Recommendation System

This project is a Python-based movie recommendation system built with pandas, TensorFlow, and an LSTM model. The system uses user-provided watch history to predict preferences and recommend movies.

## Features
1. **New User Initialization**:
   - Enter a User ID to start.
   - If the User ID does not exist in the database (a pandas DataFrame), you'll be prompted to enter your movie watch history.
   - The entered movies are added to the database with the `watch_status` set to `"watched"`.
   
2. **Movie Recommendations**:
   - Based on the entered movies, the system runs an LSTM model to predict your preferred genres and year of movies.
   - It adds 3 recommended movies to the database with the `watch_status` set to `"recommended"`.
   
3. **Returning User Options**:
   - If the User ID exists in the database, you are presented with these options:
     - View Watch List (movies with `watch_status="watched"`).
     - View Recommended Movies (movies with `watch_status="recommended"`).
     - Choose a New Recommended Movie (randomly selects one from the recommended list).
     - Get a New Recommended Movie (uses the LSTM model to add new recommendations to the database).

4. **Duplicate Recommendations**:
   - If the model recommends a movie that's already in your list (whether `watch_status="watched"` or `watch_status="recommended"`), it will recommend the next best option.

---

## Workflow

### Step 1: Enter a User ID
When you start the session with `user_session()`, you'll be prompted to enter your User ID.

- If the ID exists, you'll be presented with options.
- If the ID does not exist, you'll start by entering your movies.

Example:
```plaintext
Enter your user ID: 1
```

---

### Step 2: New User Workflow
If your User ID does not exist in the database, you'll be prompted to enter movies you have watched.

Example:
```plaintext
No records found.

Please enter some movies you have watched.

N.B. Ensure the names match those from TMDB website.

Enter movies separated by commas: Inception, The Dark Knight, Interstellar
```

These movies will be added to the database with `watch_status="watched"`. The system will then:
- Run the LSTM model to predict your preferred genres and movie year.
- Add 3 recommended movies to the database with `watch_status="recommended"`.

---

### Step 3: Returning User Options
If your User ID exists, you'll see the following options:
```plaintext
Welcome back! Choose an option:
1. View Watch List
2. View Recommended Movies
3. Choose a New Recommended Movie
4. Get a New Recommended Movie
5. Exit
```

---

### Example Scenarios

#### **New User**
```plaintext
Enter your user ID: 1
No records found.

Please enter some movies you have watched.

N.B. Ensure the names match those from TMDB website.

Enter movies separated by commas: Inception, The Dark Knight, Interstellar

From your watch history, these are your preferences:
Preferred Genres: ['Sci-Fi', 'Drama']
Preferred Year: 2010

Fetching movie recommendations based on your preferences...

Your Watch List and Recommendations have been updated!

Watched Movies:
          title
0    Inception
1  The Dark Knight
2    Interstellar

Recommended Movies:
          title
0         Arrival
1       Gravity
2  Blade Runner 2049
```

#### **Returning User**
```plaintext
Enter your user ID: 1

Welcome back! Choose an option:
1. View Watch List
2. View Recommended Movies
3. Choose a New Recommended Movie
4. Get a New Recommended Movie
5. Exit

Enter your choice: 1

Watched Movies:
          title
0    Inception
1  The Dark Knight
2    Interstellar

Enter your choice: 3

Here's a recommended movie for you to watch:
Arrival
```

---

### Step 4: Database Management
The database (`user_movie_history`) is a pandas DataFrame structured as follows:

| user_id | title              | watch_status | genres           | year | popularity |
|---------|--------------------|--------------|------------------|------|------------|
| 1       | Inception          | watched      | Sci-Fi, Drama    | 2010 | 90         |
| 1       | The Dark Knight    | watched      | Action, Thriller | 2008 | 95         |
| 1       | Arrival            | recommended  | Sci-Fi, Drama    | 2016 | 85         |

The DataFrame is updated dynamically as users interact with the system.

---

## Notes
1. **Testing**:
   - Used User ID `1` and movies like `"Inception, The Dark Knight, Interstellar"` for testing.
   
2. **Handling Duplicates**:
   - If a recommended movie is already in the user's list, the model selects the next best recommendation.
   - If the user adds a recommended movie to their watchlist, it will automatically get updated to `watched`.

3. **Future Improvements**:
   - Enhance the LSTM model and recommendation logic for better accuracy.
   - Provide more dynamic interaction features (e.g., marking movies as watched directly).
