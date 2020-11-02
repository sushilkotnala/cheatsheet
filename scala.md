
# Scala cheat sheet

## Evaluation rules
* Call by value - evaluates the function args before calling the function.
* Call by name - evaluates the function first and then args if its required.

```scala
val a = 1; // evaluated immediately
def a = 1; // evaluated when called
lazy val a = 1; // evaluate when needed only once.

def eval(s: String) // call by value
def eval(s: =>String ) // call by name
def func(s: Int*){ } // binding is sequence of ints, with varing number of ints.
```

## Higher order functions
These are functions which take function as input arg or return function as return type.

```scala
//Higher order function, it accepts function as arg
//cal() expects a, b as integers and also function f which takes two ints and returns int
def cal(a: Int, b: Int, f: (Int, Int) => Int ): Int  = {
  f(a,b)
}
// function is passed while invoking the higher order function
cal(4, 5, (a,b)=> (a *b)) 

//below function return a function
def sum(a: Int, b: Int): (Int, Int)=> Int = {
  def sumf(a: Int, b: Int): Int = a + b
  sumf
}

def multiple(a: Int, b: Int): (Int, Int)=> Int = {
  def mulitplef(a: Int, b: Int): Int = a * b
  mulitplef
}

def cube(a: Int): Int => Int = {
  def cubef(a: Int): Int = a*a*a
  cubef	
}
```
