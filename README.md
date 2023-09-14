# Movies from TMDB

This project allows you to create your own database with movies. All movies will be taken from [TMDB](https://www.themoviedb.org/) with use of TMDB API ([API documentation](https://developer.themoviedb.org/docs)).<br>
You will be able to search for movies by keywords in the database you have created, as well as find similar movies.

## How to install

1. To run the project you should already have Python 3 and pip (package-management system) installed.

2. Download the code (use git clone).

3. Create a virtual environment with its own independent set of packages using [virtualenv/venv](https://docs.python.org/3/library/venv.html). It'll help you to isolate the project from the packages located in the base environment.

4. Install all the packages used in this project, in your virtual environment which you've created on the step 3. Use the `requirements.txt` file to install dependencies:
   ```
   pip install -r requirements.txt
   ```
5. Install and run a [VPN](https://adguard-vpn.com/ru/welcome.html) if you have difficulty accessing [TMDB](https://www.themoviedb.org/).
In case the VPN download website doesn't open either, you will first need to install and enable [AdGuard Proxy for Chrome](https://chrome.google.com/webstore/detail/adguard-vpn-%E2%80%94-free-secure/hhdobjgopfphlmjbmnpglhfcgppchgje?hl=ru)

6. To use this script you also need an API key. To register for an API key, click the [API link](https://www.themoviedb.org/settings/api) from within your account settings page.


## What exactly does each script do?

To run each of the scripts below enter in your console:
```
python3 script_title.py
```
Make sure to replace script_name.py with the name of the script to be run.


### hello_api_TMDB.py
This script was created to make sure that you have a valid API key, and that you were able to connect to the API. In some countries, you will need a VPN, which we wrote about above.<br> **It is recommended to run this script first.**

Script requests an API key from you and retrieves it from console input.
The text you'd enter won't be displayed for security reasons.
```
Enter your api key v3:
```

Then it tries to get response from [one of the movies on the website (Saw II)](https://www.themoviedb.org/movie/215-saw-ii) and if an error occurs due to an invalid API key, the message `Invalid api key` will be displayed:
```
Invalid api key
```
After checking the API key, you will get the budget amount of the movie [Saw II](https://www.themoviedb.org/movie/215-saw-ii)<br>

```
4000000
```
This means that everything is in order and you can start using the rest of the scripts.


### make_own_db.py

Creates your own database (*MyFilmDB.json*) in the project root with all information about `1000 movies`. The only thing that needs to be entered from console is TMDB API Token, which should've been generated on the last [step](https://github.com/michaelmatasyants/tmdb_api#readme:~:text=To%20use%20this%20script%20you%20also%20need%20an%20API%20key.%20To%20register%20for%20an%20API%20key%2C%20click%20the%20API%20link%20from%20within%20your%20account%20settings%20page.).


**Let's take a closer look at how it works:**

Script requests an API key from you, retrieves it from console input and tries to get response from [one of the movies on the website](https://www.themoviedb.org/movie/2-ariel).
The text you'd enter won't be displayed for security reasons.
```
Enter your api key v3:
```

If an error occurs due to an invalid API key, the message `Invalid api key` will be displayed.
```
Invalid api key
```

After checking the API key you'll see:
```
please, wait, this operation may take smth like 15-20 minutes
```
Starts loading movies by making queries to each movie and saving responses.
After each movie is saved, the percentage of completed downloads is calculated and the result is displayed in the terminal.
  ```
  0.01 percent complete
  ```
Creates *MyFilmDB.json* file and saves information about each movie.


### search_in_db.py
Searches for movies by keyword in your database created with the `make_own_db.py` script discussed in the [previous step](https://github.com/michaelmatasyants/tmdb_api#make_own_dbpy). So to use this script, you should only enter the path to the database and the keyword to search for the movie.

**Let's take a closer look at how it works:**

Script requests you to enter the path to the database, to search movie in it.
```
Enter path to DataBase:
```
If the directory or file specified as a path doesn't exist, a message will be displayed:
```
File not found, sorry...
```
If the path to the database is correct, the database will be loaded and you'll be asked to enter a keyword to search for the movie:
```
Enter film to search for:
```
Script searches for a movie using the entered keyword in the movie titles from the database (*MyFilmDB.json*) and displays movies in the terminal:
```
>>> Enter film to search for:Lock

A Clockwork Orange
Dave Chappelle's Block Party
Lock, Stock and Two Smoking Barrels
Sherlock Jr.
```


### find_similar.py
Searches for similar movies by keyword in your database created with the `make_own_db.py` script [discussed earlier](https://github.com/michaelmatasyants/tmdb_api#make_own_dbpy). So to use this script, you should only enter the path to the database and the keyword to search for similar movies.

**Let's take a closer look at how it works:**

Script requests the path to the database, to search movie in it.
```
Enter path to DataBase:
```
If the directory or file specified as a path doesn't exist, a message will be displayed:
```
File not found, sorry...
```
If the path to the database is correct, the database will be loaded and you'll be prompted to enter movie title:
```
Enter film to search for:
```
First, script finds the movie in your database by searching the full title you've entered earlier.<br>
Be careful to enter the full name of the movie to find similar movies.
If no movie is found for your search, you'll receive a message:
```
There is no such movie in FilmsDB
```
Then, for each movie in the database, a match rating is calculated for the selected movie according to the following criteria:
  - If the movie belongs to the same collection, for example, to one of the "Saw" series movies, then 1000 is added to the rating;
  - Genre match - 500 is added to the rating;
  - Original language match - 300 is added to the rating;
  - Budget match - 100 is added to the rating.

The script saves the movie titles and calculated ratings for each movie. The movie entered by the user is removed from the saved movies, as it is also contained in the database and will have the highest matching rating.

After that, the script sorts all movies by rating and displays in the terminal the names of the first 8 movies with the highest rating in lexicographically sorted order.
  ```
  >>> Enter film to search for:Star Wars
  ```
  Output:
  ```
  Alien
  Army of Darkness
  Dead Man Walking
  Doctor Zhivago
  Four Rooms
  Gremlins
  Judgment Night
  Life in Loops (A Megacities RMX)
  The Lost World: Jurassic Park
  ```
