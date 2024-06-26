---
layout: default
title: What I learned
parent: Network
nav_order: 1
---

# What I learned

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Unit Testing

> Unit Testing is a fundamental aspect of software testing where individual components or functions of a software application are tested in isolation.

This approach ensures that each unit of a software performs as expected

```python
# Import the unittest library and our function
import unittest
from prime import is_prime

# A class containing all of our tests
class Tests(unittest.TestCase):

    def test_1(self):
        """Check that 1 is not prime."""
        self.assertFalse(is_prime(1))

    def test_2(self):
        """Check that 2 is prime."""
        self.assertTrue(is_prime(2))

    def test_8(self):
        """Check that 8 is not prime."""
        self.assertFalse(is_prime(8))

# Run each of the testing functions
if __name__ == "__main__":
    unittest.main()
```



## Client Testing

This testing approach ensures that individual web pages load as intended. In Django, this can be done by using a **Client**.

```python
from django.test import Client, TestCase

def test_index(self):

    # Set up client to make requests
    c = Client()

    # Send get request to index page and store response
    response = c.get("/flights/")

    # Make sure status code is 200
    self.assertEqual(response.status_code, 200)

    # Make sure three flights are returned in the context
    self.assertEqual(response.context["flights"].count(), 3)
```

## CI/CD

**Continuous Integration and Continuous Delivery** is a set of best practices that ensure code written by a team adheres to a certain standard.

- Continuous Integration:
    - Frequent merges to the main branch
    - Automated unit testing with each merge

- Continuous Delivery:
    - Short release schedules

CI/CD is incredibly useful for identifying issues immediately and frequent releases.

## GitHub Actions

GitHub Actions allow developers to create workflows where certain actions will be performed everytime someone pushes to a git repository. This is a tool used in CI/CD. It can ensure new pushes do not break any old systems and that new code will adhere to a certain style. 