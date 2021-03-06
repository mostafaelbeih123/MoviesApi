# MoviesApi Laravel Plugin
  Pulling the latest movies from https://www.themoviedb.org/.

# Creating a schedule
  Created a task that runs every day on my machine and executes a command that seeds the database. The task simply calls db:seed.

# Using Laravel Queue to handle the seeder task
  - create a table for jobs, write 'php artisan queue:table'
  - write 'php artisan migrate' to migrate the new created table
  - create a job to handle the seeding 'php artisan make:job SeedingJob'
  - copy the content of DatabaseSeeder inside the run function and copy it inside the SeedingjJob handle function
  - We need to dispatch the job, so inside web.php use the 
  ```sh
  Route::get('seed',function(){
  $job = (new SeedingJob())->delay()Carbon::now();
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
  - Create a class with a function inside that has the same code of the database seeder.
  - Inside the serviceProvide.php file add this peice of code 
  ```sh
  public function register(){
  
    $this->app->bind(''package-name'-'package-usage'',function(){
      return new Seeder();
   });
  ``` 
  - Create a directory called Facades with a script inside called Seeder.php
  - Inside the script add the following:
  ```sh
  class Seeder extends Facade{
    protected static functiongetFacadeAccessor(){
      return ''package-name'-'package-usage''
    }
  }
  ```
  - Inside config/app add the following line inside the aliases array.
  
  ```sh
  'Seeder' => 'package-name'\'package-usage'\Facades\Seeder::class,
  ```  
  - Inside the main routes\web.php add:
  ```sh
  Route::get('seed',function(){
    return Seeder::seed();
  })
  ```
  
  # Using Docker to run the API
  - Install docker
  - Install laradocks inside the project file by running this command:
  - Inside laradocks type:
  ```sh
  docker-compose up -d nginx mysql
  ```
  -Then run this command
  ```sh
  docker-compose exec workspace bash
  composer install
  
  ```
  - Connect to the database and then run the api

