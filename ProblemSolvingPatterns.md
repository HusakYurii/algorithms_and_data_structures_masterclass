The 1st challenge was aimed to practice the Problem Solving Patterns such as:

1. Frequency Counter
   This pattern uses a classic Object or Map object to collect unique keys. Each key has a value that represents the number of times the key has been encountered value.
   This approach takes O(n) Time complexity to collect the data.

   Example:

```javascript
/*
  Write a function called sameFrequency(firstNumber, secondNumber). Given two positive integers, find out if the two numbers have the same frequency of digits.
  
  Your solution MUST have the following complexities:
  Time: O(n)
*/
function sameFrequency(firstNumber, secondNumber) {
  const firstNumberString = String(firstNumber);
  const secondNumberString = String(secondNumber);

  if (firstNumberString.length !== secondNumberString.length) {
    return false;
  }

  const frequencyData = {};

  for (let char of firstNumberString) {
    frequencyData[char] =
      frequencyData[char] === undefined ? 1 : ++frequencyData[char];
  }

  for (let char of secondNumberString) {
    if (frequencyData[char] > 0) {
      frequencyData[char] -= 1;
    } else {
      return false;
    }
  }

  return true;
}

sameFrequency(182, 281); // true
sameFrequency(34, 14); // false
sameFrequency(22, 222); // false

/*
    Implement a function called, areThereDuplicates(...args) which accepts a variable number of arguments, and checks whether there are any duplicates among the arguments passed in. You can solve this using the Frequency Counter pattern.

    Restrictions:
    Time: O(n);
    Space: O(n);
    
*/
function areThereDuplicates(...inputs) {
  const data = {};
  for (const value of inputs) {
    if (data[value] !== undefined) {
      return true;
    }
    data[value] = 1;
  }
  return false;
}

areThereDuplicates(1, 2, 3); // false
areThereDuplicates(1, 2, 2); // true

/*
    Write a function that gets a list of values and check how many times a value has been being requested.
    Time: O(n);

    That task could be solved by using 2 nested for loops, but that would cost O(n^2);
*/
function countItems(values) {
  return values.reduce((acc, value) => {
    if (!acc[value]) acc[value] = 1;
    else acc[value] += 1;
    return acc;
  }, {});
}

console.log(countItems(["banana", "apple", "kiwi", "lemon", "apple"]));
// { banana: 1, apple: 2, kiwi: 1, lemon: 1 }
```

2. Multiple Pointers
   This approach uses two pointers that point at values in the data, usually in a sorted array, so we can compare them.
   This approach takes O(n) of O(n + m) Time complexity.

Example:

```javascript
/*
    Implement a function called, areThereDuplicates(...args) which accepts a variable number of arguments, and checks whether there are any duplicates among the arguments passed in. You can solve this using the Multiple Pointers pattern.

    Restrictions:
    Time: O(n log n);
    Space: O(n);
*/

function areThereDuplicatesTwoPointers(...inputs) {
  // The Array.prototype.sort() method should work Time O(n log n)
  // Then the for loop will take O(n)
  inputs.sort();
  for (let i = 0; i < inputs.length - 1; i++) {
    if (inputs[i] === inputs[i + 1]) {
      return true;
    }
  }
  return false;
}

areThereDuplicates("a", "b", "c", "a"); // true
areThereDuplicates(1, 2, 3); // false

/*
    Write a function called averagePair(numbers, targetAverage). Given a sorted array of integers and a target average, determine if there is a pair of values in the array where the average of the pair equals the target average. There may be more than one pair that matches the average target.

    Restrictions:
    Time: O(n);
    Space: O(1);
*/

function averagePair(numbers, targetAverage) {
  if (numbers.length < 2) {
    return false;
  }

  let leftPointer = 0;
  let rightPointer = numbers.length - 1;

  while (leftPointer < rightPointer) {
    const average = (numbers[leftPointer] + numbers[rightPointer]) / 2;
    if (average === targetAverage) {
      return true;
    }
    if (average < targetAverage) {
      leftPointer += 1;
    } else {
      rightPointer -= 1;
    }
  }

  return false;
}

averagePair([1, 2, 3], 2.5); // true
averagePair([1, 3, 3, 5, 6, 7, 10, 12, 19], 8); // true
averagePair([-1, 0, 3, 4, 5, 6], 4.1); // false

/*
    Write a function called isSubsequence(characters, string) which takes in two strings and checks whether the characters in the first string form a subsequence of the characters in the second string. In other words, the function should check whether the characters in the first string appear somewhere in the second string, without their order changing.

    Your solution MUST have AT LEAST the following complexities:
    Time Complexity: O(n + m)
    Space Complexity:  O(1)
*/

function isSubsequence(characters, string) {
  // if the string is shorter then the characters, return false
  if (string.length < characters.length) {
    return false;
  }
  // create two pointers, the first one is for the characters
  // the second for the string
  let characterPointer = 0;
  let stringPointer = 0;
  // run the while loop with the condition where the first pointer should be within the characters length
  while (characterPointer < characters.length) {
    // Compare the current values of characters and the string
    const sameValue = characters[characterPointer] === string[stringPointer];
    // if the values are the same move the 1st and the 2nd pointers to the right
    if (sameValue) {
      characterPointer += 1;
      stringPointer += 1;
    } // if not, move ONLY the 2nd pointer to the right
    else {
      stringPointer += 1;
    }
    // if we went through the string and we still in this while loop => return FALSE
    if (stringPointer > string.length) {
      return false;
    }
  }
  // otherwise the loop will finish and we return true
  return true;
}

isSubsequence("hello", "hello world"); // true
isSubsequence("sing", "sting"); // true
isSubsequence("abc", "abracadabra"); // true
isSubsequence("abc", "acb"); // false (order matters)
```

3. Sliding Window

4. Dive and Conquer
