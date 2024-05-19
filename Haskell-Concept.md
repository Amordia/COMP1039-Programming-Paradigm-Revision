# Haskell Programming Concepts

## Basic Maths, Lists, Functions, and Scripts

### Mathematics
Haskell handles basic arithmetic operations in a straightforward manner. For instance:

```haskell
result = 34.5 + (3.2 * 4.5)
-- result is 48.9
```

### Lists
Lists are fundamental in Haskell, supporting various operations:

- **Accessing the first element**: Using `head [1,2,3]` retrieves `1`.

  ```haskell
  firstElement = head [1,2,3]
  -- firstElement is 1
  ```

- **Concatenating lists**: `[3,2,1] ++ [1,2,3]` results in `[3,2,1,1,2,3]`.

  ```haskell
  combinedList = [3,2,1] ++ [1,2,3]
  -- combinedList is [3,2,1,1,2,3]
  ```

### Function Application
Haskell uses space for function application, which is left-associative:

```haskell
f x y  -- is equivalent to (f x) y

add a b = a + b
sumResult = add 2 3
-- sumResult is 5
```

## Types, Polymorphism, and Predefined Type Classes

### Predefined Types
Commonly used types include `Bool`, `Int`, `Float`, `Char`, and `String`.

```haskell
isTrue :: Bool
isTrue = True

number :: Int
number = 5

fraction :: Float
fraction = 3.14

character :: Char
character = 'a'

text :: String
text = "Hello, Haskell!"
```

### Type Notation
Explicit type declarations enhance readability and debugging:

```haskell
listOfInts :: [Int]
listOfInts = [3, 4]
```

### Lists and Tuples
Lists hold elements of the same type, while tuples can contain mixed types.

```haskell
list :: [Int]
list = [1, 2, 3]

tuple :: (Int, Char, String)
tuple = (1, 'a', "hello")
```

### Function Types
Indicate input and output types, e.g., `Int -> Int -> Int`.

```haskell
add :: Int -> Int -> Int
add x y = x + y

sumResult = add 5 10
-- sumResult is 15
```

### Curried Functions
Functions that return other functions, e.g., `Int -> (Int -> Int)`.

```haskell
multiply :: Int -> (Int -> Int)
multiply x y = x * y

result = (multiply 2) 3
-- result is 6
```

### Polymorphism and Overloading
Generic functions that work over any type, e.g., `[a] -> a`. Overloading allows functions like summing a list where the list elements conform to a numeric type class (`Num`).

```haskell
identity :: a -> a
identity x = x

maxElement :: (Ord a) => [a] -> a
maxElement = maximum

exampleMaxElement = maxElement [1, 2, 3, 4]
-- exampleMaxElement is 4
```

## Defining Functions

### Conditional Expressions
Branch logic using `if...then...else` constructs.

```haskell
absolute :: Int -> Int
absolute x = if x < 0 then -x else x

exampleAbsolute1 = absolute (-5)
-- exampleAbsolute1 is 5
exampleAbsolute2 = absolute 3
-- exampleAbsolute2 is 3
```

### Guarded Expressions
Use guards for more complex conditional logic:

```haskell
f :: Int -> String
f x
  | x > 0     = "Positive"
  | x < 0     = "Negative"
  | otherwise = "Zero"

exampleGuarded1 = f 5
-- exampleGuarded1 is "Positive"
exampleGuarded2 = f (-3)
-- exampleGuarded2 is "Negative"
exampleGuarded3 = f 0
-- exampleGuarded3 is "Zero"
```

### Pattern Matching
Facilitates deconstructing data types directly in function definitions.

```haskell
sumList :: [Int] -> Int
sumList [] = 0
sumList (x:xs) = x + sumList xs

exampleSumList = sumList [1, 2, 3, 4]
-- exampleSumList is 10
```

### Lambda Expressions
Anonymous functions are useful for short operations:

```haskell
increment = \x -> x + 1
exampleLambda = increment 5
-- exampleLambda is 6
```

### Operators
Haskell treats operators as functions which can be partially applied:

```haskell
sumResult = (+) 2 3
-- sumResult is 5

incrementBy2 = (+2) 3
-- incrementBy2 is 5
```

## List Comprehension and Strings

### List Comprehension
Generates lists from existing lists using a compact syntax:

```haskell
xs = [1,2,3]
ys = [4,5,6]
distances = [sqrt (x^2 + y^2) | x <- xs, y <- ys]

exampleDistances = distances
-- exampleDistances is [4.123, 5.099, 5.831, 4.472, 5.385, 6.0, 5.0, 5.831, 6.708]
```

### List Comprehension with Guards
List comprehensions with conditions:

```haskell
distancesWithGuards = [sqrt (x^2 + y^2) | x <- xs, y <- ys, x < y]

exampleDistancesWithGuards = distancesWithGuards
-- exampleDistancesWithGuards is [5.099, 5.831, 5.385, 6.0, 6.708]
```

### Strings
In Haskell, strings are lists of characters: `"abc"` is equivalent to `['a', 'b', 'c']`.

```haskell
string :: String
string = "abc"

charList :: [Char]
charList = ['a', 'b', 'c']

exampleString = string
-- exampleString is "abc"
exampleCharList = charList
-- exampleCharList is ['a', 'b', 'c']
```

