---
title: "Interactive Session 2A"
subtitle: "Data types & indexing"
editor_options: 
  chunk_output_type: console
---




# Part 1: Setup

- Create a repo on GitHub called `eds221-day2-comp`
- Clone to make a version-controlled R Project
- Create a new Quarto Markdown, saved in the root as `r-data-types`
- Create a new Jupyter Notebook, saved in the root as `py-data-types`

# Part 2: Making & indexing data in R

## Vectors!

### Making vectors

#### A character vector


::: {.cell}

```{.r .cell-code}
dogs <- c("teddy", "khora", "waffle", "banjo")

typeof(dogs)
```

::: {.cell-output .cell-output-stdout}

```
[1] "character"
```


:::

```{.r .cell-code}
class(dogs)
```

::: {.cell-output .cell-output-stdout}

```
[1] "character"
```


:::
:::


#### A numeric vector


::: {.cell}

```{.r .cell-code}
weights <- c(50, 55, 25, 35)

typeof(weights) # Hmmm what is different about this and the line below?
```

::: {.cell-output .cell-output-stdout}

```
[1] "double"
```


:::

```{.r .cell-code}
class(weights)
```

::: {.cell-output .cell-output-stdout}

```
[1] "numeric"
```


:::
:::


#### An integer vector


::: {.cell}

```{.r .cell-code}
dog_age <- c(5L, 6L, 1L, 7L)

typeof(dog_age)
```

::: {.cell-output .cell-output-stdout}

```
[1] "integer"
```


:::

```{.r .cell-code}
class(dog_age)
```

::: {.cell-output .cell-output-stdout}

```
[1] "integer"
```


:::

```{.r .cell-code}
# Check with a logical: 
is.numeric(dog_age)
```

::: {.cell-output .cell-output-stdout}

```
[1] TRUE
```


:::
:::


#### What if we combine classes? 

There is a hierarchy of classes. The broadest of all in a vector wins (if there are characters, then character will be the class of the entire vector).


::: {.cell}

```{.r .cell-code}
dog_info <- c("teddy", 50, 5L)
dog_info
```

::: {.cell-output .cell-output-stdout}

```
[1] "teddy" "50"    "5"    
```


:::

```{.r .cell-code}
typeof(dog_info)
```

::: {.cell-output .cell-output-stdout}

```
[1] "character"
```


:::

```{.r .cell-code}
class(dog_info)
```

::: {.cell-output .cell-output-stdout}

```
[1] "character"
```


:::

```{.r .cell-code}
is.character(dog_info)
```

::: {.cell-output .cell-output-stdout}

```
[1] TRUE
```


:::
:::


#### Named elements


::: {.cell}

```{.r .cell-code}
dog_food <- c(teddy = "purina", khora = "alpo", waffle = "fancy feast", banjo = "blue diamond")
dog_food
```

::: {.cell-output .cell-output-stdout}

```
         teddy          khora         waffle          banjo 
      "purina"         "alpo"  "fancy feast" "blue diamond" 
```


:::

```{.r .cell-code}
class(dog_food)
```

::: {.cell-output .cell-output-stdout}

```
[1] "character"
```


:::

```{.r .cell-code}
typeof(dog_food)
```

::: {.cell-output .cell-output-stdout}

```
[1] "character"
```


:::
:::


### Accessing bits of vectors

Use `[]` with the position or name to access elements of a vector. 


::: {.cell}

```{.r .cell-code}
dog_food[2]
```

::: {.cell-output .cell-output-stdout}

```
 khora 
"alpo" 
```


:::

```{.r .cell-code}
dog_food["khora"]
```

::: {.cell-output .cell-output-stdout}

```
 khora 
"alpo" 
```


:::
:::


Or we can specify a range of values within a vector using `[:]`. The first element in **R vectors is assigned element = 1.** This is an important distinction. In Python, the first element is assigned 0 (zero-index). 


::: {.cell}

