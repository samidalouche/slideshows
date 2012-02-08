!SLIDE incremental transition=fade
# Overview of Scala #

!SLIDE smbullets incremental transition=fade

# Background #

* Made in Switzerland
* Hybrid (Functional and OO)
* Expressive
* Statically Typed
* Concurrent
* Beautiful
* For the OPS/Managers/etc: it's Java 

!SLIDE incremental transition=fade
# Scala is Object-Oriented #
* Every value is an object
* Classes
* Traits: mixin-based composition
* Inheritance

!SLIDE incremental transition=fade
# Traits #

    @@@ Scala
    trait Similarity {
	  def isSimilar(x: Any): Boolean
	  def isNotSimilar(x: Any): Boolean = {
	    !isSimilar(x)
	  }
	}
	class Point(xc: Int, yc: Int) 
	   extends Similarity {
	...
	}

!SLIDE incremental transition=fade
# Scala is Functional #
* Every function is a value
* Higher-Order Functions
* Currying

!SLIDE incremental transition=fade
# Functions are first-class citizens #
    @@@ Scala
    def doneItems = {
    	todoItems filter itemDone
    }
    def itemDone(item: TodoItem) = item.done
    
!SLIDE incremental transition=fade

# Type inference #
    @@@ Scala
    val description = "this is a String"
    def concatenateDescription = {
    	description + description
    }
    val descriptions: List[String] = List()   
   
!SLIDE incremental transition=fade
# Immutability #
    @@@ Scala
    val list1 = List("item1", "item2")
    val list2 = "item3" :: list1


!SLIDE incremental transition=fade
# Pattern Matching #

    @@@ Scala
    def matchTest(x: Any): Any = x match {
	    case 1 => "one"
	    case "two" => 2
	    case y: Int => "scala.Int"
  	}
    

!SLIDE incremental transition=fade
# Pattern Matching (2) #

    @@@ Scala
    def matchTest(x: List[String]): String = x match {
	    case List("item1")
	    	 => "item1"
	    case List("item1", "item2") 
	    	=> "item1 and item2"
	    case List("item1", "item2", _) 
	    	=> "item1, item2, and more)
	    case _ 
	    	=> "We don't really know")
  	}
    
!SLIDE incremental transition=fade
# XML Literals #

    @@@ Scala
    def theDate(name: String) = 
	  <dateMsg addressedTo={ name }>
	    Hello, { name }! Today is 
	    { dateString }
	  </dateMsg>;
	  println(theDate("John Doe").toString())

!SLIDE bullets incremental transition=fade
# Actors #
* A revolutionary way to write concurrent applications

!SLIDE bullets incremental transition=fade
# Scala is extensible #
* Really small grammar
* No operator overloading
* infix / postfix operator

!SLIDE smbullets incremental transition=fade
# Tons of other features #
* existential types
* abstract types
* Compound types
* implicits
* views
* higher-order types
* package objects
* variance annotations (Generics)
* lazy evaluation
* parser combinators


!SLIDE incremental transition=fade
# Thank You ! #

Any Question ?
