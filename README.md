# Random Laravel Concepts in short

## 1. create vs insert

#### Insert Method: 

##### Pros:

###### Bulk Insertion:

Insert is useful for bulk insertion of multiple records in a single database query.
It allows you to insert an array of records at once, making it more efficient for large datasets.

- Performance:

When inserting a large number of records, insert can be more performant than creating individual model instances and saving them one by one.


##### Cons:

###### No Eloquent Events:

When using insert, Eloquent events (like creating, created, etc.) are not triggered. This means any custom logic tied to these events won't be executed.

###### No Mass Assignment Protection:

Mass assignment protection (fillable and guarded attributes) is not applied when using insert. You need to manually ensure the data being inserted is secure.

###### Timestamps:

Timestamps (```created_at``` and ```updated_at```) are not automatically set when using insert. If you need timestamps, you must handle them manually.

#### Create Method: 

##### Pros:

###### Eloquent Events:

Create triggers Eloquent events (creating, created, etc.), allowing you to execute custom logic before and after creating a record.

###### Mass Assignment Protection:

Mass assignment protection is applied when using the create method. You can define fillable or guarded attributes to control which fields can be mass-assigned.

###### Timestamps:

Create automatically sets timestamps (```created_at``` and ```updated_at```) on the model instance.



##### Cons:

###### Individual Inserts:

Create performs individual inserts for each record, which can be less efficient than insert for bulk insertions with a large number of records.


###### Not Suitable for Bulk Insert:

When dealing with a large number of records, calling create in a loop is not an efficient way to perform a bulk insert.


## 2. How to upgrade to latest laravel version.
To upgrade to latest version --Eg from laravel 10.10 to latest version use composer update command

```
composer update laravel/framework
```
<img width="877" alt="Screenshot 2024-03-12 at 9 47 52 PM" src="https://github.com/DiveshR/Random-Laravel-Concepts-in-short/assets/25860707/5e6fa6d5-c151-4e9c-a5e4-44a4dea22b8c">

## 3. Filtering data in sorter way
In Laravel 10.10
```
$search = '%Otwell%';

User::query()
      ->where(function ($query) use ($search) {
          $query
              ->where('first_name', 'LIKE', $search)
              ->orWhere('last_name', 'LIKE', $search)
              ->orWhere('email', 'LIKE', $search)
              ->orWhere('phone', 'LIKE', $search);
      })
```

In laravel 10.48
```
$search = '%Otwell%';

User::query()
      ->whereMultiple([
          'first_name',
          'last_name',
          'email',
          'phone'
      ], 'LIKE', $search)
```