## Recursive Functions

### Basic Recursion
Define functions that call themselves, like a factorial:

```haskell
fac :: Int -> Int
fac 0 = 1
fac n = n * fac (n-1)

exampleFac1 = fac 5
-- exampleFac1 is 120
exampleFac2 = fac 0
-- exampleFac2 is 1
```

### Recursion on Lists
Process lists recursively by splitting them into head and tail.

```haskell
sumList :: [Int] -> Int
sumList [] = 0
sumList (x:xs) = x + sumList xs

exampleSumList = sumList [1, 2, 3, 4]
-- exampleSumList is 10
```

### Mutual Recursion
Interdependent functions that call each other.

```haskell
isEven :: Int -> Bool
isEven 0 = True
isEven n = isOdd (n-1)

isOdd :: Int -> Bool
isOdd 0 = False
isOdd n = isEven (n-1)

exampleIsEven1 = isEven 4
-- exampleIsEven1 is True
exampleIsOdd1 = isOdd 3
-- exampleIsOdd1 is True
```

### Computational Efficiency
Tail recursion optimizes recursive functions for better performance.

```haskell
factorial :: Int -> Int
factorial n = facHelper n 1
  where
    facHelper 0 acc = acc
    facHelper n acc = facHelper (n-1) (n*acc)

exampleFactorial1 = factorial 5
-- exampleFactorial1 is 120
exampleFactorial2 = factorial 0
-- exampleFactorial2 is 1
```

## Higher-Order Functions

### Functions as Values and Arguments
Treat functions like any other data, e.g., passing functions as arguments.

```haskell
double = \x -> x * 2
result = double 3
-- result is 6

applyTwice :: (a -> a) -> a -> a
applyTwice f x = f (f x)

exampleApplyTwice = applyTwice double 3
-- exampleApplyTwice is 12
```

### List Aggregation
Combine list elements using a function, e.g., `foldr`.

```haskell
sumList = foldr (+) 0 [1, 2, 3, 4]
-- sumList is 10
```

### Composition
Chain functions together:

```haskell
increment = \x -> x + 1
double = \x -> x * 2

exampleComposition = (increment . double) 3
-- exampleComposition is 7
```

### Returning Function Values
Compose functions to create new functions dynamically.

```haskell
add :: Int -> Int -> Int
add x y = x + y

mult :: Int -> Int -> Int
mult x y = x * y

add3 = add 3
mult2 = mult 2

exampleComposedFunction = (add3 . mult2) 5
-- exampleComposedFunction is 13


```

## Defining Types

### Declaring New Types
Create simple type synonyms with `type`.

```haskell
type Board = [Int]

exampleBoard :: Board
exampleBoard = [1, 2, 3, 4]
-- exampleBoard is [1, 2, 3, 4]
```

### Data Declarations
Define complex data structures:

```haskell
data Answer = Yes | No | Unknown

exampleAnswer1 = Yes
-- exampleAnswer1 is Yes
exampleAnswer2 = No
-- exampleAnswer2 is No
```

### Constructors and Parametric Data Types
Build custom types with parameters to hold any type.

```haskell
data Rectangle = Rectangle Float Float

exampleRectangle = Rectangle 3.0 4.0
-- exampleRectangle is Rectangle 3.0 4.0

data Tree a = Leaf a | Node (Tree a) (Tree a)

exampleTree = Node (Leaf 1) (Node (Leaf 2) (Leaf 3))
-- exampleTree is Node (Leaf 1) (Node (Leaf 2) (Leaf 3))
```

### Recursive Data Types
Define types that reference themselves, useful for structures like trees.

```haskell
data Nat = Zero | Succ Nat

exampleNat1 = Zero
-- exampleNat1 is Zero
exampleNat2 = Succ (Succ Zero)
-- exampleNat2 is Succ (Succ Zero)
```

## Interactive Programming and I/O

### The `IO` Type
Handle input/output operations, encapsulating side effects.

```haskell
exampleIO :: IO ()
exampleIO = do
  putStrLn "Enter your name:"
  name <- getLine
  putStrLn ("Hello, " ++ name ++ "!")
```

### Using `do` Blocks
Sequence operations in a clear, imperative style.

```haskell
exampleIO :: IO ()
exampleIO = do
  putStrLn "Enter your age:"
  age <- getLine
  putStrLn ("You are " ++ age ++ " years old.")
```

### Basic I/O Operations
`putStrLn` for output, `getLine` for input.

```haskell
exampleIO :: IO ()
exampleIO = do
  putStrLn "Hello, what is your name?"
  name <- getLine
  putStrLn ("Nice to meet you, " ++ name)
```

## Lazy Evaluation

### Evaluation Strategies
Lazy evaluation delays computation until the result is needed, supporting features like infinite lists.

```haskell
ones :: [Int]
ones = 1 : ones  -- creates an infinite list of ones

exampleOnes = take 5 ones
-- exampleOnes is [1,1,1,1,1]
```

### Efficiency of Lazy Evaluation
Reduces computational overhead by avoiding unnecessary calculations.

```haskell
takeFiveOnes = take 5 ones
-- takeFiveOnes is [1, 1, 1, 1, 1]
```
