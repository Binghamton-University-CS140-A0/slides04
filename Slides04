Code from Slides3
```java
package notes;
import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.GridLayout;
import java.awt.Rectangle;

import javax.swing.BorderFactory;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.TitledBorder;
/**
 * The class FirstGUI draws two rectangles to demonstrate that the
 * translate method uses the implicit parameter to move one rectangle
 * when it is called without affecting the position of the other 
 * rectangle. Two buttons with lambda-expression listeners are used
 * to control the movement of the rectangle.
 * @author CS140
 *
 */
public class FirstGUI {

    public static void main(String[] args) 
    {
        var frame = new JFrame();

        frame.setSize(600, 400);
        frame.setTitle("Translate Rectangle");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        var rect1 = new Rectangle(190,50,100,150);
        var rect2 = new Rectangle(190,140,200,50);

        /**
         * Inner class object component is an anonymous subclass of
         * JComponent. It overrides paintComponent by drawing
         * two rectangles filled with different colors.  
         */
        JComponent component = new JComponent() 
        {
            private static final long serialVersionUID = -3483603444237111028L;
            @Override
            protected void paintComponent(Graphics g) 
            {
                super.paintComponent(g);
                Graphics2D g2 = (Graphics2D)g;
                g2.setColor(Color.RED);
                g2.fill(rect1);
                g2.setColor(Color.BLACK);
                g2.fill(rect2);
            }
        };
        
        frame.add(component);
        
        var panel = new JPanel();
        var border = BorderFactory.createTitledBorder(
                BorderFactory.createLineBorder(Color.BLUE), "Button Area",
                TitledBorder.CENTER, TitledBorder.DEFAULT_POSITION);
        panel.setBorder(border);
        panel.setLayout(new GridLayout(1,0));
        var button1 = new JButton("Translate Right");
        var button2 = new JButton("Translate Left");
        button1.addActionListener(e -> 
        {
            rect1.translate(100, 80);
            button1.setEnabled(false);
            button2.setEnabled(true);
            component.repaint();
        });
        button2.addActionListener(e -> 
        {
            rect1.translate(-100, -80);
            button1.setEnabled(true);
            button2.setEnabled(false);
            component.repaint();
        });

        panel.add(button1);
        panel.add(button2);
        button2.setEnabled(false);
        
        frame.add(panel, BorderLayout.PAGE_END);
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}
```

-----------------------------
**Inheritance**

-----------------------------

**Chapter 9**

- Inheritance is used to produce families of classes, where code reuse between the family members should be maximized.
- In Chapter 9 the technique is inheritance.
- In Chapter 10 the technique for reuse is implementation of interfaces. Code is not reused in the same way but we shall see how we gain flexibility.

- When building a javax.swing GUI, you will often make this kind of subclass:

```java
public class GraphComponent extends JComponent {
	...
}
```

- We saw BankAccount. Really it is a subclass

```java
public class BankAccount extends Object { 
	...
}
```

- Any non-final class can have subclasses:

```java
public class SavingsAccount extends BankAccount {
	...
}	
```

**Vehicle family**

- The textbook's motivational diagram:

