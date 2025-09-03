Use GHCI to interact and test your functions.
This is not the same thing as compile haskell code and run it.
## Function


### where
Permet de définir  des variable qui sont utiliser plus tard dans la fonction
Exemple :
```haskell
bmiTell :: (RealFloat a) => a -> a -> String
bmiTell weight height
 | bmi <= skinny = "You're underweight, you emo, you!"
 | bmi <= normal = "You're supposedly normal. Pffft, I bet you're ugly!"
 | bmi <= overwheight = "You're fat! Lose some weight, fatty!"
 | otherwise = "You're a whale, congratulations!"
 where bmi = weight / height ^ 2
	   skinny = 18.5
	   normal = 25.0
	   overwheight = 30.0
```
#### Scope
Les variables qui sont créer avec where Existe uniquement a l'interieur de la 
