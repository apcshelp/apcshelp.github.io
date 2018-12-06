# Anagram solving tutorial
 We will say that two words are anagrams of each other if the following conditions are met:
  1. If both words are the same length
  2. If each word contains the letters of each other exactly once.

 There are a couple of ways that you can tackle this problem. The following are what you can use:

  1. Create two arrays of the individual strings, check their lengths, and make sure each is only contained once.
  2. Use the substring method with Strings to compare and modify the two words using a for loop.

 Since you haven't learned arrays yet, here is how you should approach it.
 
 ## Step 1: Creating your method
 
 You should know how to do this already, but in case you don't:
   1. Our method is going to be a ``boolean`` type. We know this because the end result is whether or not two words are anagrams. Since the result will be either ``true`` or ``false``, we know this is a boolean method.
   2. Our method will have two parameters - both will be ``String`` because they will both be words.
  Based on this, your method will look like the following:

```java
  public static boolean isAnagram(String word1, String word2) {
      // Code here
  }
```

Now that we have our method, we can start working.

## Step 2: Preliminary checks

This solution method ensures that both of the words are **identical in length**. Because of this, we can immediately return ``false`` if the two strings aren't the same lengths (going back to the initial conditions we came to above):

```java
  public static boolean isAnagram(String word1, String word2) {
      if(word1.length() != word2.length()) {
        return false;
      }
      
      // Other stuff here
  }
```

## Step 3: String checks: An iterative approach

The easiest way to go about the checks for anagrams is the following:

1. Go through each character of the first string.
2. Get the position of the character in the second string.
3. If the position in the second string is *less than zero*, then the character doesn't exist in the second string. if this is the case, then the two words **are not anagrams**. 
4. If it exists in the second string, then remove the character at that position. You will need what is called a *helper method* for this.
5. 

If this were in pseudocode, it would look something like this:

```
for character in string1:
  int position = string2.indexOf(character)
  if position < 0:
    return false
  removeCharacter(string2, position)
```

Putting this into Java, we get....

```java
for(int i = 0; i < string1.length(); i++) { // We are starting at pos 0 (first character).
 char character = string1.charAt(i);
 int position = word2.indexOf(character);
 if(position < 0) {
     return false;
 }
 word2 = removeCharacter(word2, position);
}
return true;
```
Of course, this won't work perfectly yet - we still have to write our helper method.

## Step 3: The helper method
To write this helper method, we are going to create a copy of the string provided with the character at position ``i`` removed. Because strings are **immutable** (meaning we can't modify them directly), our process will be this:
1. Start with the original character
2. If the string is of length 1 or less, we can return an empty string.
3. Otherwise....
4. Return a new string using substring: The first part will be from positions 0 to i, and the second part will be 0 to i+1. We know this because substring goes inclusive to exclusive.
For example, if we have the following String:

(for these table representations, the number is the position of the character and the character is represented in each cell).

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| H | e | l | l | o |

and we call ``removeAt(word, 3)``:

Part one, represented by ``substring(0, 3)``, will be:

| 0 | 1 | 2 |
|---|---|---|
| H | e | l |

And part two, represented by ``substring(4, word.length())``, will be:

| 0 |
|---|
| o |

Putting these together by concatenating the strings (``word1 + word2``), we get....

| 0 | 1 | 2 | 3 |
|---|---|---|---|
| H | e | l | o |

**We do have some preconditions, however**. The position to remove the character of plus one must be less than the word's length. For example, we can't remove anything at position 8 for the string "hello" since the length is only 5 (the max would be 4 since strings are 0-indexed)!

Based on this, the code will look like this:
```java
public static String removeAt(String word, int position) {
  if(word.length() == 1 || position+1 >= word.length()) {
      return "";
  }
  String part1 = word.substring(0, position);
  String part2 = word.substring(position+1, word.length());
  return part1 + part2;
}
```
Now, we can piece these together and get our solution.

## Step 4: The final solution

To get the final solution of this problem, just make sure you have your helper method and main method together in the same class.

**If you just skipped to this section to copy-and-paste the code: Please don't. You will learn a lot more by going through the process and writing your own code. You won't be able to copy-and-paste code on the AP test.**


## Step 5: Additional Resources
If you are struggling to understand any of these concepts, please try https://codingbat.com for additional practice exercises. You can practice Strings, recursion, boolean logic, and more to help you get acquainted with it and improve.