```{.r .cell-code}
# Create a vector of car colors observed
cars <- c("red", "orange", "white", "blue", "green", "silver", "black")

# Access just the 5th element
cars[5]
```

::: {.cell-output .cell-output-stdout}

```
[1] "green"
```


:::

```{.r .cell-code}
# Access elements 2 through 4
cars[2:4]
```

::: {.cell-output .cell-output-stdout}

```
[1] "orange" "white"  "blue"  
```


:::
:::


### A warm-up for for loops:

::: {.cell}

```{.r .cell-code}
i <- 4
cars[i]
```

::: {.cell-output .cell-output-stdout}

```
[1] "blue"
```


:::

```{.r .cell-code}
i <- seq(1:3)
cars[i]
```

::: {.cell-output .cell-output-stdout}

```
[1] "red"    "orange" "white" 
```


:::
:::


### And we can update elements of a vector directly (mutable):

::: {.cell}

```{.r .cell-code}
cars[3] <- "BURRITOS!"
cars
```

::: {.cell-output .cell-output-stdout}

```
[1] "red"       "orange"    "BURRITOS!" "blue"      "green"     "silver"   
[7] "black"    
```


:::
:::



## Matrices!

### Creating matrices 

(...we did some of this in EDS 212 too!)


::: {.cell}

```{.r .cell-code}
fish_size <- matrix(c(0.8, 1.2, 0.4, 0.9), ncol = 2, nrow = 2, byrow = FALSE)

fish_size
```

::: {.cell-output .cell-output-stdout}

```
     [,1] [,2]
[1,]  0.8  0.4
[2,]  1.2  0.9
```


:::

```{.r .cell-code}
typeof(fish_size) # Returns the class of values
```

::: {.cell-output .cell-output-stdout}

```
[1] "double"
```


:::

```{.r .cell-code}
class(fish_size) # Returns matrix / array
```

::: {.cell-output .cell-output-stdout}

```
[1] "matrix" "array" 
```


:::
:::


What happens if we try to combine multiple data types into a matrix?

::: {.cell}

```{.r .cell-code}
dog_walk <- matrix(c("teddy", 5, "khora", 10), ncol = 2, nrow = 2, byrow = FALSE)

dog_walk
```

::: {.cell-output .cell-output-stdout}

```
     [,1]    [,2]   
[1,] "teddy" "khora"
[2,] "5"     "10"   
```


:::

```{.r .cell-code}
class(dog_walk)
```

::: {.cell-output .cell-output-stdout}

```
[1] "matrix" "array" 
```


:::

```{.r .cell-code}
typeof(dog_walk)
```

::: {.cell-output .cell-output-stdout}

```
[1] "character"
```


:::

```{.r .cell-code}
# Hmmmmmm once again back to the broadest category of data type in the hierarchy
```
:::


### Accessing pieces of matrices

Index using `[row, column]`.


::: {.cell}

```{.r .cell-code}
whale_travel <- matrix(data = c(31.8, 1348, 46.9, 1587), nrow = 2, ncol = 2, byrow = TRUE)

# Take a look
whale_travel
```

::: {.cell-output .cell-output-stdout}

```
     [,1] [,2]
[1,] 31.8 1348
[2,] 46.9 1587
```


:::

```{.r .cell-code}
# Access the value 1348
whale_travel[1,2] # Row 1, column 2
```

::: {.cell-output .cell-output-stdout}

```
[1] 1348
```


:::

```{.r .cell-code}
# Access the value 46.9
whale_travel[2,1]
```

::: {.cell-output .cell-output-stdout}

```
[1] 46.9
```


:::
:::


If you leave any element blank (keeping the comma), it will return all values from the other element. For example, to get everything in row 2:

::: {.cell}

```{.r .cell-code}
whale_travel[2,]
```

::: {.cell-output .cell-output-stdout}

```
[1]   46.9 1587.0
```


:::
:::


Or, to access everything in column 1: 


