<div align=center>
  <h1>JavaArgs </h1> 
  <h2>Clean Code Assignment</h2>
  <b>Submitted By:</b>
  <b>Shivang Shekhar</b><br>
  <b>Roll No: 2019900021</b>
<br><br>
 <img src="http://s.4cdn.org/image/title/105.gif">
</div><br /><br />


JavaArgs ![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg) is a java version of Args that is described in a book by Uncle Bob in his book called Clean Code.

## Disclaimer :zap:

This piece of code has been originally forked from the Args program described in: [Uncle Bob](http://butunclebob.com/ArticleS.UncleBob.CleanCodeArgs). 
I have further tried to implement a clean coding practice on this source code written in Java as part of Assignment given in Software Engineering course taught (in Spring 2020) at [International Institute of Information Technology](www.iiit.ac.in)


## How to Run :zap:

Use the  [eclipse IDE]([https://www.eclipse.org/ide/](https://www.eclipse.org/ide/)) to run JavaArgs

### Before You Run :zap:

Before you Run the code, you might also nees to check for environment setup for Java:

#### Intall or Update Java :zap:

Run:
```
  * sudo add-apt-repository ppa:openjdk-r/ppa
  * sudo apt-get update -q 
  * sudo apt install -y openjdk-11-jdk 
```

#### For Tests :zap:

Run:

```
 * Run the command given below from the root folder of this repo
 * 'java -cp "lib/junit-4.13.jar:lib/hamcrest-core-1.3.jar:build/jar/args.jar" ./test/com/cleancoder/args/ArgsTest.java testCreateWithNoSchemaOrArguments'
```

## Usage :zap:

Once you have set-up the basic requirements and your environment is ready, you may use the following code to implement the main class ```ArgsMain.java```

```Java
package com.cleancoder.args;

import java.util.Map;

public class ArgsMain {

  /**
  * This method is used to add two integers. This is
  * a the simplest form of a class method, just to
  * show the usage of various javadoc Tags.
  * @param args This is the first paramter to addNum method
  */
  public static void main(String[] args) {
    try {
      Args arg = new Args("l,p#,d*,b##, c[*], m&", args);
      boolean logging = arg.getBoolean('l');
      int port = arg.getInt('p');
      double dob = arg.getDouble('b');
      String[] cs = arg.getStringArray('c');
      Map<String, String> ma = arg.getMap('m');
     
      String directory = arg.getString('d');
      executeApplication(logging, port, directory, dob, cs, ma);
    } catch (ArgsException e) {
      System.out.printf("Argument error: %s\n", e.errorMessage());
    }
  }

  private static void executeApplication(boolean logging, int port, String directory, double dob, String[] cs, Map<String, String> ma) {
    System.out.printf("logging is %s, port:%d, directory:%s, double:%f, stringArray:%s, map:%s",logging, port, directory, dob, cs[0], ma);
  }
}
```

#### Instructions: :zap:

Add ```ArgsMain.java``` file in at the follwing path : ```root/src/com/cleancoder/args ``` in your code and  use the below schema to operate:

#### Schema :zap:

Schema:
```
 - char    - Boolean arg.
 - char*   - String arg.
 - char#   - Integer arg.
 - char##  - double arg.
 - char[*] - one element of a string array.
```

Example schema: (f,s*,n#,a##,p[*])

Coresponding command line: "-f -s Bob -n 1 -a 3.2 -p e1 -p e2 -p e3

## Objective :zap:

The goal of this exercise is to implement clean code practises in the code for JavaArgs and that include the following :

1. Removing Lints 
2. Imporving Code-coverage
3. Refactor Control Flow
4. Refactor Classes and Methods
5. End to End Test
..* Add tests for uncovered code 
..* Remove duplicate tests 
..* Add Test Annotation [Decorators]
..* Refactor if/else/try/catch conditions to improve coverage
6. Remove Code Smells 


There is a list of comprehensive actions performed under the above-mentioned points and are discussed below in detail.     


## Understanding the Code :zap:

### Class Diagram Args :zap:


![image](https://res.cloudinary.com/dhso5z9a1/image/upload/v1579950369/Class_Diagram_ynkm2n.jpg)

Or you may find it in eclipse at 
```
src/ArgsClassDiagram.ucls
```

### JavaDocs :zap:

To understand the code better follow the [JavaDocs]() given for the code.

*JavaDocs for  tests are not available so as to reduce the on-screen clutter of code and I have tried to make classes/methods/ arg names to be more descriptive in-order to save the clutter*

For more discussion on JavaDocs for test check this [Stackoverflow](https://stackoverflow.com/a/2968153/3801905) :bulb: Link.




## Clean Code :zap:

In this section I am going to discuss about the code cleaning that has been done for the JavaArgs Code.

As stated above there are some major practises that were utilised to clean the code, namely:
```
1. Removing Code Smells 
2. Imporving Code-coverage
3. Refactoring Control Flow
4. Refactoring Classes and Methods
5. End to End Testing
..* Add tests for uncovered code 
..* Remove duplicate tests 
..* Add Test Annotation [Decorators]
..* Refactoring if/else/try/catch conditions to improve coverage
6. Removing Code Lint 

```

For the above changes some tools were used which needs to be mentioned here :

* :pushpin: Code Smell : I used  [Jdeodrant](http://jdeodorant.com/) :green_heart: integration to remove code smells and lints.
* :pushpin: Code Coverage: I used [Junit](https://junit.org/junit5/) :heart:
* :pushpin: Linting : I used [CheckStyle](https://marketplace.eclipse.org/content/checkstyle-plug) :heart: to remove lint from code 

Now lets deep dive into the knitty-gritty of the various aspects of code cleaning:

### Code Coverage :zap:

* :radio_button: Code coverage has been imporved from **88.5 %** :small_red_triangle_down: to ** 91% ** :heavy_check_mark: overall.
* :radio_button: Code coverage is at a at a whopping **97%** :heavy_check_mark: if tests are not considered.

..* As per the discussion online, tests are generally not covered during the coveraged for more information check this [Stackoverflow](https://stackoverflow.com/a/24958299/3801905) :pill: link.

#### Code Coverage Improvements :zap:

Below mentioned are the refactored pieces of code that helped imporve Code Coverage:


:x: Unused lines for methods were removed to imporve coverage as they were affecting significantly.

From ```ArgsException.java``` :red_circle: --remove 
```
public  ArgsException() {}

public  ArgsException(String message) {super(message);}
```
:repeat_one:

```
public void setErrorCode(ErrorCode  errorCode) {  this.errorCode = errorCode;}
```

From  ```ArgsExceptionTest.java```  :heavy_plus_sign: Test for OK condition 

```testOkMessage()```  was not available and  **OK** enum was not covered. 

Refer below to the piece of code added :

```
public void testOkMessage() throws Exception {

ArgsException e = new ArgsException(OK, 'x', null);

assertEquals("TILT: Should not get here.", e.errorMessage());

}
```


#### Linting Improvements :zap:


From ```ArgsData.java```  :red_circle: --remove 

```
public ArgsData() {}

```
:x: Removed wildcards from all import statement in the project. [also from java utils]

There are various ways to add *imports* in java and one of the two ways is adding imports with ```wildcards (*)```, I chose to remove all the wildcards and manually add imports taking a reference from the following discussion [Stackoverflow](https://stackoverflow.com/questions/147454/why-using-a-wild-card-with-a-java-import-statement-bad/147461#147461) :pill: .

:heavy_plus_sign:  Followed some code conventions where I added ```static``` imports before all the util imports  and arranged alphabetically.


:part_alternation_mark: In file ```Argsexception.java ```  ```Return``` statement shifted from outside of switch case to default case inside switch case.

```
default:

return ""; // return statement shifted here

}
```

### Code Smells :zap:


The vanilla code form base repository had some major code smells in mainly in the follwing files 

:small_red_triangle_down:  ```Args.java```
:small_red_triangle_down: ```ArgsData.java```

So inorder to remove code smells I handled the following changes.

Those were in 

1. **God Class**
..* for ```schema``` Extract Class
2. **Long Method**
..* Extract Method for variable criteria **'m'**


The changes that are stated below are in-coherence with the following manual which clearly states the decomposition methodology. For details refer to [Jdeodrant](https://users.encs.concordia.ca/~nikolaos/jdeodorant/index.php?option=com_content&view=article&id=45)

:heavy_plus_sign: 

Name | Refactoring Type | Variable Criteria
--- | --- | ---
Long method | Extract method | **m**

---

```
if (m == null) {

throw new  ArgsException(UNEXPECTED_ARGUMENT, argChar, null);
```

Also,

:heavy_plus_sign: File ```ArgsData.java``` was created in order to decompose the following class:

Name | Refactoring Type | Variable Criteria
--- | --- | ---
God Class | Extract Class | Schema






:x: Following Code from ```Args.java``` has been decompsed into ```ArgsData.java```

```
private void parseSchemaElement(String element) throws ArgsException { 

    char elementId = element.charAt(0); 

    String elementTail = element.substring(1); 

    validateSchemaElementId(elementId); 

    if (elementTail.length() == 0) 

      marshalers.put(elementId, new BooleanArgumentMarshaler()); 

    else if (elementTail.equals("*")) 

      marshalers.put(elementId, new StringArgumentMarshaler()); 

    else if (elementTail.equals("#")) 

      marshalers.put(elementId, new IntegerArgumentMarshaler()); 

    else if (elementTail.equals("##")) 

      marshalers.put(elementId, new DoubleArgumentMarshaler()); 

    else if (elementTail.equals("[*]")) 

      marshalers.put(elementId, new StringArrayArgumentMarshaler()); 

    else if (elementTail.equals("&")) 

      marshalers.put(elementId, new MapArgumentMarshaler()); 

    else 

      throw new ArgsException(INVALID_ARGUMENT_FORMAT, elementId, elementTail); 

  } 

  

  private void validateSchemaElementId(char elementId) throws ArgsException { 

    if (!Character.isLetter(elementId)) 

      throw new ArgsException(INVALID_ARGUMENT_NAME, elementId, null); 

  } 

 

public boolean getBoolean(char arg) { 

    return BooleanArgumentMarshaler.getValue(marshalers.get(arg)); 

  } 

  

  public String getString(char arg) { 

    return StringArgumentMarshaler.getValue(marshalers.get(arg)); 

  } 

  

  public int getInt(char arg) { 

    return IntegerArgumentMarshaler.getValue(marshalers.get(arg)); 

  } 

  

  public double getDouble(char arg) { 

    return DoubleArgumentMarshaler.getValue(marshalers.get(arg)); 

  } 

  

  public String[] getStringArray(char arg) { 

    return StringArrayArgumentMarshaler.getValue(marshalers.get(arg)); 

  } 

  

  public Map<String, String> getMap(char arg) { 

    return MapArgumentMarshaler.getValue(marshalers.get(arg)); 

  } 

} 


```

## License
[MIT](https://choosealicense.com/licenses/mit/)
