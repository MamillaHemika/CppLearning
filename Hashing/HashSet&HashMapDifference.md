Hash Set and Hash Map are both implementations of associative containers in C++ and are part of the Standard Template Library (STL). Here’s a detailed comparison between the two, along with examples.

**Definition**

1. **Hash Set (std::unordered_set)**:
    - A hash set is a collection of unique elements.
    - The primary goal is to provide fast access (in average (O(1)) time complexity) to check for existence, add new elements, and remove elements.
    - It does not allow duplicates.
2. **Hash Map (std::unordered_map)**:
    - A hash map is a collection of key-value pairs.
    - It allows you to associate a unique key with a value, providing average (O(1)) access time for searching, inserting, and deleting key-value pairs.
    - Keys must be unique, but values can be duplicated.

**Key Differences:**

| **Feature** | **Hash Set (std::unordered_set)** | **Hash Map (std::unordered_map)** |
| --- | --- | --- |
| Data Structure | Holds only unique values | Holds key-value pairs |
| Duplicate Handling | Does not allow duplicates | Keys must be unique; values can be duplicates |
| Access Method | Access by value | Access by key |
| Iteration Order | No defined order | No defined order |
| Memory Requirements | Requires less memory than uninitialized maps | Requires more memory than sets due to pairs |

**Example of Hash Set**

Here's how you can use a hash set in C++:

# include &lt;iostream&gt;

# include &lt;unordered_set&gt;

int main() {

std::unordered_set&lt;int&gt; mySet;

// Inserting elements

mySet.insert(1);

mySet.insert(2);

mySet.insert(3);

mySet.insert(2); // Duplicate - will be ignored

// Checking for existence

if (mySet.find(2) != mySet.end()) {

std::cout << "2 is in the set.\\n";

}

// Iterating over the set

std::cout << "Elements in the set:\\n";

for (const auto& elem : mySet) {

std::cout << elem << " ";

}

return 0;

}

**Output:**

2 is in the set.

Elements in the set:

1 2 3

**Example of Hash Map**

Here's how to use a hash map in C++:

# include &lt;iostream&gt;

# include &lt;unordered_map&gt;

int main() {

std::unordered_map&lt;std::string, int&gt; myMap;

// Inserting key-value pairs

myMap\["apple"\] = 1;

myMap\["banana"\] = 2;

myMap\["orange"\] = 3;

// Accessing element using key

std::cout << "The value associated with 'apple' is: " << myMap\["apple"\] << '\\n';

// Checking existence of a key

if (myMap.find("banana") != myMap.end()) {

std::cout << "'banana' is in the map with value: " << myMap\["banana"\] << '\\n';

}

// Iterating over the map

std::cout << "Contents of the map:\\n";

for (const auto& pair : myMap) {

std::cout << pair.first << ": " << pair.second << '\\n';

}

return 0;

}

**Output:**

The value associated with 'apple' is: 1

'banana' is in the map with value: 2

Contents of the map:

apple: 1

banana: 2

orange: 3

**Summary**

- **Hash Set** (std::unordered_set):
  - Use it when you need a collection of unique elements and care only about existence.
  - Examples include maintaining a collection of unique usernames or unique IDs.
- **Hash Map** (std::unordered_map):
  - Use it when you need to associate unique keys with values.
  - Examples include counting occurrences of words (where the word is the key and the count is the value) or caching results.

Both hash sets and hash maps provide fast average-time operations for most use cases, making them highly efficient for various applications in competitive programming and software development.
