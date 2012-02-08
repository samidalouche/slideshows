!SLIDE transition=fade
# Crappy Java Code #

!SLIDE command
# TodoList #

!SLIDE incremental smaller transition=fade

    @@@ Java
	package org.scalamontreal.todo;
	
	import java.util.List;
	
	public class TodoList {
	    private List<TodoItem> todoItems;
	
	    public TodoList() {
	        super();
	    }
	
	    public List<TodoItem> getTodoItems() {
	        return todoItems;
	    }
	
	    public void setTodoItems(List<TodoItem> todoItems) {
	        this.todoItems = todoItems;
	    }
	
	}

!SLIDE incremental smaller transition=fade
    @@@ Java
    public List<TodoItem> getDoneItems() {
        List<TodoItem> result = new ArrayList<TodoItem>();
        for(TodoItem item: todoItems) {
            if(item.isDone()) {
                result.add(item);
            }
        }
        return result;
    }
    
    public List<TodoItem> getUrgentItems() {
        List<TodoItem> result = new ArrayList<TodoItem>();
        for(TodoItem item: todoItems) {
            if(!item.isDone() && 
               new Date().after(item.getDueDate())) {
                result.add(item); 
            }
        }
        return result;
    }
    
!SLIDE command
# TodoItem #

!SLIDE incremental smaller transition=fade

    @@@ Java
	package org.scalamontreal.todo;
	
	import java.util.Date;
	
	public class TodoItem {
	    private String title;
	    private String description;
	    private Date dueDate;
	    private boolean done;
	
	    public TodoItem() {
	        super();
	    }
	
	    public String getTitle() {
	        return title;
	    }
	
	    public void setTitle(String title) {
	        this.title = title;
	    }
	
	    public String getDescription() {
	        return description;
	    }
	
!SLIDE incremental smaller transition=fade

    @@@ Java	
	
	    public void setDescription(String description) {
	        this.description = description;
	    }
	
	    public Date getDueDate() {
	        return dueDate;
	    }
	
	    public void setDueDate(Date dueDate) {
	        this.dueDate = dueDate;
	    }
	
	    public boolean isDone() {
	        return done;
	    }
	
	    public void setDone(boolean done) {
	        this.done = done;
	    }
	    
	    
	
	}



!SLIDE smbullets incremental transition=fade
# What's the problem ? #

* Verbosity
* Getters/Setters insanity
* Mutability
* Intent is lost
* Collection Manipulation
* What is nullable ?
* ... And we have not started coding !!

!SLIDE bullets incremental transition=fade
# Let's refactor... #

!SLIDE command
# TodoList #

!SLIDE incremental smaller transition=fade
    @@@ Java
	package org.scalamontreal.todo;

	import java.util.Date;
	import java.util.List;
	
	import com.google.common.base.Preconditions;
	import com.google.common.base.Predicate;
	import com.google.common.base.Predicates;
	import com.google.common.collect.ImmutableList;
	import com.google.common.collect.Iterables;

!SLIDE incremental smaller transition=fade
    @@@ Java	
	public final class TodoList {
	    private final ImmutableList<TodoItem> todoItems;
	
	    public TodoList() {
	        this(ImmutableList.<TodoItem>of());
	    }
	    public TodoList(Iterable<TodoItem> todoItems) {
	        Preconditions.checkNotNull(todoItems);
	        this.todoItems = ImmutableList.copyOf(todoItems);
	    }

!SLIDE incremental smaller transition=fade
    @@@ Java	
	    public ImmutableList<TodoItem> getTodoItems() {
	        return todoItems;
	    }
	
	    public TodoList addTodoItem(TodoItem todoItem) {
	        ImmutableList<TodoItem> newItems = 
	                ImmutableList.copyOf(
	                        Iterables.concat(
	                                todoItems, 
	                                ImmutableList.of(todoItem)));
	        return new TodoList(newItems);
	    }
	    
	    public TodoList withTodoItems(Iterable<TodoItem> todoItems) {
	        return new TodoList(todoItems);
	    }

!SLIDE incremental smaller transition=fade
    @@@ Java	    
	    public ImmutableList<TodoItem> getDoneItems() {
	        return ImmutableList.copyOf(
	                Iterables.filter(
	                        todoItems, 
	                        new IsDonePredicate()));
	    }

!SLIDE incremental smaller transition=fade
    @@@ Java	    
	    public List<TodoItem> getUrgentItems() {
	        Iterable<TodoItem> filtered =
	                Iterables.filter(
	                    todoItems, 
	                    Predicates.and(
	                        Predicates.not(new IsDonePredicate()), 
	                        new PastDueDate()));
	        return ImmutableList.copyOf(filtered);
	    }

!SLIDE incremental smaller transition=fade
    @@@ Java	
	    private final class PastDueDate 
	       implements Predicate<TodoItem> {
	        @Override
	        public boolean apply(TodoItem todoItem) {
	            return new Date().after(todoItem.getDueDate());
	        }
	    }
	
	    private static class IsDonePredicate 
	       implements Predicate<TodoItem> {
	        @Override public boolean apply(TodoItem todoItem) {
	            return todoItem.isDone();
	        }
	        
	    }
	}

!SLIDE command
# TodoItem #

!SLIDE incremental smaller transition=fade
    @@@ Java
    package org.scalamontreal.todo;

	import java.util.Date;
	
	import com.google.common.base.Preconditions;
	import com.google.common.base.Strings;
		
!SLIDE incremental smaller transition=fade	    
    @@@ Java	
	public final class TodoItem {
	    private String title;
	    private String description;
	    private Date dueDate;
	    private boolean done;
	    
	    public TodoItem(String title, 
	    	String description, 
	    	Date dueDate) {
	        this(title, 
	        	description, 
	        	dueDate, 
	        	false);
	    }
	    
	    public TodoItem(String title, 
	    	String description, 
	    	Date dueDate, 
	    	boolean done) {
	        Preconditions.checkArgument(!Strings.isNullOrEmpty(title));
	        this.title = title;
	        this.description = description;
	        this.dueDate = dueDate;
	        this.done = done;
	    }
	    
!SLIDE incremental smaller transition=fade
    @@@ Java	
	    public String getTitle() {
	        return title;
	    }
	
	    public String getDescription() {
	        return description;
	    }
	
	    public Date getDueDate() {
	        return dueDate;
	    }
	
	    public boolean isDone() {
	        return done;
	    }

!SLIDE incremental smaller transition=fade
    @@@ Java	    
	    public TodoItem markAsDone() {
	        return new TodoItem(
	        	title, 
	        	description, 
	        	dueDate, 
	        	true);
	    }
	
	}

!SLIDE incremental smaller transition=fade    
# What's the problem ? #

* Verbosity
* Feels weird
* It's the price to pay to follow best practices in Java !   