## Church Booleans
true = \ t f . t

false = \ t f . f

not = \ b . b false true

and = \ p q . p q false

or  = \ p q . p true q 

xor = \ p q . p (not q) q



## Church numerals


## Scott Encoding Numerals
zero = \ z s.z

one = \z s. s(\z s.z)

succ = \ n. \z s. s n

add = \m n. m n (\p. succ (add p n))

pred = \n. n 0 (\i.i)

mul = \m n. m 0 (\p. add n (mul p n))

## Lists
Pair = \ a b . \ f . f a b

first = \ p . p True

second = \ p . p False

- General list template: (isEmpty, (value, rest of list))

Nil = Pair True ()

isEmpty = \ xs . first xs

head = \ xs . first (second xs)

tail = \ xs . second (second xs)

## Lambda Calculus: Lists
// append :: List a -> a -> List a

append = \ xs v . isEmpty(xs) (Pair False (Pair v Nil)) (Pair False (Pair (head xs) (append (tail xs) v)))


// prepend :: List a -> a -> List a

prepend = \ xs v . Pair False (Pair v xs)

## Count-By X
// foldl : (z -> x -> z) -> z -> List x -> z

foldl = \ fn z xs . (isEmpty (xs)) (z) (foldl fn (fn z (head xs)) (tail xs))

// append :: List a -> a -> List a

count-by = \ x n . n Nil (\p. append (count-by x p) (mul x n))



