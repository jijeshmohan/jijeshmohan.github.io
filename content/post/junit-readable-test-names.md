+++
date = "2011-12-17T17:46:00+05:30"
draft = false
title = "jUnit – Readable test names"
description="JUnit – Readable test names"
keywords = ["java", "junit","unit test"]
categories = [ "Testing","Java" ]
author = "Jijesh Mohan"
socialsharing = true
notoc = true
+++

Java camel-case function names are readable if it has only two or three words in it. Test names are little longer for specifying the context and what it’s testing. This is anyway better than adding a detailed comment for the test which will get outdated pretty soon.

The problem comes when reading the jUnit test report which contains big names. It is hard to read such test names. Here are some of the tests from the famous webdriver project:

{{< figure src="/img/junit_eclipse_plugin_1.png" >}}

These are pretty long names, Isn’t it!

One option to make it readable is to use snake-case 
``eg. test_should_return_null_when_getting_the_value_of_an_attribute_that_is_not_listed.``


But this will be a violation towards java coding style, Also it is difficult to follow two standards in TDD(snake-case for tests and camel-case for normal functions).

Another option is to make a custom runner in jUnit which converts camel-case tests names to readable text (humanize) . Here is the code

```java
public class ReadableTest extends BlockJUnit4ClassRunner {
 @Override
 protected String testName(FrameworkMethod method) {
 	return StringUtil.humanize(method.getMethod().getName());
 }
 public ReadableTest(Class<?> klass) throws InitializationError {
    super(klass);
 }
}
```

Annotate the jUnit Test class with this runner ``eg: @RunWith(ReadableTest.class)`` and run your tests.

That’s it. See the following screenshot

{{< figure src="/img/junit_eclipse_plugin.png" >}}


The same humanized test names can be seen in Jenkins also.
