#### _"Note php is very transactional..." - Matt_



## Comments
```php
// double forward slash for single line comments

#  single hashtag can also be used for comments

/* forward slash and asterisk to start a multi-lined comment
and the opposite to close it,  just as in javascript */


```


## Variables and Constants

```php

<?php
// for scipts to run php enclosure tags are needed
// php variable begin with the the $ sign
$my_var = "string";
// this is a list and is very different from an array in php
$my_var = ["variable ", "types", "are", "determined" "at", "runtime"]


// defining a constant which is an immutable variable
// convention for constants is uppercase with no $ sign
define("PI", 3.14159);

echo PI;

?>
```

**Variable Naming Properties**
- case sensitive
- dynamically typed as php is a dynamically typed language 
- must start with a letter or underscore
- can only contain letters, numbers and underscores

**Variable Scope**
- variables declared outside a function are global
- variables declared inside a function are local
- the keyword global used in front of a variable inside a function denotes a global variable can now be accessible inside the function

**Variable Types - Primitive Data Types**
- See Below
#### Variable Naming Convention

[Stack Exchange Discussion](https://softwareengineering.stackexchange.com/questions/196416/whats-the-dominant-naming-convention-for-variables-in-php-camelcase-or-undersc)

1)  _"...There is no definitive name convention for php, they differ by framework..."_

2) It seems snake_case and camelCase are most common - Me
3)  PHP owns the top-level namespace but tries to find decent descriptive names and avoid any obvious clashes. Function names use underscores between words, while **class names use both the camelCase and PascalCase rules**. -- <i> citation from php manual</i>
4) Function calls and class Names : _"... [PHP is case insensitive in that case](http://the-echoplex.net/log/php-case-sensitivity), so `aTonalFunction()` and `atonalFunction()` are both calls to the same function ..."_


## Printing and Outputting Values

**The biggest nuisance of php prints is the lack of line breaks with new statements**


**Echo**
- this is the more commonly used method for outputting values to the document
- it can contain html semantic tags to be used for formatting and html functionality - such as form

**Print**
- very similar to print except can only output one value per call and is slightly slower
- interesting it always returns 1, which allows it to be used in expressions - _gemini_
- doesn't require brackets in syntax `print $x or print($x)` are both valid
- depending on the data type will output a value or the data type

**Print_r**
 - this is used when needing to display arrays/lists

**Var_dump**
- is used when more information is needed about a variable as it includes datatype and value
- useful for inspecting values and debugging

```php
<?php
$x = "hello";
$y = "world";
$my_list = ["a", "b", "c"];
echo $x, $y; // can ouput multiple values

// print $x, $y; // can't do this - error is thrown
print($x);  
// this will output array not the values in the list
print($my_list);
// this will output the contents 
print_r($my_list);


// This will output the data type and contents but in the form of an object
// and in the case of the list the index values and the dtype for each element
var_dump($my_list);

?>
```

## PHP Primitive Data Types

