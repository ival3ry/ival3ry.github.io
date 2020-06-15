---
title: '[C] Very simple unit-test framework'
published: true
---

## Intro
In this note I want to share with you implementation of very simple unit-test framework. I think it will be superfluous to say how much the tests are important in software development.  

## Code  
```c
/* unit_test.h */
#ifndef UNIT_TEST_H
#define UNIT_TEST_H

#define UNIT_ASSERT(test, error_message)     \
  do {                                       \
    if (!(test)) return error_message;       \
  } while (0)

#define UNIT_RUN_TEST(test)                    \
  do {                                         \
    char *error_message = test();              \
    if (error_message) return error_message;   \
  } while (0);

#endif
```  
The End! :) The Unit-Test framework is ready. Let's see the example of how to use.

## How to use  
```c
/* run.c */
#include "unit_test.h"
#include <stdio.h>

/* We will test this function */
int test_me(const int num1, const int num2) { return num1 + num2; }

/* Should test one thing */
char *test_test_me()
{
  UNIT_ASSERT(test_me(2, 2) == 4, "error:test_me: 2 + 2 != 4");

  return 0;
}

/* Run all needed test */
char *run_tests()
{
  UNIT_RUN_TEST(test_test_me);
  /* Add new test here */
  
  return 0;
}

int main(void)
{

  char *result = run_tests();
  if (result != 0) {
    printf("%s\n", result);
  } else {
    printf("Tests passed\n");
  }

  return 0;
}
```  
## Conclusion  
This unit-test framework is simple, lightweight but useful! Use, improve and test your code! :)  