![](https://www.cs.binghamton.edu/~lander/cs140/chap9-1.JPG)

- The actual example the Textbook studies relates to Question classes--this is a 
UML (Unified Modeling Language) diagram:

![](https://www.cs.binghamton.edu/~lander/cs140/chap9-2.JPG)

- Class Question from section 1

```java
package sec01;
/**
   A question with a text and an answer.
 */
public class Question 
{
	private String text;
	private String answer;

	/**
      Constructs a question with empty question and answer.
	 */
	public Question() 
	{
		text = "";
		answer = "";
	}

	/**
      Sets the question text.
      @param questionText the text of this question
	 */
	public void setText(String questionText) 
	{
		text = questionText;
	}

	/**
      Sets the answer for this question.
      @param correctResponse the answer
	 */
	public void setAnswer(String correctResponse) 
	{
		answer = correctResponse;
	}

	/**
      Checks a given response for correctness.
      @param response the response to check
      @return true if the response was correct, false otherwise
	 */
	public boolean checkAnswer(String response) 
	{
		return response.equals(answer);
	}

	/**
      Displays this question.
	 */
	public void display() 
	{
		System.out.println(text);
	}
}
```

- Tester

```java
package sec01;
import java.util.Scanner;
/**
   This program shows a simple quiz with one question.
 */
public class QuestionDemo1 
{
	public static void main(String[] args) 
	{
		try(var in = new Scanner(System.in)) 
		{
			var q = new Question();
			q.setText("Who was the inventor of Java?");
			q.setAnswer("James Gosling");      

			q.display();
			System.out.print("Your answer: ");
			var response = in.nextLine();
			System.out.println(q.checkAnswer(response));
		}
	}
}
```

**Changing the behavior with a subclass**

- The subclass has an additional field. It also has an additional method and it modifies the behavior of the display method (this is called *overriding*)
- Here is a more thorough Unified Modeling Language (UML) diagram:

![](https://www.cs.binghamton.edu/~lander/cs140/chap9-3.JPG)

```java
package sec03;
// sec03 has its own copy of the class Question
import java.util.ArrayList;
/**
   A question with multiple choices.
 */
public class ChoiceQuestion extends Question 
{
	private ArrayList<String> choices;

	/**
      Constructs a choice question with no choices.
	 */
	public ChoiceQuestion() 
	{
		choices = new ArrayList<String>();
	}

	/**
      Adds an answer choice to this question.
      @param choice the choice to add
      @param correct true if this is the correct choice, false otherwise
	 */
	public void addChoice(String choice, boolean correct) 
	{
		choices.add(choice);
		if (correct) 
		{
			// Convert choices.size() to string
			String choiceString = "" + choices.size();
			setAnswer(choiceString);
		}
	}

	public void display() 
	{
		// Display the question text
		super.display(); /// Pay attention to super.display()
		// Display the answer choices
		for (int i = 0; i < choices.size(); i++) 
		{
			int choiceNumber = i + 1;
			System.out.println(choiceNumber + ": " + choices.get(i));     
		}
	}
}
```

- Tester

```java
package sec03;
import java.util.Scanner;
/**
   This program shows a simple quiz with two choice questions.
 */
public class QuestionDemo2 
{
	public static void main(String[] args) 
	{
		var first = new ChoiceQuestion();
		first.setText("What was the original name of the Java language?");
		first.addChoice("*7", false);
		first.addChoice("Duke", false);
		first.addChoice("Oak", true);
		first.addChoice("Gosling", false);

		var second = new ChoiceQuestion();
		second.setText("In which country was the inventor of Java born?");
		second.addChoice("Australia", false);
		second.addChoice("Canada", true);
		second.addChoice("Denmark", false);
		second.addChoice("United States", false);

		presentQuestion(first);
		presentQuestion(second);
	}

	/**
      Presents a question to the user and checks the response.
      @param q the question
	 */
	public static void presentQuestion(ChoiceQuestion q) 
	{
		q.display();
		System.out.print("Your answer: ");
		try (var in = new Scanner(System.in)) 
		{
			var response = in.nextLine();
			System.out.println(q.checkAnswer(response));
		}
	}
}
```

**super.display()**

- The textbook demonstrates there is sometimes a need to call the parent version of the method that is overridden (using "super.")

**polymorphism (dynamic dispatching)**

- In `public static void presentQuestion(ChoiceQuestion q)` the line `q.display()` illustrates a call to the method in `ChoiceQuestion`.
- In the following class of Section 4 `public static void presentQuestion(Question q)`, the call `q.display()` is using *polymorphism* 
(also called *dynamic dispatching*), where the first time it is calls the method in Question and the second time it is calling
the method in `ChoiceQuestion`.
- We will see later how this is achieved.
- In the code after that called `new_version`, we will see that the dynamic dispatching is the same but it depends on the type of the implicit
parameter "this" instead of the type of "q"

```java
package sec04;
import java.util.Scanner;
// the code for Question and ChoiceQuestion are copied from Section 3
/**
   This program shows a simple quiz with two question types.
*/
public class QuestionDemo3 
{
   public static void main(String[] args) 
   {
      var first = new Question();
      first.setText("Who was the inventor of Java?");
      first.setAnswer("James Gosling");

      var second = new ChoiceQuestion();
      second.setText("In which country was the inventor of Java born?");
      second.addChoice("Australia", false);
      second.addChoice("Canada", true);
      second.addChoice("Denmark", false);
      second.addChoice("United States", false);

      presentQuestion(first);
      presentQuestion(second);
   }

   /**
      Presents a question to the user and checks the response.
      @param q the question
   */
   public static void presentQuestion(Question q) 
   {
      q.display();
      System.out.print("Your answer: ");
      try (var in = new Scanner(System.in)) 
      {
    	  var response = in.nextLine();
    	  System.out.println(q.checkAnswer(response));
      }
   }
}
```

**The new version**

- See that when a *constructor* has parameters in the parent class, the subclass will have to 
use `super(...)` in its constructor. Calls to `super(...)` in a constructor must come FIRST.
- Note for the future, C++ achieves the parameter passing completely differently
- When you are calling "super.method()" to call a parent method, that can go anywhere in the body of the method where you need it.
- C++ also has a different notation instead of "super.method()".
- This Java notation does not apply to `static` methods:
- If the `static` method `meth()` appears in the class `Parent` and its subclass `Child`, then you call one
with `Parent.meth()` and the other with `Child.meth()`

```java
package new_version;
import java.util.Scanner;
/**
 * A question with a text and an answer.
 */
public class Question 
{
	private String text;
	private String answer;
	/**
	 * Constructs the Question with the questions text and
	 * the correct answer if available
	 * @param qText the text of the question
	 * @param correctResponse the correct answer if available
	 */
	public Question(String qText, String correctResponse) 
	{
		text = qText;
		answer = correctResponse;
	}

	//setText is no longer needed

	/**
	 * Sets the answer for this question. It may need to changed from
	 * the one given in the constructor.
	 * @param correctResponse the answer
	 */
	public void setAnswer(String correctResponse) 
	{
		answer = correctResponse;
	}
	/**
	 * Checks a given response for correctness.
	 * @param response the response to check
	 * @return true if the response was correct, false otherwise
	 */
	public boolean checkAnswer(String response) 
	{
		return response.equals(answer);
	}
	/**
	 * Displays this question.
	 */
	public void display() 
	{
		System.out.println(text);
	}
	/**
	 * Presents a question to the user and checks the response.
	 */
	public void presentQuestion() 
	{
		display();
		System.out.print("Your answer: ");
		try(var in = new Scanner(System.in)) 
		{
			var response = in.nextLine();
			System.out.println(checkAnswer(response));
		}
	}
}
```

- New ChoiceQuestion

```java
package new_version;
import java.util.ArrayList;
/**
 * A question with multiple choices.
 */
public class ChoiceQuestion extends Question 
{
	private ArrayList<String> choices;
	/**
	 * Constructs a ChoiceQuestion with the text of the question
	 * but no correct answer.
	 * @param qText the text of the question
	 */
	public ChoiceQuestion(String qText) 
	{
		super(qText, "");
		choices = new ArrayList<>();
	}
	/**
	 * Adds an answer choice to this question.
	 * @param choice the choice to add
	 * @param correct true if this is the correct choice, false otherwise
	 */
	public void addChoice(String choice, boolean correct) 
	{
		choices.add(choice);
		if (correct) 
		{
			// Convert choices.size() to string
			String choiceString = "" + choices.size();
			setAnswer(choiceString);
		}
	}
	public void display() 
	{
		// Display the question text
		super.display();
		// Display the answer choices
		for (int i = 0; i < choices.size(); i++) 
		{
			System.out.println((i+1) + ": " + choices.get(i));     
		}
	}
}
```

- New Tester

```java
package new_version;
/**
 * This program shows a simple quiz with two question types.
 */
public class QuestionDemo4 
{
	public static void main(String[] args) 
	{
		var first = new Question("Who was the inventor of Java?",
				"James Gosling");

		var second = new ChoiceQuestion(
				"In which country was the inventor of Java born?");
		second.addChoice("Australia", false);
		second.addChoice("Canada", true);
		second.addChoice("Denmark", false);
		second.addChoice("United States", false);

		first.presentQuestion();
		second.presentQuestion();
	}
}
```

**Various Topics in the Textbook**

- Common Error 9.1 emphasizes that it is a temptation to put “text” in as a field of ChoiceQuestion 
because you CANNOT WRITE

```java
public ChoiceQuestion(String qText) 
{
	text = qText; // instead of super(qText, "");
	choices = new ArrayList<>();
}
```

- If you were to put a local variable `text` in ChoiceQuestion, will give the Figure on Page 313 where
two different text storage locations 
- The design of `void presentQuestion()` in `Question` of the `new_version` package is discussed in Special Topic 9.2
- Although the example used the Question and ChoiceQuestion in `sect03`, the explanation of how the code runs also 
focuses on how the implicit parameter "this" determines the call to "display()"
- The textbook describes how `super(...)` is used to pass parameters to the parent constructor from a child class on page 318
- The overall structure of a `ChoiceQuestion` object called `first` in `QuestionDemo2` is shown here:

![](https://www.cs.binghamton.edu/~lander/cs140/chap9-4.JPG)

**Polymorphism--see Page 442**

- See the item: Dynamic Method Lookup and the Implicit Parameter. 
- The addresses (addr.) are in the binary code of the program. 
- This is the VMT of the ChoiceQuestion class. (Probably there is a second VMT for super. calls)

![](https://www.cs.binghamton.edu/~lander/cs140/chap9-5.JPG)

- `QuestionDemo4` in `new_version` uses the VMT above

![](https://www.cs.binghamton.edu/~lander/cs140/chap9-6.JPG)

**Forcing methods to be overridden**

- The textbook has the example of `Account` with a method deductFees (probably monthly)
- Suppose the expectation is that there are several Account subclasses: `SavingsAccount`, `BusinessAccount`, 
`CertificateOfDeposit`, `CreditCard`, `DebitCard`, etc., each with individual rules about fees
- How to be *sure* that the programmers of the subclass implements deductFees for the subclass?
- There are two standard ways
- In Account:

```java
public void deductFees() 
{
	throw new UnsupportedOperationException(
		"This class does not implement deductFees");
}
```

- or

```java
public abstract void deductFees();
```

- However, abstract methods can only appear in abstract classes (see Special Topic 9.3):

```java
public abstract class Account 
{
	public abstract void deductFees();
}
```

- Rules for abstract classes:
- We will call a class *concrete* if it is not abstract
- If the parent class is abstract and has abstract methods, then concrete subclasses have to implement all of the 
abstract methods in the parent.
- There may be abstract subclasses that do not implement the abstract methods.

```java
public class SavingsAccount extends Account 
{
	// need to implement deductFees here
}
```

**Final methods and classes**

- If a method is final, it cannot be overridden

```java
public final boolean checkPassword(String pwd) {
	...
} // no-one can change this in a subclass
```

```java
public final class String 
{
...
} // cannot make a subclass
```

**Protected Access**

- We could have 

```java
public class Question 
{
	protected String text; // access in subclasses
	...				     // and same package
}
```

- Then in the subclass

```java
@Override
public void display()
{
	System.out.println(text);
	for(int i = 0; i < choices.size(); i++) {
		System.out.println((i+1) + ": " + choices.get(i));
	}
}	
```

- But the textbook outlines that the negative implications are essentially the same 
as those for public fields

**Inheriting code from a parent**

- The subclass "inherits" all the public, protected methods from its parent class (and package private methods 
if the subclass is in the same package)
- Multiple wording is possible:

```
	class B extends A
```

- B is the subclass, A is the superclass
- B is the child class, A is the parent class
- B is the derived class, A is the base class
- Suppose A contains a method anyMeth:

```java
package pack1;
import pack.Type1;
import pack.Type2;
public class A 
{
	public Type1 anyMeth(Type2 parm) 
	{
		...
	}
}

package pack2;
import pack1.A;
public class B extends A {
	...
}

package pack3;
import pack.Type1;
import pack.Type2;
import pack2.B;
public class Tester 
{
	public static void main(String[] args) 
	{
		B aVar = new B();
		Type2 x = new Type2();
		Type1 y = aVar.anyMeth(x); // uses the code from A
	}
}
```

**Object: The Cosmic Superclass**

- When you make a subclass, you can choose to change the code that executes when a parent's method 
is called on a child object
- This process is called *overriding* the parent method (or the *ancestor* method)
- An *ancestor* class is either the parent or an ancestor of the parent (i.e. the parent of the parent 
of the parent ... of this class)
- If A is an ancestor of B, then B is a *descendant* of A
- For example `Object` is an ancestor of every Java class and Java classes are all descendants of `Object`
- Every class inherits or overrides the public and protected methods in `Object`
- The class Object has the `toString` method

```java
public String toString() 
{
	return getClass().getName() + "@" + Integer.toHexString(hashCode( ));
}
```

- Example

```
package pkg;
public class Person 
{ 
	...
}
```

- If we do not define our own `toString` in the `Person` class, then

```java
Person p = new Person();
System.out.println(p);
```

gives

```
pkg.Person@b049e72a
```

- See <a href="https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/Object.html#getClass()" target="blank">public final Class<?> getClass()</a>
in class `Object`, <a href="https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/Class.html#getName()" target="blank">public String getName()</a>
in class <a href="https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/Class.html" target="blank">public final class Class<T> extends Object...</a>, and 
<a href="https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/Class.html#getSimpleName()" target="blank">public String getSimpleName()</a>

- More descriptive `toString`

```java
public class Person 
{
	private String firstNames; 
	private String lastNames;
	private int ssn;
	private DateAndPlaceOfBirth placeDob;
	private StreetUSAddress address;

	public String getSSN() 
	{
		return String.format("%03d-%02d-%04d", ssn/1000000,ssn%1000000/10000, ssn%10000); 
	}
	
	@Override
	public String toString() 
	{
		return firstNames + " " + lastNames
		+ " (" + getSSN() + "),\n" + placeDob // calls placeDob.toString()
		+ "\n" + address; // calls address.toString()
	}
}
```

- The "+" concatenator of Strings keeps allocating more storage, so <a href="https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/StringBuilder.html" target="blank">java.lang.StringBuilder</a> is preferred
because it works efficiently like ArrayList.
- However, there is this now a note in String Implementation Note:
"The implementation of the string concatenation operator is left to the discretion of a Java compiler, as long as the compiler ultimately conforms to The Java™ Language Specification. For example, the javac compiler may implement the operator with StringBuffer, StringBuilder, or java.lang.invoke.StringConcatFactory depending on the JDK version. The implementation of string conversion is typically through the method toString, defined by Object and inherited by all classes in Java."

```java
public class Person 
{
	private String firstNames; 
	private String lastNames;
	private int ssn;
	private DateAndPlaceOfBirth placeDob;
	private StreetUSAddress address;

	public String getSSN() 
	{
		return String.format("%03d-%02d-%04d", ssn/1000000,ssn%1000000/10000, ssn%10000); 
	}
	
	@Override
	public String toString() 
	{
		StringBuilder sb = new StringBuilder(firstNames);
		sb.append(" ");
		sb.append(lastNames);
		sb.append(" (");
		sb.append(getSSN());
		sb.append("),\n");
		sb.append(placeDob); // calls placeDob.toString()
		sb.append("\n");
		sb.append(address); // calls address.toString()
		return sb.toString();
	}
}
```

**The equals method in Object**

- The method <a href="https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)" target="blank">equals</a> as it appears in the class Object:

```java
public boolean equals(Object obj) 
{
	return (this == obj); 
}
```

- It makes sense that you override equals in String. The code is on the next slide
- If the BankAccount has a unique account ID, that would be a reason for equality
- The textbook example is Stamp, Page ???. The need to override the equals method would depend on the application. 
- Should two identical-looking but separate stamps be equal?

```java
public class Stamp 
{
	private String color;
	private int value;
	...
	public Stamp(String aColor, int aValue) 
	{
		color = aColor;
		value = aValue;
	}
	public String getColor() 
	{
		return color;
	}

	public int getValue() 
	{
		return value;
	}

	public boolean equals(Object otherObject) 
	{
		Stamp other = (Stamp) otherObject;
		return color.equals(other.color) && value == other.value;
	)
	// see below for overriding hashCode()
```

- Part of the actual implementation of equals in String:

```java
 * Copyright (c) 1994, 2018, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
...
    public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String aString = (String)anObject;
            if (coder() == aString.coder()) {
                return isLatin1() ? StringLatin1.equals(value, aString.value)
                                  : StringUTF16.equals(value, aString.value);
            }
        }
        return false;
    }

// information about coder is package private and not in the API	
// In the package private class final class StringLatin1:

    @HotSpotIntrinsicCandidate
    public static boolean equals(byte[] value, byte[] other) {
        if (value.length == other.length) {
            for (int i = 0; i < value.length; i++) {
                if (value[i] != other[i]) {
                    return false;
                }
            }
            return true;
        }
        return false;
    }	
```

**What is anObject instanceof String?**

- For how we only discuss *classes*, later will will extend the discussion to *interfaces*
- `obj instanceof SomeClass` is true if an only if `obj` is currently an instance of some
class X and X is either `SomeClass` or a descendant of `SomeClass`.
- Rememeber we have to expand this explanation when we get to interfaces and enums.
- The test `anObject instanceof String` is special however.
- Since the class `String` is final, there are no descendants of String, so `anObject instanceof String` can only be true
if `abObject` *is* a String.
- Important NOTE, `null instanceof Anything` is false.

**Looking deeper at the overriding equals when classes are not final**

- If we pay attention to

```java
	public boolean equals(Object otherObject) {
		Stamp other = (Stamp) otherObject;
		return color.equals(other.color) && value == other.value;
	}
```

- We will get a ClassCastException from `(Stamp) otherObject` if `otherObject` is not a `Stamp`
- Therefore we use `instanceof`

```java
	public boolean equals(Object otherObject) 
	{
		if(this == otherObject) // this is a quick shortcut
		{
			return true;
		}
		if(otherObject instanceof Stamp 
		{
			Stamp other = (Stamp) otherObject;
			return color.equals(other.color) && value == other.value;
		}
		return false;
	}
```

- There is a problem however. 
- Suppose there is a subclass of `Stamp` called `UnusedStamp`
- The `instanceof Stamp` will also return true of an `UnusedStamp` and we could now find a used and unused Stamp
being considered equal.
- A more precise test is to compare the class of the objects, thus eliminating the issue we just raised:

```java
	public boolean equals(Object otherObject) {
		if(this == otherObject) // this is a quick shortcut
		{
			return true;
		}
		if(otherObject == null) 
		{
			return false;
		}
		// cannot call otherObject.getClass() if otherObject == null
		if(getClass() != otherObject.getClass()) 
		{ 
			return false;
		}
		Stamp other = (Stamp) otherObject;
		return color.equals(other.color) && value == other.value;
	}
```

- Note that getClass() returnes a reference to the *UNIQUE* class object for any class, so we 
can test with !=

**The hashCode problem**

- In Chapter 15 we discover that `HashSet` and `HashMap` use a combination of `equals()` and `hashCode()`
- In fact in the Java API: 
"If two objects are equal according to the equals(Object) method, then calling the hashCode 
method on each of the two objects must produce the same integer result"

**If we override equals(Object) we must override hashCode()**

```java
	// in Stamp
	public int hashCode() 
	{
		return 31*color.hashCode() + value;
	}
```

- Since `equals` is overridden in `String`, `hashCode` must be overridden


```java
 * Copyright (c) 1994, 2018, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
...
    public int hashCode() {
        int h = hash;
        if (h == 0 && value.length > 0) {
            hash = h = isLatin1() ? StringLatin1.hashCode(value)
                                  : StringUTF16.hashCode(value);
        }
        return h;
    }
 
// information about coder is package private and not in the API	
// In the package private class final class StringLatin1:

    public static int hashCode(byte[] value) {
        int h = 0;
        for (byte v : value) {
            h = 31 * h + (v & 0xff);
        }
        return h;
    }
```

- See <a href="https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/String.html#hashCode()" target="blank">public int hashCode()</a> in `String`
- Usually we multiply the fields of an object repeatedly by 29 or 31 so that each field get a different power of the multiplier.
- Compare what is now mistakenly called Horner’s method—see <a href="http://en.wikipedia.org/wiki/Horner%27s_method" target="blank">Horner's method</a>
- Out of interest there are hash codes associated with the primitive types:
- For int, byte, short, char, use the value itself as an int
- For long x, use Long.hashCode(x);
- For float x, use Float.hashCode(x);
- For double x, use Double.hashCode(x);
- For boolean x, use Boolean.hashCode(x); (false gives 1237, true gives 1231)

These values are shown in the main method of Stamp: here are the versions discussed above:

```java
package ch09.stamps;

public class Stamp1 
{
	private String color;
	private int value;

	public Stamp1(String color, int value) 
	{
		this.color = color;
		this.value = value;
	}

	public String getColor() 
	{
		return color;
	}

	public int getValue() 
	{
		return value;
	}

	// First version in textbook. Can throw NullPointerException or
	// ClassCastException
	@Override
	public boolean equals(Object otherObject) 
	{
		var other = (Stamp1) otherObject;
		return color.equals(other.color) && value == other.value;
	}

	// autogenerated by Eclipse:

	@Override
	public int hashCode() 
	{
		final int prime = 31;
		int result = 1;
		result = prime * result + ((color == null) ? 0 : color.hashCode());
		result = prime * result + value;
		return result;
	}

	public static void main(String[] args) 
	{
		System.out.println("p1 = new Stamp1(\"Blue\", 75)");
		System.out.println("p2 = new Stamp1(\"Blue\", 75)");
		System.out.println("p3 = new Stamp1(\"Green\", 120)");
		System.out.println("q1 = \"abc\"");
		System.out.println("q2 = (Stamp1)null");

		var p1 = new Stamp1("Blue", 75);
		var p2 = new Stamp1("Blue", 75);
		var p3 = new Stamp1("Green", 120);
		var q1 = "abc"; 
		var q2 = (Stamp1)null;
		System.out.println(p1.equals(p2));
		System.out.println(p1.equals(p3));
		try 
		{
			System.out.println(p1.equals(q1));
		} catch(ClassCastException e) 
		{
			System.out.println("ClassCastException for p1.equals(q1), message: " + e.getMessage());
		}
		try 
		{
			System.out.println(p1.equals(q2));
		} catch(NullPointerException e) 
		{
			System.out.println("NullPointerException for p1.equals(q2), message: " + e.getMessage());
		}
		System.out.println("---------------");		
		System.out.println("Boolean.hashCode(false): " + Boolean.hashCode(false));
		System.out.println("Boolean.hashCode(true): " + Boolean.hashCode(true));
		System.out.println("Integer.hashCode(7): " + Integer.hashCode(7));
		System.out.println("Byte.hashCode((byte)7): " + Byte.hashCode((byte)7));
		System.out.println("Short.hashCode((short)-7): " + Short.hashCode((short)-7));
		System.out.println("Character.hashCode('A'): " + Character.hashCode('A'));
		System.out.println("Long.hashCode(77777777777777L): " + Long.hashCode(77777777777777L));
		System.out.println("Float.hashCode(7.5F): " + Float.hashCode(7.5F));
		System.out.println("Double.hashCode(7.5): " + Double.hashCode(7.5));
		System.out.println("---------------");		

		@SuppressWarnings("unchecked")
		Class<Stamp1> c = (Class<Stamp1>)p1.getClass();
		System.out.println("Calling toString on a class object:");
		System.out.println(c);
	}
}
```

```java
package ch09.stamps;

public class Stamp2 
{
	private String color;
	private int value;

	public Stamp2(String color, int value) 
	{
		this.color = color;
		this.value = value;
	}

	public String getColor() 
	{
		return color;
	}

	public int getValue() 
	{
		return value;
	}

	// Version that uses instanceof. It could allow a subclass object
	// to equal a parent object erroneously
	@Override
	public boolean equals(Object otherObject) 
	{
		if(this == otherObject) return true;
		if(otherObject instanceof Stamp2) 
		{
			var other = (Stamp2) otherObject;
			return color.equals(other.color) && value == other.value;
		}
		return false;
	}

	// autogenerated by Eclipse:
	
	@Override
	public int hashCode() 
	{
		final int prime = 31;
		int result = 1;
		result = prime * result + ((color == null) ? 0 : color.hashCode());
		result = prime * result + value;
		return result;
	}
	
	public static void main(String[] args) 
	{
		System.out.println("p1 = new Stamp2(\"Blue\", 75)");
		System.out.println("p2 = new Stamp2(\"Blue\", 75)");
		System.out.println("p3 = new Stamp2(\"Green\", 120)");
		System.out.println("q1 = \"abc\"");
		System.out.println("q2 = (Stamp2)null");

		var p1 = new Stamp2("Blue", 75);
		var p2 = new Stamp2("Blue", 75);
		var p3 = new Stamp2("Green", 120);
		var q1 = "abc"; 
		var q2 = (Stamp2)null;
		System.out.println(p1.equals(p2));
		System.out.println(p1.equals(p3));
		System.out.println(p1.equals(q1));
		System.out.println(p1.equals(q2));
	}
}
```

```java
package ch09.stamps;

public class Stamp3 
{
	private String color;
	private int value;

	public Stamp3(String color, int value) 
	{
		this.color = color;
		this.value = value;
	}

	public String getColor() 
	{
		return color;
	}

	public int getValue() 
	{
		return value;
	}

	// Version using getClass(). Eliminates the parent/subclass problem
	// @Override
	public boolean equals(Object otherObject) 
	{
		if(this == otherObject) 
		{
			return true;
		}
		if(otherObject == null || getClass() != otherObject.getClass()) 
		{
			return false;
		}
		Stamp3 other = (Stamp3) otherObject;
		return color.equals(other.color) && value == other.value;
	}	

	// autogenerated by Eclipse:
	
	@Override
	public int hashCode() 
	{
		final int prime = 31;
		int result = 1;
		result = prime * result + ((color == null) ? 0 : color.hashCode());
		result = prime * result + value;
		return result;
	}

	public static void main(String[] args) 
	{
		System.out.println("p1 = new Stamp3(\"Blue\", 75)");
		System.out.println("p2 = new Stamp3(\"Blue\", 75)");
		System.out.println("p3 = new Stamp3(\"Green\", 120)");
		System.out.println("q1 = \"abc\"");
		System.out.println("q2 = (Stamp3)null");

		var p1 = new Stamp3("Blue", 75);
		var p2 = new Stamp3("Blue", 75);
		var p3 = new Stamp3("Green", 120);
		var q1 = "abc"; 
		var q2 = (Stamp3)null;
		System.out.println(p1.equals(p2));
		System.out.println(p1.equals(p3));
		System.out.println(p1.equals(q1));
		System.out.println(p1.equals(q2));
	}
}

```

```java
package ch09.stamps;

import java.awt.Color;

public class Stamp4 
{
	private String color;
	private int value;

	public Stamp4(String color, int value) 
	{
		this.color = color;
		this.value = value;
	}

	public String getColor() 
	{
		return color;
	}

	public int getValue() 
	{
		return value;
	}

	// autogenerated by Eclipse:
	
	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Stamp4 other = (Stamp4) obj;
		if (color == null) {
			if (other.color != null)
				return false;
		} else if (!color.equals(other.color))
			return false;
		if (value != other.value)
			return false;
		return true;
	}

	@Override
	public int hashCode() 
	{
		final int prime = 31;
		int result = 1;
		result = prime * result + ((color == null) ? 0 : color.hashCode());
		result = prime * result + value;
		return result;
	}

	public static void main(String[] args) 
	{
		System.out.println("p1 = new Stamp4(\"Blue\", 75)");
		System.out.println("p2 = new Stamp4(\"Blue\", 75)");
		System.out.println("p3 = new Stamp4(\"Green\", 120)");
		System.out.println("q1 = \"abc\"");
		System.out.println("q2 = (Stamp4)null");

		var p1 = new Stamp4("Blue", 75);
		var p2 = new Stamp4("Blue", 75);
		var p3 = new Stamp4("Green", 120);
		var q1 = "abc"; 
		var q2 = (Stamp4)null;
		System.out.println(p1.equals(p2));
		System.out.println(p1.equals(p3));
		System.out.println(p1.equals(q1));
		System.out.println(p1.equals(q2));
	}
}

```
