Moebius Solutions Application Answer
========================
> VERSION: 2018-01-02

QUESTION 1. Why does this code not work? How do you fix it?
----------------

```
public class Example {
	public List<Integer> removeBigNumbers(List<Integer> data) {
		for (Integer i : data) {
			if (i > 10) {
				data.remove(i);
			}
		}
		return data;
	}
}
```
_Response:_** The above code tries to remove object(s) from a List while looping through the same List. As a result, the code throws ConcurrentModificationException. To fix it, an iterator is needed to safely remove the object(s). Fixed code below.
```
public class Example {
	public List<Integer> removeBigNumbers(List<Integer> data) {
		Iterator<Integer> dataList = data.iterator();
		while(dataList.hasNext()) {
			if(dataList.next() > 10) {
				dataList.remove();				
			}
		}
		return data;
	}
}
```

QUESTION 2: Programming Task
----------------
Write a class that implements the following interface, assuming that all methods are used with approximately the same frequency.

```
interface ItemStore {

	Interface Item {
		String getID();
		String getTag();
	}

	/**
	 * Adds an {@link Item} to the store, replacing any existing item with the
	 * same {@link Item#id} value.
	 */
	public void put(Item item);

	/**
	 * Retrieves the {@link Item} with the given {@link Item#id} value, or
	 * null if no such {@link Item} exists in the store.
	 */
	public Item get(String id);

	/**
	 * Delete all {@link Item}s with the specified tag.
	 */
	public void dropAllByTag(String tag);
	
	/**
	 * Returns the number of Items in the store
	 */
	 public int size();
}
```
```
//TODO
```

QUESTION 3: Memory Management
----------------
_Response_**: Below is the fixed class. 
```
public class SmallMemoryMessageTest {

    public static void main(String []args) {
        MessageProcessor processor = Util.createMessageProcessor();
        MessageArchiver archiver = Util.createMessageArchiver();
        List<Message> messages = new ArrayList<>();
        for (int i = 0; i < Util.EXPECTED_TOTAL; i++) {
            Message msg = Util.random();
            processor.processMessage(msg);
            messages.add(msg);
        }
        archiver.archiveMessages(messages, m -> m.getSubject().startsWith("A"));

        /*
         *  DO NOT CHANGE ANYTHING BELOW THIS LINE.
         *  PROGRAM MUST EXIT SUCCESSFULLY
         */
        Util.validate();
    }
}
```

QUESTION 4: Debugging
----------------

```
package com.moesol.hr.bugs;

public class Bug1 {
	private Integer rating;

	public int rating() {
		return rating;
	}

	public static void main(String[] args) {
		System.out.println("rating:"
			+ new Bug1().rating());
	}
}
```

The program above throws a `NullPointerException` with this stack trace:

```
Exception in thread "main" java.lang.NullPointerException
	at com.moesol.hr.bugs.Bug1.rating(Bug1.java:7)
	at com.moesol.hr.bugs.Bug1.main(Bug1.java:12)
```

What is happening? How can it be fixed?

_Response_**: The rating variable for `new Bug1()` is instantiated but never initialized, so the rating never points to anything and as a result the program throws a `NullPointerException`. To fix it, a constructor can be used to initialize the rating variable to a default value whenever an instance of Bug1 is created. Fixed code below.

```
package com.moesol.hr.bugs;

public class Bug1 {
	private Integer rating;

	public Bug1(){
		rating = 10; //autoboxing
	}

	public int rating() {
		return rating;
	}

	public static void main(String[] args) {
		System.out.println("rating:"
			+ new Bug1().rating());
	}
}
```

QUESTION 5: Wrong Result
----------------

The following program produces inconsistent results. It should always output
this:

```
counter is 20000
```

Please correct the program.
```
public class WrongAnswer {

	private int counter = 0;

	public static void main(String[] args) {
		new WrongAnswer().run();
	}

	private void run() {
		try {
			Thread t1 = new Thread(this::incrementToOnHundred);
			Thread t2 = new Thread(this::incrementToOnHundred);
			t1.start();
			t2.start();
			t1.join();
			t2.join();
			System.out.println("counter is " + counter);
		} catch (InterruptedException e) {
			System.err.println("fatal error, unexpected interrupt exception");
			System.exit(2);
		}
	}

	private void incrementToOnHundred() {
		for (int i = 0; i < 10_000; i++) {
			doSomeFakeWork();
		}
	}

	private void doSomeFakeWork() {
		counter++;
	}
}
```
_Response_**: The program produces inconsistent results because the Thread t2 starts before the Thread t1 is died. To fix it, make Thread t1 die before starting Thread t2. Fixed code below.
```
public class WrongAnswer {

	private int counter = 0;

	public static void main(String[] args) {
		new WrongAnswer().run();
	}

	private void run() {
		try {
			Thread t1 = new Thread(this::incrementToOnHundred);
			Thread t2 = new Thread(this::incrementToOnHundred);
			t1.start();
			t1.join(); 	//FIXED HERE
			t2.start();	//FIXED HERE
			t2.join();
			System.out.println("counter is " + counter);
		} catch (InterruptedException e) {
			System.err.println("fatal error, unexpected interrupt exception");
			System.exit(2);
		}
	}

	private void incrementToOnHundred() {
		for (int i = 0; i < 10_000; i++) {
			doSomeFakeWork();
		}
	}

	private void doSomeFakeWork() {
		counter++;
	}
}
```

BONUS: Programming Puzzle Bonus!
----------------









