# Multi-Auth-Create-Multiple-Authentication-in-Laravel

However, In this example, we will add the following three types of users as below:

1) User

2) Manager

3) Admin

When we log in as admin then it will redirect on admin routes, If you log in as manager then it will redirect on manager routes.

So, let's see follow simple steps:

## Step 1: Install Laravel 9 ##

``` composer create-project laravel/laravel example-app ```

## Step 2: Database Configuration ##

.env

## Step 3: Update Migration and Model ##

 ``` <?php
  
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
  
class UsersVerify extends Migration
{
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
```
```
php artisan migrate
```
Let's update User Model as below code:
```
namespace App\Models;
  
use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Laravel\Sanctum\HasApiTokens;
use Illuminate\Database\Eloquent\Casts\Attribute;
  
class User extends Authenticatable
{
    use HasApiTokens, HasFactory, Notifiable;
  
    /**
     * The attributes that are mass assignable.
     *
     * @var array

     */
    protected $fillable = [
        'name',
        'email',
        'password',
        'type'
    ];
  
    /**
     * The attributes that should be hidden for serialization.
     *
     * @var array

     */
    protected $hidden = [
        'password',
        'remember_token',
    ];
  
    /**
     * The attributes that should be cast.
     *
     * @var array

     */
    protected $casts = [
        'email_verified_at' => 'datetime',
    ];
 
    /**
     * Interact with the user's first name.
     *
     * @param  string  $value
     * @return \Illuminate\Database\Eloquent\Casts\Attribute
     */
    protected function type(): Attribute
    {
        return new Attribute(
            get: fn ($value) =>  ["user", "admin", "manager"][$value],
        );
    }
}
```
## Step 4: Create Auth using scaffold ## 
Now, in this step, we will create auth scaffold command to create login, register and dashboard. so run following commands:



