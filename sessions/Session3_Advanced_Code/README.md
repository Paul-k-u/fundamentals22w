# Session 3 | 24.10.2022 - Advanced Code

***Disclaimer:*** *This page offers supporting material for an Interaction Design course held at [KISD](https://kisd.de) in the winter term 2022/23. Visit the [landing page](https://github.com/KISDinteractive/fundamentals22w) of this course for more information.*

**Links for the Session**

- [We started this session with the code of the previous one](src/Code1_grid/Code1_grid.pde)

## 2.5 Closing of Previous Loops-Session

We didn't close the previous session about loops, so here you go:

### for-loop vs. while loop

We've learned how to use the for-loop. There is a second type of loop, the **while-loop**, that doesbasically the same thing. Here are some differences and the implementation:

![while-loop](img/while-loop.jpg)



### Nested Loops

Lastly, we looked at the concept of nested loops. How could we generate something like this (called a "matrix" of circles)?

**Target:**

<img src="img/nested_loop_task.jpg" width="50%" alt="a matrix of 12 by 12 circles">



Using two regular for-loops would only result in a vertical and horizontal array of circles:

<img src="img/two_for_loops.jpg" width="100%" alt="using two loops results in a vertical and a horizontal line of circle, but no matrix">



Let's imagine the *matrix* consists of 3 x 3 elements. We could split it up in:

<img src="img/matrix.png" width="100%" alt="a 3 by 3 matrix showing how to access the circles using their column and row">

We can achieve that by creating **a for-loop for iterating through the columns that is nested inside a for-loop iterating through the rows:**

![nested_loop_code](img/nested_loop_code.jpg)



So the final code for nested loops goes like this ([link to code file](src/Code2_NestedLoops/Code2_NestedLoops.pde)):

```processing
int interval= 60; //how much space (in pixels) between lines?
int amount= 20;   //how many lines?

void setup() {
  size(800, 800);
  background(255);
}

void draw() {  
  //iterate through rows
  for (int row = 0; row<amount; row++) {
    //iterate through columns
    for (int column = 0; column<amount; column++) {
      circle(column*interval, row*interval, 50);
    }
  }
}
```



## 3.1 Arrays

Arrays are in general arrangements / sequences of things

You can think of them as a freight train of shipping containers, as we used to think of them when we learned that variables are a container that holds data of a certain type. Arrays and our metaphoric trian have much in common:

- The **train** has **many wagons**** of the **same type** (e.g. shipping container) in a **fixed order.**

- An **array** has **many elements** of the **same type** (e.g. int variables) in a **fixed order.**



Before we had to name each variable with a unique name. In an array we can access/manipulate them by using the **array name** and their **position (called "index")** in the array:

![array_train_metaphor](img/array_train_metaphor.jpg)



### "Create" Arrays

We can "create" (declare & initalize to be precise) arrays by doing:

```processing
int[] posY = {0,100,200,300,400};
```

<img src="img/create_array.jpg" width="80%" alt="screenshot of array syntax described above">

There are other ways of "creating" arrays, that you can look up in the syntax!

### "Use" Arrays

We can "use" (call & assign to be precise) arrays in a similar way than variables. Call the 4th element of an array for instance (array always start to count at 0, so the 4th element is index number 3):

```processing
if (posY[3]>whatever){ ...
```

The same way we can (re-)assign values:

```processing
posY[3] = 100;
```

<img src="img/use_array.jpg" width="80%" alt="screenshot of array syntax described above">



### Multidimensional Arrays

With the train metaphor we learned a so-called one dimensional array, as it stores only a single row of elements.

There can also be 

- two dimensional arrays (imagine a train with two floors of containers
- three dimensional arrays (Imagine a container ship that stores containers not only one behind the other and on top of each other, but also side by side)
- arrays with more than three dimensions (difficult to imagine, used in higher level concepts and in math)

An examplary assignment using a 2D array would look like this: 

```processing
posY[1][3] = 100;
```

Check out the Processing documentation for more information!



### Falling Blobs

In the course, we wrote a sketch that creates 5 blobs that fall "down" the screen at different speeds and with different starting positions. Here is the final code ([link to code file](src/Code4_FallingBlobs/Code4_FallingBlobs.pde)):

```processing
int[] posY = {0, 100, 200, 300, 400}; //starting position of 5 blobs
int[] speeds = {1, 2, 3, 4, 5};       //speed of 5 blobs

void setup() {
  size(800, 800);
}

void draw() {
  //styling stuff
  background(255);
  fill(0);

  for (int i = 0; i < 5; i = i+1) {
    //increment position of current (i) blob by adding "speeds"
    posY[i] = posY[i] + speeds[i];

    //draw current (i) circle with corresponding posY
    circle (i*150, posY[i], 50);
    
    //set back at the end of the screen
    if (posY[i] > height) {
      posY[i]=0;
    }
  }
}
```



## 3.2 Binary Numbers
### Understanding the Numeral Systems
The Decimal System, used by most modern civilizations to represent numbers and do math with them, is just one of an infinite amount of numeral systems, which all follow the same internal logic, and most naturally can be explained through the Decimal System:
- Numeral Systems have a **base, which represents the number of tokens (or states) a digit is able to hold. _In Decimal there are **ten** tokens: 0, 1, 2, ,3 ,4 ,5, 6, 7, 8, 9_
- Counting up works by iterating through the tokens _( 0 -> 1 -> 2 -> 3 ... )_ until the last token is reached _(9)_
- In order to count higher than the token with the highest value, two things have to happen:
  - the current digit is reset to Zero
  - at the same time, either a new digit is introduced to the left - or an already existing digit on the left is incremented by one
- Following this logic, every new digit introduced extends the possible values represented by the factor of the base ( = amount of tokens). _In Decimal this means, every new digit **tenfolds** the possible values represented by the numeral system_
- As a consequence, counting from the right, the value of every is multiplied with incremental exponents of the base, starting with one. _In Decimal this means, the value of the digit _on the _farthest_ right is_ multiplied by 1, the digit left of that is multiplied by 10, the digit to the left of that is multiplied by 100 etc._

So for exampple, the number '123' or 'onehundred-and-twenty-three' in the decimal system is represented as 1 * 100 + 2 * 10 + 3 * 1

<img src="img/decimal.png" width="90%">


### The Binary System
The Binary System is a numeral system with a base of **two**. Thus every digit is only able two represent one of two states: **0** or **1**. The Binary system follows exactly the same inner logic, as all other numeral systems, and was very important for the development of machine-based calculation and computing. Since every new digit only **doubles** the possible values represented, a number represented in the binary systems takes more digits than the same number represented in decimal. Counting up from 0 to 9 in the Binary System produces the following numbers:

0 -> 0

1 -> 1

2 -> 10

3 -> 11

4 -> 100

5 -> 101

6 -> 110

7 -> 111

8 -> 1000

9 -> 1001


A digit in binary is referred to as a **Bit** and is the smallest chunk of information in Computer Science, it can only hold a **0** or **1**, respectively **on** or **off**. 
Very commonly Bits are organized as groups of 8, which are also called **Byte**. Holding 8 Bits, a Byte by itself is able to hold values between 0 and 255. Thus, the Example from before '123' can be represented as **01111011**

<img src="img/binary123.png" width="80%" >

There were reasons, why early and present computation is utilizing binary numbers under the hood. 
- It is possible to perform normal mathematical operations in binary because the inner logic of numeral systems persists. This means math still works as normal.

- There is a field of mathematics called _Boolean Algebra_, which is specialized to formalize logical statements as binary **true** or **false** expressions. It is relatively easy to represent and to read out only two states, much easier than to differentiate 10 nuances of a state for a direct projection of the decimal system. This 'robustness' made it possible to represent and read out binary information through many technologies like punchcards, relays, vacuum tubes and transistors - it is just necessary to differentiate between 2 states, 1/0, on/off, present/missing, high/low.  

## 3.3 Binary Data & Machines (and Punchcards)
Some noticeable milestones in the history of binary machines were:

The Jacquard Loom:
- Joseph Marie Jacquard
- Patented in 1801
- Looms utilized punchcards to automate the creation of patterned weaves in textiles
- The patterns were translated into patterns of holes on cardboard cards -> punchcards
- The punchcards were used in a mechanical lever mechanism 
- Depending on the presence or absence of a hole at the contact point between levers and punchcard, the levers pulled only the right strings for a specific pattern
- Thus punchcards held binary information, represented as the presence or absence of holes
- The punchcards of the Jacquard Loom are often referred to as the first implementation of _software_, because in contrast to the loom itself, they were relatively easy to manipulate. In consequence, the same loom was able to weave multiple patterns just by changing the punchcards.

The Hollerith Tabulating Machine​
- Hermann Hollerith
- Patented in 1889
- Tabulating machines were used to read out information coded onto punchcards
- The readout utilized electricity and two hinged plates controlled by a lever
- When the lever was actuated and the punchcard was between the plates, spring-loaded needles were passing through the holes and closed an electric circuit.
- If there were no holes at the contact points, the electric circuit wouldn't close
- The contacts which were activated by a needle, drove forward the counting hands of a multitude of dials that could be evaluated by humans
- Again the presence or absence of holes in the punchcard held binary data controlling the machine

Early Tabulating Machines weren't computers though, they were only able to read and write information from and to punchcards. Over the decades the ability for simple calculations was added, until tabulating and calculation machines became programmable general purpose computers.

Punchcards remained a primary medium for input and output until the 80s. The biggest computer program every deployed on punchcards was running SAGE, the first real-time and network-based air-defense-system. It was written on 62500 punchcards worth of ~ 5MB of data.

## 3.5 Functions

<img src=img/photoshop.png width=80% >

Software sometimes consists of millions lines of code​ and is written and maintained by many people. Thus it has to be organized. This is why software usually is divided into modules, which communicate with each other through defined interfaces. These modules should be ideally as self-contained as possible, indepented and their interfaces should be of course compatible.  

​For now, the primary technqiue for organizing code will be **functions**, which (when done right) make code more organized, modular and reusable.

Functions are a layer of abstraction. As variables are an abstraction for values, functions are an abstrctions for behavior. As with built-in variables, in Processing there are a lot of built-in functions, which already were used during the course, like:

```processing
void setup() {...}
void draw() {...}
circle(posX,posY,50);
rect(mouseX,mouseY,100,100);
```
Analog to variables, in order to utilize own functions, they have to be defined first:

<img src=img/ownfunctions.png width=80% >

​
Regarding the code for one falling blob, one way to utilize functions would be to "outsource" the following two lines: 

```processing
background(255);
fill(0);
```

<img src=img/ownfunction2.png width=80% >


<img src=img/ownfunction3.png width=80% >

It is also possible to define parameters for own functions, in order to interact and manipulate the values  inside the function when the function is called.

<img src=img/ownfunction4.png width=80% >

### Task: Recreate the rect() function of processing with an own function, which draws a rectangle with 4 lines.


**Example Solution**: [Code File](https://github.com/KISDinteractive/fundamentals22w/tree/main/sessions/Session3_Advanced_Code/src/Code5_myRect)

**Special:** you could also solve the Task by using point() only. The result would look [like this (code file)](src/Code_5_myRect_alternativeVersionUsingPoints/Code_5_myRect_alternativeVersionUsingPoints.pde).

