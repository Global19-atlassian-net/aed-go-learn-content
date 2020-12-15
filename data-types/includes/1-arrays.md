# Arrays

Arrays in Go are a fixed-length data structure of a particular type. They can have zero or more elements, you have to define the size when you declare or initialize them, and **you can't resize them once created**. Therefore, arrays are not commonly used in Go programs, but they're the foundation for slices and maps.

## Declare arrays

To declare an array in Go, you have to define the data type of its elements and the number of elements the array can hold. You can then access each element in the array with the subscript notation where zero it's the first element, and the last element is one less than the array length (length - 1).

For instance, let's use the following code:

```go
package main

import "fmt"

func main() {
    var a [3]int
    a[1] = 10
    fmt.Println(a[0])
    fmt.Println(a[1])
    fmt.Println(a[len(a)-1])
}
```

When you run the above code, you get the following output:

```output
0
10
0
```

Notice that even though you simply declared an array, you don't get an error when accessing its elements. By default, Go initializes each element with the default data type. In this case, the default value for `int` is zero. But you can assign a value to a specific position, that's why you see `a[1] = 10`, and you can access that element using the same notation. Also, notice that to print out the first element, we used `a[0]`, and for the last one, we used `a[len(a)-1]`. `len` is a built-in function in Go to get the number of elements in an array, slice, or map.

## Initialize arrays

You can also initialize an array with other values than the default ones when you're declaring an array. For instance, you can use the following code to see and test the syntax:

```go
package main

import "fmt"

func main() {
    cities := [5]string{"New York", "Paris", "Berlin", "Madrid"}
    fmt.Println("Cities:", cities)
}
```

Run the above code, you should see this:

```output
Cities: [New York Paris Berlin Madrid ]
```

Notice that even though the array should have five elements, we don't need to assign a value to all elements. As we've seen before, the latest position has an empty string because it's the default value for a string data type.

## Ellipsis in Arrays

Another way of declaring and initializing an array when you don't know how many positions you'll need, but you know how many data you'll have, you can use an ellipsis (`...`), like this:

```go
q := [...]int{1, 2, 3}
```

Let's modify the program we used in the previous section to use an ellipsis; the code should look like this:

```go
package main

import "fmt"

func main() {
    cities := [...]string{"New York", "Paris", "Berlin", "Madrid"}
    fmt.Println("Cities:", cities)
}
```

Run the above code, you should see a similar output, like this:

```output
Cities: [New York Paris Berlin Madrid]
```

Can you see the difference? There's no empty string at the end. The array length was determined by the strings you put when initializing it, and you're not reserving memory you don't know if you'll end up needing.

Another interesting way of initializing an array is to use ellipsis and only specify a value for the latest position. For instance, use the following code:

```go
package main

import "fmt"

func main() {
    numbers := [...]int{99: -1}
    fmt.Println("First Position:", numbers[0])
    fmt.Println("Last Position:", numbers[99])
    fmt.Println("Length:", len(numbers))
}
```

Run this code, and you'll get the output:

```output
First Position: 0
Last Position: -1
Length: 100
```

Notice how the array length is 100 because you specified a value for the 99th position, and the first position prints out the default value (zero).

## Multi-dimensional arrays

Go has support for multi-dimensional arrays when you need to work with complex data structures. Let's create a program where you declare and initialize a two-dimensional array. Use the following code:

```go
package main

import "fmt"

func main() {
    var twoD [3][5]int
    for i := 0; i < 3; i++ {
        for j := 0; j < 5; j++ {
            twoD[i][j] = (i + 1) * (j + 1)
        }
        fmt.Println("Row", i, twoD[i])
    }
    fmt.Println("\nAll at once:", twoD)
}
```

Run the above program, you should see an output like this:

```output
Row 0 [1 2 3 4 5]
Row 1 [2 4 6 8 10]
Row 2 [3 6 9 12 15]

All at once: [[1 2 3 4 5] [2 4 6 8 10] [3 6 9 12 15]]
```

You've declared a two-dimensional array specifying how many positions the array would have in the second dimension, like this `var twoD [3][5]int`. You could think about this array as one data structure with columns and rows, like a spreadsheet or a matrix. At this point, all positions have a default value of zero. In the `for` loop, we're initializing every position with a different value pattern at every row. Finally, you print out all its values to the terminal.

What if you want to declare a three-dimensional array? Well, you might guess what the syntax would be, right? You can do it like this:

```go
package main

import "fmt"

func main() {
    var threeD [3][5][2]int
    for i := 0; i < 3; i++ {
        for j := 0; j < 5; j++ {
            for k := 0; k < 2; k++ {
                threeD[i][j][k] = (i + 1) * (j + 1) * (k + 1)
            }
        }
    }
    fmt.Println("\nAll at once:", threeD)
}
```

Run the above code, you should see an output like this:

```output
All at once: [[[1 2] [2 4] [3 6] [4 8] [5 10]] [[2 4] [4 8] [6 12] [8 16] [10 20]] [[3 6] [6 12] [9 18] [12 24] [15 30]]]
```

If we format the output in a more readable format, you could have something like this:

```output
All at once: 
[
    [
        [1 2] [2 4] [3 6] [4 8] [5 10]
    ] 
    [
        [2 4] [4 8] [6 12] [8 16] [10 20]
    ] 
    [
        [3 6] [6 12] [9 18] [12 24] [15 30]
    ]
]
```

Notice how the structure changes from a two-dimensional array. You can continue having more dimensions as you need, but we'll leave it here for now as we have other data types to explore.
