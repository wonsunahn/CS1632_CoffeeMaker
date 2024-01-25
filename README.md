- [CS 1632 - Software Quality Assurance](#cs-1632---software-quality-assurance)
  * [Deliverable 2](#deliverable-2)
  * [Running the Program](#running-the-program)
  * [Running Unit Tests](#running-unit-tests)
  * [Development Methodology](#development-methodology)
  * [Expected Outcome](#expected-outcome)
  * [Verifying the Test Cases](#verifying-the-test-cases)
  * [Additional Requirements](#additional-requirements)
- [Grading](#grading)
- [Submission](#submission)
- [GradeScope Feedback](#gradescope-feedback)
- [Groupwork Plan](#groupwork-plan)
- [Resources](#resources)

# CS 1632 - Software Quality Assurance
Spring Semester 2024

* DUE: February 13, 2024 before start of class

**GitHub Classroom Link:** TBD

## Description

In this deliverable, we will build a game called CoffeeMakerQuest.
CoffeeMakerQuest is an old school text-based adventure game where the player
searches a house for coffee, cream, and sugar to make a cup of coffee for
herself.  Just like for Exercise 2, you will practice Test Driven Development
so that you always code under the cover of unit testing.  You will also do an
integration test at the end.

You will modify the classes in the source tree in the following ways:

* CoffeeMakerQuest.java - The CoffeeMakerQuest interface with a createInstance method with which to create CoffeeMakerQuest objects of different types.  **Fill in** the part where the method creates a mock CoffeeMakerQuest type.
* CoffeeMakerQuestImpl.java - An implementation of the CoffeeMakerQuest interface.  **Fill in** the class with member variables and method implementations.  When a newline is required as part of a string, take care to use the pre-defined platform-independent newline variable.
* Game - Contains the main method of the game.  This class is already complete.
* InstanceType.java - This is a Java enumeration for instance types, and you don't need to touch.
* Item.java - This is another Java enumeration for item types, and you don't need to touch.
* Player.java - The Player interface with a createInstance method with which to create Players of different types.  **Fill in** the part where the method creates a mock Player type.
* PlayerImpl.java - An implementation of the Player interface.  **Fill in** the class with member variables and method implementations.  When a newline is required as part of a string, take care to use the pre-defined platform-independent newline variable.
* Room.java - The Room interface with a createInstance method with which to create Rooms of different types.  **Fill in** the part where the method creates a mock Room type.
* RoomImpl.java - An implementation of the Room interface.  **Fill in** the class with member variables and method implementations.  When a newline is required as part of a string, take care to use the pre-defined platform-independent newline variable.
* RoomsJSONParser.java - Class that generates a list of rooms by reading in the rooms.config JSON file.  This class is already complete.

* CoffeeMakerQuestUnitTest.java - The JUnit class that unit tests CoffeeMakerQuest objects.
* PlayerUnitTest.java - The JUnit class that unit tests Player objects.
* RoomUnitTest.java - The JUnit class that unit tests Room objects.
* GameIntegrationTest.java - The JUnit class that integration tests the entire CoffeeMakerQuest game.

All source code locations where you need to add code is marked with "// TODO"
comments.  These comments conveniently show up in the Problems pane of your
VSCode IDE.

## Running the Program

### Using VSCode

You can run the program using the VSCode "Run and Debug" extension on the left
menu (the one that looks like a play icon with a bug attached to it).  Once you
click on it, you will see a dropdown menu on the topside.  

1. To launch the solution version of the program, choose "Launch GameSolution"
and then press the green play button.  

   After you launch the program, you can start playing the game:

   ```
   Coffee Maker Quest 1.0

   You see a Small room.
   It has a Quaint sofa.
   A Magenta door leads North.

    INSTRUCTIONS (N,S,L,I,D,H) >
   ...
   ```

1. To launch the current implementation of the program, choose "Launch Game"
and then press the green play button.  You will get the below output:

   ```
   Please make sure that the rooms.config file has doors at all interconnected rooms.
   ```

   The game fails to even initialize correctly.  It will work as expected once you are done.

### Using Commandline

You can also run the program on the commandline using Maven.

1. To launch the solution version of the program, you simply need to invoke the
solution jar file included in the folder:

   ```
   java -jar rentacat-solution-1.0.0.jar
   ```

1. To launch the current implementation of the program, you first need to
compile the program using the 'test-compile' phase on Maven:

   ```
   mvn test-compile
   ```

   If the compilation is successful, all soure codes under src/ are compiled to
class files under target/classes.  Make sure you invoke the 'test-compile'
phase and not the 'compile' phase.  The former will compile both your
implementation classes under the src/main folder and your test classes under
the src/test folder.  The latter will only compile your implementation classes.

   Next, invoke the 'exec' phase, which is configured to invoked RentACatImpl in pom.xml:

   ```
   mvn exec:java 
   ```

## Testing the Program

Again, you can use either VSCode or the commandline to test your program.

### Using VSCode

You can run the program using the VSCode "Testing" extension on the left menu
(the one that looks like a flask icon).  Once you click on it, you will see
options to run the entire test suite, an individual JUnit test class, or an
individual JUnit test method. 

The "Testing" extension solely invokes the JUnit test classes and does not
invoke third party Maven testing plugins listed in the pom.xml file, such as
Jacoco.  For that, you will have to invoke Maven directly as explained below.

### Using Commandline

You can invoke the 'test' phase in Maven:

   ```
   mvn test
   ```

   The Maven framework looks for any JUnit test classes under src/test/, and
invokes them one by one.  You should get a result that looks like this:

```
...
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running edu.pitt.cs.CatUnitTest
[INFO] Tests run: 7, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.081 s -- in edu.pitt.cs.CatUnitTest
[INFO] Running edu.pitt.cs.RentACatIntegrationTest
[INFO] Tests run: 10, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.001 s -- in edu.pitt.cs.RentACatIntegrationTest
[INFO] Running edu.pitt.cs.RentACatUnitTest
[INFO] Tests run: 10, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.001 s -- in edu.pitt.cs.RentACatUnitTest
[INFO] 
[INFO] Results:
[INFO]
[INFO] Tests run: 27, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO]
[INFO] --- jacoco:0.8.11:report (post-unit-test) @ rentacat ---
[INFO] Loading execution data file C:\Users\mrabb\Documents\github\cs1632\CS1632_RentACat\target\jacoco.exec
[INFO] Analyzed bundle 'rentacat' with 5 classes
[INFO] 
[INFO] --- jacoco:0.8.11:check (check-unit-test) @ rentacat ---
[INFO] Loading execution data file C:\Users\mrabb\Documents\github\cs1632\CS1632_RentACat\target\jacoco.exec
[INFO] Analyzed bundle 'rentacat' with 5 classes
[WARNING] Rule violated for class edu.pitt.cs.RentACatImpl: instructions covered ratio is 0.00, but expected minimum is 0.20
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  6.047 s
[INFO] Finished at: 2024-01-23T09:34:07-05:00
[INFO] ------------------------------------------------------------------------
...
```

Note that out of the 27 tests run, 0 tests were failures.  Apparently, all
tests passed!  So are we done?  Far from it!  The reason that there are no
failures is because all test cases are currently empty.  Pay attention to the
following line in the output:

```
[WARNING] Rule violated for class edu.pitt.cs.RentACatImpl: instructions covered ratio is 0.00, but expected minimum is 0.20
```

It is saying that the test phase expected a minimum of 20% instruction coverage
for the RentACatImpl class, but the tests achieved 0%.  Hence that is why it
says 'BUILD FAILURE' in the end.  We were only able to cover 0% exactly
becauase all test cases are empty.  You can see for yourself in all the test
classes under the src/test/ folder that all test cases have just // TODO
comments in them.  The 20% coverage threshold is configured in the pom.xml file
in the Jacoco plugin section:

```
   ...
   <configuration>
     <dataFile>${project.build.directory}/jacoco.exec</dataFile>
     <rules>
       <rule>
	 <element>CLASS</element>
	 <limits>
	   <limit>
	     <counter>INSTRUCTION</counter>
	     <value>COVEREDRATIO</value>
	     <minimum>20%</minimum>
	   </limit>
	 </limits>
	 <includes>
	    <include>edu.pitt.cs.RentACatImpl</include>
	 </includes>
       </rule>
     </rules>
   </configuration>
   ...
```

Jacoco is short for the **Ja**va **Co**de **Co**verage tool.  The documentation
on how to configure like the above is given at:
https://www.eclemma.org/jacoco/trunk/doc/check-mojo.html We will talk more
about Jacoco later in the [Measuring Code Coverage](#measuring-code-coverage)
section.

## Software Developement Life Cycle using Test Driven Development

Now we know how to run the program and test the program, it is time to get to
work in completing the Rent-A-Cat system.

We will try to apply the Test Driven Development (TDD) model and the
Red-Green-Refactor (RGR) loop.  Try writing the test case(s) FIRST before
writing the code for a feature.  This way, you will always have 100% test
coverage for the code you have written and are writing.  Hence, if you break
any part of it in the course of adding a feature or refactoring your code, you
will know immediately.  Otherwise, if you test at the very end, it will be much
harder to find the defect and fix it.

Then, the logical order with which to write the code is the following:

1. CatUnitTest.java - Write the unit tests for Cat (Red: most tests will initially fail).
1. CatImpl.java - Write the implementation for Cat (Green: all tests should pass now).  Refactor as needed.
1. RentACatUnitTest.java - Write the unit tests for RentACat (Red: most tests will initially fail).
1. RentACatImpl.java - Write the implementation for RentACat (Green: all tests should pass now).  Refactor as needed.
1. RentACatIntegrationTest.java - Write integration tests for the Rent-A-Cat system (Hopefully everything works together).  Fortunately for you, you will be able to reuse a lot of the code you already wrote for RentACatUnitTest.java since many tests are going to look the same regardless of whether it is a unit test or integration test, with a few exceptions.

When writing the JUnit test cases, please pay close attention to the Javadoc
comment above each test method that describes the preconditions, execution
steps, and postconditions for that test case.  Also, please note that all or
part of the preconditions may be fulfilled by the test fixture built in the
@Before setUp() method in every JUnit test class.

In the @Before setUp() method of each test class, you are asked to create Cat
objects and RentACat objects that comprise the test fixture, as part of your
TODOs.  You have a choice between creating real objects or mock objects,
depending on the testing situation.  I will leave it up to you to make the
correct decision based on the lectures.  If you are creating a mock object, you
will have to fill in the TODO code for creating that mock object in either the
Cat.java or RentACat.java interfaces.

Another thing you need to do in the @Before setUp() method is to hijack the
system output for testing purposes.  Please refer to the
[textbook](../../software-quality-assurance-textbook.pdf) chapter 14.6 on
Testing System Output.  In short, you need to first back up the original system
output which is going to stdout (the standard output to your console).  Then
you need to replace it with a ByteArrayOutputStream variable named "out".  Now
all prints to System.out will be stored in the "out" buffer, which can be
converted to a String for testing purposes using out.toString().  In the @After
tearDown() method, you will restore stdout to system output.  Now, this may
complicate print debugging since all your debugging messages will go to "out"
instead of being printed to your console.  For debugging purposes, you can use
System.err.println rather than System.out.println, which uses the stderr
stream, which still goes to the console.  In VSCode, stderr is routed to a
special console called the Debug Console that is available as a tab on the
bottom pane.

### Verifying Your Test Cases

While you are still in the Red phase of the RGR loop, it is hard to have
confidence in your test code if you are a novice JUnit tester, especially since
your test is most likely failing.  To ease development, I have provided a
solution version of the software and also a buggy version of the software in
the rentacat-solution-1.0.0.jar file.  The JAR file includes the CatSolution
and RentACatSolution classes along with CatBuggy and RentACatBuggy classes.
Being a JAR file, the source code of those classes are not available to you
(for obvious reasons), but you can still invoke them.

In order to create solution versions of the Cat and RentACat classes do the
following in the @Before setUp() method:

```
c1 = Cat.createInstance(InstanceType.SOLUTION, 1, "Jennyanydots");
```
```
r = RentACat.createInstance(InstanceType.SOLUTION);
```

In order to create buggy versions, do the following:

```
c1 = Cat.createInstance(InstanceType.BUGGY, 1, "Jennyanydots");
```
```
r = RentACat.createInstance(InstanceType.BUGGY);
```

If you implemented your test case correctly, it should always pass for the
solution object and it should almost always fail for the buggy object.  There
are only 3 exceptions where the buggy object passes and they are:
RentACatIntegrationTest.testGetCatNullNumCats0(),
RentACatUnitTest.testGetCatNullNumCats0(), and
RentACatUnitTest.testGetCatNumCats3().

After you are done writing the test cases, please don't forget to revert back
to the IMPL InstanceType, to be able to test your own code for the green phase.

## Measuring Code Coverage

Code coverage is a metric that measures what percentage of the code base a
particular test run covered.  There are several ways to measure code coverage,
but the most widespread method is to measure the percentage of code lines
covered.  Typically a code coverage of above 80\% or 90\% is targeted in
software organizations.  I will require that level of coverage for the
Deliverable.  Since this is just an exercise, the minimum coverage is set to be
20%, which you should be able to achieve easily.

Jacoco (**Ja**va **Co**de **Co**verage tool), is one of the most popular code
coverage measurement tools among Java developers, and that's what we will use
in this class.  Jacoco has already been integrated into the test phase of our
Maven project, so you should already have coverage statistics generated from
your last 'mvn test' run at:

```
target/site/jacoco/
```

Now, if any of your JUnit tests failed, Jacoco will not generate the report.
I recommend that you makes your tests pass before running it.  If you want
to force Jacoco to produce the report even with test failures, do:

```
mvn jacoco:report
```

The statistics are generated XML (jacoco.xml), CSV (jacoco.csv), and HTML
(index.html) formats.  The XML and CSV formats are designed to be easily
readable by later stages of the testing pipeline that automatically generate
reports or send notifications to developers.  The HTML format is meant for
human cosumption.  Try opening index.html and drill down to either the CatImpl
class or the RentACatImpl class, which are the classes under test which we are
interested in measuring code coverage for.  If you have implemented all the
test cases, it should look similar to the following screenshots:

<img alt="Code Coverage Jacoco" src=code_coverage_cat.png width=700>

<img alt="Code Coverage Jacoco" src=code_coverage_rentacat.png width=700>

## Additional Requirements

* Code coverage of the class CoffeeMakerQuestImpl when the JUnit TestRunner is
  run should be at an absolute minimum of **90%**.  If coverage falls below
that number, add more unit tests to CoffeeMakerQuestTest.  View the detailed
line-by-line Jacoco coverage report for CoffeeMakerQuestImpl to see which lines
you are missing and come up with test cases that are able to hit those lines.

* For this program, no requirements are given as the requirement is that you
  mimic the output of the given **coffeemaker.jar** file (note that this jar
file is slightly different from the version provided to you for Deliverable 1
as I have fixed most of the bugs!).  If GradeScope gives you a failure because
your output is different from the reference output, it will show you where the
difference is between brackets [].  In fact, GradeScope itself uses JUnit
behind the scenes to test your program and showing the difference in brackets
is a JUnit assertEquals feature.

* You are asked to complete CoffeeMakerQuestImpl, but there are other support
  classes as well such as Player and Room.  You are expected to use the methods
provided in those classes and not repeat the code somewhere else.  In fact,
this is an important software testability principle called **DRY (Don't Repeat
Yourself)**.  For example, the Player class has the method
**Player.getInventoryString** that prints out the inventory contents based on
the current items.  You are required to use that method and not implement a
similar method of your own.

* Write at least one **private method** while implementing
  CoffeeMakerQuestImpl.  In general, private methods of a Java class work as
"helper" methods that implement a sub-functionality of a public method.  You
have the freedom to choose what sub-functionality you want to encapsulate
within a private method.  Also, add at least one unit test that directly tests
a private method at the very bottom of CoffeeMakerQuestTest.  Use **Java
reflection** to do this.

* Coding style is also important for software quality in the long run (even
  though they are not technically defects as we learned).  In particular, a
uniform naming convention greatly improves the readability of your code.  A
widely used convention is called
[lowerCamelCase](https://en.wikipedia.org/wiki/Naming_convention_(programming)#Java)
convention.  That is the convention that was [first adopted when Sun
Microsystems first created the Java
language](https://www.oracle.com/technetwork/java/codeconventions-135099.html).
This is still the convention at the biggest companies using Java like
[Oracle](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html)
and [Google](https://google.github.io/styleguide/javaguide.html#s5-naming).
Please make sure you follow the lower camel case convention for all your
variables and methods for this project.  There is less agreement on other
formatting issues like indentation and line wrapping, but try to maintain a
uniform convention whatever you choose.

# Grading

* GradeScope autograder: 70% of grade
* Private method added and tested: 5% of grade
* Source code style (lower camel case naming / formatting): 10% of grade
* Report (including coverage stats): 15% of grade

Please review the grading_rubric.txt for details.

# Submission

Each group will do one submissions to GradeScope as usual.

The submission is done in two parts:

1. Submit your GitHub Classroom Deliverable 2 repository to GradeScope at the
   **Deliverable 2 GitHub** link.  Once you submit, GradeScope will run the
autograder to grade you and give feedback.  If you get deductions, fix your
code based on the feedback and resubmit.  Repeat until you don't get
deductions.

1.  Please use the [ReportTemplate.docx](ReportTemplate.docx) file provided in
    this directory to write a short report.  A PDF version of the file is at
[ReportTemplate.pdf](ReportTemplate.pdf).  On the first page introduction,
please describe the division of work between group members and also any
difficulties you faced while using JUnit.  On the second page, paste a
screenshot of code coverage stats **after** having completed the coding.
Please refer to [Exercise 2](/exercises/2#measuring-code-coverage) on how to
create the screenshot.  Submit to GradeScope at the **Deliverable 2 Coverage**
link.  Your screenshot should look like this:

   <img alt="Code Coverage Jacoco" src=code_coverage_jacoco.png>

   Make sure that the coverage of CoffeeMakerQuestImpl is showing and the
overall coverage is above **90%** as shown above.

# GradeScope Feedback

It is encouraged that you submit to GradeScope early and often.  Please use the
feedback you get on each submission to improve your code!

The GradeScope autograder works in 3 phases:

1. CoffeeMakerQuestImpl verification using CoffeeMakerQuestTestSolution:
   CoffeeMakerQuestTestSolution is the solution implementation of
CoffeeMakerQuestTest.  The purpose of this phase is to verify that CoffeeMakerQuestImpl (your CoffeeMakerQuest implementation) does not have any defects.

1. CoffeeMakerQuestTest on CoffeeMakerQuestSolution: CoffeeMakerQuestTest is your submitted JUnit test for CoffeeMakerQuest.  The purpose of this phase is
   to test CoffeeMakerQuestTest itself for defects.  CoffeeMakerQuestSolution is the solution implementation of CoffeeMakerQuest and contains no defects (that I know of).  Hence, all tests in CoffeeMakerQuestTest should pass.

1. CoffeeMakerQuestTest on CoffeeMakerQuestBuggy: CoffeeMakerQuestTest is your submitted JUnit test for CoffeeMakerQuest.  The purpose of this phase is
   to test CoffeeMakerQuestTest against the buggy CoffeeMakerQuestBuggy
implementation.  The class CoffeeMakerQuestBuggy is given to you as part of
the coffeemaker.jar file.  Since CoffeeMakerQuestBuggy is buggy, you
expect the tests to fail this time.  If CoffeeMakerQuestTestSolution fails a
test but CoffeeMakerQuestTest passes a test (or vice versa), then this indicates a problem.

# Groupwork Plan

Just like for Exercise 2, I recommend that you divide the list of methods to
implement / test into two halves and working on one half each.  Please document
how you divided the work in your report.

# Resources

These links are the same ones posted at the end of the slides:

* JUnit User manual:  
https://junit.org/junit5/docs/current/user-guide/  
The Writing Tests section is probably the most useful.

* JUnit Reference Javadoc:  
http://junit.sourceforge.net/javadoc/  
For looking up methods only, not a user guide.

* Mockito User Manual:  
https://javadoc.io/static/org.mockito/mockito-core/3.2.4/org/mockito/Mockito.html  
Most useful is the sections about verification and stubbing.

* Jacoco User Manual:  
https://www.jacoco.org/userdoc/index.html