::: {.cell}

```{.r .cell-code}
whale_travel[, 1]
```

::: {.cell-output .cell-output-stdout}

```
[1] 31.8 46.9
```


:::
:::


What happens if I only give a matrix one element? That's the position in the matrix *as if populated by column.* Check out a few:

::: {.cell}

```{.r .cell-code}
whale_travel[3]
```

::: {.cell-output .cell-output-stdout}

```
[1] 1348
```


:::
:::


## Lists


::: {.cell}

```{.r .cell-code}
urchins <- list("blue", c(1, 2, 3), c("a cat", "a dog"), 5L)

urchins
```

::: {.cell-output .cell-output-stdout}

```
[[1]]
[1] "blue"

[[2]]
[1] 1 2 3

[[3]]
[1] "a cat" "a dog"

[[4]]
[1] 5
```


:::
:::

### Accessing pieces of a list

Important: a single [] returns a list. [[]] returns the item STORED in the list. 

::: {.cell}

```{.r .cell-code}
urchins[[2]]
```

::: {.cell-output .cell-output-stdout}

```
[1] 1 2 3
```


:::

```{.r .cell-code}
# Compare that to: 
urchins[2]
```

::: {.cell-output .cell-output-stdout}

```
[[1]]
[1] 1 2 3
```


:::
:::


### Naming list items? Sure thing! 


::: {.cell}

```{.r .cell-code}
tacos <- list(topping = c("onion", "cilantro", "guacamole"), filling = c("beans", "meat", "veggie"), price = c(6.75, 8.25, 9.50))

# The whole thing
tacos
```

::: {.cell-output .cell-output-stdout}

```
$topping
[1] "onion"     "cilantro"  "guacamole"

$filling
[1] "beans"  "meat"   "veggie"

$price
[1] 6.75 8.25 9.50
```


:::

```{.r .cell-code}
# Just get one piece of it: 
tacos[[2]]
```

::: {.cell-output .cell-output-stdout}

```
[1] "beans"  "meat"   "veggie"
```


:::

```{.r .cell-code}
#...or, the same thing:
tacos$filling
```

::: {.cell-output .cell-output-stdout}

```
[1] "beans"  "meat"   "veggie"
```


:::
:::


## Data frames 

A data frame is a list containing vectors of the same length, where each column is a variable stored in a vector. Let's make one: 


::: {.cell}

```{.r .cell-code}
fruit <- data.frame(type = c("apple", "banana", "peach"), 
                    mass = c(130, 195, 150))

# Look at it
fruit
```

::: {.cell-output .cell-output-stdout}

```
    type mass
1  apple  130
2 banana  195
3  peach  150
```


:::

```{.r .cell-code}
# Check the class
class(fruit)
```

::: {.cell-output .cell-output-stdout}

```
[1] "data.frame"
```


:::
:::


### Access elements from a data frame

