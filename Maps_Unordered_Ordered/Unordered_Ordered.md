In C++, maps are part of the Standard Template Library (STL) and are used to store key-value pairs. There are two types of maps in C++: **ordered maps** (implemented with std::map) and **unordered maps** (implemented with std::unordered_map). Below, I'll provide detailed explanations of both types, along with examples, dry runs, and intuitions for each.

**Ordered Maps (std::map)**

**Description:**

- std::map is an associative container that stores elements in key-value pairs.
- It maintains the order of its keys based on their underlying values, which means keys are sorted.
- It is typically implemented as a Red-Black Tree.
- Provides logarithmic time complexity for insertion, deletion, and access.

**Syntax:**

# include &lt;map&gt;

std::map&lt;KeyType, ValueType&gt; mapName;

**Basic Operations:**

1. **Insertion**:
    - insert() or operator\[\] can be used to add elements.
2. **Access**:
    - Access a value using the key: mapName\[key\].
3. **Iteration**:
    - You can iterate using iterators or range-based loops.
4. **Deletion**:
    - Use erase(key) to remove an element by its key.

**Example:**

# include &lt;iostream&gt;

# include &lt;map&gt;

int main() {

std::map&lt;int, std::string&gt; myMap;

// Inserting elements

myMap.insert({3, "Three"});

myMap\[1\] = "One";

myMap\[2\] = "Two";

// Accessing an element

std::cout << "Key 2: " << myMap\[2\] << std::endl;

// Iterating through map

for (const auto& pair : myMap) {

std::cout << pair.first << ": " << pair.second << std::endl;

}

// Erasing an element

myMap.erase(2);

// Print after erasure

std::cout << "After erasing key 2:" << std::endl;

for (const auto& pair : myMap) {

std::cout << pair.first << ": " << pair.second << std::endl;

}

return 0;

}

**Output:**

Key 2: Two

1: One

2: Two

3: Three

After erasing key 2:

1: One

3: Three

**Dry Run:**

1. We insert three key-value pairs into the map. The internal ordering based on keys becomes:
    - 1 -> "One"
    - 2 -> "Two"
    - 3 -> "Three"
2. We access the value associated with key 2, which gives us "Two".
3. Iterating through the map in a for-loop prints the elements in the order of keys:
    - 1: One
    - 2: Two
    - 3: Three
4. After erasing the key 2, the remaining elements are:
    - 1: One
    - 3: Three

**Unordered Maps (std::unordered_map)**

**Description:**

- std::unordered_map is also an associative container that stores key-value pairs, but it does not maintain any order among the keys.
- It uses a hash table as its underlying data structure.
- Provides average constant time complexity for insertion, deletion, and access.

**Syntax:**

# include &lt;unordered_map&gt;

std::unordered_map&lt;KeyType, ValueType&gt; unorderedMapName;

**Basic Operations:**

1. **Insertion**:
    - Use insert() or operator\[\].
2. **Access**:
    - Access values using keys: unorderedMapName\[key\].
3. **Iteration**:
    - You can iterate using iterators or range-based loops.
4. **Deletion**:
    - Use erase(key).

**Example:**

# include &lt;iostream&gt;

# include &lt;unordered_map&gt;

int main() {

std::unordered_map&lt;int, std::string&gt; myUnorderedMap;

// Inserting elements

myUnorderedMap.insert({3, "Three"});

myUnorderedMap\[1\] = "One";

myUnorderedMap\[2\] = "Two";

// Accessing an element

std::cout << "Key 2: " << myUnorderedMap\[2\] << std::endl;

// Iterating through unordered map

for (const auto& pair : myUnorderedMap) {

std::cout << pair.first << ": " << pair.second << std::endl;

}

// Erasing an element

myUnorderedMap.erase(2);

// Print after erasure

std::cout << "After erasing key 2:" << std::endl;

for (const auto& pair : myUnorderedMap) {

std::cout << pair.first << ": " << pair.second << std::endl;

}

return 0;

}

**Output (may vary due to unordered nature):**

Key 2: Two

3: Three

1: One

2: Two

After erasing key 2:

3: Three

1: One

**Dry Run:**

1. Similar to the ordered map, we insert three key-value pairs. However, the internal order is not defined as it's based on hashing.
2. Accessing the value associated with key 2 gives "Two".
3. Iterating through the unordered map will show elements in arbitrary order because the order is maintained by their hash values.
4. After erasing key 2, the remaining elements will display without any guaranteed order.

**Key Differences:**

| **Feature** | **std::map** | **std::unordered_map** |
| --- | --- | --- |
| Order | Ordered (sorted by key) | Unordered |
| Internal structure | Red-Black Tree | Hash Table |
| Complexity | O(log n) for search/insert | O(1) average for search/insert |
| Memory Usage | Generally higher | Generally lower |
| Iteration Order | Sorted by keys | Arbitrary |

**When to Use Which:**

- Use std::map when you need ordered data and need to perform range queries.
- Use std::unordered_map when average access speed is more important than order, and you don't need sorted keys.
