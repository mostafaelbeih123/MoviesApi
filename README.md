# MoviesApi
Pulling the latest movies from https://www.themoviedb.org/

# Creating a schedule
Since I run my machine on windows not Unix I coudln't use cron job for task scheduling so I created a task that runs every day on my machine and executes a command that seeds the database. I created a new command called custom:command for seeding.

# Using Laravel Queue to handle the seeder task

1- create a table fo jobs write 'php artisan queue:table'
2- write 'php artisan migrate' to migrate the new createdd table
3- create a job to handle the seeding 'php artisan make:job SeedingJob'
4- copy the content of DatabaseSeeder inside the run function and copy it inside the SeedinjJob handle function
5- 