Use [row#, col#], or name the column (then element number).

::: {.cell}

```{.r .cell-code}
fruit[1,2]
```

::: {.cell-output .cell-output-stdout}

```
[1] 130
```


:::

```{.r .cell-code}
fruit[3,1]
```

::: {.cell-output .cell-output-stdout}

```
[1] "peach"
```


:::
:::

::: {.cell}

```{.r .cell-code}
fruit[2,1] <- "pineapple"
fruit
```

::: {.cell-output .cell-output-stdout}

```
       type mass
1     apple  130
2 pineapple  195
3     peach  150
```


:::
:::


# Part 3: Making & indexing data in Python

::: {.cell}

```{.r .cell-code}
py_install("numpy")
py_install("pandas")
```
:::

::: {.cell}

```{.python .cell-code}

import numpy as np
import pandas as pd
```
:::


## Vectors and matrices in Python


::: {.cell}

```{.python .cell-code}
teddy = [1,2,8]
teddy_vec = np.array(teddy)

teddy_vec
```

::: {.cell-output .cell-output-stdout}

```
array([1, 2, 8])
```


:::

```{.python .cell-code}
type(teddy_vec)
```

::: {.cell-output .cell-output-stdout}

```
<class 'numpy.ndarray'>
```


:::
:::


A **list** is mutable - you can change it directly! 

::: {.cell}

```{.python .cell-code}
teddy[1] = 1000

# See that element 1 is updated directly! 
teddy
```

::: {.cell-output .cell-output-stdout}

```
[1, 1000, 8]
```


:::
:::


A **tuple** is immutable - you'll get yelled at if you try to change it! 

::: {.cell}

```{.python .cell-code}
khora = (1, 5, 12)
type(khora)
```

::: {.cell-output .cell-output-stdout}

```
<class 'tuple'>
```


:::

```{.python .cell-code}

# khora[1] = 16 # Nope. 
```
:::


A more involved list (note: you can also use list() to create lists in python).

::: {.cell}

```{.python .cell-code}
waffle = [["cat", "dog", "penguin"], 2, "a burrito", [1,2,5]]

waffle
```

::: {.cell-output .cell-output-stdout}

```
[['cat', 'dog', 'penguin'], 2, 'a burrito', [1, 2, 5]]
```


:::

```{.python .cell-code}
# Access an element from the list waffle:
waffle[0] # Default just returns that piece (not as a list)
```

::: {.cell-output .cell-output-stdout}

```
['cat', 'dog', 'penguin']
```


:::
:::


We can reassign pieces of a list: 

::: {.cell}

```{.python .cell-code}
waffle[1] = "AN EXTRAVAGANZA"

waffle
```

::: {.cell-output .cell-output-stdout}

```
[['cat', 'dog', 'penguin'], 'AN EXTRAVAGANZA', 'a burrito', [1, 2, 5]]
```


:::
:::


## Make a pandas DataFrame in python

### First, a dictionary example:


::: {.cell}

```{.python .cell-code}
fox = {'sound': ["screech", "squeal", "bark"], 'age': [2, 6, 10]}

fox['sound']
```

::: {.cell-output .cell-output-stdout}

```
['screech', 'squeal', 'bark']
```


:::

```{.python .cell-code}
fox['age']
```

::: {.cell-output .cell-output-stdout}

```
[2, 6, 10]
```


:::
:::

::: {.cell}

```{.python .cell-code}
cows = {'name': ["moo", "spots", "happy"], 'location': ["pasture", "prairie", "barn"], 'height': [5.7, 5.4, 4.9]}

cows_df = pd.DataFrame(cows)

# Take a look
cows_df
```

::: {.cell-output .cell-output-stdout}

```
    name location  height
0    moo  pasture     5.7
1  spots  prairie     5.4
2  happy     barn     4.9
```


:::

```{.python .cell-code}
# Get a column
cows_df['name']
```

::: {.cell-output .cell-output-stdout}

```
0      moo
1    spots
2    happy
Name: name, dtype: object
```


:::

```{.python .cell-code}
# Get an element using df.at[]
cows_df.at[1, 'name']
```

::: {.cell-output .cell-output-stdout}

```
'spots'
```


:::
:::


### Side-by-side: R data frame & Pandas DataFrame


::: {.cell}

```{.r .cell-code}
home_sales <- data.frame(
  state = c("CA", "NV", "OR"),
  sales = c(38000, 4670, 2750)
)

home_sales
```

::: {.cell-output .cell-output-stdout}

```
  state sales
1    CA 38000
2    NV  4670
3    OR  2750
```


:::
:::

::: {.cell}

```{.python .cell-code}
home_sales = {'state': ["CA", "NV", "OR"], 'sales': [38000, 4670, 2750]}

home_sales = pd.DataFrame(home_sales)

home_sales
```

::: {.cell-output .cell-output-stdout}

```
  state  sales
0    CA  38000
1    NV   4670
2    OR   2750
```


:::
:::



## End (for now...)

