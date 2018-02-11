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

  -create a directory inside the project called packages
  -create another directory inside call it 'package-name' with a directory inside name it'package-usage'
  -now create another directory called src to make things orgnized
  - You should have now packages->'package-name'->'package-usage'-> src and we will add scripts to it
  -Run composer init. Now you should have a composer.json file
  - Create directore routes and routes.php inside it.
  - Create ServiceProvider
  ```sh
  public function boot(){
  
    require __DIR__.'/routes/routes.php';
    
   }
  ```
  -Register serviceProvider in config/app.php.
  -Add the namespace inside the main composer.json file.
  -Run 'composer dump-autoload'.
  - Inside src create seeder.php.
  - Create a class with a function inside that has the same code of the database seefer.
  


