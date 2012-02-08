!SLIDE transition=fade
# Let's dive into Scala #

!SLIDE command
# TodoList #

!SLIDE incremental smaller transition=fade

    @@@ Scala
	package org.scalamontreal.todo
	import java.util.Date
	
	final case class TodoList(
	    val todoItems: List[TodoItem]) {
	    require(todoItems != null)
	    
	    def addItem(item: TodoItem) = {
	      copy(todoItems=item :: todoItems) 
	    }
	    
	    def doneItems = todoItems filter (_.done)
	    
	    def urgentItems = todoItems filter (
	        (item:TodoItem) => 
	            !item.done 
	            && item.dueDate.map (new Date().after(_))
	                .getOrElse(false)
	    )
	}

!SLIDE command
# TodoItem #

!SLIDE incremental smaller transition=fade
    @@@ Scala
    package org.scalamontreal.todo
	import java.util.Date
	
	final case class TodoItem(
	    val title: String, 
	    val description: Option[String], 
	    val dueDate: Option[Date], 
	    val done: Boolean = false) {
	  // paranoid preconditions
	  require(title != null)
	  require(description != null)
	  require(dueDate != null)
	
	  def markAsDone() = copy(done=true)
	}