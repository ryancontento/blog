---
title: "Multidimensional Arrays in C#"
date: 2022-07-09T14:05:58-04:00
draft: false
categories: [C#, Development]
tags: [.NET, C#, Arrays]
---

## What Are Multidimensional Arrays?

A multidimensional array is an array of arrays. This means it will have multiple levels. This is also commonly called a matrix or table. In this article, we will be going over how to implement a simple 2D array in C# and some other options for taking this technique a bit further!

## 2D Arrays

Here are 3 standard arrays of strings:

```csharp

string[] fruit = {"apple", "banana", "peach"}
string[] vegetable = {"peas", "kale", "carrot"}
string[] meat = {"chicken", "beef", "lamb"}

```

Now, what if we wanted to combine these foods into one large array? Using 2D arrays, we can combine the 3 standard arrays into one array of string, lets call it refrigerator:

```csharp

string[,] refrigerator = { {"apple", "banana", "peach"},
							{"peas", "kale", "carrot"},
							{"chicken", "beef", "lamb"}
						};

```

It is already becoming clear how this can be useful for tables.

To access one of the elements, just provide the index for the row and column. Our fruit array is now row index 0, our vegetable array is now index 1, and our meat array is now index 2. Inside of each of these, the items follow the same pattern, 0-2.

Let’s say we want to access the carrots from out refrigerator. We will need to do the following:

```csharp

refrigerator[1,2];

```

We can use this to change what is in our refrigerator. Maybe we want to replace our kale with some spinach:

```csharp

refrigerator[1,1] = "spinach"

```

If we want to check what is now in our refrigerator, we can just loop over it:

```csharp

foreach(string food in refrigerator)
{
	Console.WriteLine(food);
}

```

To demonstrate how useful this can be for tables, we will print this to the console with the correct rows and columns. We can do this by nesting two for loops:

```csharp

// First loop is for the first dimension array
for (int i = 0; i < refrigerator.GetLength(0); i++)
{
	// Second loop for second dimension
	for (int j = 0; j < refrigerator.GetLength(1); j++)
	{
		// Note, we will use Console.Write inside the loop to keep the same line,
		// and we add an empty string to separate them.
		Console.Write(refrigerator[i,j] + " ");
	}
	// We then print an empty new line to break for the new row
	Console.WriteLine();
}

```

## 3D Arrays

As you might have guessed, we can take this further than one array of arrays. What about a 3D array? Well, let’s take a look at an example of an array which will consist of an array, and inside of each of those, will be another set of arrays. To keep this one a bit clearer we will just be using arrays of integers:

```csharp

int[,,] threeDArray = { { {1, 2, 3}, {4, 5, 6}, {7, 8, 9} },
						{ {1, 2, 3}, {4, 5, 6}, {7, 8, 9} },
						{ {1, 2, 3}, {4, 5, 6}, {7, 8, 9} }
					  };

```

To access one of the ints, we will be using the same technique as above, but with an additional index for the new array. If we want to change the middle rows middle array of “4, 5, 6” to “4, 5, 5”, we will simply do:

```csharp

threeDArray[1,1,2] = 5;

```

In the future I may make another post expanding on these topics to populate an HTML table. If you have any questions, comments, or requests for covering specifics, please feel free to reach out [here](<[https://ryancontento.dev/#contact](https://ryancontento.dev/#contact)>).