**Variable Types - Primitive Data Types**
- [Lists vs arrays](https://www.php.net/manual/en/function.list.php) :  Lists are not a different unique datatype from an array in php (like in python).  PHP does have a list function that is used to explode and assign the contents of an array to unique variable names.   **Basic Arrays** are indexable collections. **Associative arrays** are key-value pairs like JS objects/ python dictionaries.  **Multi-dimensional arrays** 
- string : Same as as JS and Python with a data limit of 2GB.
- int : Any integer, can be defined in different bases ie hex and can be negative.
- float : Any decimal number, format is double float.
- boolean : true or false and has the 1 , 0 value.  Same as JS and Python in terms of operators.
- Object:   An object is a specific instance of a class.  It can store data and methods to operate on that data
- NULL -> $x = null;  Pandas equivalent is NaN.  Used to represent empty values in a variable;
- Resource  - virtually identical to js objects according to one source (lost the link? :( ).  [W3](https://www.w3schools.com/php/php_datatypes.asp#:~:text=PHP%20Resource,type%20is%20a%20database%20call.)
says it's not an actual formal data type but a the storing of a reference to either functions or resources external to php.  [Tutorials Point  has a table](https://www.tutorialspoint.com/php-resources) and suggests it can be a source of data such as a stream, file or database and its reference is stored in a resource variable.    See Below

**Basic Datatypes**
```php
<?php
// for formatting create an html element
$line = "<br>";
// directly create an array with either notation 
$arr_1 = ["pink", "blue", "cyan"];
$arr_2 = array(1, 2, 3);
var_dump($arr_1);
echo $line;
var_dump($arr_2);

// Associative array
$ass_arr = ["name" => "bill", 
			"age" => 33, 
			"city" => "nelson"]; 

echo $ass_arr . $line;
// Multidimensional array - can be associative - but not exclusively, can be a 
// matrix
$multi_arr = [ 
	["name" => "Sue", "age" => 25], 
	["name" => "Bob", "age" => 30] ];
echo $multi_arr . $line;
// understanding the list function
// is passes each element in $arr_1 to the new variables - destructures
list($c_1, $c_2, $c_3) = $arr_1;

echo $c_1 . $line . $c_2 . $line;


//strings can be single of double quotes
$a = 'my string : each character is a byte';
echo $a . $line;


// int - in octal(base 8) form or hex form (base 16)
// note both will be displayed in base 10
$b = 0123;
$c = 0x1A;
echo $b . $line . $c . $line;

// Objects
?>
```

**Objects**
```php
<?php

/* What is interesting about php classes / objects is the fully run. 
Notice how the var dump returns the array even though battle() is never 
called */

class Character {
	 // properties
	 public $armour = "shield";
	 public $weapon = "laser beam";
	//methods 
	function battle(){
	   $arr = array(this->$armour, this->$weapon);
	   return $arr;
	}
}

$elf = new Character;
var_dump($elf);

?>

```


**Null**
```php
<?php
// x and y are both null values and will be " == " but z will not
$x = NULL;
$y;  // $y is automatically assigned NULL
$z = "";  
```



**Resources**
```php
<?php
// linking to the database as a resource
// assumes you are runnign a mysql server

// use this link to add an insert into our toy db
// create a connection to the db aka our resource
$link = mysqli_connect("localhost", "admin", "password", "demo-db");

// check connection aka the resource validity
if ($link ===false){
	// disconnect the process 
	die("ERROR : Could not connect to db. " . mysqli_connect_error());
} else {
	// communitcate host info
	echo "Connection Successfull. Host Info : " . mysqli_get_host_info($link) . "<br>";
}

// create a query notice the sql starement doens't need a semicolon in the quotes that is done automatically
$firstname = "haryy";
$email = "harry@exampleemail.com";
$sqlInsert = "INSERT INTO employees (firstname, email) VALUES('$firstname', '$email')";

//  we test and post in one line
if(mysqli_query($link, $sqlInsert)){
	echo "new record created " . "<br>";
} else {
	echo "Error creating record ". mysqli_error($link);
}
// when were done close the connection to the resource
// releasing system resources 
$mysqli_close($link);

?>
```


### Resources 
How are they created, managed  and why are they important?
 
External resources are pivotal to php because we connect to databases, and other api web routes that require authentication and from we acquire data.  Ensuring that we close these connections  releases the hardware and connection resources  and improves security risks.
Some resources have detectors, (a resource counting system) and when there are no more references this is automatically detected and the garbage collector releases the memory. **This is not the case with database!!**


[Source php docs](https://www.php.net/manual/en/language.types.resource.php)
[List of Resource types](https://www.php.net/manual/en/resource.php)



## Operators
[Source ](https://condor.depaul.edu/sjost/hci430/documents/op-tables.htm)

**Arithmetic Operators**

| Example | Name           | Meaning                                                            |     |
| ------- | -------------- | ------------------------------------------------------------------ | --- |
| $x + $y | Addition       | Computes the sum of $x and $y.                                     |     |
| $x - $y | Subtraction    | Computes the difference $x minus $y.                               |     |
| $x * $y | Multiplication | Computes the product $x times $y.                                  |     |
| $x / $y | Division       | Computes the floating point quotient $x divided by $y.             |     |
| $x % $y | Mod            | Computes the remainder of $x divided by $y using integer division. |     |
|         |                |                                                                    |     |
**Concatenation Operator**

|Example|Name|Meaning|
|---|---|---|
|$x . $y|Concatenation|Combines $x and $y into a single string.|

**Assignment Operators**

| Example   | Name              | Meaning                |
| --------- | ----------------- | ---------------------- |
| $x = $y;  | Assignment        | Assign $x to $y.       |
| $x += $y; | Plus Equal        | Replace $x by $x + $y. |
| $x -= $y; | Minus Equal       | Replace $x by $x - $y. |
| $x *= $y; | Times Equal       | Replace $x by $x * $y. |
| $x /= $y; | Divide Equal      | Replace $x by $x / $y. |
| $x %= $y; | Mod Equal         | Replace $x by $x % $y. |
| $x .= $y; | Concatenate Equal | Replace $x by $x . $y. |

**Comparison Operators**

|Example|Name|Meaning|
|---|---|---|
|$x == $y|Equal To|$x is equal to $y|
|$x === $y|Identical To|$x is equal to $y and they are of the same datatype.|
|$x != $y|Not Equal To|$x is not equal to $y|
|$x <> $y|Not Equal To|$x is not equal to $y|
|$x !== $y|Not Identical To|$x is not equal to $y or they are not of the same datatype|
|$x < $y|Less Than|$x is strictly less than $y|
|$x <= $y|Less Than or Equal|$x is less than or equal to $y|
|$x > $y|Greater Than|$x is strictly greater than $y|
|$x >= $y|Equals|$x is greater than or equal to $y|

**Logical Operators**

|Example|Name|Meaning|
|---|---|---|
|$x and $y|Logical And|Returns TRUE if both $x and $y are TRUE, otherwise FALSE.|
|$x or $y|Logical Or|Returns TRUE if $x or $y or both are TRUE, otherwise FALSE.|
|$x xor $y|Logical Exclusive Or|Returns TRUE if $x or $y but not both are TRUE,  <br>otherwise FALSE.|
|!$x|Logical Not|Returns FALSE if $x is TRUE, otherwise TRUE.|
|$x && $y|Logical And|Returns TRUE if both $x and $y are TRUE, otherwise FALSE.|
|$x \| $y|Logical OR|Returns TRUE if $x or $y or both TRUE, otherwise FALSE.|

<i>Note that even though and has the same meaning as && and or has the same meaning as ||, they have different precedences.</i>

## If Elseif Else Conditionals

```php
<?php 
$link = mysqli_connect("localhost", "admin", "password", "demo-database");
$firstname = "harry";
$email = "harry@exampleemail.com";
$sqlInsert = "INSERT INTO employees (firstname, email) VALUES('$firstname', '$email')";

// note the if else syntax if identical to JS
if(mysqli_query($link, $sqlInsert)){
	echo "new record created " . "<br>";
} else {
	echo "Error creating record ". mysqli_error($link);
}
?>
```

## Loops :  for, foreach & while

```php
<?php

// Note the for loop is in the following code block allong with functions
$line_bs = "<br>";
$arr = array("blue", "green", "red", "cyan", "yellow");
$arr_2 = array(
	"name" => "ramsey",
	"age" => 105,
	"department" => "tech"
);
$x = 0;
$y = 20;

// For each loop is ideal for arrays
echo $line_bs;
foreach($arr as $value){
	echo $value . "<br>";
}

// for each looping through associative arrays!
foreach($arr_2 as $key => $value){
	echo $key ." is ". $value ."<br>";
}

// while loop format is consistent w JS and python
while($x <= $y){
	echo $x . $line_bs;
	$x++; // notice that $x is globally scoped without global as it's not in a function
}

// the do ... while changes the syntax and the order but still verymuch the same as while
// notice the syntax the ';' needs to only be after the conditional
$x=0;
$y=20;

do{
	echo $y . $line_bs;
	$y--;
}
while($y >= $x);

?>
```

## Functions  

```php
<?php
// function delcaration and passing of values is identical syntactically as JS
function reverse($arr){
	$rev = [];
	// for loops syntax almost exactly the same as JS
	// except the delimiter between iterable declarations is a ';'
	for($i=(count($arr) - 1); $i>=0; $i--){
		array_push($rev, $arr[$i]);
	};
	return $rev;
};

$list = [5, 4, 3, 2, 1, 0];

$rev_arr = reverse($list);

print_r($rev_arr );
?>
```

## Dates 
#sql-dates
Farting around with dates collected from an SQL table is PITA in php.  According to the post below converting the timestamp in the SQL query is the cleanest way
[S.O. Post w two Solutions](https://stackoverflow.com/questions/5547252/convert-mysql-timestamp-into-actual-date-and-time)

 ```sql
SELECT DATE_FORMAT(timestamp_col,'%M %D, %Y') FROM Mytable;

-- or 

SELECT DATE_FORMAT(timestamp,'%Y-%m-%d') FROM Mytable;

```

Rather than


You have two solutions :

- Use [**`strtotime()`**](https://www.php.net/strtotime) to parse the date to a timestamp, and [**`date()`**](https://www.php.net/manual/en/function.date.php) to re-format it to a string
- Or use the [**`DateTime`**](https://www.php.net/datetime) class
```php

echo date('M j Y g:i A', strtotime('2010-05-29 01:17:35'));

$dt = new DateTime('2010-05-29 01:17:35');
echo $dt->format('M j Y g:i A');

```

Having said that binding issues can arise because the variable gets processed by the method then it has lost the association to the variable name.

```php
$query = "SELECT
Blogs.BlogID,
Blogs.Title,
Blogs.Blog,
DATE_FORMAT(Blogs.Date, '%Y-%m-%d') AS FormattedDate,
Blogs.UserID,
Users.GivenNames,
Users.Lastname
FROM Blogs
INNER JOIN Users
WHERE Blogs.UserID = Users.UserID";

// ...
// now $post['Date'] is no longer a column title but 
// $post['Formated] is now part of the associated array returned and contains 
// the correct date

// so looping through the tabular data now won't throw errors

  

foreach($posts as $post) {
echo "<div class='topic'>";
echo "<h2>" . $post["Title"] . "</h2>";
echo "<p>". $post["Blog"] . "</p>";
echo "<p>Author : <i>". $post["GivenNames"] . "&nbsp" . $post['Lastname']." </i><p>";

echo "<p>ID : ". $post["BlogID"] ."&nbsp Date : ". $post['FormattedDate']."</p>";

}
```

See [[GPT  MySQL Dates#Prompt]]

