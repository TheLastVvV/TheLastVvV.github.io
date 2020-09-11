---
title: Automated testing in C++ with Google Tests.
excerpt: Learn the automation of testing in C++ using Google Tests.
show_hero: false
categories:
- Learn
tags:
- C++
- Testing
- Automation
- GoogleTests
date: 2019-07-16 00:40 +0530
---
The goal of testing is to verify the correctness, reliability and stability
of an application.

## Types of testing

1. Unit testing
2. Integration testing
3. Acceptance testing

As developers we perform only unit testing and integration testing.

**Unit testing** is used to isolate a block of code and test it.
**Integration testing** used is for verifying the correctness of an
application when integrated with other components.
**Acceptance testing** is used by the end user to test the software for
accepting it.

## Grouping test suites

The tests are grouped as:

1. **Functional tests** to verify the working of an application for a set of
   correct inputs.
2. **Error handling tests** to verify the error handling abilty of an
   application for a set of error inputs.
3. **Input combination tests** to verify the behavior and correctness of an
   application for all possible inputs.
4. **Boundary tests** to verify the edge cases and limits of an application.
5. **Performance tests** to verify time and space requirements of an
   application.

## Block diagram

![Automated unit testing block diagram][TestingBlockDiagram]

## Example: Correct the Spelling app

Let's take a sample application which corrects the spelling when you give it a
word in english. This application is used to solve the jumbled words puzzle.
It was written by me when I could not solve the jumbled words puzzle sent to me
by my friends.

Today we use this application to learn how to automate unit testing using the
Google Tests library.

### Brief discussion of the app

The code for the application is hosted on github at [CTS][cts].

- **Application** corrects the spelling (CorrectSpell.cpp).
- **Dependents** NA, (main.cpp).
- **Dependencies** spell checker libraries such as Gnu's Aspell
  (AspellChecker.cpp).
- **Test Code** tests for main code (test_CorrectSpell.cpp).
- **Mock Dependencies** not used but maybe required to mock aspell.

The code for the application logic is self explanatory and it is in `inc` and
`src` folders.
The code for automating unit testing using GoogleTests is written in
`test/test_CorrectSpell.cpp` file. The test code for other interfaces such as
the spell checker interface and spell checker classes are not written to save
my time. 

You are encouraged to implement the same and hence learn to use Google
Tests library to automate testing for C++ applications.
{: .lead} 

The screenshot of the test binary `test_CorrectTheSpelling` executed in my
system is provided below for your reference.

![Google Tests screenshot][GoogleTestsRunScreenShot]

## References

To learn more about automated unit testing using Google Tests in real world
applications go through the test code in [OpenCV][opencv]. It uses Google Tests
with some modifications to automate the testing process for the entire opencv
library. The opencv library is big enough to provide us with the immense
intricate knowledge required to implement an automated testing system.

[cts]: https://github.com/manid2/ProgramsForFun/tree/master/Applications/CorrectTheSpelling/
[opencv]: https://github.com/opencv/opencv

[TestingBlockDiagram]: {{ '/assets/images/' | relative_url |
append: "/post_cpp_auto_testing/automated_unit_testing_block_diagram.jpg" }}
[GoogleTestsRunScreenShot]: {{ '/assets/images/' | relative_url |
append: "/post_cpp_auto_testing/automated_unit_testing_screenshot.jpg" }}
