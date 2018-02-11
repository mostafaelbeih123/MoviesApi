# MoviesApi
Pulling the latest movies from https://www.themoviedb.org/

# Creating a schedule
Since I run my machine on windows not Unix I coudln't use cron job for task scheduling so I created a task that runs every day on my machine and executes a command that seeds the database. I created a new command called custom:command for seeding.


