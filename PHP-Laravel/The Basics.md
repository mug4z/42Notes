PHP can be inside html code. With the tag
```php
<?php
$message="Hello World"; 
php echo $mesage
?>

<?= $message ?>
```

In PHP the rule of literal string and string with variable woks like with bash
```php
$var = "salut";
echo "$var salut"; // echo salut salut
echo '$var salut'; // echo $var salut
```
## Operator
Concatenation operator is the dot `.`

## Data Types
```php
$var = "Salut"; // string
$bool = true; // bool true
$boolF = false; // bool false
```
## Variables
Declare variable like this
```php
$var = "Salut";
```

## Conditions
```php
$var = true;
if($var) {
	$message = "Salut";
} else {
	$message = "Pas salut";
}
```

### Equality is 3 =  ===
```php
<?php if ($book['author'] === 'Andy Weir'): ?>
    <li><?= $book['name'] ?> (<?= $book['releaseYear'] ?>)</li>
<?php endif; ?>
```
## Arrays
Declaring arrays
```php
?php
        $books = [
            "LOL",
            "POUET",
            "LUL",
            "NOUGA",
        ];
      ?>

```
### Associative Arrays
```php
$books = [
    [
        "name" => "Do Androids Dream of Electric Sheep?",
        "author" => "Philip K. Dick",
        "purchaseUrl" => "https://example.com/androids-dream"
    ],
    [
        "name" => "Project Hail Mary",
        "author" => "Andy Weir",
        "purchaseUrl" => "https://example.com/hail-mary"
    ]
];
```
Access it like
```php
$books[0]['name']
```


## Loop
```php
foreach ($books as $book) {
	echo "<li> {$book}</li>";
};
```

## Function
```php
function filterByAuthor($books) {
    // function logic here
}

```
### Lambda functrion (anonymous function)
```php
  $test = function () {
        return 'TEST FUNCTION';
      };
```