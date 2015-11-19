# XCTestCheatSheet


[![Language](https://img.shields.io/badge/Language-Swift_2-orange.svg)](https://developer.apple.com/swift) ![License](https://img.shields.io/badge/License-MIT-blue.svg) [![Platforms](https://img.shields.io/badge/Platforms-iOS | OS X | tvOS | watchOS-lightgrey.svg)](https://developer.apple.com/)

A simple list of XCTest setup functions and assertions.

## XCTestCase

###Class Set Up and Tear Down
For each test class, testing starts by running the **class** `setUp()` method and ends with the **class** `tearDown()` method. You can override both class methods to run custom code before and after all of the test methods in the class execute.

```
override class func setUp() {
    // custom setup before any tests run
}

override class func tearDown() {
    // custom teardown after all tests have run
}
```

###Instance Set Up and Tear Down
For each test method, a new instance of the class is allocated and its **instance** `setUp()` method executed. After that it runs the test method, and after that the **instance** `tearDown()` method. This sequence repeats for all the test methods in the class. After the last test method teardown in the class has been run, Xcode executes the class teardown method and moves on to the next class.

```
override func setUp() {
    super.setUp()
    // called before the invocation of each test method in the class
}

override func tearDown() {
    // called before the invocation of each test method in the class
    super.tearDown()
}
```

### Functional Test Case

Each instance method in a XCTestCase subclass with a name that begins with 'test' is recognised as a test, and evaluates any assertions within the function to produce a test result.

```
func testExample() {
    // Code to test
}
```

### Performance Test Case
A performance test takes a block of code and runs it ten times, calculating the average execution time and the standard deviation for the runs. The averaging of these individual measurements can then be compared against a baseline to evaluate test success or failure.

```
func testPerformanceExample() {
    self.measureBlock {
        // Code to performance test
    }
}
```

### Asynchronous Test Case
With the aid of the XCTestExpectation class you are able to test asynchronous code by waiting for the completion of an asynchronous callback or timeout.

```
func testAsyncExample() {
    // Create an expectation object.
    let expectation = expectationWithDescription("Appropriate test name")
    
    // Execute the asynchronous function you wish to test
    exampleAsyncFunc() { (results, error) -> Void in
        // Provide various assertions on results
        
        // If callback fulfilled
        expectation.fulfill()
    }
    
    // The test will pause until the timeout, in this case 2 seconds, is hit or all expectations are fulfilled.
    waitForExpectationsWithTimeout(2) { error in
    
    }
}
```

### Common Assertions
A list of commonly used XCTest assertions.

| Assertion                           | Comment                                |
|--------------------------------------|----------------------------------------|
| `XCTAssert(expression, format…)`     | Generates a pass when expression evaluates to `true`.|
| `XCTAssertTrue(expression, format...)`| Generates a pass when expression evaluates to `true`. |
| `XCTAssertFalse(expression, format...)`| Generates a pass when expression evaluates to `false`. |
| `XCTAssertEqual(expression1, expression2, format…)`| Generates a pass when expression1 is equal to expression2.|
| `XCTAssertNotEqual(expression1, expression2, format…)`    | Generates a pass when expression1 is NOT equal to expression2.|
|`XCTAssertGreaterThan[OrEqual](expression1, expression2, format...)`|Generates a pass when expression1 is greater than [or equal] to expression2.|
|`XCTAssertLessThan[OrEqual](expression1, expression2, format...) `|Generates a pass when expression1 is less than [or equal] to expression2.|
| `XCTAssertEqualWithAccuracy(expression1, expression2, accuracy, format...)` | Generates a pass when expression1 is equal to expression2 within a given accuracy. Useful when comparing `Float` or `Double` values. |
| `XCTAssertNotEqualWithAccuracy(expression1, expression2, accuracy, format...)` | Generates a pass when expression1 is NOT equal to expression2 within a given accuracy. Useful when comparing `Float` or `Double` values. |
| `XCTAssertNil(expression, format...)` | Generates a pass when expression is `nil`. |
| `XCTAssertNotNil(expression, format...)` | Generates a pass when expression is NOT `nil`. |
| `XCTFail(format...)` | Unconditional failure, sometimes used as a placeholder for draft tests. |






