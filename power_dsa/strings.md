# Complete Comprehensive Notes on Character Arrays and Strings

## Table of Contents
1. [Character Variables vs Character Arrays](#character-variables-vs-character-arrays)
2. [What are Strings?](#what-are-strings)
3. [Core String Fundamentals](#core-string-fundamentals)
4. [Character Handling](#character-handling)
5. [String Traversal Techniques](#string-traversal-techniques)
6. [Frequency Counting](#frequency-counting)
7. [Two Pointer Technique](#two-pointer-technique)
8. [Sliding Window Pattern](#sliding-window-pattern)
9. [Palindrome Concepts](#palindrome-concepts)
10. [Anagram Concepts](#anagram-concepts)
11. [Pattern Matching](#pattern-matching)
12. [Substring vs Subsequence](#substring-vs-subsequence)
13. [String Building & Modification](#string-building-and-modification)
14. [String Pool and Memory Management](#string-pool-and-memory-management)
15. [Complete Problem Solutions](#complete-problem-solutions)

---

## Character Variables vs Character Arrays

### Character Variables
A single character variable can only store **one character**.

```cpp
char a = 'z';  // Stores only one character
```

**Memory Representation:**
```
+---+
| z |  <- Variable 'a'
+---+
```

### Problem with Character Variables
If you want to store a name like "Babbar" (6 characters), a single character variable cannot do it.

**Solution:** Use Character Arrays or Strings

---

## What are Strings?

### Definition
- In C++: A **1-dimensional character type array**
- A string is a sequence/collection of characters

```cpp
// String representation
char name[] = {'B', 'a', 'b', 'b', 'a', 'r', '\0'};
```

**Memory Representation:**
```
Index:  0    1    2    3    4    5    6
      +----+----+----+----+----+----+----+
      | B  | a  | b  | b  | a  | r  | \0 |
      +----+----+----+----+----+----+----+
```

---

## Core String Fundamentals

### Null Character (String Terminator)

#### What is Null Character?
- Symbol: `\0`
- ASCII Value: **0**
- Purpose: Acts as a **terminator** to mark the end of a string

```cpp
char name[20];
cin >> name;  // Input: "love"
```

**Automatic Null Character Addition:**
```
Index:  0    1    2    3    4
      +----+----+----+----+----+
      | l  | o  | v  | e  | \0 |
      +----+----+----+----+----+
```

### Multiple Null Characters

```cpp
char arr[] = {'a', '\0', 'b', '\0', 'c', '\0'};
cout << arr;  // Output: a
```

**Why?** Printing stops at the **first** null character encountered.

---

## Character Handling

### Understanding `'a'` vs `"a"`

```cpp
// Single character (char)
char ch = 'a';      // Single quotes - primitive type
cout << sizeof(ch); // 1 byte

// String (char array or string)
char str[] = "a";   // Double quotes - array with 'a' and '\0'
cout << sizeof(str); // 2 bytes ('a' + '\0')
```

```java
// Java
char c = 'a';       // Primitive - 2 bytes (Unicode)
String s = "a";     // Object - reference to String object
```

```python
# Python
ch = 'a'           # Single character string
s = "a"            # String
# Python doesn't have char type, only strings
```

**Key Differences:**

| Aspect | `'a'` (char) | `"a"` (String) |
|--------|--------------|----------------|
| Type | Character | String/Array |
| Memory | 1 byte (C++) / 2 bytes (Java) | Multiple bytes |
| Null terminator | No | Yes (C/C++) |
| Manipulation | Direct value | Array operations |

### ASCII Values

```cpp
// Character to ASCII
char ch = 'A';
int ascii = ch;  // ascii = 65
cout << (int)'A';  // 65

// ASCII to Character
int value = 97;
char ch = (char)value;  // ch = 'a'

// Important ASCII values
// 'A' = 65, 'Z' = 90
// 'a' = 97, 'z' = 122
// '0' = 48, '9' = 57
// Space = 32
```

```java
// Java
char ch = 'A';
int ascii = (int)ch;  // ascii = 65
char fromAscii = (char)97;  // 'a'
```

```python
# Python
ch = 'A'
ascii_val = ord(ch)  # 65
char_from_ascii = chr(97)  # 'a'
```

**ASCII Table (Important Range):**
```
Digits:    '0'-'9'   → 48-57
Uppercase: 'A'-'Z'   → 65-90
Lowercase: 'a'-'z'   → 97-122
Space:     ' '       → 32
```

### Case Conversion

```cpp
// Uppercase to Lowercase
char toUpperToLower(char ch) {
    if(ch >= 'A' && ch <= 'Z') {
        return ch + 32;  // or ch - 'A' + 'a'
    }
    return ch;
}

// Lowercase to Uppercase
char toLowerToUpper(char ch) {
    if(ch >= 'a' && ch <= 'z') {
        return ch - 32;  // or ch - 'a' + 'A'
    }
    return ch;
}

// Using built-in functions (C++)
#include <cctype>
char lower = tolower('A');  // 'a'
char upper = toupper('a');  // 'A'
```

```java
// Java
char lower = Character.toLowerCase('A');  // 'a'
char upper = Character.toUpperCase('a');  // 'A'
```

```python
# Python
lower = 'A'.lower()  # 'a'
upper = 'a'.upper()  # 'A'
```

**How Case Conversion Works:**
```
ASCII difference between 'a' and 'A' = 97 - 65 = 32

To convert 'B' to 'b':
Method 1: 'B' + 32 = 66 + 32 = 98 = 'b'
Method 2: 'B' - 'A' + 'a' = 66 - 65 + 97 = 98 = 'b'
```

### Checking Character Types

```cpp
bool isAlphabet(char ch) {
    return (ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z');
}

bool isDigit(char ch) {
    return (ch >= '0' && ch <= '9');
}

bool isUpperCase(char ch) {
    return (ch >= 'A' && ch <= 'Z');
}

bool isLowerCase(char ch) {
    return (ch >= 'a' && ch <= 'z');
}

bool isAlphanumeric(char ch) {
    return isAlphabet(ch) || isDigit(ch);
}

bool isSpecialChar(char ch) {
    return !isAlphanumeric(ch) && ch != ' ';
}

// Using built-in functions (C++)
#include <cctype>
isalpha('a');   // true
isdigit('5');   // true
isalnum('A');   // true
isspace(' ');   // true
```

```java
// Java
Character.isLetter('a');      // true
Character.isDigit('5');       // true
Character.isLetterOrDigit('A'); // true
Character.isWhitespace(' ');  // true
```

```python
# Python
'a'.isalpha()    # True
'5'.isdigit()    # True
'A'.isalnum()    # True
' '.isspace()    # True
'a'.isupper()    # False
'A'.isupper()    # True
```

### Character Type Checking - Complete Example

```cpp
void characterAnalysis(string s) {
    int alphabets = 0, digits = 0, special = 0, spaces = 0;
    int uppercase = 0, lowercase = 0;
    
    for(char ch : s) {
        if(isalpha(ch)) {
            alphabets++;
            if(isupper(ch)) uppercase++;
            else lowercase++;
        }
        else if(isdigit(ch)) {
            digits++;
        }
        else if(isspace(ch)) {
            spaces++;
        }
        else {
            special++;
        }
    }
    
    cout << "Alphabets: " << alphabets << endl;
    cout << "Uppercase: " << uppercase << endl;
    cout << "Lowercase: " << lowercase << endl;
    cout << "Digits: " << digits << endl;
    cout << "Spaces: " << spaces << endl;
    cout << "Special: " << special << endl;
}

// Usage
characterAnalysis("Hello World 123!");
// Output:
// Alphabets: 10
// Uppercase: 2
// Lowercase: 8
// Digits: 3
// Spaces: 2
// Special: 1
```

```java
// Java version
public static void characterAnalysis(String s) {
    int alphabets = 0, digits = 0, special = 0, spaces = 0;
    int uppercase = 0, lowercase = 0;
    
    for(char ch : s.toCharArray()) {
        if(Character.isLetter(ch)) {
            alphabets++;
            if(Character.isUpperCase(ch)) uppercase++;
            else lowercase++;
        }
        else if(Character.isDigit(ch)) {
            digits++;
        }
        else if(Character.isWhitespace(ch)) {
            spaces++;
        }
        else {
            special++;
        }
    }
    
    System.out.println("Alphabets: " + alphabets);
    System.out.println("Uppercase: " + uppercase);
    System.out.println("Lowercase: " + lowercase);
    System.out.println("Digits: " + digits);
    System.out.println("Spaces: " + spaces);
    System.out.println("Special: " + special);
}
```

```python
# Python version
def character_analysis(s):
    alphabets = digits = special = spaces = 0
    uppercase = lowercase = 0
    
    for ch in s:
        if ch.isalpha():
            alphabets += 1
            if ch.isupper():
                uppercase += 1
            else:
                lowercase += 1
        elif ch.isdigit():
            digits += 1
        elif ch.isspace():
            spaces += 1
        else:
            special += 1
    
    print(f"Alphabets: {alphabets}")
    print(f"Uppercase: {uppercase}")
    print(f"Lowercase: {lowercase}")
    print(f"Digits: {digits}")
    print(f"Spaces: {spaces}")
    print(f"Special: {special}")

# Usage
character_analysis("Hello World 123!")
```

---

## String Traversal Techniques

### 1. Character-by-Character Traversal (Forward)

```cpp
string s = "hello";

// Method 1: Using index
for(int i = 0; i < s.length(); i++) {
    cout << s[i] << " ";
}

// Method 2: Using iterator
for(char ch : s) {
    cout << ch << " ";
}

// Method 3: Using iterator (C++)
for(string::iterator it = s.begin(); it != s.end(); it++) {
    cout << *it << " ";
}
```

```java
// Java
String s = "hello";

// Method 1: Using charAt
for(int i = 0; i < s.length(); i++) {
    System.out.print(s.charAt(i) + " ");
}

// Method 2: Using toCharArray
for(char ch : s.toCharArray()) {
    System.out.print(ch + " ");
}

// Method 3: Using chars() stream
s.chars().forEach(ch -> System.out.print((char)ch + " "));
```

```python
# Python
s = "hello"

# Method 1: Using index
for i in range(len(s)):
    print(s[i], end=" ")

# Method 2: Direct iteration
for ch in s:
    print(ch, end=" ")

# Method 3: Using enumerate
for i, ch in enumerate(s):
    print(ch, end=" ")
```

### 2. Backward Traversal

```cpp
string s = "hello";

// Method 1: Using index
for(int i = s.length() - 1; i >= 0; i--) {
    cout << s[i] << " ";
}

// Method 2: Reverse iterator (C++)
for(auto it = s.rbegin(); it != s.rend(); it++) {
    cout << *it << " ";
}
```

```java
// Java
String s = "hello";

// Method 1: Using index
for(int i = s.length() - 1; i >= 0; i--) {
    System.out.print(s.charAt(i) + " ");
}

// Method 2: Using StringBuilder
StringBuilder sb = new StringBuilder(s);
System.out.println(sb.reverse().toString());
```

```python
# Python
s = "hello"

# Method 1: Using index
for i in range(len(s)-1, -1, -1):
    print(s[i], end=" ")

# Method 2: Using reversed
for ch in reversed(s):
    print(ch, end=" ")

# Method 3: Slicing
print(s[::-1])
```

### 3. Two-Pointer Traversal (Left-Right)

```cpp
void twoPointerTraversal(string s) {
    int left = 0;
    int right = s.length() - 1;
    
    while(left < right) {
        cout << "Left: " << s[left] << ", Right: " << s[right] << endl;
        left++;
        right--;
    }
}

// Usage
twoPointerTraversal("hello");
// Output:
// Left: h, Right: o
// Left: e, Right: l
```

```java
// Java
public static void twoPointerTraversal(String s) {
    int left = 0;
    int right = s.length() - 1;
    
    while(left < right) {
        System.out.println("Left: " + s.charAt(left) + ", Right: " + s.charAt(right));
        left++;
        right--;
    }
}
```

```python
# Python
def two_pointer_traversal(s):
    left = 0
    right = len(s) - 1
    
    while left < right:
        print(f"Left: {s[left]}, Right: {s[right]}")
        left += 1
        right -= 1
```

### 4. Index vs Character Access

```cpp
string s = "hello";

// Index access - can modify (in some languages)
s[0] = 'H';  // Works in C++
cout << s;   // "Hello"

// Character access - read-only
char ch = s[0];  // Get character
cout << ch;      // 'H'

// Safe access with bounds checking
char ch = s.at(0);  // Throws exception if out of bounds
```

```java
// Java - Strings are immutable
String s = "hello";
char ch = s.charAt(0);  // Can only read, not modify
// s.charAt(0) = 'H';   // ERROR in Java

// Use StringBuilder for mutability
StringBuilder sb = new StringBuilder("hello");
sb.setCharAt(0, 'H');
System.out.println(sb);  // "Hello"
```

```python
# Python - Strings are immutable
s = "hello"
# s[0] = 'H'  # ERROR in Python

# Use list for mutability
s_list = list(s)
s_list[0] = 'H'
s = ''.join(s_list)  # "Hello"

# Or use slicing
s = 'H' + s[1:]  # "Hello"
```

---

## Frequency Counting

### 1. Frequency Array (Fixed Size)

#### For Lowercase Letters Only (26 characters)

```cpp
void frequencyCountLowercase(string s) {
    int freq[26] = {0};  // Initialize all to 0
    
    // Count frequencies
    for(char ch : s) {
        if(ch >= 'a' && ch <= 'z') {
            freq[ch - 'a']++;
        }
    }
    
    // Print frequencies
    for(int i = 0; i < 26; i++) {
        if(freq[i] > 0) {
            cout << (char)('a' + i) << ": " << freq[i] << endl;
        }
    }
}

// Usage
frequencyCountLowercase("hello");
// Output:
// e: 1
// h: 1
// l: 2
// o: 1
```

```java
// Java
public static void frequencyCountLowercase(String s) {
    int[] freq = new int[26];  // All initialized to 0
    
    for(char ch : s.toCharArray()) {
        if(ch >= 'a' && ch <= 'z') {
            freq[ch - 'a']++;
        }
    }
    
    for(int i = 0; i < 26; i++) {
        if(freq[i] > 0) {
            System.out.println((char)('a' + i) + ": " + freq[i]);
        }
    }
}
```

```python
# Python
def frequency_count_lowercase(s):
    freq = [0] * 26
    
    for ch in s:
        if 'a' <= ch <= 'z':
            freq[ord(ch) - ord('a')] += 1
    
    for i in range(26):
        if freq[i] > 0:
            print(f"{chr(ord('a') + i)}: {freq[i]}")

# Using collections.Counter
from collections import Counter

def frequency_count_lowercase_counter(s):
    freq = Counter(ch for ch in s if 'a' <= ch <= 'z')
    for ch, count in sorted(freq.items()):
        print(f"{ch}: {count}")
```

**Mapping Logic:**
```
Character → Index Mapping:
'a' - 'a' = 0
'b' - 'a' = 1
'c' - 'a' = 2
...
'z' - 'a' = 25

Index → Character Mapping:
'a' + 0 = 'a'
'a' + 1 = 'b'
'a' + 2 = 'c'
...
'a' + 25 = 'z'
```

#### For Both Upper and Lowercase (52 characters)

```cpp
void frequencyCountBothCases(string s) {
    int freq[52] = {0};
    // 0-25: lowercase (a-z)
    // 26-51: uppercase (A-Z)
    
    for(char ch : s) {
        if(ch >= 'a' && ch <= 'z') {
            freq[ch - 'a']++;
        }
        else if(ch >= 'A' && ch <= 'Z') {
            freq[26 + (ch - 'A')]++;
        }
    }
    
    // Print lowercase
    for(int i = 0; i < 26; i++) {
        if(freq[i] > 0) {
            cout << (char)('a' + i) << ": " << freq[i] << endl;
        }
    }
    
    // Print uppercase
    for(int i = 26; i < 52; i++) {
        if(freq[i] > 0) {
            cout << (char)('A' + i - 26) << ": " << freq[i] << endl;
        }
    }
}
```

```python
# Python
def frequency_count_both_cases(s):
    freq = [0] * 52
    
    for ch in s:
        if 'a' <= ch <= 'z':
            freq[ord(ch) - ord('a')] += 1
        elif 'A' <= ch <= 'Z':
            freq[26 + ord(ch) - ord('A')] += 1
    
    # Print lowercase frequencies
    for i in range(26):
        if freq[i] > 0:
            print(f"{chr(ord('a') + i)}: {freq[i]}")
    
    # Print uppercase frequencies
    for i in range(26, 52):
        if freq[i] > 0:
            print(f"{chr(ord('A') + i - 26)}: {freq[i]}")
```

#### For All ASCII Characters (128 or 256)

```cpp
void frequencyCountAllASCII(string s) {
    int freq[256] = {0};  // For extended ASCII
    
    for(char ch : s) {
        freq[(unsigned char)ch]++;
    }
    
    // Print frequencies
    for(int i = 0; i < 256; i++) {
        if(freq[i] > 0) {
            cout << (char)i << " (ASCII " << i << "): " << freq[i] << endl;
        }
    }
}
```

```python
# Python
def frequency_count_all_ascii(s):
    freq = [0] * 256
    
    for ch in s:
        freq[ord(ch)] += 1
    
    for i in range(256):
        if freq[i] > 0:
            print(f"{chr(i)} (ASCII {i}): {freq[i]}")
```

### 2. HashMap/Map Usage

#### Basic HashMap Frequency Counting

```cpp
#include <unordered_map>

void frequencyCountHashMap(string s) {
    unordered_map<char, int> freq;
    
    // Count frequencies
    for(char ch : s) {
        freq[ch]++;
    }
    
    // Print frequencies
    for(auto pair : freq) {
        cout << pair.first << ": " << pair.second << endl;
    }
}
```

```java
// Java equivalent
import java.util.HashMap;
import java.util.Map;

public static void frequencyCountHashMap(String s) {
    Map<Character, Integer> freq = new HashMap<>();
    
    for(char ch : s.toCharArray()) {
        freq.put(ch, freq.getOrDefault(ch, 0) + 1);
    }
    
    for(Map.Entry<Character, Integer> entry : freq.entrySet()) {
        System.out.println(entry.getKey() + ": " + entry.getValue());
    }
}
```

```python
# Python
def frequency_count_hashmap(s):
    freq = {}
    
    for ch in s:
        freq[ch] = freq.get(ch, 0) + 1
    
    for ch, count in freq.items():
        print(f"{ch}: {count}")

# Using collections.Counter
from collections import Counter

def frequency_count_counter(s):
    freq = Counter(s)
    for ch, count in freq.items():
        print(f"{ch}: {count}")
```

#### Advanced HashMap Operations

```cpp
// Increment frequency
map[ch]++;

// Decrement frequency
map[ch]--;

// Remove if count becomes zero
if(map[ch] == 0) {
    map.erase(ch);
}

// Check if character exists
if(map.find(ch) != map.end()) {
    // Character exists
}

// Get frequency (with default)
int count = map.count(ch) ? map[ch] : 0;
```

```python
# Python
# Increment frequency
freq[ch] = freq.get(ch, 0) + 1

# Decrement frequency
if ch in freq:
    freq[ch] -= 1
    if freq[ch] == 0:
        del freq[ch]

# Check if character exists
if ch in freq:
    # Character exists

# Get frequency (with default)
count = freq.get(ch, 0)
```

#### Comparing Two Frequency Maps

```cpp
bool areFrequenciesEqual(string s1, string s2) {
    if(s1.length() != s2.length()) return false;
    
    unordered_map<char, int> freq1, freq2;
    
    for(char ch : s1) freq1[ch]++;
    for(char ch : s2) freq2[ch]++;
    
    return freq1 == freq2;
}
```

```python
# Python
def are_frequencies_equal(s1, s2):
    if len(s1) != len(s2):
        return False
    
    freq1, freq2 = {}, {}
    
    for ch in s1:
        freq1[ch] = freq1.get(ch, 0) + 1
    
    for ch in s2:
        freq2[ch] = freq2.get(ch, 0) + 1
    
    return freq1 == freq2

# Using Counter
from collections import Counter

def are_frequencies_equal_counter(s1, s2):
    return Counter(s1) == Counter(s2)
```

### 3. When to Use Array vs HashMap

| Scenario | Use Frequency Array | Use HashMap |
|----------|-------------------|-------------|
| Only lowercase letters | ✓ (size 26) | - |
| Upper + lowercase | ✓ (size 52) | - |
| Known ASCII range | ✓ (size 128/256) | - |
| Unknown character set | - | ✓ |
| Unicode characters | - | ✓ |
| Space efficiency matters | ✓ | - |
| Need flexibility | - | ✓ |
| Faster access | ✓ | - |

### 4. Zero Count Checking

```cpp
bool hasZeroCount(int freq[], int size) {
    for(int i = 0; i < size; i++) {
        if(freq[i] == 0) return true;
    }
    return false;
}

bool allZeroCount(int freq[], int size) {
    for(int i = 0; i < size; i++) {
        if(freq[i] != 0) return false;
    }
    return true;
}
```

```python
# Python
def has_zero_count(freq):
    return any(count == 0 for count in freq)

def all_zero_count(freq):
    return all(count == 0 for count in freq)
```

---

## Two Pointer Technique

### Core Concepts

The two-pointer technique uses two pointers that traverse the data structure from different directions or at different speeds.

### Pattern 1: Pointers Moving Together (Same Direction)

```cpp
// Remove duplicates from sorted array
int removeDuplicates(vector<int>& nums) {
    if(nums.empty()) return 0;
    
    int i = 0;  // Slow pointer
    
    for(int j = 1; j < nums.size(); j++) {  // Fast pointer
        if(nums[i] != nums[j]) {
            i++;
            nums[i] = nums[j];
        }
    }
    
    return i + 1;
}
```

```java
// Java
public int removeDuplicates(int[] nums) {
    if(nums.length == 0) return 0;
    
    int i = 0;  // Slow pointer
    
    for(int j = 1; j < nums.length; j++) {  // Fast pointer
        if(nums[i] != nums[j]) {
            i++;
            nums[i] = nums[j];
        }
    }
    
    return i + 1;
}
```

```python
# Python
def remove_duplicates(nums):
    if not nums:
        return 0
    
    i = 0  # Slow pointer
    
    for j in range(1, len(nums)):  # Fast pointer
        if nums[i] != nums[j]:
            i += 1
            nums[i] = nums[j]
    
    return i + 1
```

### Pattern 2: Pointers Moving Towards Each Other

```cpp
// Two sum in sorted array
vector<int> twoSum(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;
    
    while(left < right) {
        int sum = nums[left] + nums[right];
        
        if(sum == target) {
            return {left, right};
        }
        else if(sum < target) {
            left++;   // Need larger sum
        }
        else {
            right--;  // Need smaller sum
        }
    }
    
    return {-1, -1};
}
```

```python
# Python
def two_sum(nums, target):
    left, right = 0, len(nums) - 1
    
    while left < right:
        current_sum = nums[left] + nums[right]
        
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1  # Need larger sum
        else:
            right -= 1  # Need smaller sum
    
    return [-1, -1]
```

### Pattern 3: Expanding Pointers (From Center)

```cpp
// Expand around center for palindrome
int expandAroundCenter(string s, int left, int right) {
    while(left >= 0 && right < s.length() && s[left] == s[right]) {
        left--;
        right++;
    }
    return right - left - 1;  // Length of palindrome
}
```

```python
# Python
def expand_around_center(s, left, right):
    while left >= 0 and right < len(s) and s[left] == s[right]:
        left -= 1
        right += 1
    
    return right - left - 1  # Length of palindrome
```

### Common Two-Pointer Patterns

#### 1. Palindrome Check

```cpp
bool isPalindrome(string s) {
    int left = 0;
    int right = s.length() - 1;
    
    while(left < right) {
        if(s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    
    return true;
}
```

```python
# Python
def is_palindrome(s):
    left, right = 0, len(s) - 1
    
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    
    return True
```

#### 2. Reverse String

```cpp
void reverseString(string& s) {
    int left = 0;
    int right = s.length() - 1;
    
    while(left < right) {
        swap(s[left], s[right]);
        left++;
        right--;
    }
}
```

```python
# Python
def reverse_string(s):
    s = list(s)  # Convert to list since strings are immutable
    left, right = 0, len(s) - 1
    
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
    
    return ''.join(s)
```

#### 3. Remove Element

```cpp
int removeElement(vector<int>& nums, int val) {
    int i = 0;
    
    for(int j = 0; j < nums.size(); j++) {
        if(nums[j] != val) {
            nums[i] = nums[j];
            i++;
        }
    }
    
    return i;
}
```

```python
# Python
def remove_element(nums, val):
    i = 0
    
    for j in range(len(nums)):
        if nums[j] != val:
            nums[i] = nums[j]
            i += 1
    
    return i
```

#### 4. Valid Palindrome (With Character Filtering)

```cpp
bool isPalindrome(string s) {
    int left = 0;
    int right = s.length() - 1;
    
    while(left < right) {
        // Skip non-alphanumeric from left
        while(left < right && !isalnum(s[left])) {
            left++;
        }
        
        // Skip non-alphanumeric from right
        while(left < right && !isalnum(s[right])) {
            right--;
        }
        
        // Compare (case-insensitive)
        if(tolower(s[left]) != tolower(s[right])) {
            return false;
        }
        
        left++;
        right--;
    }
    
    return true;
}
```

```python
# Python
def is_palindrome_with_filtering(s):
    left, right = 0, len(s) - 1
    
    while left < right:
        # Skip non-alphanumeric from left
        while left < right and not s[left].isalnum():
            left += 1
        
        # Skip non-alphanumeric from right
        while left < right and not s[right].isalnum():
            right -= 1
        
        # Compare (case-insensitive)
        if s[left].lower() != s[right].lower():
            return False
        
        left += 1
        right -= 1
    
    return True
```

### Practice Problems - Two Pointer

**Basic:**
1. [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
2. [Reverse String](https://leetcode.com/problems/reverse-string/)
3. [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

**Intermediate:**
4. [Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)
5. [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/)

---

## Sliding Window Pattern

### Core Concepts

Sliding window is an optimization technique used to solve problems involving arrays/strings where we need to find subarrays/substrings satisfying certain conditions.

### Types of Sliding Windows

1. **Fixed Size Window** - Window size remains constant
2. **Variable Size Window** - Window size changes based on conditions

### Fixed Size Window

#### Template

```cpp
// Find maximum sum subarray of size k
int maxSumFixedWindow(vector<int>& arr, int k) {
    int n = arr.size();
    if(n < k) return -1;
    
    // Calculate sum of first window
    int windowSum = 0;
    for(int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    
    int maxSum = windowSum;
    
    // Slide the window
    for(int i = k; i < n; i++) {
        windowSum = windowSum - arr[i-k] + arr[i];
        maxSum = max(maxSum, windowSum);
    }
    
    return maxSum;
}
```

```python
# Python
def max_sum_fixed_window(arr, k):
    n = len(arr)
    if n < k:
        return -1
    
    # Calculate sum of first window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide the window
    for i in range(k, n):
        window_sum = window_sum - arr[i-k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum
```

#### Fixed Window String Problem

```cpp
// Check if string s2 contains permutation of s1
bool checkInclusion(string s1, string s2) {
    if(s1.length() > s2.length()) return false;
    
    vector<int> s1Freq(26, 0), s2Freq(26, 0);
    
    // Count frequency of s1 and first window of s2
    for(int i = 0; i < s1.length(); i++) {
        s1Freq[s1[i] - 'a']++;
        s2Freq[s2[i] - 'a']++;
    }
    
    // Check if first window matches
    if(s1Freq == s2Freq) return true;
    
    // Slide the window
    for(int i = s1.length(); i < s2.length(); i++) {
        // Add new character
        s2Freq[s2[i] - 'a']++;
        
        // Remove old character
        s2Freq[s2[i - s1.length()] - 'a']--;
        
        // Check if current window matches
        if(s1Freq == s2Freq) return true;
    }
    
    return false;
}
```

```python
# Python
def check_inclusion(s1, s2):
    if len(s1) > len(s2):
        return False
    
    s1_freq = [0] * 26
    s2_freq = [0] * 26
    
    # Count frequency of s1 and first window of s2
    for i in range(len(s1)):
        s1_freq[ord(s1[i]) - ord('a')] += 1
        s2_freq[ord(s2[i]) - ord('a')] += 1
    
    # Check if first window matches
    if s1_freq == s2_freq:
        return True
    
    # Slide the window
    for i in range(len(s1), len(s2)):
        # Add new character
        s2_freq[ord(s2[i]) - ord('a')] += 1
        
        # Remove old character
        s2_freq[ord(s2[i - len(s1)]) - ord('a')] -= 1
        
        # Check if current window matches
        if s1_freq == s2_freq:
            return True
    
    return False
```

### Variable Size Window

#### Template - Exact Match

```cpp
// Find subarray with exact sum k
int subarraySum(vector<int>& nums, int k) {
    int left = 0, right = 0;
    int currentSum = 0;
    int count = 0;
    
    while(right < nums.size()) {
        // Expand window
        currentSum += nums[right];
        
        // Shrink window if needed
        while(currentSum > k && left <= right) {
            currentSum -= nums[left];
            left++;
        }
        
        // Check condition
        if(currentSum == k) {
            count++;
        }
        
        right++;
    }
    
    return count;
}
```

```python
# Python
def subarray_sum(nums, k):
    left = 0
    current_sum = 0
    count = 0
    
    for right in range(len(nums)):
        # Expand window
        current_sum += nums[right]
        
        # Shrink window if needed
        while current_sum > k and left <= right:
            current_sum -= nums[left]
            left += 1
        
        # Check condition
        if current_sum == k:
            count += 1
    
    return count
```

#### Template - At Most K

```cpp
// Longest substring with at most k distinct characters
int lengthOfLongestSubstringKDistinct(string s, int k) {
    unordered_map<char, int> freq;
    int left = 0;
    int maxLen = 0;
    
    for(int right = 0; right < s.length(); right++) {
        // Expand window
        freq[s[right]]++;
        
        // Shrink window if condition violated
        while(freq.size() > k) {
            freq[s[left]]--;
            if(freq[s[left]] == 0) {
                freq.erase(s[left]);
            }
            left++;
        }
        
        // Update answer
        maxLen = max(maxLen, right - left + 1);
    }
    
    return maxLen;
}
```

```python
# Python
def length_of_longest_substring_k_distinct(s, k):
    freq = {}
    left = 0
    max_len = 0
    
    for right in range(len(s)):
        # Expand window
        freq[s[right]] = freq.get(s[right], 0) + 1
        
        # Shrink window if condition violated
        while len(freq) > k:
            freq[s[left]] -= 1
            if freq[s[left]] == 0:
                del freq[s[left]]
            left += 1
        
        # Update answer
        max_len = max(max_len, right - left + 1)
    
    return max_len
```

### Sliding Window with Frequency Map

#### Core Operations

```cpp
// 1. Add character to window
freq[s[right]]++;
matchCount++;  // If needed

// 2. Remove character from window
freq[s[left]]--;
if(freq[s[left]] == 0) {
    freq.erase(s[left]);
}
matchCount--;  // If needed

// 3. Check window validity
if(freq.size() <= k) {
    // Valid window
}

// 4. Update answer
maxLen = max(maxLen, right - left + 1);
```

#### Example: Longest Substring Without Repeating Characters

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> freq;
    int left = 0;
    int maxLen = 0;
    
    for(int right = 0; right < s.length(); right++) {
        // Add character to window
        freq[s[right]]++;
        
        // Shrink window until no duplicates
        while(freq[s[right]] > 1) {
            freq[s[left]]--;
            if(freq[s[left]] == 0) {
                freq.erase(s[left]);
            }
            left++;
        }
        
        // Update maximum length
        maxLen = max(maxLen, right - left + 1);
    }
    
    return maxLen;
}
```

```python
# Python
def length_of_longest_substring(s):
    freq = {}
    left = 0
    max_len = 0
    
    for right in range(len(s)):
        # Add character to window
        freq[s[right]] = freq.get(s[right], 0) + 1
        
        # Shrink window until no duplicates
        while freq[s[right]] > 1:
            freq[s[left]] -= 1
            if freq[s[left]] == 0:
                del freq[s[left]]
            left += 1
        
        # Update maximum length
        max_len = max(max_len, right - left + 1)
    
    return max_len
```

### Window Shrinking Logic

```cpp
// Pattern 1: Shrink while condition violated
while(condition_violated && left <= right) {
    // Remove left element
    // Move left pointer
    left++;
}

// Pattern 2: Shrink to make window valid
while(freq.size() > k) {
    freq[s[left]]--;
    if(freq[s[left]] == 0) {
        freq.erase(s[left]);
    }
    left++;
}

// Pattern 3: Shrink and update answer during shrinking
while(condition_met) {
    minLen = min(minLen, right - left + 1);
    // Shrink from left
    left++;
}
```

### Common Patterns

#### 1. Maximum Length Pattern

```cpp
int maxLength = 0;
while(right < n) {
    // Expand window
    // Add element
    
    // Shrink if needed
    while(invalid_condition) {
        // Remove element
        // Move left
    }
    
    // Update maximum
    maxLength = max(maxLength, right - left + 1);
    right++;
}
```

#### 2. Minimum Length Pattern

```cpp
int minLength = INT_MAX;
while(right < n) {
    // Expand window
    // Add element
    
    // Shrink while valid
    while(valid_condition) {
        // Update minimum
        minLength = min(minLength, right - left + 1);
        // Remove element
        // Move left
    }
    
    right++;
}
```

#### 3. Count Pattern

```cpp
int count = 0;
while(right < n) {
    // Expand window
    // Add element
    
    // Shrink to make exact
    while(condition) {
        // Shrink
    }
    
    // Count valid windows
    if(exact_condition) {
        count++;
    }
    
    right++;
}
```

### Practice Problems - Sliding Window

**Fixed Window:**
1. [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
2. [Maximum Sum Subarray of Size K](https://practice.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1)

**Variable Window - Maximum:**
3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
4. [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
5. [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
6. [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

**Variable Window - Minimum:**
7. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
8. [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

**Count Based:**
9. [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/)
10. [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/)

**Advanced:**
11. [Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

---

## Palindrome Concepts

### What is a Palindrome?

A palindrome is a string that reads the same forwards and backwards.

**Examples:**
- "noon" → Palindrome
- "racecar" → Palindrome
- "A man a plan a canal Panama" → Palindrome (ignoring case and spaces)
- "hello" → NOT a palindrome

### Even vs Odd Length Palindromes

```cpp
// Even length: "abba"
//              ↑  ↑
//            center

// Odd length: "racecar"
//               ↑
//             center
```

### Expand Around Center Technique

```cpp
// Helper function to expand around center
int expandAroundCenter(string s, int left, int right) {
    while(left >= 0 && right < s.length() && s[left] == s[right]) {
        left--;
        right++;
    }
    return right - left - 1;  // Length of palindrome
}

// Find longest palindromic substring
string longestPalindrome(string s) {
    if(s.empty()) return "";
    
    int start = 0, maxLen = 0;
    
    for(int i = 0; i < s.length(); i++) {
        // Check for odd length palindrome
        int len1 = expandAroundCenter(s, i, i);
        
        // Check for even length palindrome
        int len2 = expandAroundCenter(s, i, i + 1);
        
        int len = max(len1, len2);
        
        if(len > maxLen) {
            maxLen = len;
            start = i - (len - 1) / 2;
        }
    }
    
    return s.substr(start, maxLen);
}
```

```python
# Python
def expand_around_center(s, left, right):
    while left >= 0 and right < len(s) and s[left] == s[right]:
        left -= 1
        right += 1
    return right - left - 1

def longest_palindrome(s):
    if not s:
        return ""
    
    start, max_len = 0, 0
    
    for i in range(len(s)):
        # Check for odd length palindrome
        len1 = expand_around_center(s, i, i)
        
        # Check for even length palindrome
        len2 = expand_around_center(s, i, i + 1)
        
        length = max(len1, len2)
        
        if length > max_len:
            max_len = length
            start = i - (length - 1) // 2
    
    return s[start:start + max_len]
```

**Visualization:**
```
For "babad":

i=0, 'b':
  Odd:  b → length 1
  Even: ba → length 0

i=1, 'a':
  Odd:  bab → length 3  ✓ (longest so far)
  Even: ab → length 0

i=2, 'b':
  Odd:  aba → length 3
  Even: ba → length 0

i=3, 'a':
  Odd:  bad → length 1
  Even: ad → length 0

i=4, 'd':
  Odd:  d → length 1
  Even: (out of bounds)

Result: "bab" or "aba" (length 3)
```

### Ignoring Spaces and Symbols

```cpp
bool isPalindromeIgnoreSymbols(string s) {
    int left = 0;
    int right = s.length() - 1;
    
    while(left < right) {
        // Skip non-alphanumeric from left
        while(left < right && !isalnum(s[left])) {
            left++;
        }
        
        // Skip non-alphanumeric from right
        while(left < right && !isalnum(s[right])) {
            right--;
        }
        
        // Compare (case-insensitive)
        if(tolower(s[left]) != tolower(s[right])) {
            return false;
        }
        
        left++;
        right--;
    }
    
    return true;
}

// Usage
isPalindromeIgnoreSymbols("A man, a plan, a canal: Panama");  // true
```

```python
# Python
def is_palindrome_ignore_symbols(s):
    left, right = 0, len(s) - 1
    
    while left < right:
        # Skip non-alphanumeric from left
        while left < right and not s[left].isalnum():
            left += 1
        
        # Skip non-alphanumeric from right
        while left < right and not s[right].isalnum():
            right -= 1
        
        # Compare (case-insensitive)
        if s[left].lower() != s[right].lower():
            return False
        
        left += 1
        right -= 1
    
    return True

# Usage
is_palindrome_ignore_symbols("A man, a plan, a canal: Panama")  # True
```

### Palindrome Permutation Logic

A string can form a palindrome if:
- **Even length:** All characters have even frequency
- **Odd length:** All characters have even frequency except one

```cpp
bool canPermutePalindrome(string s) {
    unordered_map<char, int> freq;
    
    // Count frequencies
    for(char ch : s) {
        freq[ch]++;
    }
    
    // Count characters with odd frequency
    int oddCount = 0;
    for(auto pair : freq) {
        if(pair.second % 2 != 0) {
            oddCount++;
        }
    }
    
    // At most one character can have odd frequency
    return oddCount <= 1;
}

// Usage
canPermutePalindrome("civic");     // true
canPermutePalindrome("ivicc");     // true (permutation: civic)
canPermutePalindrome("hello");     // false
```

```python
# Python
def can_permute_palindrome(s):
    freq = {}
    
    # Count frequencies
    for ch in s:
        freq[ch] = freq.get(ch, 0) + 1
    
    # Count characters with odd frequency
    odd_count = 0
    for count in freq.values():
        if count % 2 != 0:
            odd_count += 1
    
    # At most one character can have odd frequency
    return odd_count <= 1

# Using collections.Counter
from collections import Counter

def can_permute_palindrome_counter(s):
    freq = Counter(s)
    odd_count = sum(1 for count in freq.values() if count % 2 != 0)
    return odd_count <= 1
```

**Explanation:**
```
"civic" → c:2, i:2, v:1
Odd count: 1 (only 'v') → Can form palindrome ✓

"ivicc" → i:2, v:1, c:2
Odd count: 1 (only 'v') → Can form palindrome ✓
Rearrange: "civic"

"hello" → h:1, e:1, l:2, o:1
Odd count: 3 → Cannot form palindrome ✗
```

### Count Palindromic Substrings

```cpp
int countSubstrings(string s) {
    int count = 0;
    
    for(int i = 0; i < s.length(); i++) {
        // Count odd length palindromes
        count += expandAndCount(s, i, i);
        
        // Count even length palindromes
        count += expandAndCount(s, i, i + 1);
    }
    
    return count;
}

int expandAndCount(string s, int left, int right) {
    int count = 0;
    
    while(left >= 0 && right < s.length() && s[left] == s[right]) {
        count++;
        left--;
        right++;
    }
    
    return count;
}

// Usage
countSubstrings("aaa");  // 6
// Substrings: a, a, a, aa, aa, aaa
```

```python
# Python
def count_substrings(s):
    count = 0
    
    for i in range(len(s)):
        # Count odd length palindromes
        count += expand_and_count(s, i, i)
        
        # Count even length palindromes
        count += expand_and_count(s, i, i + 1)
    
    return count

def expand_and_count(s, left, right):
    count = 0
    
    while left >= 0 and right < len(s) and s[left] == s[right]:
        count += 1
        left -= 1
        right += 1
    
    return count

# Usage
count_substrings("aaa")  # 6
```

### Practice Problems - Palindrome

**Basic:**
1. [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
2. [Palindrome Number](https://leetcode.com/problems/palindrome-number/)
3. [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/)

**Intermediate:**
4. [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
5. [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)
6. [Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation/)

**Advanced:**
7. [Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/)
8. [Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/)

---

## Anagram Concepts

### What is an Anagram?

Two strings are anagrams if they contain the same characters with the same frequency, but possibly in a different order.

**Examples:**
- "listen" and "silent" → Anagrams
- "anagram" and "nagaram" → Anagrams
- "hello" and "world" → NOT anagrams

**Key Point:** Order doesn't matter, only character frequency matters.

### Check if Two Strings are Anagrams

#### Method 1: Sorting

```cpp
bool isAnagram(string s, string t) {
    if(s.length() != t.length()) return false;
    
    sort(s.begin(), s.end());
    sort(t.begin(), t.end());
    
    return s == t;
}

// Time: O(n log n)
// Space: O(1) or O(n) depending on sort implementation
```

```python
# Python
def is_anagram_sort(s, t):
    if len(s) != len(t):
        return False
    
    return sorted(s) == sorted(t)
```

#### Method 2: Frequency Array

```cpp
bool isAnagram(string s, string t) {
    if(s.length() != t.length()) return false;
    
    int freq[26] = {0};
    
    // Increment for s, decrement for t
    for(int i = 0; i < s.length(); i++) {
        freq[s[i] - 'a']++;
        freq[t[i] - 'a']--;
    }
    
    // Check if all frequencies are zero
    for(int i = 0; i < 26; i++) {
        if(freq[i] != 0) return false;
    }
    
    return true;
}

// Time: O(n)
// Space: O(1) - fixed size array
```

```python
# Python
def is_anagram_frequency(s, t):
    if len(s) != len(t):
        return False
    
    freq = [0] * 26
    
    # Increment for s, decrement for t
    for i in range(len(s)):
        freq[ord(s[i]) - ord('a')] += 1
        freq[ord(t[i]) - ord('a')] -= 1
    
    # Check if all frequencies are zero
    return all(count == 0 for count in freq)
```

#### Method 3: HashMap

```cpp
bool isAnagram(string s, string t) {
    if(s.length() != t.length()) return false;
    
    unordered_map<char, int> freq;
    
    // Count frequency in s
    for(char ch : s) {
        freq[ch]++;
    }
    
    // Decrement frequency for t
    for(char ch : t) {
        freq[ch]--;
        if(freq[ch] == 0) {
            freq.erase(ch);
        }
    }
    
    return freq.empty();
}

// Time: O(n)
// Space: O(k) where k is number of distinct characters
```

```python
# Python
def is_anagram_hashmap(s, t):
    if len(s) != len(t):
        return False
    
    freq = {}
    
    # Count frequency in s
    for ch in s:
        freq[ch] = freq.get(ch, 0) + 1
    
    # Decrement frequency for t
    for ch in t:
        if ch not in freq:
            return False
        freq[ch] -= 1
        if freq[ch] == 0:
            del freq[ch]
    
    return len(freq) == 0

# Using Counter
from collections import Counter

def is_anagram_counter(s, t):
    return Counter(s) == Counter(t)
```

### Find All Anagrams in a String

Use sliding window with frequency matching.

```cpp
vector<int> findAnagrams(string s, string p) {
    vector<int> result;
    if(s.length() < p.length()) return result;
    
    vector<int> pFreq(26, 0), windowFreq(26, 0);
    
    // Count frequency of pattern
    for(char ch : p) {
        pFreq[ch - 'a']++;
    }
    
    // Process first window
    for(int i = 0; i < p.length(); i++) {
        windowFreq[s[i] - 'a']++;
    }
    
    // Check first window
    if(pFreq == windowFreq) {
        result.push_back(0);
    }
    
    // Slide the window
    for(int i = p.length(); i < s.length(); i++) {
        // Add new character
        windowFreq[s[i] - 'a']++;
        
        // Remove old character
        windowFreq[s[i - p.length()] - 'a']--;
        
        // Check if current window is anagram
        if(pFreq == windowFreq) {
            result.push_back(i - p.length() + 1);
        }
    }
    
    return result;
}

// Usage
findAnagrams("cbaebabacd", "abc");  // [0, 6]
// At index 0: "cba" is anagram of "abc"
// At index 6: "bac" is anagram of "abc"
```

```python
# Python
def find_anagrams(s, p):
    result = []
    if len(s) < len(p):
        return result
    
    p_freq = [0] * 26
    window_freq = [0] * 26
    
    # Count frequency of pattern
    for ch in p:
        p_freq[ord(ch) - ord('a')] += 1
    
    # Process first window
    for i in range(len(p)):
        window_freq[ord(s[i]) - ord('a')] += 1
    
    # Check first window
    if p_freq == window_freq:
        result.append(0)
    
    # Slide the window
    for i in range(len(p), len(s)):
        # Add new character
        window_freq[ord(s[i]) - ord('a')] += 1
        
        # Remove old character
        window_freq[ord(s[i - len(p)]) - ord('a')] -= 1
        
        # Check if current window is anagram
        if p_freq == window_freq:
            result.append(i - len(p) + 1)
    
    return result
```

### Group Anagrams

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> groups;
    
    for(string s : strs) {
        // Create a key by sorting
        string key = s;
        sort(key.begin(), key.end());
        
        // Add to corresponding group
        groups[key].push_back(s);
    }
    
    // Extract all groups
    vector<vector<string>> result;
    for(auto pair : groups) {
        result.push_back(pair.second);
    }
    
    return result;
}

// Usage
vector<string> words = {"eat", "tea", "tan", "ate", "nat", "bat"};
groupAnagrams(words);
// Output: [["eat","tea","ate"], ["tan","nat"], ["bat"]]
```

```python
# Python
def group_anagrams(strs):
    groups = {}
    
    for s in strs:
        # Create a key by sorting
        key = ''.join(sorted(s))
        
        # Add to corresponding group
        if key not in groups:
            groups[key] = []
        groups[key].append(s)
    
    # Extract all groups
    return list(groups.values())

# Using defaultdict
from collections import defaultdict

def group_anagrams_defaultdict(strs):
    groups = defaultdict(list)
    
    for s in strs:
        key = ''.join(sorted(s))
        groups[key].append(s)
    
    return list(groups.values())
```

### Minimum Steps to Make Anagram

```cpp
int minSteps(string s, string t) {
    int freq[26] = {0};
    
    // Count frequencies
    for(char ch : s) {
        freq[ch - 'a']++;
    }
    
    for(char ch : t) {
        freq[ch - 'a']--;
    }
    
    // Count characters that need to be changed
    int steps = 0;
    for(int i = 0; i < 26; i++) {
        if(freq[i] > 0) {
            steps += freq[i];
        }
    }
    
    return steps;
}

// Usage
minSteps("leetcode", "practice");  // 5
// Need to change: l, e, o, c, d in "leetcode"
```

```python
# Python
def min_steps(s, t):
    freq = [0] * 26
    
    # Count frequencies
    for ch in s:
        freq[ord(ch) - ord('a')] += 1
    
    for ch in t:
        freq[ord(ch) - ord('a')] -= 1
    
    # Count characters that need to be changed
    steps = 0
    for count in freq:
        if count > 0:
            steps += count
    
    return steps
```

### Practice Problems - Anagram

**Basic:**
1. [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
2. [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

**Intermediate:**
3. [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
4. [Minimum Number of Steps to Make Two Strings Anagram](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/)

**Advanced:**
5. [Find Anagram Mappings](https://leetcode.com/problems/find-anagram-mappings/)

---

## Pattern Matching (Naive Search)

### Naive Pattern Matching Algorithm

The naive approach checks for the pattern at every position in the text.

```cpp
vector<int> naivePatternSearch(string text, string pattern) {
    vector<int> positions;
    int n = text.length();
    int m = pattern.length();
    
    // Check pattern at each position
    for(int i = 0; i <= n - m; i++) {
        int j;
        
        // Check if pattern matches at position i
        for(j = 0; j < m; j++) {
            if(text[i + j] != pattern[j]) {
                break;  // Mismatch
            }
        }
        
        // If we completed inner loop, pattern found
        if(j == m) {
            positions.push_back(i);
        }
    }
    
    return positions;
}

// Usage
naivePatternSearch("AABAACAADAABAABA", "AABA");
// Output: [0, 9, 12]
```

```python
# Python
def naive_pattern_search(text, pattern):
    positions = []
    n = len(text)
    m = len(pattern)
    
    # Check pattern at each position
    for i in range(n - m + 1):
        j = 0
        
        # Check if pattern matches at position i
        while j < m and text[i + j] == pattern[j]:
            j += 1
        
        # If we completed inner loop, pattern found
        if j == m:
            positions.append(i)
    
    return positions
```

**Visualization:**
```
Text:    A A B A A C A A D A A B A A B A
Pattern: A A B A

Position 0:
A A B A A C A A D A A B A A B A
A A B A ✓ (Match found)

Position 1:
A A B A A C A A D A A B A A B A
  A A B A ✗ (Mismatch at position 2)

Position 9:
A A B A A C A A D A A B A A B A
                  A A B A ✓ (Match found)
```

**Time Complexity:** O(n * m)
- Outer loop: O(n)
- Inner loop: O(m)

### strStr() Implementation (Find Needle in Haystack)

```cpp
int strStr(string haystack, string needle) {
    if(needle.empty()) return 0;
    
    int n = haystack.length();
    int m = needle.length();
    
    if(m > n) return -1;
    
    for(int i = 0; i <= n - m; i++) {
        int j;
        for(j = 0; j < m; j++) {
            if(haystack[i + j] != needle[j]) {
                break;
            }
        }
        
        if(j == m) {
            return i;  // Return first occurrence
        }
    }
    
    return -1;  // Not found
}

// Usage
strStr("hello", "ll");  // 2
strStr("aaaaa", "bba"); // -1
```

```python
# Python
def str_str(haystack, needle):
    if not needle:
        return 0
    
    n = len(haystack)
    m = len(needle)
    
    if m > n:
        return -1
    
    for i in range(n - m + 1):
        j = 0
        while j < m and haystack[i + j] == needle[j]:
            j += 1
        
        if j == m:
            return i  # Return first occurrence
    
    return -1  # Not found
```

### Using Built-in Functions

```cpp
// C++
string text = "hello world";
string pattern = "world";

// Method 1: find()
size_t pos = text.find(pattern);
if(pos != string::npos) {
    cout << "Found at position: " << pos << endl;  // 6
}

// Method 2: find all occurrences
pos = 0;
while((pos = text.find(pattern, pos)) != string::npos) {
    cout << "Found at: " << pos << endl;
    pos += pattern.length();
}
```

```python
# Python
text = "hello world"
pattern = "world"

# Method 1: find()
pos = text.find(pattern)  # 6
if pos != -1:
    print(f"Found at position: {pos}")

# Method 2: find all occurrences
pos = 0
while True:
    pos = text.find(pattern, pos)
    if pos == -1:
        break
    print(f"Found at: {pos}")
    pos += len(pattern)
```

### Practice Problems - Pattern Matching

**Basic:**
1. [Implement strStr()](https://leetcode.com/problems/implement-strstr/)
2. [Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

**Intermediate:**
3. [Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern/)

**Advanced:**
4. [Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)
5. [KMP Algorithm](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)
6. [Rabin-Karp Algorithm](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)

---

## Substring vs Subsequence

### Critical Difference

| Aspect | Substring | Subsequence |
|--------|-----------|-------------|
| Continuity | **Continuous** characters | Can skip characters |
| Order | Maintains order | Maintains order |
| Example | "abc" from "abcde" | "ace" from "abcde" |

### Substring

A substring is a **contiguous** sequence of characters within a string.

```cpp
// All substrings of "abc"
Substrings: "", "a", "b", "c", "ab", "bc", "abc"

// Generate all substrings
vector<string> getAllSubstrings(string s) {
    vector<string> substrings;
    int n = s.length();
    
    for(int i = 0; i < n; i++) {
        for(int j = i; j < n; j++) {
            substrings.push_back(s.substr(i, j - i + 1));
        }
    }
    
    return substrings;
}

// Total substrings = n(n+1)/2 + 1 (including empty)
```

```python
# Python
def get_all_substrings(s):
    substrings = []
    n = len(s)
    
    for i in range(n):
        for j in range(i, n):
            substrings.append(s[i:j+1])
    
    return substrings

# All substrings of "abc"
substrings = get_all_substrings("abc")
# ['a', 'ab', 'abc', 'b', 'bc', 'c']
```

**Example:**
```
String: "abc"

Starting at 0: "a", "ab", "abc"
Starting at 1: "b", "bc"
Starting at 2: "c"

Total: 6 non-empty substrings
```

### Subsequence

A subsequence is a sequence that can be derived by deleting some or no elements **without changing the order** of remaining elements.

```cpp
// Some subsequences of "abc"
Subsequences: "", "a", "b", "c", "ab", "ac", "bc", "abc"

// Check if s2 is subsequence of s1
bool isSubsequence(string s1, string s2) {
    int i = 0, j = 0;
    
    while(i < s1.length() && j < s2.length()) {
        if(s1[i] == s2[j]) {
            j++;
        }
        i++;
    }
    
    return j == s2.length();
}

// Total subsequences = 2^n
```

```python
# Python
def is_subsequence(s1, s2):
    i, j = 0, 0
    
    while i < len(s1) and j < len(s2):
        if s1[i] == s2[j]:
            j += 1
        i += 1
    
    return j == len(s2)

# Generate all subsequences (using recursion)
def generate_subsequences(s):
    def backtrack(start, current):
        if start == len(s):
            subsequences.append(''.join(current))
            return
        
        # Include current character
        current.append(s[start])
        backtrack(start + 1, current)
        current.pop()
        
        # Exclude current character
        backtrack(start + 1, current)
    
    subsequences = []
    backtrack(0, [])
    return subsequences
```

**Example:**
```
String: "abc"

Subsequences (using binary representation):
000 → ""
001 → "c"
010 → "b"
011 → "bc"
100 → "a"
101 → "ac"
110 → "ab"
111 → "abc"

Total: 8 subsequences (including empty)
```

### Key Differences with Examples

```cpp
string s = "abcde";

// Substrings (continuous):
"abc" → Valid ✓
"abd" → Invalid ✗ (not continuous)
"ace" → Invalid ✗ (not continuous)

// Subsequences (order maintained, can skip):
"abc" → Valid ✓
"abd" → Valid ✓
"ace" → Valid ✓
"aec" → Invalid ✗ (order not maintained)
```

### Common Problems

#### Longest Common Substring

```cpp
int longestCommonSubstring(string s1, string s2) {
    int n = s1.length(), m = s2.length();
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));
    int maxLen = 0;
    
    for(int i = 1; i <= n; i++) {
        for(int j = 1; j <= m; j++) {
            if(s1[i-1] == s2[j-1]) {
                dp[i][j] = dp[i-1][j-1] + 1;
                maxLen = max(maxLen, dp[i][j]);
            }
        }
    }
    
    return maxLen;
}

// Usage
longestCommonSubstring("abcde", "abfce");  // 2 ("ab")
```

```python
# Python
def longest_common_substring(s1, s2):
    n, m = len(s1), len(s2)
    dp = [[0] * (m + 1) for _ in range(n + 1)]
    max_len = 0
    
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
                max_len = max(max_len, dp[i][j])
    
    return max_len
```

#### Longest Common Subsequence

```cpp
int longestCommonSubsequence(string s1, string s2) {
    int n = s1.length(), m = s2.length();
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));
    
    for(int i = 1; i <= n; i++) {
        for(int j = 1; j <= m; j++) {
            if(s1[i-1] == s2[j-1]) {
                dp[i][j] = dp[i-1][j-1] + 1;
            }
            else {
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    
    return dp[n][m];
}

// Usage
longestCommonSubsequence("abcde", "ace");  // 3 ("ace")
```

```python
# Python
def longest_common_subsequence(s1, s2):
    n, m = len(s1), len(s2)
    dp = [[0] * (m + 1) for _ in range(n + 1)]
    
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[n][m]
```

### Practice Problems - Substring vs Subsequence

**Substring Problems:**
1. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
2. [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
3. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

**Subsequence Problems:**
4. [Is Subsequence](https://leetcode.com/problems/is-subsequence/)
5. [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
6. [Number of Matching Subsequences](https://leetcode.com/problems/number-of-matching-subsequences/)

---

## String Building & Modification

### Immutability of Strings

In Java (and similar languages), strings are **immutable** - once created, they cannot be changed.

```java
String s = "Hello";
s = s + " World";  // Creates NEW object, doesn't modify original

// Memory:
// Original: "Hello" (now eligible for garbage collection)
// New: "Hello World"
```

**Why Immutability?**
1. **Security:** Prevents modification of shared data
2. **Thread Safety:** Can be safely shared between threads
3. **Caching:** String pool optimization
4. **Hash Code:** Can cache hash code

### String vs StringBuilder vs StringBuffer

```java
// 1. String - Immutable
String s = "";
for(int i = 0; i < 1000; i++) {
    s += i;  // Creates 1000 new objects! O(n²)
}

// 2. StringBuilder - Mutable, NOT thread-safe
StringBuilder sb = new StringBuilder();
for(int i = 0; i < 1000; i++) {
    sb.append(i);  // Modifies same object! O(n)
}
String result = sb.toString();

// 3. StringBuffer - Mutable, thread-safe
StringBuffer sbuf = new StringBuffer();
for(int i = 0; i < 1000; i++) {
    sbuf.append(i);  // Synchronized operations
}
```

**Comparison:**

| Feature | String | StringBuilder | StringBuffer |
|---------|--------|---------------|--------------|
| Mutability | Immutable | Mutable | Mutable |
| Thread-Safe | Yes | No | Yes |
| Performance | Slowest | Fastest | Slower than StringBuilder |
| Use When | Small/constant | Single-threaded | Multi-threaded |

### StringBuilder Methods

```java
StringBuilder sb = new StringBuilder();

// Append
sb.append("Hello");
sb.append(' ');
sb.append("World");
// Result: "Hello World"

// Insert
sb.insert(5, " Beautiful");
// Result: "Hello Beautiful World"

// Delete
sb.delete(5, 15);  // Delete from index 5 to 15
// Result: "Hello World"

// Delete character at index
sb.deleteCharAt(0);
// Result: "ello World"

// Replace
sb.replace(0, 4, "Hi");
// Result: "Hi World"

// Reverse
sb.reverse();
// Result: "dlroW iH"

// Convert to String
String result = sb.toString();

// Get character at index
char ch = sb.charAt(0);

// Set character at index
sb.setCharAt(0, 'H');

// Length
int len = sb.length();

// Capacity
int cap = sb.capacity();  // Default: 16

// Clear (reuse)
sb.setLength(0);
```

### When to Use append()

```java
// Efficient string building
StringBuilder sb = new StringBuilder();
for(int i = 0; i < n; i++) {
    sb.append(arr[i]);
    if(i < n - 1) {
        sb.append(", ");
    }
}
String result = sb.toString();

// Example: Build CSV
StringBuilder csv = new StringBuilder();
for(String value : values) {
    csv.append(value).append(",");
}
// Remove trailing comma
if(csv.length() > 0) {
    csv.setLength(csv.length() - 1);
}
```

### String to char[] and vice versa

```cpp
// C++
// String to char array
string s = "hello";
char arr[6];
strcpy(arr, s.c_str());

// char array to string
char arr[] = "world";
string s(arr);
string s2 = string(arr);

// String to vector<char>
string s = "hello";
vector<char> vec(s.begin(), s.end());

// vector<char> to string
vector<char> vec = {'h', 'e', 'l', 'l', 'o'};
string s(vec.begin(), vec.end());
```

```java
// Java
// String to char array
String s = "hello";
char[] arr = s.toCharArray();

// char array to String
char[] arr = {'h', 'e', 'l', 'l', 'o'};
String s = new String(arr);

// String to Character array (wrapper)
String s = "hello";
Character[] arr = s.chars()
                   .mapToObj(c -> (char)c)
                   .toArray(Character[]::new);
```

```python
# Python
# String to list of characters
s = "hello"
char_list = list(s)  # ['h', 'e', 'l', 'l', 'o']

# List of characters to string
char_list = ['h', 'e', 'l', 'l', 'o']
s = ''.join(char_list)  # "hello"

# String to bytes
s = "hello"
bytes_obj = s.encode('utf-8')  # b'hello'

# Bytes to string
bytes_obj = b'hello'
s = bytes_obj.decode('utf-8')  # "hello"
```

### char to String Conversion

```cpp
// C++
char ch = 'a';

// Method 1: Using string constructor
string s(1, ch);

// Method 2: Using push_back
string s = "";
s.push_back(ch);

// Method 3: Using +=
string s = "";
s += ch;
```

```java
// Java
char ch = 'a';

// Method 1: String valueOf
String s = String.valueOf(ch);

// Method 2: Character toString
String s = Character.toString(ch);

// Method 3: Concatenation (creates new object)
String s = "" + ch;

// Method 4: String constructor
String s = new String(new char[]{ch});
```

```python
# Python
ch = 'a'

# Python has no char type, only strings
s = 'a'  # This is already a string

# Convert single character to string
s = str(ch)  # "a"

# Convert character from ASCII
ch = chr(97)  # 'a'
ascii_val = ord('a')  # 97
```

### Practice Problems - String Building

1. [String Compression](https://leetcode.com/problems/string-compression/)
2. [Remove All Adjacent Duplicates in String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
3. [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)
4. [Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)

---

## String Pool and Memory Management

### String Pool Concept

String Pool is a **special memory region** in the heap where Java stores string literals.

```java
String a = "Hello";
String b = "Hello";
String c = new String("Hello");
```

**Memory Representation:**
```
Stack:              String Pool (Heap):        Heap:
+---+               +-------+                 +-------+
| a | ------------> | Hello |                 | Hello |
+---+               +-------+                 +-------+
                       ↑                         ↑
+---+                  |                         |
| b | -----------------+                         |
+---+                                            |
                                                 |
+---+                                            |
| c | ---------------------------------------------+
+---+
```

### Benefits of String Pool

1. **Memory Optimization:**
   - Same string stored only once
   - Multiple references can point to same object

2. **Performance:**
   - Faster string comparison
   - Reduced memory footprint

```java
String s1 = "Hello";  // Created in pool
String s2 = "Hello";  // Reuses from pool
String s3 = new String("Hello");  // Created in heap

System.out.println(s1 == s2);  // true (same reference)
System.out.println(s1 == s3);  // false (different references)
System.out.println(s1.equals(s3));  // true (same value)
```

### Intern() Method

Forces a string to be added to the string pool.

```java
String s1 = new String("Hello");  // Heap
String s2 = s1.intern();  // Now in pool

String s3 = "Hello";  // Pool

System.out.println(s2 == s3);  // true (same reference)
```

### String Comparison Revisited

#### Using == (Reference Comparison)

```java
String a = "Hello";
String b = "Hello";
System.out.println(a == b);  // true (same object in pool)

String c = new String("Hello");
System.out.println(a == c);  // false (different objects)
```

#### Using .equals() (Value Comparison)

```java
String a = "Hello";
String c = new String("Hello");
System.out.println(a.equals(c));  // true (same value)
```

### Immutability and Security

```java
// Example 1: Multiple references
String s1 = "Password123";
String s2 = "Password123";
String s3 = "Password123";

// All point to same object in pool
// If strings were mutable and s1 changes password:
// s1 = "NewPassword";  // This would affect s2 and s3 too!
// Security breach!

// But since strings are immutable:
s1 = "NewPassword";  // Creates new object, s2 and s3 unchanged
```

**Visualization:**
```
Before: s1, s2, s3 → "Password123"
After:  s1 → "NewPassword"
        s2, s3 → "Password123" (unchanged)
```

### Memory Allocation

```java
// String literals - Pool
String s1 = "Hello";  // Pool

// New keyword - Heap (outside pool)
String s2 = new String("Hello");  // Heap

// Concatenation - Heap
String s3 = "Hello" + "World";  // Pool (compile-time constant)
String s4 = s1 + "World";  // Heap (runtime)
```

### Garbage Collection with Strings

```java
String s1 = "Hello";
s1 = "World";  // "Hello" becomes eligible for GC

String s2 = new String("Test");
s2 = null;  // "Test" eligible for GC

String s3 = "Reused";
String s4 = "Reused";
s3 = null;
s4 = null;
// "Reused" NOT eligible for GC (still in pool)
```

---

## Complete Problem Solutions

### 1. Reverse Words in a String

**Problem:** Reverse the order of words in a string.

```cpp
string reverseWords(string s) {
    // Step 1: Remove leading, trailing, and multiple spaces
    string cleaned = "";
    bool inWord = false;
    
    for(char ch : s) {
        if(ch != ' ') {
            cleaned += ch;
            inWord = true;
        }
        else if(inWord) {
            cleaned += ' ';
            inWord = false;
        }
    }
    
    // Remove trailing space if any
    if(!cleaned.empty() && cleaned.back() == ' ') {
        cleaned.pop_back();
    }
    
    // Step 2: Reverse entire string
    reverse(cleaned.begin(), cleaned.end());
    
    // Step 3: Reverse each word
    int start = 0;
    for(int i = 0; i <= cleaned.length(); i++) {
        if(i == cleaned.length() || cleaned[i] == ' ') {
            reverse(cleaned.begin() + start, cleaned.begin() + i);
            start = i + 1;
        }
    }
    
    return cleaned;
}

// Usage
reverseWords("  hello  world  ");  // "world hello"
reverseWords("a good   example");  // "example good a"
```

```java
// Java
public String reverseWords(String s) {
    // Step 1: Clean spaces
    String[] words = s.trim().split("\\s+");
    
    // Step 2: Reverse array
    int left = 0, right = words.length - 1;
    while(left < right) {
        String temp = words[left];
        words[left] = words[right];
        words[right] = temp;
        left++;
        right--;
    }
    
    // Step 3: Join with single space
    return String.join(" ", words);
}
```

```python
# Python
def reverse_words(s):
    # Step 1: Clean spaces and split
    words = s.split()
    
    # Step 2: Reverse list
    words.reverse()
    
    # Step 3: Join with single space
    return ' '.join(words)

# One-liner
def reverse_words_oneliner(s):
    return ' '.join(reversed(s.split()))
```

**Visualization:**
```
Input: "the sky is blue"

Step 1: Clean spaces → "the sky is blue"

Step 2: Reverse entire string → "eulb si yks eht"

Step 3: Reverse each word:
  "eulb" → "blue"
  "si" → "is"
  "yks" → "sky"
  "eht" → "the"
  
Result: "blue is sky the"
```

**Practice:** [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)

---

### 2. Reverse Words in a String III

**Problem:** Reverse characters in each word, but keep word order.

```cpp
string reverseWords(string s) {
    int start = 0;
    
    for(int i = 0; i <= s.length(); i++) {
        if(i == s.length() || s[i] == ' ') {
            // Reverse word from start to i-1
            reverse(s.begin() + start, s.begin() + i);
            start = i + 1;
        }
    }
    
    return s;
}

// Usage
reverseWords("Let's take LeetCode contest");
// Output: "s'teL ekat edoCteeL tsetnoc"
```

```python
# Python
def reverse_words_iii(s):
    # Convert to list since strings are immutable
    chars = list(s)
    start = 0
    
    for i in range(len(chars) + 1):
        if i == len(chars) or chars[i] == ' ':
            # Reverse word from start to i-1
            left, right = start, i - 1
            while left < right:
                chars[left], chars[right] = chars[right], chars[left]
                left += 1
                right -= 1
            start = i + 1
    
    return ''.join(chars)

# One-liner using list comprehension
def reverse_words_iii_oneliner(s):
    return ' '.join(word[::-1] for word in s.split())
```

**Practice:** [Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)

---

### 3. First Unique Character

**Problem:** Find the first non-repeating character in a string.

```cpp
int firstUniqChar(string s) {
    // Count frequency
    int freq[26] = {0};
    for(char ch : s) {
        freq[ch - 'a']++;
    }
    
    // Find first character with frequency 1
    for(int i = 0; i < s.length(); i++) {
        if(freq[s[i] - 'a'] == 1) {
            return i;
        }
    }
    
    return -1;
}

// Usage
firstUniqChar("leetcode");  // 0 ('l')
firstUniqChar("loveleetcode");  // 2 ('v')
firstUniqChar("aabb");  // -1
```

```python
# Python
def first_uniq_char(s):
    # Count frequency
    freq = [0] * 26
    for ch in s:
        freq[ord(ch) - ord('a')] += 1
    
    # Find first character with frequency 1
    for i, ch in enumerate(s):
        if freq[ord(ch) - ord('a')] == 1:
            return i
    
    return -1

# Using Counter
from collections import Counter

def first_uniq_char_counter(s):
    freq = Counter(s)
    
    for i, ch in enumerate(s):
        if freq[ch] == 1:
            return i
    
    return -1
```

**Practice:** [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)

---

### 4. Isomorphic Strings

**Problem:** Two strings are isomorphic if characters can be replaced to get the other string.

```cpp
bool isIsomorphic(string s, string t) {
    if(s.length() != t.length()) return false;
    
    unordered_map<char, char> mapS, mapT;
    
    for(int i = 0; i < s.length(); i++) {
        char c1 = s[i], c2 = t[i];
        
        // Check s -> t mapping
        if(mapS.count(c1)) {
            if(mapS[c1] != c2) return false;
        }
        else {
            mapS[c1] = c2;
        }
        
        // Check t -> s mapping
        if(mapT.count(c2)) {
            if(mapT[c2] != c1) return false;
        }
        else {
            mapT[c2] = c1;
        }
    }
    
    return true;
}

// Usage
isIsomorphic("egg", "add");  // true (e->a, g->d)
isIsomorphic("foo", "bar");  // false (o->o and o->a conflict)
```

```python
# Python
def is_isomorphic(s, t):
    if len(s) != len(t):
        return False
    
    map_s, map_t = {}, {}
    
    for c1, c2 in zip(s, t):
        # Check s -> t mapping
        if c1 in map_s:
            if map_s[c1] != c2:
                return False
        else:
            map_s[c1] = c2
        
        # Check t -> s mapping
        if c2 in map_t:
            if map_t[c2] != c1:
                return False
        else:
            map_t[c2] = c1
    
    return True

# Using set and zip
def is_isomorphic_set(s, t):
    return len(set(zip(s, t))) == len(set(s)) == len(set(t))
```

**Practice:** [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)

---

### 5. Longest Substring Without Repeating Characters

**Problem:** Find length of longest substring without repeating characters.

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> lastSeen;
    int maxLen = 0;
    int left = 0;
    
    for(int right = 0; right < s.length(); right++) {
        char ch = s[right];
        
        // If character seen before and in current window
        if(lastSeen.count(ch) && lastSeen[ch] >= left) {
            left = lastSeen[ch] + 1;
        }
        
        // Update last seen position
        lastSeen[ch] = right;
        
        // Update max length
        maxLen = max(maxLen, right - left + 1);
    }
    
    return maxLen;
}

// Usage
lengthOfLongestSubstring("abcabcbb");  // 3 ("abc")
lengthOfLongestSubstring("bbbbb");     // 1 ("b")
lengthOfLongestSubstring("pwwkew");    // 3 ("wke")
```

```python
# Python
def length_of_longest_substring(s):
    last_seen = {}
    max_len = 0
    left = 0
    
    for right, ch in enumerate(s):
        # If character seen before and in current window
        if ch in last_seen and last_seen[ch] >= left:
            left = last_seen[ch] + 1
        
        # Update last seen position
        last_seen[ch] = right
        
        # Update max length
        max_len = max(max_len, right - left + 1)
    
    return max_len
```

**Visualization:**
```
"abcabcbb"

Window: [a] → length 1
Window: [ab] → length 2
Window: [abc] → length 3 ✓
Window: [abc|a] → 'a' repeats, move left
Window: [bca] → length 3
Window: [cab] → length 3
Window: [abc] → length 3
Window: [abc|b] → 'b' repeats, move left
Window: [cb] → length 2
Window: [cbb] → 'b' repeats, move left
Window: [b] → length 1

Max: 3
```

**Practice:** [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

---

### 6. Longest Repeating Character Replacement

**Problem:** Find longest substring with same character after k replacements.

```cpp
int characterReplacement(string s, int k) {
    unordered_map<char, int> freq;
    int maxFreq = 0;
    int maxLen = 0;
    int left = 0;
    
    for(int right = 0; right < s.length(); right++) {
        // Add character to window
        freq[s[right]]++;
        maxFreq = max(maxFreq, freq[s[right]]);
        
        // Window size - max frequency = replacements needed
        int replacements = (right - left + 1) - maxFreq;
        
        // If replacements needed > k, shrink window
        if(replacements > k) {
            freq[s[left]]--;
            left++;
        }
        
        // Update max length
        maxLen = max(maxLen, right - left + 1);
    }
    
    return maxLen;
}

// Usage
characterReplacement("AABABBA", 1);  // 4 ("AABA" or "ABBB")
characterReplacement("ABAB", 2);     // 4 (replace all to same)
```

```python
# Python
def character_replacement(s, k):
    freq = {}
    max_freq = 0
    max_len = 0
    left = 0
    
    for right in range(len(s)):
        # Add character to window
        freq[s[right]] = freq.get(s[right], 0) + 1
        max_freq = max(max_freq, freq[s[right]])
        
        # Window size - max frequency = replacements needed
        replacements = (right - left + 1) - max_freq
        
        # If replacements needed > k, shrink window
        if replacements > k:
            freq[s[left]] -= 1
            left += 1
        
        # Update max length
        max_len = max(max_len, right - left + 1)
    
    return max_len
```

**Explanation:**
```
"AABABBA", k=1

Window "A": maxFreq=1, replacements=0, length=1
Window "AA": maxFreq=2, replacements=0, length=2
Window "AAB": maxFreq=2, replacements=1, length=3
Window "AABA": maxFreq=3, replacements=1, length=4 ✓
Window "AABAB": maxFreq=3, replacements=2 > k
  Shrink: "ABAB": maxFreq=2, replacements=2 > k
  Shrink: "BAB": maxFreq=2, replacements=1, length=3
Window "BABB": maxFreq=3, replacements=1, length=4 ✓
Window "BABBA": maxFreq=3, replacements=2 > k
  Shrink: "ABBA": maxFreq=2, replacements=2 > k
  Shrink: "BBA": maxFreq=2, replacements=1, length=3

Max: 4
```

**Practice:** [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

---

### 7. Minimum Window Substring

**Problem:** Find minimum window in s that contains all characters of t.

```cpp
string minWindow(string s, string t) {
    if(s.length() < t.length()) return "";
    
    // Count frequency of characters in t
    unordered_map<char, int> required, window;
    for(char ch : t) {
        required[ch]++;
    }
    
    int requiredChars = required.size();
    int formedChars = 0;
    
    int left = 0, right = 0;
    int minLen = INT_MAX;
    int minLeft = 0;
    
    while(right < s.length()) {
        // Add character from right
        char ch = s[right];
        window[ch]++;
        
        // Check if frequency matches
        if(required.count(ch) && window[ch] == required[ch]) {
            formedChars++;
        }
        
        // Try to shrink window
        while(left <= right && formedChars == requiredChars) {
            // Update result if current window is smaller
            if(right - left + 1 < minLen) {
                minLen = right - left + 1;
                minLeft = left;
            }
            
            // Remove character from left
            char leftChar = s[left];
            window[leftChar]--;
            
            if(required.count(leftChar) && window[leftChar] < required[leftChar]) {
                formedChars--;
            }
            
            left++;
        }
        
        right++;
    }
    
    return minLen == INT_MAX ? "" : s.substr(minLeft, minLen);
}

// Usage
minWindow("ADOBECODEBANC", "ABC");  // "BANC"
minWindow("a", "a");                 // "a"
minWindow("a", "aa");                // ""
```

```python
# Python
def min_window(s, t):
    if len(s) < len(t):
        return ""
    
    # Count frequency of characters in t
    required = {}
    for ch in t:
        required[ch] = required.get(ch, 0) + 1
    
    required_chars = len(required)
    formed_chars = 0
    
    window = {}
    left, right = 0, 0
    min_len = float('inf')
    min_left = 0
    
    while right < len(s):
        # Add character from right
        ch = s[right]
        window[ch] = window.get(ch, 0) + 1
        
        # Check if frequency matches
        if ch in required and window[ch] == required[ch]:
            formed_chars += 1
        
        # Try to shrink window
        while left <= right and formed_chars == required_chars:
            # Update result if current window is smaller
            if right - left + 1 < min_len:
                min_len = right - left + 1
                min_left = left
            
            # Remove character from left
            left_char = s[left]
            window[left_char] -= 1
            
            if left_char in required and window[left_char] < required[left_char]:
                formed_chars -= 1
            
            left += 1
        
        right += 1
    
    return "" if min_len == float('inf') else s[min_left:min_left + min_len]
```

**Visualization:**
```
s = "ADOBECODEBANC", t = "ABC"

Required: {A:1, B:1, C:1}

Window "ADOBEC": ✓ Contains all, length=6
  Try shrinking: "DOBEC" ✗ Missing A
  
Continue expanding...

Window "ADOBECODEBA": ✓ Contains all, length=11
  Shrink: "DOBECODEBA": ✓ length=10
  Shrink: "OBECODEBA": ✗ Missing D? No, ✓ length=9
  ...continue...
  Shrink: "CODEBA": ✗ Missing O? No, ✓ length=6
  Shrink: "ODEBA": ✗ Missing C
  
Continue expanding...

Window "ODEBANC": ✓ Contains all, length=7
  Shrink: "DEBANC": ✗ Missing O
  
Window "EBANC": ✗
  Continue...
  
Window "BANC": ✓ length=4 ← Minimum

Result: "BANC"
```

**Practice:** [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

---

### 8. String Compression

**Problem:** Compress string using counts of repeated characters.

```cpp
int compress(vector<char>& chars) {
    int write = 0;  // Position to write
    int i = 0;      // Position to read
    
    while(i < chars.size()) {
        char currentChar = chars[i];
        int count = 0;
        
        // Count consecutive characters
        while(i < chars.size() && chars[i] == currentChar) {
            i++;
            count++;
        }
        
        // Write character
        chars[write++] = currentChar;
        
        // Write count if > 1
        if(count > 1) {
            string countStr = to_string(count);
            for(char c : countStr) {
                chars[write++] = c;
            }
        }
    }
    
    return write;
}

// Usage
vector<char> chars = {'a','a','b','b','c','c','c'};
int newLen = compress(chars);
// chars = {'a','2','b','2','c','3'}, newLen = 6
```

```python
# Python
def compress(chars):
    write = 0  # Position to write
    i = 0      # Position to read
    
    while i < len(chars):
        current_char = chars[i]
        count = 0
        
        # Count consecutive characters
        while i < len(chars) and chars[i] == current_char:
            i += 1
            count += 1
        
        # Write character
        chars[write] = current_char
        write += 1
        
        # Write count if > 1
        if count > 1:
            count_str = str(count)
            for c in count_str:
                chars[write] = c
                write += 1
    
    return write
```

**Visualization:**
```
Input: ['a','a','b','b','b','c','c','c']

i=0: 'a' appears 2 times
  Write 'a', '2'
  write=2

i=2: 'b' appears 3 times
  Write 'b', '3'
  write=4

i=5: 'c' appears 3 times
  Write 'c', '3'
  write=6

Result: ['a','2','b','3','c','3']
Length: 6
```

**Practice:** [String Compression](https://leetcode.com/problems/string-compression/)

---

### 9. Remove All Adjacent Duplicates

**Problem:** Remove all adjacent duplicate characters.

```cpp
string removeDuplicates(string s) {
    string result = "";
    
    for(char ch : s) {
        if(!result.empty() && result.back() == ch) {
            result.pop_back();  // Remove duplicate
        }
        else {
            result.push_back(ch);  // Add character
        }
    }
    
    return result;
}

// Usage
removeDuplicates("abbaca");  // "ca"
// Process: a -> ab -> a -> ac -> ca
```

```python
# Python
def remove_duplicates(s):
    result = []
    
    for ch in s:
        if result and result[-1] == ch:
            result.pop()  # Remove duplicate
        else:
            result.append(ch)  # Add character
    
    return ''.join(result)

# Using stack
def remove_duplicates_stack(s):
    stack = []
    
    for ch in s:
        if stack and stack[-1] == ch:
            stack.pop()
        else:
            stack.append(ch)
    
    return ''.join(stack)
```

**Visualization:**
```
"abbaca"

Stack: []
Add 'a': [a]
Add 'b': [a, b]
Add 'b': [a, b] → 'b' == 'b', remove → [a]
Add 'a': [a] → 'a' == 'a', remove → []
Add 'c': [c]
Add 'a': [c, a]

Result: "ca"
```

**Practice:** [Remove All Adjacent Duplicates in String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

---

### 10. Valid Parentheses

**Problem:** Check if parentheses are balanced.

```cpp
bool isValid(string s) {
    stack<char> st;
    
    for(char ch : s) {
        // Opening brackets
        if(ch == '(' || ch == '{' || ch == '[') {
            st.push(ch);
        }
        // Closing brackets
        else {
            if(st.empty()) return false;
            
            char top = st.top();
            
            if((ch == ')' && top == '(') ||
               (ch == '}' && top == '{') ||
               (ch == ']' && top == '[')) {
                st.pop();
            }
            else {
                return false;
            }
        }
    }
    
    return st.empty();
}

// Usage
isValid("()[]{}");  // true
isValid("([)]");    // false
isValid("{[]}");    // true
```

```python
# Python
def is_valid(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    
    for ch in s:
        if ch in mapping.values():  # Opening bracket
            stack.append(ch)
        elif ch in mapping:  # Closing bracket
            if not stack or stack[-1] != mapping[ch]:
                return False
            stack.pop()
        else:
            return False  # Invalid character
    
    return not stack
```

**Visualization:**
```
"({[]})"

Stack: []
'(': [( ]
'{': [(, { ]
'[': [(, {, [ ]
']': Matches '[', pop → [(, { ]
'}': Matches '{', pop → [( ]
')': Matches '(', pop → []

Stack empty → Valid ✓
```

**Practice:** [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

---

## Edge Case Handling

### Common Edge Cases to Consider

```cpp
// 1. Empty String
string s = "";
if(s.empty()) {
    // Handle empty string
}

// 2. Single Character
if(s.length() == 1) {
    // Handle single character
}

// 3. All Same Characters
"aaaaaaa"

// 4. No Repeating Characters
"abcdefg"

// 5. Null or Invalid Input
if(s == nullptr || s.empty()) {
    return defaultValue;
}

// 6. Case Sensitivity
"Hello" vs "hello"

// 7. Special Characters
"a!b@c#d"

// 8. Spaces
"  hello  world  "

// 9. Unicode Characters
"hello 世界"

// 10. Very Large Input
string s(1000000, 'a');  // 1 million characters
```

```python
# Python
# 1. Empty String
s = ""
if not s:
    # Handle empty string

# 2. Single Character
if len(s) == 1:
    # Handle single character

# 3. All Same Characters
"aaaaaaa"

# 4. No Repeating Characters
"abcdefg"

# 5. None or Invalid Input
if s is None or not s:
    return default_value

# 6. Case Sensitivity
"Hello" vs "hello"

# 7. Special Characters
"a!b@c#d"

# 8. Spaces
"  hello  world  "

# 9. Unicode Characters
"hello 世界"

# 10. Very Large Input
s = 'a' * 1000000  # 1 million characters
```

### Template for Edge Case Handling

```cpp
string processString(string s) {
    // Handle null/empty
    if(s.empty()) {
        return "";  // or appropriate default
    }
    
    // Handle single character
    if(s.length() == 1) {
        return s;  // or process as needed
    }
    
    // Handle case sensitivity
    transform(s.begin(), s.end(), s.begin(), ::tolower);
    
    // Handle special characters
    string filtered = "";
    for(char ch : s) {
        if(isalnum(ch)) {
            filtered += ch;
        }
    }
    
    // Main logic
    // ...
    
    return result;
}
```

```python
# Python
def process_string(s):
    # Handle None/empty
    if not s:
        return ""  # or appropriate default
    
    # Handle single character
    if len(s) == 1:
        return s  # or process as needed
    
    # Handle case sensitivity
    s = s.lower()
    
    # Handle special characters
    filtered = ''.join(ch for ch in s if ch.isalnum())
    
    # Main logic
    # ...
    
    return result
```

---

## Time & Space Complexity Analysis

### Common Patterns

| Operation | Time | Space | Example |
|-----------|------|-------|---------|
| Single pass | O(n) | O(1) | Reverse string |
| Nested loop | O(n²) | O(1) | All substrings |
| Sorting | O(n log n) | O(1) or O(n) | Anagram check |
| Hash map | O(n) | O(k) | Frequency count |
| Sliding window | O(n) | O(k) | Longest substring |
| Two pointer | O(n) | O(1) | Palindrome check |

### Analysis Examples

#### Example 1: Palindrome Check
```cpp
bool isPalindrome(string s) {
    int left = 0, right = s.length() - 1;
    while(left < right) {
        if(s[left] != s[right]) return false;
        left++; right--;
    }
    return true;
}
```
- **Time:** O(n) - Single pass with two pointers
- **Space:** O(1) - Only two integer variables

#### Example 2: Anagram Check with Sorting
```cpp
bool isAnagram(string s, string t) {
    sort(s.begin(), s.end());
    sort(t.begin(), t.end());
    return s == t;
}
```
- **Time:** O(n log n) - Sorting dominates
- **Space:** O(1) or O(n) - Depends on sort implementation

#### Example 3: Longest Substring Without Repeating
```cpp
int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> lastSeen;
    int maxLen = 0, left = 0;
    for(int right = 0; right < s.length(); right++) {
        // ... sliding window logic
    }
    return maxLen;
}
```
- **Time:** O(n) - Single pass
- **Space:** O(min(n, k)) - Hash map stores at most k distinct characters

---

## Final Summary & Checklist

### Must-Know Concepts

✅ **Character Handling:**
- `'a'` vs `"a"` difference
- ASCII values and conversions
- Case conversion techniques
- Character type checking

✅ **Traversal:**
- Forward, backward, two-pointer
- Index vs character access

✅ **Frequency Counting:**
- When to use array (fixed size)
- When to use HashMap (variable/unknown)
- Increment/decrement patterns

✅ **Two Pointer:**
- Same direction
- Opposite direction
- Expand from center

✅ **Sliding Window:**
- Fixed size window
- Variable size window
- When to expand vs shrink
- Tracking max/min length

✅ **Palindrome:**
- Even vs odd length
- Expand around center
- Ignoring special characters

✅ **Anagram:**
- Frequency matching
- Sorting vs frequency array
- Window-based matching

✅ **StringBuilder:**
- When to use over String
- Avoid O(n²) concatenation

✅ **Edge Cases:**
- Empty string
- Single character
- All same/all different
- Special characters

### Problem-Solving Strategy

1. **Understand the Problem**
   - Read carefully
   - Identify input/output
   - Note constraints

2. **Identify Pattern**
   - Frequency counting?
   - Sliding window?
   - Two pointer?
   - Palindrome?
   - Anagram?

3. **Choose Data Structure**
   - Array for fixed size
   - HashMap for dynamic
   - Stack for matching
   - StringBuilder for building

4. **Consider Edge Cases**
   - Empty/null
   - Single element
   - All same/different
   - Special characters

5. **Optimize**
   - Can we do better than O(n²)?
   - Do we need extra space?
   - Can we use two pointers instead of nested loops?

### Practice Plan

**Week 1-2: Basics**
- Character handling
- Simple traversal
- Frequency counting
- Basic two pointer

**Week 3-4: Intermediate**
- Palindrome problems
- Anagram problems
- Simple sliding window
- String building

**Week 5-6: Advanced**
- Variable sliding window
- Minimum window problems
- Complex pattern matching
- Optimization techniques

---

## Complete Problem List by Topic

### 1. Basic String Operations
- [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)
- [Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)

### 2. Palindrome Problems
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/)
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

### 3. Anagram Problems
- [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
- [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
- [Minimum Number of Steps to Make Two Strings Anagram](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/)

### 4. Frequency Array / HashMap
- [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)
- [Sort Characters by Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)
- [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)
- [Determine if Two Strings Are Close](https://leetcode.com/problems/determine-if-two-strings-are-close/)
- [Check If a Sentence Is Pangram](https://leetcode.com/problems/check-if-the-sentence-is-pangram/)

### 5. Sliding Window
**Core:**
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
- [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

**Distinct Characters:**
- [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
- [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/)
- [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/)

**Minimum Window:**
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

### 6. Pattern Matching
- [Implement strStr()](https://leetcode.com/problems/implement-strstr/)
- [Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)
- [Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

### 7. Longest Substring Variations
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [Longest Substring with At Least K Repeating Characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)
- [Longest Nice Substring](https://leetcode.com/problems/longest-nice-substring/)

### 8. String Manipulation
- [String Compression](https://leetcode.com/problems/string-compression/)
- [Remove All Adjacent Duplicates in String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
- [Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)
- [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

---

## Conclusion

Mastering strings requires understanding:
1. **Core concepts** - character handling, null terminator, immutability
2. **Patterns** - two pointer, sliding window, frequency counting
3. **Data structures** - arrays, hash maps, stacks
4. **Optimization** - choosing right approach for time/space complexity
5. **Practice** - solving diverse problems to build intuition
