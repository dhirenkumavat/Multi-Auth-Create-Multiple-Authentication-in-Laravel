# Multi-Auth-Create-Multiple-Authentication-in-Laravel

However, In this example, we will add the following three types of users as below:

1) User

2) Manager

3) Admin

When we log in as admin then it will redirect on admin routes, If you log in as manager then it will redirect on manager routes.

So, let's see follow simple steps:

Step 1: Install Laravel 9

composer create-project laravel/laravel example-app

Step 2: Database Configuration

.env

Step 3: Update Migration and Model

<?php
  
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
  
class UsersVerify extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('users_verify', function (Blueprint $table) {
            $table->integer('user_id');
            $table->string('token');
            $table->timestamps();
        });
  
        Schema::table('users', function (Blueprint $table) {
            $table->boolean('is_email_verified')->default(0);
        });
    }
  
    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        
    }
}



