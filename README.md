# MoviesApi
  Pulling the latest movies from https://www.themoviedb.org/.

# Creating a schedule
  Since I run my machine on windows not Unix I coudln't use cron job for task scheduling so I created a task that runs every day on my  machine and executes a command that seeds the database. I created a new command called custom:command for seeding.

# Using Laravel Queue to handle the seeder task
  - create a table fo jobs write 'php artisan queue:table'
  - write 'php artisan migrate' to migrate the new createdd table
  - create a job to handle the seeding 'php artisan make:job SeedingJob'
  - copy the content of DatabaseSeeder inside the run function and copy it inside the SeedinjJob handle function
  - We need to dispatch the job create, so inside web.php use the 
  ```sh
  Route::get('seed',function(){
  $job = (new SeedinJob())->delay()Carbon::now();
  dispatch($job);
  );
  ```
  - Final step is processing the job. Write 'php artisan queue:work'


# Creating the task as laravel plugin



