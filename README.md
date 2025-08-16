
| User Prompt: |
|-------------|
| I am Studying C++ STANDARD TEMPLATE LIBRARY AND your task is to give me the code for each container with all their functions and methods and everything about them along with what it does in the comment explaining clearly what it does in the comment // and i want you to include everything there is in vector set and other container dont leave anything start from array then pair then vector and so on |

Of course\! I will provide you with a comprehensive guide to the C++ Standard Template Library (STL) containers. We'll go through them in a logical order, starting with the simpler ones and moving to the more complex ones.

Each section will include:

1.  A brief explanation of the container.
2.  The necessary header file.
3.  A C++ code example demonstrating its major functions and methods, with detailed comments explaining each one.

Let's begin this journey into the C++ STL\!

-----

### Introduction to STL Containers

The STL containers are template classes that manage collections of objects. They are broadly categorized into:

  * **Sequence Containers:** Manage a collection of elements in a linear sequence. (`array`, `vector`, `deque`, `list`, `forward_list`)
  * **Associative Containers:** Manage a sorted collection of elements, allowing for fast searching. (`set`, `multiset`, `map`, `multimap`)
  * **Unordered Associative Containers:** Manage an unsorted collection of elements using hash tables for very fast searching on average. (`unordered_set`, `unordered_multiset`, `unordered_map`, `unordered_multimap`)
  * **Container Adapters:** Provide a different interface for an underlying sequence container. (`stack`, `queue`, `priority_queue`)

-----

### `std::pair` (Utility, not a true container)

While not a container itself, `std::pair` is a fundamental building block, especially for maps. It's a simple structure that holds exactly two elements of potentially different types.

**Header:** `<utility>`

```cpp
#include <iostream>
#include <utility> // Required for std::pair
#include <string>

void demonstrate_pair() {
    std::cout << "\n--- std::pair Demonstration ---\n";

    // --- Constructors and Initialization ---

    // Default constructor
    std::pair<int, std::string> p1;
    p1.first = 1;         // Assigning to the first element
    p1.second = "Apple";  // Assigning to the second element

    // Initialization constructor
    std::pair<int, std::string> p2(2, "Banana");

    // Initializer list constructor (C++11)
    std::pair<int, std::string> p3 = {3, "Cherry"};

    // Using std::make_pair to deduce types
    auto p4 = std::make_pair(4, "Dragonfruit");

    std::cout << "p2: (" << p2.first << ", " << p2.second << ")\n";
    std::cout << "p4: (" << p4.first << ", " << p4.second << ")\n";

    // --- Comparison ---
    // Pairs are compared lexicographically: first elements are compared,
    // and if they are equal, the second elements are compared.
    if (p2 < p3) {
        std::cout << "p2 is less than p3.\n"; // This will be printed
    }

    // --- Swapping ---
    p2.swap(p3);
    std::cout << "After swap, p2: (" << p2.first << ", " << p2.second << ")\n"; // Now (3, "Cherry")

    // --- Structured Binding (C++17) ---
    // A modern way to unpack pairs and tuples
    auto [id, name] = p4;
    std::cout << "Unpacked p4 using structured binding: id = " << id << ", name = " << name << "\n";
}

int main() {
    demonstrate_pair();
    return 0;
}
```

-----

### 1\. `std::array`

`std::array` is a fixed-size sequence container that encapsulates a C-style array. Its size is determined at compile time and cannot be changed.

**Header:** `<array>`

```cpp
#include <iostream>
#include <array>     // Required for std::array
#include <algorithm> // for std::sort

// Helper function to print the array contents
void print_array(const auto& arr) {
    for (const auto& elem : arr) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;
}

void demonstrate_array() {
    std::cout << "\n--- std::array Demonstration ---\n";

    // --- Initialization ---
    // The size must be a compile-time constant.
    std::array<int, 5> my_array = {10, 20, 30, 40, 50};

    // --- Element Access ---

    // .at(pos): Access element with bounds checking. Throws std::out_of_range if pos is invalid.
    std::cout << "Element at index 1 using .at(): " << my_array.at(1) << std::endl;

    // operator[]: Access element without bounds checking (faster but potentially unsafe).
    std::cout << "Element at index 2 using []: " << my_array[2] << std::endl;
    my_array[0] = 11; // Modify an element

    // .front(): Access the first element.
    std::cout << "First element using .front(): " << my_array.front() << std::endl;

    // .back(): Access the last element.
    std::cout << "Last element using .back(): " << my_array.back() << std::endl;

    // .data(): Get a raw pointer to the underlying C-style array.
    int* p = my_array.data();
    std::cout << "First element via .data() pointer: " << *p << std::endl;

    // --- Iterators ---
    // Iterators allow you to traverse the container.
    std::cout << "Iterating through the array: ";
    for (auto it = my_array.begin(); it != my_array.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;
    // .begin(): Returns an iterator to the first element.
    // .end(): Returns an iterator to one past the last element.
    // .cbegin(), .cend(): Const versions of the above.
    // .rbegin(), .rend(): Reverse iterators for iterating backwards.

    // --- Capacity ---

    // .empty(): Checks if the array is empty. For std::array, it's false unless size is 0.
    std::cout << "Is the array empty? " << (my_array.empty() ? "Yes" : "No") << std::endl;

    // .size(): Returns the number of elements in the array (which is fixed).
    std::cout << "Size of the array: " << my_array.size() << std::endl;

    // .max_size(): Returns the maximum possible number of elements (same as .size() for std::array).
    std::cout << "Max size of the array: " << my_array.max_size() << std::endl;

    // --- Modifiers ---

    // .fill(value): Sets all elements in the array to a specific value.
    std::array<int, 5> filled_array;
    filled_array.fill(100);
    std::cout << "Array after .fill(100): ";
    print_array(filled_array);

    // .swap(other): Swaps the contents of two arrays of the same type and size.
    my_array.swap(filled_array);
    std::cout << "my_array after swapping with filled_array: ";
    print_array(my_array);

    // Use with STL algorithms
    std::sort(filled_array.begin(), filled_array.end()); // Swap back to sort original
    std::cout << "Original array after sorting: ";
    print_array(filled_array);
}

int main() {
    demonstrate_array();
    return 0;
}
```

-----

### 2\. `std::vector`

`std::vector` is a dynamic array that can grow and shrink in size at runtime. It stores its elements in a contiguous block of memory, allowing for fast random access.

**Header:** `<vector>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // for std::find

// Helper function to print vector
void print_vector(const std::vector<int>& vec) {
    std::cout << "Vector: ";
    for (const int& val : vec) {
        std::cout << val << " ";
    }
    std::cout << "(size: " << vec.size() << ", capacity: " << vec.capacity() << ")" << std::endl;
}

void demonstrate_vector() {
    std::cout << "\n--- std::vector Demonstration ---\n";

    // --- Constructors ---
    std::vector<int> v1;                               // Default constructor (empty)
    std::vector<int> v2(5, 100);                       // Fill constructor: 5 integers with value 100
    std::vector<int> v3 = {1, 2, 3, 4, 5};             // Initializer list (C++11)
    std::vector<int> v4(v3.begin(), v3.begin() + 3);   // Range constructor: elements from v3
    std::vector<int> v5(v3);                           // Copy constructor

    // --- Element Access ---
    // Same as std::array: .at(), [], .front(), .back(), .data()
    std::cout << "v3[1]: " << v3[1] << std::endl;
    std::cout << "v3.at(2): " << v3.at(2) << std::endl;
    std::cout << "v3.front(): " << v3.front() << std::endl;
    std::cout << "v3.back(): " << v3.back() << std::endl;

    // --- Iterators ---
    // Same as std::array: .begin(), .end(), .rbegin(), .rend(), etc.
    std::cout << "v3 using iterators: ";
    for (auto it = v3.cbegin(); it != v3.cend(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // --- Capacity ---
    print_vector(v3);
    // .size(): Number of elements currently in the vector.
    // .capacity(): Number of elements the vector can hold before needing to reallocate memory.
    // .max_size(): Maximum possible number of elements.
    // .empty(): Checks if the vector is empty (size is 0).
    std::cout << "v3 is empty? " << (v3.empty() ? "Yes" : "No") << std::endl;

    // .reserve(n): Request a change in capacity. Guarantees no reallocations until size exceeds n.
    v3.reserve(20);
    std::cout << "After reserving space for 20 elements:\n";
    print_vector(v3);

    // .shrink_to_fit(): Reduces capacity to fit the size.
    v3.shrink_to_fit();
    std::cout << "After shrink_to_fit():\n";
    print_vector(v3);


    // --- Modifiers ---

    // .assign(count, value): Replaces contents with `count` copies of `value`.
    v2.assign(3, 99);
    print_vector(v2);

    // .push_back(value): Appends an element to the end. Might cause reallocation. O(1) amortized.
    v3.push_back(6);
    v3.push_back(7);
    std::cout << "After push_back(6) and push_back(7):\n";
    print_vector(v3);

    // .pop_back(): Removes the last element. Does not shrink capacity.
    v3.pop_back();
    std::cout << "After pop_back():\n";
    print_vector(v3);

    // .insert(pos, value): Inserts an element at a specific position. Invalidates iterators.
    v3.insert(v3.begin() + 1, 88); // Insert 88 at index 1
    std::cout << "After inserting 88 at index 1:\n";
    print_vector(v3);
    // Other overloads: .insert(pos, count, value), .insert(pos, range_begin, range_end)

    // .emplace_back(args...): Constructs an element in-place at the end. More efficient than push_back for objects.
    v3.emplace_back(9); // Same as push_back for simple types like int

    // .emplace(pos, args...): Constructs an element in-place at a specific position.
    v3.emplace(v3.begin(), 0);
    std::cout << "After emplace_back(9) and emplace(begin(), 0):\n";
    print_vector(v3);

    // .erase(pos): Erases the element at a specific position.
    v3.erase(v3.begin() + 2); // Erase element at index 2
    std::cout << "After erasing element at index 2:\n";
    print_vector(v3);

    // .erase(start, end): Erases a range of elements.
    v3.erase(v3.begin() + 3, v3.end()); // Erase from index 3 to the end
    std::cout << "After erasing range from index 3 to end:\n";
    print_vector(v3);

    // .resize(new_size): Changes the number of elements. Fills with default values if growing.
    v3.resize(5);
    std::cout << "After resize(5):\n";
    print_vector(v3);

    // .swap(other): Swaps the contents with another vector.
    v1.swap(v3);
    std::cout << "v1 after swapping with v3:\n";
    print_vector(v1);

    // .clear(): Removes all elements from the vector (size becomes 0).
    v1.clear();
    std::cout << "v1 after clear():\n";
    print_vector(v1);
}

int main() {
    demonstrate_vector();
    return 0;
}
```

-----

### 3\. `std::set`

`std::set` is an associative container that stores a collection of **unique** elements in a **sorted** order. It is typically implemented as a balanced binary search tree (like a Red-Black Tree), which allows for fast search, insertion, and deletion operations (logarithmic time complexity, $O(\\log N)$).

**Header:** `<set>`

```cpp
#include <iostream>
#include <set>
#include <string>

// Helper function to print the set
void print_set(const std::set<int>& s) {
    std::cout << "Set: { ";
    for (int elem : s) {
        std::cout << elem << " ";
    }
    std::cout << "}" << std::endl;
}

void demonstrate_set() {
    std::cout << "\n--- std::set Demonstration ---\n";

    // --- Initialization ---
    std::set<int> s1 = {40, 20, 50, 10, 30, 20}; // Elements are automatically sorted and duplicates removed

    std::cout << "Initial set (duplicates are ignored, elements are sorted):\n";
    print_set(s1);

    // --- Modifiers ---

    // .insert(value): Inserts an element. Returns a pair: an iterator to the element
    // and a bool indicating if the insertion was successful.
    auto result = s1.insert(60);
    std::cout << "Inserted 60. Success? " << (result.second ? "Yes" : "No") << std::endl;
    result = s1.insert(40); // Try to insert a duplicate
    std::cout << "Inserted 40. Success? " << (result.second ? "Yes" : "No") << std::endl;
    print_set(s1);

    // .emplace(args...): Constructs element in-place and inserts it. More efficient.
    s1.emplace(5);
    std::cout << "After emplace(5):\n";
    print_set(s1);

    // .erase(key): Removes an element by its value. Returns number of elements removed (0 or 1).
    size_t num_erased = s1.erase(30);
    std::cout << "Erased 30. Count: " << num_erased << std::endl;
    print_set(s1);

    // .erase(iterator): Removes an element at the given iterator position.
    auto it_to_erase = s1.find(50);
    if (it_to_erase != s1.end()) {
        s1.erase(it_to_erase);
        std::cout << "Erased 50 using iterator.\n";
    }
    print_set(s1);

    // .clear(): Removes all elements.
    // .swap(other): Swaps contents with another set.

    // --- Lookup Operations (all are O(log N)) ---

    // .count(key): Returns the number of elements with a specific key (0 or 1 for set).
    std::cout << "Count of 40 in set: " << s1.count(40) << std::endl;
    std::cout << "Count of 99 in set: " << s1.count(99) << std::endl;

    // .find(key): Returns an iterator to the element if found, otherwise returns .end().
    auto it = s1.find(40);
    if (it != s1.end()) {
        std::cout << "Found 40 in the set." << std::endl;
    } else {
        std::cout << "Did not find 40 in the set." << std::endl;
    }

    // .contains(key) (C++20): A simpler way to check for existence.
    if (s1.contains(20)) {
        std::cout << "The set contains 20." << std::endl;
    }

    // --- Bound Operations ---
    // These are useful for finding ranges.
    std::set<int> s2 = {10, 20, 30, 40, 50};
    print_set(s2);

    // .lower_bound(key): Returns an iterator to the first element that is NOT LESS than key.
    auto lb = s2.lower_bound(25);
    std::cout << "Lower bound of 25 is: " << *lb << std::endl; // -> 30

    // .upper_bound(key): Returns an iterator to the first element that is GREATER than key.
    auto ub = s2.upper_bound(25);
    std::cout << "Upper bound of 25 is: " << *ub << std::endl; // -> 30

    ub = s2.upper_bound(30);
    std::cout << "Upper bound of 30 is: " << *ub << std::endl; // -> 40

    // .equal_range(key): Returns a pair of iterators [lower_bound, upper_bound].
    auto range = s2.equal_range(30);
    std::cout << "Equal range of 30 is: [" << *range.first << ", " << *range.second << ")\n";
}

int main() {
    demonstrate_set();
    return 0;
}
```

*Note on `std::multiset`*: It is almost identical to `std::set`, but it allows duplicate elements. The `.count(key)` method can return values greater than 1, and `.equal_range(key)` will give you the full range of all duplicate elements.\*

-----

This covers the first few and most fundamental containers. I will continue with `std::map`, `std::unordered_set`, `std::unordered_map`, other sequence containers (`deque`, `list`), and finally the container adapters in the next parts to avoid making a single response overwhelmingly long. Please let me know when you are ready for the next set of containers\!


| User Prompt: |
|-------------|
| I am Studying C++ STANDARD TEMPLATE LIBRARY AND your task is to give me the code for each container with all their functions and methods and everything about them along with what it does in the comment explaining clearly what it does in the comment // and i want you to include everything there is in vector set and other container dont leave anything start from array then pair then vector and so on |

```cpp
#include <iostream>
#include <map>
#include <string>

// Helper function to print the map
void print_map(const std::map<std::string, int>& m) {
    std::cout << "Map: {
";
    for (const auto& pair : m) {
        // pair.first is the key (const)
        // pair.second is the value
        std::cout << "  \"" << pair.first << "\": " << pair.second << ",
";
    }
    std::cout << "}
";
}

void demonstrate_map() {
    std::cout << "
--- std::map Demonstration ---
";

    // --- Initialization ---
    std::map<std::string, int> student_scores;

    // --- Modifiers: Inserting Elements ---

    // 1. Using operator[]
    // If the key doesn't exist, it creates a new element with a default-constructed value (0 for int) and then assigns.
    // If the key exists, it overwrites the value.
    student_scores["Alice"] = 95;
    student_scores["Bob"] = 88;
    student_scores["Charlie"] = 72;
    std::cout << "After inserting with []:
";
    print_map(student_scores);

    // 2. Using .insert() with std::pair
    // This is safer as it does NOT overwrite an existing key.
    // It returns a pair: an iterator to the element and a bool indicating success.
    auto result = student_scores.insert(std::make_pair("David", 91));
    std::cout << "Inserted David. Success? " << (result.second ? "Yes" : "No") << std::endl;

    result = student_scores.insert({"Alice", 100}); // Trying to insert an existing key
    std::cout << "Inserted Alice again. Success? " << (result.second ? "Yes" : "No") << std::endl;
    std::cout << "Value for Alice remains: " << student_scores["Alice"] << std::endl; // Value is still 95
    print_map(student_scores);

    // 3. Using .emplace()
    // Constructs the key-value pair in-place. More efficient than .insert().
    student_scores.emplace("Eve", 85);
    std::cout << "After emplace(\"Eve\", 85):
";
    print_map(student_scores);

    // 4. Using .try_emplace() (C++17)
    // Like emplace, but only constructs the value if the key doesn't already exist.
    // It does not move from its arguments if insertion fails.
    student_scores.try_emplace("Frank", 99);       // Frank is new, will be inserted.
    student_scores.try_emplace("Alice", 0);        // Alice exists, nothing happens.
    std::cout << "After try_emplace(\"Frank\", 99) and try_emplace(\"Alice\", 0):
";
    print_map(student_scores);

    // 5. Using insert_or_assign() (C++17)
    // Inserts if key doesn't exist, otherwise updates the value.
    // Returns a pair: iterator to the element and bool (true if inserted, false if assigned).
    auto res_ioa = student_scores.insert_or_assign("Bob", 90); // Bob exists, value updated.
    std::cout << "insert_or_assign for Bob: " << (res_ioa.second ? "Inserted" : "Assigned") << std::endl;
    res_ioa = student_scores.insert_or_assign("Grace", 78); // Grace is new, inserted.
    std::cout << "insert_or_assign for Grace: " << (res_ioa.second ? "Inserted" : "Assigned") << std::endl;
    print_map(student_scores);

    // --- Element Access ---

    // 1. Using operator[]
    // WARNING: If the key does not exist, this will create a new element!
    std::cout << "Score of Bob: " << student_scores["Bob"] << std::endl;
    // std::cout << "Score of Zack: " << student_scores["Zack"] << std::endl; // This would add "Zack": 0 to the map

    // 2. Using .at()
    // Safer access. Throws std::out_of_range if the key does not exist.
    try {
        std::cout << "Score of Alice: " << student_scores.at("Alice") << std::endl;
        // std::cout << "Score of Zack: " << student_scores.at("Zack") << std::endl; // This would throw an exception
    } catch (const std::out_of_range& e) {
        std::cerr << "Error: " << e.what() << '
';
    }

    // --- Lookup Operations (all are O(log N)) ---

    // .find(key): Returns an iterator to the element if found, otherwise returns .end().
    auto it = student_scores.find("Eve");
    if (it != student_scores.end()) {
        std::cout << "Found Eve with score: " << it->second << std::endl;
    } else {
        std::cout << "Eve not found." << std::endl;
    }

    // .count(key): Returns 1 if the key exists, 0 otherwise.
    std::cout << "Does Charlie exist? Count: " << student_scores.count("Charlie") << std::endl;

    // .contains(key) (C++20): A more direct way to check for key existence.
    if (student_scores.contains("David")) {
        std::cout << "The map contains a record for David." << std::endl;
    }

    // --- Modifiers: Removing Elements ---

    // .erase(key): Removes an element by its key. Returns the number of elements removed (0 or 1).
    size_t num_erased = student_scores.erase("Charlie");
    std::cout << "Erased Charlie. Count: " << num_erased << std::endl;
    print_map(student_scores);

    // .erase(iterator): Removes an element at a specific iterator position.
    auto it_to_erase = student_scores.find("Frank");
    if (it_to_erase != student_scores.end()) {
        student_scores.erase(it_to_erase);
        std::cout << "Erased Frank using an iterator.
";
    }
    print_map(student_scores);

    // --- Capacity ---
    // .empty(): Checks if the map is empty.
    // .size(): Returns the number of key-value pairs.
    std::cout << "Current size of map: " << student_scores.size() << std::endl;

    // --- Bound Operations (like std::set) ---
    // .lower_bound(key): Iterator to first element with key not less than the given key.
    // .upper_bound(key): Iterator to first element with key greater than the given key.
    auto lb = student_scores.lower_bound("Bob");
    if (lb != student_scores.end()) {
        std::cout << "Lower bound of \"Bob\" is key: \"" << lb->first << "\"" << std::endl;
    }
}

int main() {
    demonstrate_map();
    return 0;
}
```


| User Prompt: |
|-------------|
| I want you to tell me leach and every way to assign, access and all dont leave even a single thing i need everything lets start from array |

Of course. I understand you want a completely exhaustive guide, covering every method, nuance, and way of interacting with each container. Let's start from the beginning with `std::array` and be extremely thorough.

-----

### Masterclass: `std::array`

`std::array` is a container that encapsulates a fixed-size C-style array. It is defined in the `<array>` header.

**Core Characteristics:**

  * **Fixed Size:** The size of a `std::array` is determined at compile-time and cannot be changed. This size is part of its type. `std::array<int, 5>` and `std::array<int, 6>` are two completely different types.
  * **Contiguous Memory:** Its elements are stored in a single, contiguous block of memory, just like a C-style array. This allows for efficient element access and traversal.
  * **Aggregate Type:** It's an aggregate, which means it can be initialized directly from an initializer list (`{...}`).
  * **Value Semantics:** It behaves like a regular value. It can be copied and assigned, which copies all elements.
  * **Performance:** Offers the same raw performance as a C-style array (no overhead for access) but with the benefits of a standard container (iterators, size information, etc.).

-----

### The Complete Code for `std::array`

```cpp
#include <iostream>
#include <array>
#include <stdexcept> // Required for std::out_of_range
#include <algorithm> // Required for std::sort, std::for_each
#include <numeric>   // Required for std::accumulate

// Helper function to print an array's contents and its size
template <typename T, std::size_t N>
void print_array(const std::string& name, const std::array<T, N>& arr) {
    std::cout << name << " (size " << N << "): [ ";
    for (const auto& elem : arr) {
        std::cout << elem << " ";
    }
    std::cout << "]" << std::endl;
}

int main() {
    std::cout << "--- 1. Initialization and Assignment ---\n\n";

    // 1.1. Aggregate Initialization (the most common way)
    // All elements are provided.
    std::array<int, 5> arr1 = {10, 20, 30, 40, 50};
    print_array("arr1 (full initialization)", arr1);

    // 1.2. Partial Aggregate Initialization
    // Fewer initializers than the size of the array. The remaining elements are value-initialized.
    // For fundamental types like 'int', value-initialization means zero-initialization.
    std::array<int, 5> arr2 = {11, 22}; // arr2 will be {11, 22, 0, 0, 0}
    print_array("arr2 (partial initialization)", arr2);

    // 1.3. Zero Initialization
    // Using an empty initializer list value-initializes all elements.
    std::array<int, 5> arr3 = {}; // arr3 will be {0, 0, 0, 0, 0}
    print_array("arr3 (zero initialization)", arr3);

    // 1.4. Default Initialization (Leaves non-class types with indeterminate values!)
    // WARNING: This is dangerous for fundamental types as their values will be garbage.
    std::array<int, 5> arr4; // Values of arr4 are indeterminate (garbage)
    std::cout << "arr4 (default initialization): [ contains garbage values ]" << std::endl;

    // 1.5. Copy Initialization
    std::array<int, 5> arr5 = arr1;
    print_array("arr5 (copy of arr1)", arr5);

    // 1.6. Copy Assignment
    // Overwrites all elements of arr4 with elements from arr1.
    arr4 = arr1;
    print_array("arr4 (assigned from arr1)", arr4);

    // 1.7. `fill()` method - Assigns a single value to all elements.
    std::array<int, 5> arr6;
    arr6.fill(100); // arr6 becomes {100, 100, 100, 100, 100}
    print_array("arr6 (filled with 100)", arr6);

    // 1.8. `swap()` method - Swaps the content of two arrays.
    // This is a member function. Both arrays must be of the same type AND size.
    arr1.swap(arr6);
    print_array("arr1 (after swap with arr6)", arr1);
    print_array("arr6 (after swap with arr1)", arr6);

    // 1.9. `std::swap()` - The non-member function version (also works).
    std::swap(arr1, arr6);
    print_array("arr1 (swapped back with std::swap)", arr1);

    // 1.10. `std::to_array` (C++20) - Deduces type and size to create an array.
    auto arr7 = std::to_array({1, 8, 2, 7, 3}); // Deduces std::array<int, 5>
    print_array("arr7 (from std::to_array)", arr7);
    auto arr8 = std::to_array("Hi"); // Deduces std::array<char, 3> for {'H', 'i', '\0'}
    print_array("arr8 (from std::to_array)", arr8);

    std::cout << "\n\n--- 2. Element Access ---\n\n";

    // 2.1. `operator[]` - The square bracket accessor.
    // Provides the fastest access. NO bounds checking. Accessing out of bounds is undefined behavior.
    std::cout << "arr1[0] = " << arr1[0] << std::endl; // Access first element
    arr1[4] = 55; // Modify last element
    std::cout << "arr1[4] after modification = " << arr1[4] << std::endl;
    // std::cout << arr1[5]; // UNDEFINED BEHAVIOR - program could crash or act weirdly.

    // 2.2. `at()` method - Safe access.
    // PERFORMS bounds checking. Throws `std::out_of_range` if the index is invalid.
    std::cout << "arr1.at(1) = " << arr1.at(1) << std::endl;
    try {
        arr1.at(5) = 99; // This will throw an exception
    } catch (const std::out_of_range& e) {
        std::cerr << "Caught exception when accessing arr1.at(5): " << e.what() << '\n';
    }

    // 2.3. `front()` - Direct access to the first element.
    // Equivalent to `arr1[0]` or `*arr1.begin()`.
    std::cout << "arr1.front() = " << arr1.front() << std::endl;

    // 2.4. `back()` - Direct access to the last element.
    // Equivalent to `arr1[arr1.size() - 1]`.
    std::cout << "arr1.back() = " << arr1.back() << std::endl;

    // 2.5. `data()` - Get a raw pointer to the underlying data.
    // Useful for interoperability with C-style functions that expect pointers.
    int* p_data = arr1.data();
    std::cout << "Value at the beginning of data() pointer: " << *p_data << std::endl;
    *(p_data + 1) = 22; // Modify the second element via pointer arithmetic
    print_array("arr1 (after modification via data())", arr1);

    // 2.6. `std::get<I>` (compile-time index access)
    // The index `I` must be a compile-time constant.
    std::cout << "std::get<2>(arr1) = " << std::get<2>(arr1) << std::endl;
    std::get<2>(arr1) = 33;
    std::cout << "std::get<2>(arr1) after modification = " << std::get<2>(arr1) << std::endl;


    std::cout << "\n\n--- 3. Iterators ---\n\n";
    std::sort(arr1.begin(), arr1.end()); // Use iterators with an algorithm
    print_array("arr1 (sorted)", arr1);

    // 3.1. Forward Iterators
    // .begin(): iterator to the first element.
    // .end(): iterator to PAST the last element.
    std::cout << "Forward iteration with begin/end: ";
    for (auto it = arr1.begin(); it != arr1.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 3.2. Const Forward Iterators
    // .cbegin() / .cend(): 'const_iterator' versions. Cannot be used to modify elements.
    std::cout << "Forward iteration with cbegin/cend: ";
    for (auto it = arr1.cbegin(); it != arr1.cend(); ++it) {
        // *it = 100; // This would be a COMPILE ERROR because 'it' is a const_iterator
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 3.3. Reverse Iterators
    // .rbegin(): reverse iterator pointing to the last element.
    // .rend(): reverse iterator pointing to BEFORE the first element.
    std::cout << "Reverse iteration with rbegin/rend: ";
    for (auto it = arr1.rbegin(); it != arr1.rend(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 3.4. Const Reverse Iterators
    // .crbegin() / .crend(): const versions of reverse iterators.
    std::cout << "Reverse iteration with crbegin/crend: ";
    for (auto it = arr1.crbegin(); it != arr1.crend(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    std::cout << "\n\n--- 4. Capacity and Size ---\n\n";
    
    // 4.1. `empty()` - Checks if the array has a size of 0.
    // This is a `constexpr`, so it can be evaluated at compile-time.
    std::cout << "Is arr1 empty? " << (arr1.empty() ? "Yes" : "No") << std::endl;
    std::array<int, 0> empty_arr;
    std::cout << "Is empty_arr empty? " << (empty_arr.empty() ? "Yes" : "No") << std::endl;
    
    // 4.2. `size()` - Returns the number of elements.
    // This is a `constexpr`. For `std::array<T, N>`, it always returns `N`.
    std::cout << "Size of arr1: " << arr1.size() << std::endl;
    
    // 4.3. `max_size()` - Returns the maximum possible number of elements.
    // For `std::array`, this is always the same as `size()`.
    std::cout << "Max size of arr1: " << arr1.max_size() << std::endl;
    
    
    std::cout << "\n\n--- 5. Non-Member Functions and Utilities ---\n\n";

    // 5.1. Relational Operators (==, !=, <, >, <=, >=)
    // They perform lexicographical comparison on the elements.
    std::array<int, 5> arr1_copy = arr1;
    std::array<int, 5> arr_different = {1, 2, 3, 4, 5};
    std::cout << "arr1 == arr1_copy? " << (arr1 == arr1_copy ? "Yes" : "No") << std::endl;
    std::cout << "arr1 != arr_different? " << (arr1 != arr_different ? "Yes" : "No") << std::endl;
    std::cout << "arr1 < arr_different? " << (arr1 < arr_different ? "Yes" : "No") << std::endl; // Compares 10 vs 1

    // 5.2. Structured Bindings (C++17)
    // A clean way to unpack the array's elements into named variables.
    // The number of variables must exactly match the array size.
    auto [a, b, c, d, e] = arr_different;
    std::cout << "Unpacked arr_different: a=" << a << ", b=" << b << ", c=" << c << ", d=" << d << ", e=" << e << std::endl;
    
    return 0;
}
```

### Summary of `std::array`

  * **When to use it:** Use `std::array` when you know the size of your collection at compile time and you do not need it to change. It is a direct, safe, and modern replacement for C-style arrays (`int arr[5];`). Examples: a 3D coordinate point (`std::array<float, 3>`), a fixed-size buffer, or a lookup table.
  * **Strengths:**
      * Zero-cost abstraction over C-style arrays.
      * Knows its own size (`.size()`).
      * Provides safe access (`.at()`) and iterators for use with STL algorithms.
      * Can be returned from functions by value easily.
  * **Weaknesses:**
      * Inflexible size. If you need a collection that can grow or shrink, you must use `std::vector` or another dynamic container.

This covers every aspect of creating, assigning, accessing, and using `std::array`. Are you ready for the deep dive into `std::pair` and `std::tuple`?


| User Prompt: |
|-------------|
| Yes |

```cpp
#include <iostream>
#include <utility> // Required for std::pair, std::make_pair, std::piecewise_construct
#include <string>
#include <vector>
#include <tuple>   // Required for std::tuple, std::make_tuple, std::tie, etc.

void demonstrate_pair() {
    std::cout << "
// --- std::pair Masterclass --- //
";

    // --- 1. Initialization and Construction ---

    // 1.1. Default Constructor
    // The elements 'first' and 'second' are themselves default-constructed.
    // For int, this means it has an indeterminate (garbage) value. For std::string, it's an empty string.
    std::pair<int, std::string> p1;
    std::cout << "1.1. p1 (default constructed): { " << p1.first << " (garbage), \"" << p1.second << "\" }" << std::endl;

    // 1.2. Value Initialization
    // Using {} ensures elements are value-initialized (0 for int, empty for string).
    std::pair<int, std::string> p2{};
    std::cout << "1.2. p2 (value initialized): { " << p2.first << ", \"" << p2.second << "\" }" << std::endl;

    // 1.3. Constructor with values
    std::pair<int, std::string> p3(1, "Apple");
    std::cout << "1.3. p3 (value constructor): { " << p3.first << ", \"" << p3.second << "\" }" << std::endl;

    // 1.4. Copy Constructor
    std::pair<int, std::string> p4(p3);
    std::cout << "1.4. p4 (copy of p3): { " << p4.first << ", \"" << p4.second << "\" }" << std::endl;

    // 1.5. Move Constructor (C++11)
    // Efficiently moves resources from a temporary pair.
    std::pair<int, std::string> p5(std::pair<int, std::string>(2, "Banana"));
    std::cout << "1.5. p5 (move constructed): { " << p5.first << ", \"" << p5.second << "\" }" << std::endl;

    // 1.6. std::make_pair() helper function
    // Deduces the types automatically, which was very useful before C++17's class template argument deduction.
    auto p6 = std::make_pair(3, "Cherry"); // p6 is of type std::pair<int, const char*>
    std::cout << "1.6. p6 (from make_pair): { " << p6.first << ", \"" << p6.second << "\" }" << std::endl;

    // 1.7. Piecewise Construction (for complex objects)
    // Constructs the 'first' and 'second' members in-place using the provided arguments,
    // avoiding the creation of temporary objects.
    // Here, we construct a vector with 3 elements of value 100, and a string from 5 'X' characters.
    std::pair<std::vector<int>, std::string> p7(
        std::piecewise_construct,
        std::forward_as_tuple(3, 100),       // Arguments for std::vector's constructor
        std::forward_as_tuple(5, 'X')        // Arguments for std::string's constructor
    );
    std::cout << "1.7. p7.second (piecewise): " << p7.second << std::endl;


    // --- 2. Assignment ---

    // 2.1. Copy Assignment
    p2 = p3;
    std::cout << "2.1. p2 (copy assigned from p3): { " << p2.first << ", \"" << p2.second << "\" }" << std::endl;

    // 2.2. Move Assignment
    p1 = std::pair<int, std::string>(4, "Dragonfruit");
    std::cout << "2.2. p1 (move assigned): { " << p1.first << ", \"" << p1.second << "\" }" << std::endl;


    // --- 3. Element Access ---

    // 3.1. Public members .first and .second
    p1.first = 5;
    p1.second = "Elderberry";
    std::cout << "3.1. p1 after modifying .first & .second: { " << p1.first << ", \"" << p1.second << "\" }" << std::endl;

    // 3.2. std::get<I> (I must be a compile-time constant 0 or 1)
    std::get<0>(p1) = 6; // Access .first
    std::get<1>(p1) = "Fig"; // Access .second
    std::cout << "3.2. p1 after modifying via std::get: { " << std::get<0>(p1) << ", \"" << std::get<1>(p1) << "\" }" << std::endl;


    // --- 4. Comparison Operators ---
    // Comparisons are done lexicographically: .first is compared first.
    // If .first members are equal, then .second members are compared.
    std::pair<int, std::string> p_comp1(10, "Zebra");
    std::pair<int, std::string> p_comp2(20, "Apple");
    std::pair<int, std::string> p_comp3(10, "Yak");

    std::cout << "4. Comparison: (10, Z) < (20, A)? " << std::boolalpha << (p_comp1 < p_comp2) << std::endl; // true, because 10 < 20
    std::cout << "4. Comparison: (10, Z) < (10, Y)? " << std::boolalpha << (p_comp1 < p_comp3) << std::endl; // false, because 10==10 and 'Z' > 'Y'
    std::cout << "4. Comparison: (10, Z) == (10, Z)? " << std::boolalpha << (p_comp1 == p_comp1) << std::endl; // true


    // --- 5. Swapping ---

    // 5.1. Member function swap()
    p1.swap(p3);
    std::cout << "5.1. p1 after member swap with p3: { " << p1.first << ", \"" << p1.second << "\" }" << std::endl;

    // 5.2. Non-member function std::swap() (usually preferred)
    std::swap(p1, p3);
    std::cout << "5.2. p1 after std::swap with p3: { " << p1.first << ", \"" << p1.second << "\" }" << std::endl;


    // --- 6. Structured Bindings (C++17) ---
    // The most convenient and modern way to unpack a pair into named variables.
    auto [id, name] = p1;
    std::cout << "6. Unpacked p1 with structured bindings: id=" << id << ", name=\"" << name << "\"" << std::endl;
}

void demonstrate_tuple() {
    std::cout << "

// --- std::tuple Masterclass --- //
";

    // A tuple is a generalization of a pair to any number of elements.

    // --- 1. Initialization and Construction ---

    // 1.1. Default constructor (elements are default-constructed)
    std::tuple<int, std::string, double> t1;

    // 1.2. Constructor with values
    std::tuple<int, std::string, double> t2(1, "Hello", 3.14);

    // 1.3. Copy/Move constructors work similarly to std::pair

    // 1.4. std::make_tuple() helper function (deduces types)
    auto t3 = std::make_tuple(2, std::string("World"), 2.718);

    // --- 2. Element Access ---
    // MUST use std::get<I>(). There are no .first, .second, etc. members.
    // The index I must be a compile-time constant.
    std::cout << "2. Accessing t2: { "
              << std::get<0>(t2) << ", "
              << std::get<1>(t2) << ", "
              << std::get<2>(t2) << " }" << std::endl;

    // Modification via std::get
    std::get<1>(t3) = "C++";
    std::cout << "2. t3 after modification: { " << std::get<0>(t3) << ", " << std::get<1>(t3) << " }" << std::endl;

    // --- 3. Unpacking a tuple ---

    // 3.1. Structured Bindings (C++17) - The BEST way
    auto [id, message, value] = t3;
    std::cout << "3.1. Unpacked t3 with structured bindings: id=" << id << ", msg=\"" << message << "\", val=" << value << std::endl;

    // 3.2. std::tie() - The traditional way (pre-C++17)
    // Creates a tuple of lvalue-references to existing variables.
    // Useful for assigning from a function that returns a tuple.
    int my_id;
    std::string my_msg;
    double my_val;

    std::tie(my_id, my_msg, my_val) = t3; // Unpacks t3 into these variables
    std::cout << "3.2. Unpacked t3 with std::tie: id=" << my_id << ", msg=\"" << my_msg << "\", val=" << my_val << std::endl;

    // Using std::ignore with std::tie to skip an element
    std::tie(std::ignore, my_msg, std::ignore) = t2;
    std::cout << "3.2. Unpacked only the string from t2: \"" << my_msg << "\"" << std::endl;


    // --- 4. Tuple Helper Functions ---

    // 4.1. std::tuple_size - Gets the number of elements at COMPILE TIME.
    constexpr size_t size_of_t3 = std::tuple_size<decltype(t3)>::value;
    std::cout << "4.1. Compile-time size of t3: " << size_of_t3 << std::endl;

    // 4.2. std::tuple_element - Gets the type of an element at a given index.
    std::tuple_element<1, decltype(t3)>::type string_from_tuple = std::get<1>(t3);
    std::cout << "4.2. Variable of deduced type from tuple element 1: \"" << string_from_tuple << "\"" << std::endl;

    // 4.3. std::tuple_cat - Concatenates multiple tuples.
    auto t4 = std::tuple_cat(t2, t3, std::make_tuple(true, 'Z'));
    std::cout << "4.3. Concatenated tuple t4: { "
              << std::get<0>(t4) << ", " << std::get<1>(t4) << ", "
              << std::get<2>(t4) << ", " << std::get<3>(t4) << ", "
              << std::get<4>(t4) << ", " << std::get<5>(t4) << ", "
              << std::get<6>(t4) << " }" << std::endl;

    // Comparison and swap work just like for std::pair (lexicographically).
}

int main() {
    demonstrate_pair();
    demonstrate_tuple();
    return 0;
}
```


| User Prompt: |
|-------------|
| Yes next |

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <stdexcept> // For std::out_of_range
#include <algorithm> // For std::sort, std::find

// Helper function to print a vector's state
template <typename T>
void print_vector(const std::string& name, const std::vector<T>& vec) {
    std::cout << name << ": [ ";
    for (const auto& elem : vec) {
        std::cout << elem << " ";
    }
    std::cout << "]"
              << " | size: " << vec.size()
              << " | capacity: " << vec.capacity() << std::endl;
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Default Constructor
    // Creates an empty vector with size 0 and capacity 0.
    std::vector<int> v1;
    print_vector("v1 (default)", v1);

    // 1.2. Fill Constructor
    // Creates a vector with 'n' elements, each initialized to 'value'.
    std::vector<int> v2(5, 100); // 5 integers with the value 100
    print_vector("v2 (fill)", v2);

    // 1.3. Range Constructor
    // Copies elements from a range [first, last).
    std::vector<int> v3(v2.begin(), v2.begin() + 3); // Copies the first 3 elements of v2
    print_vector("v3 (range)", v3);

    // 1.4. Copy Constructor
    // Creates a new vector as a copy of an existing one.
    std::vector<int> v4(v3);
    print_vector("v4 (copy)", v4);

    // 1.5. Move Constructor (C++11)
    // "Steals" the internal data from a temporary vector, which is very efficient.
    std::vector<int> v5(std::vector<int>{1, 2, 3});
    print_vector("v5 (move)", v5);

    // 1.6. Initializer List Constructor (C++11)
    // The most common way to create a vector with initial values.
    std::vector<int> v6 = {10, 20, 30, 40, 50};
    print_vector("v6 (initializer list)", v6);


    std::cout << "

--- 2. Assignment ---

";

    // 2.1. Copy Assignment Operator (=)
    v1 = v6;
    print_vector("v1 (copy assigned)", v1);

    // 2.2. Move Assignment Operator (=)
    v1 = std::vector<int>{9, 8, 7};
    print_vector("v1 (move assigned)", v1);

    // 2.3. Initializer List Assignment
    v1 = {99, 88, 77, 66};
    print_vector("v1 (initializer list assigned)", v1);

    // 2.4. assign() method
    // Replaces the entire content of the vector.
    v2.assign(4, -1); // Fill version: 4 elements with value -1
    print_vector("v2 (assign fill)", v2);
    v3.assign(v6.begin(), v6.end()); // Range version
    print_vector("v3 (assign range)", v3);


    std::cout << "

--- 3. Capacity Management ---

";
    std::vector<int> cap_vec = {1};
    print_vector("cap_vec (initial)", cap_vec);

    // 3.1. size(): Number of elements currently in the vector.
    // 3.2. capacity(): Storage space currently allocated. Always >= size().
    // 3.3. empty(): Returns true if size() is 0.
    std::cout << "Is cap_vec empty? " << std::boolalpha << cap_vec.empty() << std::endl;

    // 3.4. reserve(): Increase the capacity to a value >= new_cap.
    // Useful for preventing reallocations if you know how many elements you'll add.
    cap_vec.reserve(10);
    print_vector("cap_vec (reserved 10)", cap_vec);
    cap_vec.push_back(2); // No reallocation will happen here
    cap_vec.push_back(3); // or here...
    print_vector("cap_vec (after pushes)", cap_vec);

    // 3.5. shrink_to_fit(): Requests the container to reduce its capacity to fit its size.
    // This is a non-binding request; the library implementation is free to ignore it.
    cap_vec.shrink_to_fit();
    print_vector("cap_vec (shrunk)", cap_vec);

    // 3.6. resize(): Changes the size of the vector.
    cap_vec.resize(8); // If new size > old size, new elements are value-initialized (0 for int)
    print_vector("cap_vec (resized to 8)", cap_vec);
    cap_vec.resize(2); // If new size < old size, elements are destroyed from the end.
    print_vector("cap_vec (resized to 2)", cap_vec);

    // 3.7. max_size(): The absolute maximum number of elements the vector could theoretically hold.
    std::cout << "Max size for a vector<int>: " << cap_vec.max_size() << std::endl;


    std::cout << "

--- 4. Element Access ---

";
    std::vector<int> acc_vec = {10, 20, 30};

    // 4.1. operator[]: Fast, but NO bounds checking.
    std::cout << "acc_vec[1] = " << acc_vec[1] << std::endl;
    // std::cout << acc_vec[5]; // Undefined Behavior!

    // 4.2. at(): Slower, but SAFE. Performs bounds checking and throws std::out_of_range.
    try {
        std::cout << "acc_vec.at(2) = " << acc_vec.at(2) << std::endl;
        std::cout << acc_vec.at(5);
    } catch (const std::out_of_range& e) {
        std::cerr << "Caught exception: " << e.what() << std::endl;
    }

    // 4.3. front(): Direct access to the first element.
    std::cout << "acc_vec.front() = " << acc_vec.front() << std::endl;

    // 4.4. back(): Direct access to the last element.
    std::cout << "acc_vec.back() = " << acc_vec.back() << std::endl;

    // 4.5. data(): Returns a direct pointer to the underlying C-style array.
    int* p_data = acc_vec.data();
    std::cout << "First element via data(): " << *p_data << std::endl;
    *(p_data + 1) = 22; // Modify element via pointer
    print_vector("acc_vec (modified via data())", acc_vec);


    std::cout << "

--- 5. Modifiers (Adding/Removing Elements) ---

";
    std::vector<int> mod_vec = {100, 200, 300};
    print_vector("mod_vec (initial)", mod_vec);

    // 5.1. push_back(): Appends an element to the end. Amortized O(1).
    mod_vec.push_back(400);
    print_vector("mod_vec (pushed 400)", mod_vec);

    // 5.2. emplace_back() (C++11): Constructs the element in-place at the end.
    // More efficient than push_back for complex objects as it avoids creating a temporary.
    mod_vec.emplace_back(500); // For int, it's the same as push_back.
    print_vector("mod_vec (emplaced 500)", mod_vec);

    // 5.3. pop_back(): Removes the last element. Does not shrink capacity. O(1).
    mod_vec.pop_back();
    print_vector("mod_vec (popped back)", mod_vec);

    // 5.4. insert(): Inserts elements at a specified position. Slow (O(N)).
    // **IMPORTANT**: insert/erase can invalidate all iterators, pointers, and references to elements.
    auto it_insert = mod_vec.begin() + 1;
    mod_vec.insert(it_insert, 150); // Insert single value
    print_vector("mod_vec (inserted 150)", mod_vec);

    it_insert = mod_vec.begin() + 2;
    mod_vec.insert(it_insert, 2, 175); // Insert 2 copies of 175
    print_vector("mod_vec (inserted 2x 175)", mod_vec);

    // 5.5. emplace() (C++11): Constructs element in-place at a specified position. Slow (O(N)).
    mod_vec.emplace(mod_vec.begin(), 50);
    print_vector("mod_vec (emplaced 50)", mod_vec);

    // 5.6. erase(): Removes elements. Slow (O(N)).
    mod_vec.erase(mod_vec.begin() + 1); // Erase the second element
    print_vector("mod_vec (erased 2nd elem)", mod_vec);

    mod_vec.erase(mod_vec.begin() + 2, mod_vec.end()); // Erase a range of elements
    print_vector("mod_vec (erased range)", mod_vec);

    // 5.7. clear(): Removes all elements. Size becomes 0, capacity is unchanged.
    mod_vec.clear();
    print_vector("mod_vec (cleared)", mod_vec);


    std::cout << "

--- 6. Non-Member Functions and Utilities ---

";
    std::vector<int> util_vec = {5, 1, 4, 2, 3};
    std::vector<int> util_vec2 = {5, 1, 4, 2, 3};
    std::vector<int> util_vec3 = {9, 8, 7};

    // 6.1. Relational Operators (==, !=, <, etc.)
    // Perform lexicographical comparison.
    std::cout << "util_vec == util_vec2? " << std::boolalpha << (util_vec == util_vec2) << std::endl; // true
    std::cout << "util_vec < util_vec3? " << std::boolalpha << (util_vec < util_vec3) << std::endl;  // true, because 5 < 9

    // 6.2. std::swap()
    std::swap(util_vec, util_vec3);
    print_vector("util_vec (swapped)", util_vec);
    print_vector("util_vec3 (swapped)", util_vec3);

    // 6.3. std::erase / std::erase_if (C++20)
    // A convenient way to remove all elements matching a value or predicate.
    std::vector<int> erase_vec = {1, 2, 3, 2, 4, 2, 5};
    std::erase(erase_vec, 2); // Remove all elements with the value 2
    print_vector("erase_vec (erased 2s)", erase_vec);

    std::erase_if(erase_vec, [](int x){ return x % 2 == 1; }); // Remove all odd numbers
    print_vector("erase_vec (erased odds)", erase_vec);

    return 0;
}
```


| User Prompt: |
|-------------|
| Continue |

```cpp
#include <iostream>
#include <deque>
#include <string>
#include <algorithm> // For std::sort
#include <stdexcept> // For std::out_of_range

// Helper function to print a deque's state
// Note: Deque does not have capacity().
template <typename T>
void print_deque(const std::string& name, const std::deque<T>& deq) {
    std::cout << name << ": [ ";
    for (const auto& elem : deq) {
        std::cout << elem << " ";
    }
    std::cout << "]"
              << " | size: " << deq.size() << std::endl;
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Default Constructor
    std::deque<int> d1;
    print_deque("d1 (default)", d1);

    // 1.2. Fill Constructor
    std::deque<int> d2(5, 100); // 5 integers with the value 100
    print_deque("d2 (fill)", d2);

    // 1.3. Range Constructor
    std::deque<int> d3(d2.begin(), d2.begin() + 3);
    print_deque("d3 (range)", d3);

    // 1.4. Copy Constructor
    std::deque<int> d4(d3);
    print_deque("d4 (copy)", d4);

    // 1.5. Move Constructor
    std::deque<int> d5(std::deque<int>{1, 2, 3});
    print_deque("d5 (move)", d5);

    // 1.6. Initializer List Constructor
    std::deque<int> d6 = {10, 20, 30, 40, 50};
    print_deque("d6 (initializer list)", d6);


    std::cout << "

--- 2. Element Access ---

";
    // Access methods are identical to std::vector's interface.
    // Note: There is NO .data() method because memory is not contiguous.

    // 2.1. operator[]: Fast, NO bounds checking.
    std::cout << "d6[1] = " << d6[1] << std::endl;

    // 2.2. at(): Safe, performs bounds checking.
    try {
        std::cout << "d6.at(2) = " << d6.at(2) << std::endl;
        std::cout << d6.at(10);
    } catch (const std::out_of_range& e) {
        std::cerr << "Caught exception: " << e.what() << std::endl;
    }

    // 2.3. front(): Direct access to the first element.
    std::cout << "d6.front() = " << d6.front() << std::endl;

    // 2.4. back(): Direct access to the last element.
    std::cout << "d6.back() = " << d6.back() << std::endl;


    std::cout << "

--- 3. Modifiers (The Main Feature of Deque) ---

";
    std::deque<int> mod_deq = {100, 200, 300};
    print_deque("mod_deq (initial)", mod_deq);

    // 3.1. push_back(): Appends an element to the end. Amortized O(1).
    mod_deq.push_back(400);
    print_deque("mod_deq (pushed back 400)", mod_deq);

    // 3.2. pop_back(): Removes the last element. O(1).
    mod_deq.pop_back();
    print_deque("mod_deq (popped back)", mod_deq);

    // 3.3. push_front(): Prepends an element to the beginning. Amortized O(1).
    // THIS IS THE KEY ADVANTAGE OVER VECTOR.
    mod_deq.push_front(50);
    print_deque("mod_deq (pushed front 50)", mod_deq);

    // 3.4. pop_front(): Removes the first element. O(1).
    mod_deq.pop_front();
    print_deque("mod_deq (popped front)", mod_deq);

    // 3.5. emplace_back() / emplace_front() (C++11)
    // Constructs elements in-place at either end.
    mod_deq.emplace_back(400);
    mod_deq.emplace_front(50);
    print_deque("mod_deq (emplaced front/back)", mod_deq);

    // 3.6. insert(): Inserts elements at a specified position. Slow in the middle (O(N)).
    auto it_insert = mod_deq.begin() + 2;
    mod_deq.insert(it_insert, 150);
    print_deque("mod_deq (inserted 150 in middle)", mod_deq);

    // 3.7. erase(): Removes elements. Slow in the middle (O(N)).
    mod_deq.erase(mod_deq.begin() + 3);
    print_deque("mod_deq (erased from middle)", mod_deq);

    // 3.8. clear(): Removes all elements. Size becomes 0.
    mod_deq.clear();
    print_deque("mod_deq (cleared)", mod_deq);


    std::cout << "

--- 4. Capacity Management ---

";
    std::deque<int> cap_deq = {1, 2, 3, 4, 5};
    print_deque("cap_deq (initial)", cap_deq);

    // 4.1. size(): Number of elements.
    // 4.2. empty(): Returns true if size() is 0.
    std::cout << "Is cap_deq empty? " << std::boolalpha << cap_deq.empty() << std::endl;

    // 4.3. resize(): Changes the size of the deque.
    cap_deq.resize(8); // New elements are value-initialized (0 for int)
    print_deque("cap_deq (resized to 8)", cap_deq);
    cap_deq.resize(3); // Elements are destroyed from the end.
    print_deque("cap_deq (resized to 3)", cap_deq);

    // 4.4. shrink_to_fit(): Releases unused memory blocks.
    // This is a non-binding request.
    cap_deq.shrink_to_fit();
    print_deque("cap_deq (shrunk)", cap_deq);
    
    // NOTE: std::deque has no .capacity() or .reserve() members.

    // Using with STL algorithms
    // Deque iterators are random-access iterators, so algorithms like std::sort work.
    std::deque<int> sort_deq = {50, 10, 40, 20, 30};
    std::sort(sort_deq.begin(), sort_deq.end());
    print_deque("sort_deq (sorted)", sort_deq);

    return 0;
}
```


| User Prompt: |
|-------------|
| Continue |

```cpp
#include <iostream>
#include <list>
#include <string>
#include <numeric> // For std::iota

// Helper function to print a list's state
template <typename T>
void print_list(const std::string& name, const std::list<T>& lst) {
    std::cout << name << ": [ ";
    for (const auto& elem : lst) {
        std::cout << elem << " ";
    }
    std::cout << "]"
              << " | size: " << lst.size() << std::endl;
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";
    // Constructors are similar to vector/deque
    std::list<int> l1;                               // Default
    std::list<int> l2(4, 100);                       // Fill
    std::list<int> l3 = {10, 20, 30, 40, 50};         // Initializer List
    std::list<int> l4(l3);                           // Copy
    print_list("l3 (initializer list)", l3);


    std::cout << "

--- 2. Element Access ---

";
    // NO operator[] or at()!
    // 2.1. front(): Direct access to the first element.
    std::cout << "l3.front() = " << l3.front() << std::endl;

    // 2.2. back(): Direct access to the last element.
    std::cout << "l3.back() = " << l3.back() << std::endl;


    std::cout << "

--- 3. Modifiers (Insertion/Deletion) ---

";
    // These operations are all very fast (O(1)).
    l3.push_back(60);
    print_list("l3 (pushed back 60)", l3);
    l3.pop_back();
    print_list("l3 (popped back)", l3);
    l3.push_front(0);
    print_list("l3 (pushed front 0)", l3);
    l3.pop_front();
    print_list("l3 (popped front)", l3);

    // insert() is also O(1) given an iterator
    auto it = l3.begin();
    std::advance(it, 2); // Move iterator to the 3rd position (points to 30)
    l3.insert(it, 25);
    print_list("l3 (inserted 25)", l3);

    // erase() is also O(1)
    it = l3.begin(); // Reset iterator
    std::advance(it, 3); // Move to 4th position (points to 30)
    l3.erase(it);
    print_list("l3 (erased 30)", l3);


    std::cout << "

--- 4. List-Specific Operations ---

";
    std::list<int> lA = {1, 2, 3, 4, 5};
    std::list<int> lB = {10, 20, 30};
    print_list("lA (initial)", lA);
    print_list("lB (initial)", lB);

    // 4.1. splice(): Moves elements from one list to another without copying.
    // This is an extremely fast O(1) operation, regardless of how many elements are moved.
    auto pos = lA.begin();
    std::advance(pos, 2); // Position in lA after '2'
    lA.splice(pos, lB); // Move ALL elements from lB into lA at 'pos'
    print_list("lA (after splicing all of lB)", lA);
    print_list("lB (now empty)", lB);

    // 4.2. remove(): Removes all elements with a specific value.
    lA.push_back(20);
    lA.push_back(20);
    print_list("lA (before remove)", lA);
    lA.remove(20); // O(N) operation
    print_list("lA (after removing all 20s)", lA);

    // 4.3. remove_if(): Removes all elements satisfying a predicate.
    lA.remove_if([](int n){ return n > 10; }); // Remove elements greater than 10
    print_list("lA (after removing elements > 10)", lA);

    // 4.4. merge(): Merges a sorted list into another. Both lists must be sorted first.
    std::list<int> m1 = {1, 5, 9};
    std::list<int> m2 = {2, 3, 8, 10};
    m1.merge(m2); // m2 becomes empty after the merge
    print_list("m1 (merged)", m1);
    print_list("m2 (merged, now empty)", m2);

    // 4.5. sort(): std::list has its own member sort function.
    // The global std::sort requires random-access iterators, which list doesn't have.
    std::list<int> s1 = {8, 2, 6, 1, 9, 3, 5, 7, 4};
    s1.sort();
    print_list("s1 (sorted)", s1);

    // 4.6. reverse(): Reverses the order of elements in O(N).
    s1.reverse();
    print_list("s1 (reversed)", s1);

    // 4.7. unique(): Removes consecutive duplicate elements.
    std::list<int> u1 = {1, 2, 2, 2, 3, 3, 1, 1, 2};
    u1.unique();
    print_list("u1 (after unique)", u1); // Note: non-consecutive 1s remain


    std::cout << "

--- 5. Capacity and Size ---

";
    // Same as deque: size(), empty(), max_size(). No capacity() or reserve().
    std::cout << "l3 size: " << l3.size() << std::endl;
    std::cout << "Is l1 empty? " << std::boolalpha << l1.empty() << std::endl;

    return 0;
}
```


| User Prompt: |
|-------------|
| Continue |

```cpp
#include <iostream>
#include <forward_list>
#include <string>
#include <iterator> // For std::distance

// Helper function to print a forward_list
template <typename T>
void print_forward_list(const std::string& name, const std::forward_list<T>& fl) {
    std::cout << name << ": [ ";
    for (const auto& elem : fl) {
        std::cout << elem << " ";
    }
    // Note: No .size() member function. We could calculate it, but it's slow (O(N)).
    std::cout << "]" << std::endl;
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";
    // Similar to other sequence containers
    std::forward_list<int> fl1;                      // Default
    std::forward_list<int> fl2(5, 100);              // Fill
    std::forward_list<int> fl3 = {10, 20, 30, 40};   // Initializer List
    print_forward_list("fl3 (initializer list)", fl3);


    std::cout << "

--- 2. Element Access ---

";
    // Only access to the front is provided.
    // 2.1. front(): Direct access to the first element.
    if (!fl3.empty()) {
        std::cout << "fl3.front() = " << fl3.front() << std::endl;
    }
    // NO .back(), operator[], or .at()


    std::cout << "

--- 3. Modifiers (The 'after' paradigm) ---

";
    // 3.1. before_begin(): Returns an iterator to the position *before* the first element.
    // This "off-the-start" iterator is crucial for modifying the head of the list.
    auto it_before = fl3.before_begin();

    // 3.2. insert_after(): Inserts element(s) after a given position. O(1).
    it_before = fl3.insert_after(it_before, 5); // Insert 5 at the very beginning
    print_forward_list("fl3 (inserted 5 at front)", fl3);

    // 'it_before' now points to the new element '5'. Let's insert after it.
    fl3.insert_after(it_before, 6);
    print_forward_list("fl3 (inserted 6 after 5)", fl3);

    // 3.3. emplace_after(): Constructs element in-place after a given position. O(1).
    fl3.emplace_after(it_before, 7);
    print_forward_list("fl3 (emplaced 7 after 5)", fl3);

    // 3.4. push_front() / emplace_front(): Convenience wrappers for inserting at the beginning.
    fl3.push_front(0);
    print_forward_list("fl3 (pushed front 0)", fl3);

    // 3.5. erase_after(): Erases the element *after* a given position. O(1).
    // Let's erase the '6' which is after the '5' (iterator 'it_before' still points to 5).
    fl3.erase_after(it_before);
    print_forward_list("fl3 (erased element after 5)", fl3);

    // 3.6. pop_front(): Convenience wrapper for erasing the first element.
    fl3.pop_front();
    print_forward_list("fl3 (popped front)", fl3);


    std::cout << "

--- 4. Forward_list-Specific Operations ---

";
    std::forward_list<int> flA = {1, 2, 3, 4, 5};
    std::forward_list<int> flB = {10, 20, 30};
    print_forward_list("flA (initial)", flA);
    print_forward_list("flB (initial)", flB);

    // 4.1. splice_after(): Moves elements from one list to another. O(1).
    auto pos_A = flA.before_begin();
    std::advance(pos_A, 2); // Iterator points to element '2'
    flA.splice_after(pos_A, flB); // Move all of flB to after '2' in flA.
    print_forward_list("flA (after splice)", flA);
    print_forward_list("flB (now empty)", flB);

    // Other operations are similar to std::list
    // 4.2. remove() / remove_if()
    flA.remove(20);
    print_forward_list("flA (removed 20)", flA);

    // 4.3. merge() (both lists must be sorted)
    std::forward_list<int> m1 = {1, 5, 9};
    std::forward_list<int> m2 = {2, 3, 8};
    m1.merge(m2);
    print_forward_list("m1 (merged)", m1);

    // 4.4. sort()
    std::forward_list<int> s1 = {8, 2, 6, 1, 9, 3};
    s1.sort();
    print_forward_list("s1 (sorted)", s1);

    // 4.5. reverse()
    s1.reverse();
    print_forward_list("s1 (reversed)", s1);

    // 4.6. unique()
    std::forward_list<int> u1 = {1, 1, 2, 3, 3, 3, 1};
    u1.unique();
    print_forward_list("u1 (unique)", u1);


    std::cout << "

--- 5. Capacity and Size ---

";

    // 5.1. empty(): Checks if the list has zero elements. This is fast (O(1)).
    std::cout << "Is fl1 empty? " << std::boolalpha << fl1.empty() << std::endl;

    // 5.2. max_size(): Maximum possible number of elements.
    std::cout << "Max size of fl1: " << fl1.max_size() << std::endl;

    // 5.3. Getting the size (The slow way)
    // There is NO .size() member. You must use std::distance.
    long list_size = std::distance(fl3.begin(), fl3.end());
    std::cout << "Calculated size of fl3 is: " << list_size << std::endl;

    // 5.4. clear(): Removes all elements.
    fl3.clear();
    print_forward_list("fl3 (cleared)", fl3);

    return 0;
}
```


| User Prompt: |
|-------------|
| Continue |

```cpp
#include <iostream>
#include <set>
#include <string>
#include <functional> // For std::greater

// Helper function to print a set's contents
template <typename T, typename C>
void print_set(const std::string& name, const std::set<T, C>& s) {
    std::cout << name << ": { ";
    for (const auto& elem : s) {
        std::cout << elem << " ";
    }
    std::cout << "}"
              << " | size: " << s.size() << std::endl;
}

struct Point {
    int x, y;
    // For the custom comparator lambda/functor to work
    bool operator<(const Point& other) const {
        if (x < other.x) return true;
        if (x > other.x) return false;
        return y < other.y;
    }
};

// Custom comparator as a struct (functor)
struct PointCmp {
    bool operator()(const Point& a, const Point& b) const {
        // Sort by distance from origin
        return (a.x * a.x + a.y * a.y) < (b.x * b.x + b.y * b.y);
    }
};


int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Default Constructor (uses std::less for sorting)
    std::set<int> s1;

    // 1.2. Initializer List
    std::set<int> s2 = {40, 20, 50, 10, 30, 20, 40}; // Duplicates are automatically ignored
    print_set("s2 (initializer list)", s2);

    // 1.3. Range Constructor
    std::set<int> s3(s2.begin(), s2.end());
    print_set("s3 (range)", s3);

    // 1.4. Custom Comparator (descending order)
    std::set<int, std::greater<int>> s4 = {40, 20, 50, 10, 30};
    print_set("s4 (descending order)", s4);
    
    // 1.5. Custom Comparator for a custom type (struct)
    std::set<Point, PointCmp> s5 = {{3,4}, {1,1}, {0,5}}; // {1,1}, {3,4}, {0,5} sorted by distance
    std::cout << "s5 (custom type/comparator): { ";
    for(const auto& p : s5) std::cout << "(" << p.x << "," << p.y << ") ";
    std::cout << "}
";


    std::cout << "

--- 2. Modifiers (Insertion) ---

";
    // All insertion operations are O(log N).

    // 2.1. insert(): Returns a std::pair<iterator, bool>
    // The iterator points to the element (either newly inserted or the existing one).
    // The bool is 'true' if insertion took place, 'false' if the element was already there.
    auto result = s2.insert(25);
    std::cout << "Inserted 25. Success? " << std::boolalpha << result.second << ". Element is " << *result.first << std::endl;
    result = s2.insert(30); // 30 already exists
    std::cout << "Inserted 30. Success? " << std::boolalpha << result.second << ". Element is " << *result.first << std::endl;
    print_set("s2 (after inserts)", s2);

    // 2.2. emplace() (C++11): Constructs the element in-place. More efficient for complex types.
    s2.emplace(35);
    print_set("s2 (after emplace)", s2);

    // 2.3. emplace_hint(): Provides a "hint" iterator where the element might fit.
    // If the hint is correct, insertion can be amortized O(1). If not, it's still O(log N).
    s2.emplace_hint(s2.end(), 60); // Good hint
    print_set("s2 (after emplace_hint)", s2);


    std::cout << "

--- 3. Modifiers (Deletion) ---

";
    // All erase operations are O(log N).

    // 3.1. erase(key): Removes an element by its value.
    // Returns the number of elements erased (0 or 1 for std::set).
    size_t num_erased = s2.erase(30);
    std::cout << "Erased 30. Number of elements erased: " << num_erased << std::endl;
    print_set("s2 (after erasing 30)", s2);

    // 3.2. erase(iterator): Removes the element at the iterator's position.
    auto it_to_erase = s2.find(50);
    if (it_to_erase != s2.end()) {
        s2.erase(it_to_erase);
        std::cout << "Erased 50 using an iterator." << std::endl;
    }
    print_set("s2 (after erasing 50)", s2);


    std::cout << "

--- 4. Lookup Operations (The Main Feature) ---

";
    // All lookup operations are O(log N).

    // 4.1. count(key): Returns 1 if the element exists, 0 otherwise.
    std::cout << "Count of 40 in s2: " << s2.count(40) << std::endl;
    std::cout << "Count of 99 in s2: " << s2.count(99) << std::endl;

    // 4.2. find(key): The primary way to find an element.
    // Returns an iterator to the element if found, or the .end() iterator if not.
    auto it_find = s2.find(40);
    if (it_find != s2.end()) {
        std::cout << "Found element: " << *it_find << std::endl;
    } else {
        std::cout << "Element not found." << std::endl;
    }

    // 4.3. contains(key) (C++20): A more modern and readable way to check for existence.
    std::cout << "s2 contains 20? " << std::boolalpha << s2.contains(20) << std::endl;
    std::cout << "s2 contains 99? " << std::boolalpha << s2.contains(99) << std::endl;

    // 4.4. lower_bound(key): Returns an iterator to the first element that is NOT LESS than key.
    // (i.e., the first element that is >= key)
    auto it_lb = s2.lower_bound(22);
    std::cout << "Lower bound of 22 is: " << *it_lb << std::endl; // -> 25

    // 4.5. upper_bound(key): Returns an iterator to the first element that is GREATER than key.
    auto it_ub = s2.upper_bound(25);
    std::cout << "Upper bound of 25 is: " << *it_ub << std::endl; // -> 35

    // 4.6. equal_range(key): Returns a pair of iterators [lower_bound, upper_bound].
    // For std::set, the range will contain at most one element.
    auto range = s2.equal_range(25);
    std::cout << "Elements in equal_range for 25: ";
    for (auto it = range.first; it != range.second; ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    return 0;
}
```


| User Prompt: |
|-------------|
| Continue |

```cpp
#include <iostream>
#include <set> // The header for both set and multiset
#include <string>
#include <functional>

// Helper function to print a multiset's contents
template <typename T, typename C>
void print_multiset(const std::string& name, const std::multiset<T, C>& ms) {
    std::cout << name << ": { ";
    for (const auto& elem : ms) {
        std::cout << elem << " ";
    }
    std::cout << "}"
              << " | size: " << ms.size() << std::endl;
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Initializer List with duplicates
    // All duplicates are preserved and sorted.
    std::multiset<int> ms1 = {40, 20, 50, 10, 30, 20, 40, 20};
    print_multiset("ms1 (initializer list)", ms1);

    // 1.2. Custom Comparator (descending order)
    std::multiset<int, std::greater<int>> ms2 = {40, 20, 50, 10, 30, 20, 40};
    print_multiset("ms2 (descending order)", ms2);


    std::cout << "

--- 2. Modifiers (Insertion) ---

";
    // Insertion is O(log N).

    // 2.1. insert(): Insertion always succeeds.
    // It returns an iterator to the newly added element.
    // Unlike std::set, it does NOT return a pair with a bool.
    auto it_inserted = ms1.insert(25);
    std::cout << "Inserted 25. The new element is: " << *it_inserted << std::endl;

    it_inserted = ms1.insert(20); // Insert another '20'
    std::cout << "Inserted another 20. The new element is: " << *it_inserted << std::endl;
    print_multiset("ms1 (after inserts)", ms1);

    // 2.2. emplace() (C++11): Constructs the element in-place.
    ms1.emplace(35);
    print_multiset("ms1 (after emplace)", ms1);


    std::cout << "

--- 3. Modifiers (Deletion) ---

";

    // 3.1. erase(key): Removes ALL elements with the given value.
    // Returns the number of elements that were erased. This is a key difference from std::set.
    size_t num_erased = ms1.erase(20);
    std::cout << "Erased all 20s. Number of elements erased: " << num_erased << std::endl;
    print_multiset("ms1 (after erasing all 20s)", ms1);

    // 3.2. erase(iterator): Removes only the single element at the iterator's position.
    // This is how you remove just one instance of a duplicate key.
    auto it_to_erase = ms1.find(40); // find() gets an iterator to the FIRST '40'
    if (it_to_erase != ms1.end()) {
        ms1.erase(it_to_erase);
        std::cout << "Erased a single 40 using an iterator." << std::endl;
    }
    print_multiset("ms1 (after erasing one 40)", ms1);


    std::cout << "

--- 4. Lookup Operations (The Main Feature) ---

";
    std::multiset<int> ms_lookup = {10, 20, 20, 20, 30, 40, 40, 50};
    print_multiset("ms_lookup (for lookups)", ms_lookup);

    // 4.1. count(key): Returns the number of times an element appears. O(log N + count).
    std::cout << "Count of 20 in ms_lookup: " << ms_lookup.count(20) << std::endl;
    std::cout << "Count of 99 in ms_lookup: " << ms_lookup.count(99) << std::endl;

    // 4.2. find(key): Returns an iterator to the FIRST element matching the key. O(log N).
    auto it_find = ms_lookup.find(20);
    if (it_find != ms_lookup.end()) {
        std::cout << "Found first instance of 20. Value: " << *it_find << std::endl;
    }

    // 4.3. lower_bound(key): Iterator to the first element >= key.
    auto it_lb = ms_lookup.lower_bound(20);
    std::cout << "Lower bound of 20 is: " << *it_lb << std::endl;

    // 4.4. upper_bound(key): Iterator to the first element > key.
    auto it_ub = ms_lookup.upper_bound(20);
    std::cout << "Upper bound of 20 is: " << *it_ub << std::endl; // -> 30

    // 4.5. equal_range(key): The CANONICAL way to work with duplicates.
    // Returns a pair of iterators [lower_bound, upper_bound] that defines
    // the complete range of all elements equal to the key.
    auto range = ms_lookup.equal_range(20);
    std::cout << "Iterating through all elements equal to 20: ";
    for (auto it = range.first; it != range.second; ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // You can calculate the count using the range.
    std::cout << "Distance of equal_range for 20: " << std::distance(range.first, range.second) << std::endl;

    return 0;
}
```


| User Prompt: |
|-------------|
| continue |

```cpp
#include <iostream>
#include <map>
#include <string>
#include <functional> // For std::greater

// Helper function to print a map's contents
template <typename K, typename V, typename C>
void print_map(const std::string& name, const std::map<K, V, C>& m) {
    std::cout << name << " (size " << m.size() << "): {
";
    for (const auto& pair : m) {
        // pair.first is the key
        // pair.second is the value
        std::cout << "  [" << pair.first << "] = " << pair.second << "
";
    }
    std::cout << "}
";
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Default Constructor
    std::map<std::string, int> m1;

    // 1.2. Initializer List (C++11)
    // Use curly braces for the map and for each key-value pair.
    std::map<std::string, int> m2 = {
        {"Banana", 7},
        {"Apple", 10},
        {"Orange", 5},
        {"Apple", 12} // The second "Apple" is ignored as keys must be unique.
    };
    print_map("m2 (initializer list)", m2);

    // 1.3. Custom Comparator (sorts keys in descending order)
    std::map<std::string, int, std::greater<std::string>> m3(m2.begin(), m2.end());
    print_map("m3 (descending keys)", m3);


    std::cout << "

--- 2. Element Access ---

";

    // 2.1. operator[] - The most common, but potentially dangerous, accessor.
    // - If the key EXISTS, it returns a reference to its value.
    // - If the key DOES NOT EXIST, it INSERTS a new element with that key and a
    //   value-initialized value (0 for int, empty string, etc.), then returns a reference to it.
    std::cout << "m2[\"Apple\"] = " << m2["Apple"] << std::endl; // Access existing
    m2["Apple"] = 15; // Modify existing
    std::cout << "m2[\"Apple\"] after modification = " << m2["Apple"] << std::endl;

    std::cout << "Accessing m2[\"Pear\"]..." << std::endl;
    m2["Pear"] = 0; // "Pear" does not exist, so it is created with value 0, then assigned 0.
    print_map("m2 (after accessing \"Pear\")", m2);

    // 2.2. at() - The safe way to access.
    // - If the key EXISTS, it returns a reference to its value.
    // - If the key DOES NOT EXIST, it throws a std::out_of_range exception.
    try {
        std::cout << "m2.at(\"Banana\") = " << m2.at("Banana") << std::endl;
        std::cout << m2.at("Grape"); // This will throw
    } catch (const std::out_of_range& e) {
        std::cerr << "Caught exception: " << e.what() << std::endl;
    }


    std::cout << "

--- 3. Modifiers (Insertion) ---

";

    // 3.1. insert(): The safe way to insert. Does not overwrite.
    // Returns std::pair<iterator, bool>. bool is true if insertion happened.
    auto result = m2.insert({"Cherry", 20});
    std::cout << "Inserted \"Cherry\". Success? " << std::boolalpha << result.second << std::endl;
    result = m2.insert({"Apple", 99}); // Already exists, fails to insert.
    std::cout << "Inserted \"Apple\" again. Success? " << std::boolalpha << result.second << std::endl;
    print_map("m2 (after insert)", m2);

    // 3.2. insert_or_assign() (C++17): Explicitly inserts or updates.
    // Returns std::pair<iterator, bool>. bool is true if insertion happened, false if assignment happened.
    auto res_ioa = m2.insert_or_assign("Banana", 9); // Assigns
    std::cout << "\"Banana\" was " << (res_ioa.second ? "inserted" : "assigned") << std::endl;
    res_ioa = m2.insert_or_assign("Mango", 25); // Inserts
    std::cout << "\"Mango\" was " << (res_ioa.second ? "inserted" : "assigned") << std::endl;
    print_map("m2 (after insert_or_assign)", m2);

    // 3.3. emplace(): Constructs the key-value pair in-place. Avoids creating temporaries.
    m2.emplace("Kiwi", 18);
    print_map("m2 (after emplace)", m2);

    // 3.4. try_emplace() (C++17): Inserts only if the key does not already exist.
    // Does not move from its arguments if insertion fails, which can be an efficiency gain.
    m2.try_emplace("Fig", 30); // Succeeds
    m2.try_emplace("Kiwi", 0); // Fails, value for "Kiwi" remains 18
    print_map("m2 (after try_emplace)", m2);


    std::cout << "

--- 4. Modifiers (Deletion) ---

";

    // 4.1. erase(key): Removes an element by its key. O(log N).
    // Returns the number of elements erased (0 or 1 for map).
    size_t num_erased = m2.erase("Orange");
    std::cout << "Erased \"Orange\". Count: " << num_erased << std::endl;
    print_map("m2 (after erasing Orange)", m2);

    // 4.2. erase(iterator): Removes the element at the iterator's position. Amortized O(1).
    auto it_to_erase = m2.find("Pear");
    if (it_to_erase != m2.end()) {
        m2.erase(it_to_erase);
    }
    print_map("m2 (after erasing Pear)", m2);


    std::cout << "

--- 5. Lookup Operations ---

";
    // All lookups are O(log N).

    // 5.1. find(key): The primary lookup method.
    // Returns an iterator to the element, or .end() if not found.
    auto it_find = m2.find("Banana");
    if (it_find != m2.end()) {
        std::cout << "Found \"Banana\" with value " << it_find->second << std::endl;
    }

    // 5.2. count(key): Returns 1 if key exists, 0 otherwise.
    std::cout << "Count of \"Kiwi\": " << m2.count("Kiwi") << std::endl;
    std::cout << "Count of \"Grape\": " << m2.count("Grape") << std::endl;

    // 5.3. contains(key) (C++20): Modern, readable check for existence.
    if (m2.contains("Apple")) {
        std::cout << "Map contains the key \"Apple\"." << std::endl;
    }

    // lower_bound, upper_bound, and equal_range also exist and work on keys.


    std::cout << "

--- 6. Iteration with Structured Bindings (C++17) ---

";
    std::cout << "Modern iteration over m2:
";
    for (const auto& [fruit, count] : m2) {
        std::cout << "  There are " << count << " of " << fruit << ".
";
    }

    return 0;
}
```


| User Prompt: |
|-------------|
| continue |

```cpp
#include <iostream>
#include <map> // Header for both map and multimap
#include <string>
#include <vector>

// Helper function to print a multimap's contents
template <typename K, typename V>
void print_multimap(const std::string& name, const std::multimap<K, V>& mm) {
    std::cout << name << " (size " << mm.size() << "): {
";
    for (const auto& pair : mm) {
        std::cout << "  [" << pair.first << "] = " << pair.second << "
";
    }
    std::cout << "}
";
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Initializer List with duplicate keys
    std::multimap<std::string, std::string> event_log = {
        {"user1", "login"},
        {"user2", "login"},
        {"user1", "view_page"},
        {"user3", "login"},
        {"user1", "logout"},
        {"user2", "logout"}
    };
    print_multimap("event_log", event_log);


    std::cout << "

--- 2. Modifiers (Insertion) ---

";
    // Insertion is O(log N) and always succeeds.

    // 2.1. insert(): Returns an iterator to the newly added element.
    auto it_inserted = event_log.insert({"user2", "update_settings"});
    std::cout << "Inserted {\"user2\", \"update_settings\"}. New element key: "
              << it_inserted->first << ", value: " << it_inserted->second << std::endl;

    // 2.2. emplace(): Constructs the element in-place.
    event_log.emplace("user3", "view_page");
    print_multimap("event_log (after inserts)", event_log);


    std::cout << "

--- 3. Modifiers (Deletion) ---

";

    // 3.1. erase(key): Removes ALL elements with the given key.
    // Returns the number of elements erased.
    size_t num_erased = event_log.erase("user3");
    std::cout << "Erased all events for \"user3\". Count: " << num_erased << std::endl;
    print_multimap("event_log (after erasing user3)", event_log);

    // 3.2. erase(iterator): Removes only the single element at the iterator's position.
    auto it_to_erase = event_log.find("user1"); // find() gets an iterator to the FIRST "user1" event
    if (it_to_erase != event_log.end()) {
        event_log.erase(it_to_erase); // Erases the "login" event for user1
        std::cout << "Erased a single event for \"user1\" using an iterator." << std::endl;
    }
    print_multimap("event_log (after erasing one user1 event)", event_log);


    std::cout << "

--- 4. Lookup Operations (The Main Feature) ---

";
    // NOTE: No operator[] or at()

    // 4.1. count(key): Returns the number of elements with a specific key. O(log N + count).
    std::cout << "Number of events for \"user1\": " << event_log.count("user1") << std::endl;
    std::cout << "Number of events for \"user-unknown\": " << event_log.count("user-unknown") << std::endl;

    // 4.2. find(key): Returns an iterator to the FIRST element matching the key. O(log N).
    auto it_find = event_log.find("user2");
    if (it_find != event_log.end()) {
        std::cout << "First event found for \"user2\": " << it_find->second << std::endl;
    }

    // 4.3. equal_range(key): The BEST way to work with duplicate keys.
    // Returns a pair of iterators that defines the complete range of all elements for a key.
    std::cout << "
All events for \"user2\":
";
    auto range = event_log.equal_range("user2");
    for (auto it = range.first; it != range.second; ++it) {
        std::cout << "  - " << it->second << "
";
    }

    // Example: Get all values for a key into a vector
    std::vector<std::string> user1_actions;
    auto user1_range = event_log.equal_range("user1");
    for (auto it = user1_range.first; it != user1_range.second; ++it) {
        user1_actions.push_back(it->second);
    }
    std::cout << "
Actions for user1 collected into a vector: ";
    for(const auto& action : user1_actions) std::cout << action << " ";
    std::cout << std::endl;

    return 0;
}
```


| User Prompt: |
|-------------|
| continue |

```cpp
#include <iostream>
#include <unordered_set>
#include <string>

// Helper function to print an unordered_set
template <typename T>
void print_unordered_set(const std::string& name, const std::unordered_set<T>& us) {
    std::cout << name << ": { ";
    for (const auto& elem : us) {
        std::cout << elem << " ";
    }
    std::cout << "}"
              << " | size: " << us.size()
              << " | bucket_count: " << us.bucket_count()
              << " | load_factor: " << us.load_factor() << std::endl;
}

// --- For using a custom type in an unordered_set ---
struct Point {
    int x, y;
    // 1. We need an equality operator (==)
    bool operator==(const Point& other) const {
        return x == other.x && y == other.y;
    }
};

// 2. We need to provide a hash function.
// This is the modern, recommended way: specialize the std::hash template.
namespace std {
    template <>
    struct hash<Point> {
        size_t operator()(const Point& p) const {
            // A simple way to combine hashes of members
            auto h1 = std::hash<int>{}(p.x);
            auto h2 = std::hash<int>{}(p.y);
            // A common pattern for combining hashes
            return h1 ^ (h2 << 1);
        }
    };
}


int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Initializer List
    // Note the unpredictable order of elements! It is not sorted.
    std::unordered_set<int> us1 = {40, 20, 50, 10, 30, 20, 40}; // Duplicates are ignored
    print_unordered_set("us1 (initializer list)", us1);

    // 1.2. With a custom type
    std::unordered_set<Point> us2 = {{3, 4}, {1, 2}, {5, 6}, {1, 2}};
    std::cout << "us2 (custom type): { ";
    for(const auto& p : us2) std::cout << "(" << p.x << "," << p.y << ") ";
    std::cout << "}
";


    std::cout << "

--- 2. Modifiers (Insertion & Deletion) ---

";
    // Average case for all is O(1).

    // 2.1. insert(): Returns std::pair<iterator, bool>
    auto result = us1.insert(25);
    std::cout << "Inserted 25. Success? " << std::boolalpha << result.second << std::endl;
    result = us1.insert(30); // 30 already exists
    std::cout << "Inserted 30. Success? " << std::boolalpha << result.second << std::endl;
    print_unordered_set("us1 (after inserts)", us1);

    // 2.2. erase(key): Removes an element by its value.
    // Returns number of elements erased (0 or 1).
    size_t num_erased = us1.erase(30);
    std::cout << "Erased 30. Count: " << num_erased << std::endl;
    print_unordered_set("us1 (after erasing 30)", us1);


    std::cout << "

--- 3. Lookup Operations (The Main Feature) ---

";
    // Average case for all is O(1).

    // 3.1. find(key): The primary lookup method.
    // Returns an iterator to the element, or .end() if not found.
    auto it_find = us1.find(40);
    if (it_find != us1.end()) {
        std::cout << "Found element: " << *it_find << std::endl;
    }

    // 3.2. count(key): Returns 1 if key exists, 0 otherwise.
    std::cout << "Count of 50 in us1: " << us1.count(50) << std::endl;
    std::cout << "Count of 99 in us1: " << us1.count(99) << std::endl;

    // 3.3. contains(key) (C++20): Modern, readable check for existence.
    if (us1.contains(20)) {
        std::cout << "us1 contains 20." << std::endl;
    }


    std::cout << "

--- 4. Hash Table Interface (Bucket API) ---

";

    // 4.1. bucket_count(): The number of buckets in the hash table.
    // 4.2. load_factor(): The ratio of elements to buckets (size / bucket_count).
    // If the load factor exceeds max_load_factor(), the container may rehash.
    std::cout << "Current max_load_factor: " << us1.max_load_factor() << std::endl;

    // 4.3. bucket(key): Tells you which bucket a key would be in.
    size_t bucket_index = us1.bucket(50);
    std::cout << "The element 50 is in bucket #" << bucket_index << std::endl;

    // 4.4. bucket_size(n): How many elements are in the n-th bucket.
    std::cout << "Bucket #" << bucket_index << " has " << us1.bucket_size(bucket_index) << " element(s)." << std::endl;

    // 4.5. rehash(n): Manually set the number of buckets to at least n.
    us1.rehash(100); // Request at least 100 buckets
    print_unordered_set("us1 (after rehash)", us1);

    return 0;
}
```


| User Prompt: |
|-------------|
| continue |

```cpp
#include <iostream>
#include <unordered_set> // Header for both unordered_set and unordered_multiset
#include <string>

// Helper function to print an unordered_multiset
template <typename T>
void print_unordered_multiset(const std::string& name, const std::unordered_multiset<T>& ums) {
    std::cout << name << ": { ";
    for (const auto& elem : ums) {
        std::cout << elem << " ";
    }
    std::cout << "}"
              << " | size: " << ums.size()
              << " | bucket_count: " << ums.bucket_count() << std::endl;
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Initializer List with duplicates
    // All duplicates are preserved. The order is not guaranteed.
    std::unordered_multiset<int> ums1 = {40, 20, 50, 10, 30, 20, 40, 20};
    print_unordered_multiset("ums1 (initializer list)", ums1);


    std::cout << "

--- 2. Modifiers (Insertion) ---

";
    // Insertion is average O(1) and always succeeds.

    // 2.1. insert(): Returns an iterator to the newly added element.
    auto it_inserted = ums1.insert(25);
    std::cout << "Inserted 25. The new element is: " << *it_inserted << std::endl;

    it_inserted = ums1.insert(20); // Insert another '20'
    std::cout << "Inserted another 20. The new element is: " << *it_inserted << std::endl;
    print_unordered_multiset("ums1 (after inserts)", ums1);


    std::cout << "

--- 3. Modifiers (Deletion) ---

";

    // 3.1. erase(key): Removes ALL elements with the given value.
    // Returns the number of elements that were erased.
    size_t num_erased = ums1.erase(20);
    std::cout << "Erased all 20s. Number of elements erased: " << num_erased << std::endl;
    print_unordered_multiset("ums1 (after erasing all 20s)", ums1);

    // 3.2. erase(iterator): Removes only the single element at the iterator's position.
    auto it_to_erase = ums1.find(40); // find() gets an iterator to the FIRST '40'
    if (it_to_erase != ums1.end()) {
        ums1.erase(it_to_erase);
        std::cout << "Erased a single 40 using an iterator." << std::endl;
    }
    print_unordered_multiset("ums1 (after erasing one 40)", ums1);


    std::cout << "

--- 4. Lookup Operations (The Main Feature) ---

";
    std::unordered_multiset<std::string> word_bag = {"apple", "banana", "apple", "orange", "apple", "banana"};
    print_unordered_multiset("word_bag (for lookups)", word_bag);

    // 4.1. count(key): Returns the number of times an element appears. Average O(count).
    std::cout << "Count of \"apple\" in word_bag: " << word_bag.count("apple") << std::endl;
    std::cout << "Count of \"grape\" in word_bag: " << word_bag.count("grape") << std::endl;

    // 4.2. find(key): Returns an iterator to the FIRST element matching the key. Average O(1).
    auto it_find = word_bag.find("banana");
    if (it_find != word_bag.end()) {
        std::cout << "Found first instance of \"banana\"." << std::endl;
    }

    // 4.3. equal_range(key): The BEST way to work with duplicates.
    // Returns a pair of iterators that defines the complete range of all elements equal to the key.
    std::cout << "
Iterating through all instances of \"apple\":
";
    auto range = word_bag.equal_range("apple");
    for (auto it = range.first; it != range.second; ++it) {
        std::cout << "  - Found an \"" << *it << "\"
";
    }

    return 0;
}
```


| User Prompt: |
|-------------|
| continue |

```cpp
#include <iostream>
#include <unordered_map>
#include <string>
#include <vector>

// Helper function to print an unordered_map
template <typename K, typename V>
void print_unordered_map(const std::string& name, const std::unordered_map<K, V>& um) {
    std::cout << name << " (size " << um.size() << "): {
";
    for (const auto& [key, value] : um) { // Using C++17 structured bindings
        std::cout << "  [" << key << "] = " << value << "
";
    }
    std::cout << "}
";
}

// Custom struct for keys
struct User {
    int id;
    std::string username;

    bool operator==(const User& other) const {
        return id == other.id && username == other.username;
    }
};

// Hash function for the custom User struct
namespace std {
    template <>
    struct hash<User> {
        size_t operator()(const User& u) const {
            auto h1 = std::hash<int>{}(u.id);
            auto h2 = std::hash<std::string>{}(u.username);
            return h1 ^ (h2 << 1); // Combine hashes
        }
    };
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Initializer List
    // Note the unpredictable order of elements.
    std::unordered_map<std::string, int> word_counts = {
        {"banana", 7},
        {"apple", 10},
        {"orange", 5},
        {"apple", 12} // Second "apple" is ignored
    };
    print_unordered_map("word_counts", word_counts);

    // 1.2. With a custom key type
    std::unordered_map<User, std::string> user_permissions = {
        {{101, "alice"}, "admin"},
        {{102, "bob"}, "user"},
        {{103, "charlie"}, "guest"}
    };
    std::cout << "user_permissions map created.
";


    std::cout << "

--- 2. Element Access ---

";

    // 2.1. operator[]: Fast access. Inserts if key doesn't exist.
    std::cout << "Count for \"apple\": " << word_counts["apple"] << std::endl;
    word_counts["apple"] = 15; // Modify existing value
    std::cout << "New count for \"apple\": " << word_counts["apple"] << std::endl;
    std::cout << "Accessing \"pear\" (which doesn't exist)..." << std::endl;
    word_counts["pear"] = 1; // Creates "pear" with value 0, then assigns 1.
    print_unordered_map("word_counts (after adding pear)", word_counts);

    // 2.2. at(): Safe access. Throws if key doesn't exist.
    try {
        std::cout << "Count for \"orange\": " << word_counts.at("orange") << std::endl;
        std::cout << word_counts.at("grape"); // Throws std::out_of_range
    } catch (const std::exception& e) {
        std::cerr << "Caught exception: " << e.what() << std::endl;
    }


    std::cout << "

--- 3. Modifiers (Insertion & Deletion) ---

";

    // 3.1. insert(): Safely inserts, does not overwrite. Returns pair<iterator, bool>.
    auto result = word_counts.insert({"cherry", 20});
    std::cout << "Inserted \"cherry\". Success? " << std::boolalpha << result.second << std::endl;
    result = word_counts.insert({"apple", 99}); // Fails, key exists
    std::cout << "Inserted \"apple\" again. Success? " << std::boolalpha << result.second << std::endl;

    // 3.2. insert_or_assign() (C++17): Inserts or updates.
    word_counts.insert_or_assign("banana", 9); // Assigns
    word_counts.insert_or_assign("mango", 25); // Inserts
    print_unordered_map("word_counts (after insert_or_assign)", word_counts);

    // 3.3. erase(key): Removes an element by its key.
    size_t num_erased = word_counts.erase("orange");
    std::cout << "
Erased \"orange\". Count: " << num_erased << std::endl;
    print_unordered_map("word_counts (after erase)", word_counts);


    std::cout << "

--- 4. Lookup Operations ---

";
    // All are average O(1).

    // 4.1. find(key): Primary lookup method.
    User bob = {102, "bob"};
    auto it_find = user_permissions.find(bob);
    if (it_find != user_permissions.end()) {
        std::cout << "Found user \"bob\". Permissions: " << it_find->second << std::endl;
    }

    // 4.2. count(key): Returns 1 if key exists, 0 otherwise.
    std::cout << "Count of key \"mango\": " << word_counts.count("mango") << std::endl;

    // 4.3. contains(key) (C++20): Modern, readable check.
    if (word_counts.contains("apple")) {
        std::cout << "The map contains the key \"apple\"." << std::endl;
    }

    // The bucket interface (bucket_count, load_factor, etc.) is also available,
    // just like in std::unordered_set.

    return 0;
}
```


| User Prompt: |
|-------------|
| continue |

```cpp
#include <iostream>
#include <stack>
#include <queue>
#include <vector>
#include <deque>
#include <string>

// --- std::stack Demonstration ---
void demonstrate_stack() {
    std::cout << "
--- std::stack Masterclass (LIFO) ---

";

    // By default, std::stack uses std::deque<int>
    std::stack<int> s1;

    // You can specify a different underlying container, like std::vector
    std::stack<int, std::vector<int>> s2;

    std::cout << "--- Operations ---
";

    // 1. empty(): Checks if the stack is empty.
    std::cout << "Is s1 empty initially? " << std::boolalpha << s1.empty() << std::endl;

    // 2. push(): Adds an element to the top of the stack.
    std::cout << "Pushing 10, 20, 30 onto the stack...
";
    s1.push(10);
    s1.push(20);
    s1.push(30);

    // 3. size(): Returns the number of elements.
    std::cout << "Current size of s1: " << s1.size() << std::endl;

    // 4. top(): Returns a reference to the top element WITHOUT removing it.
    std::cout << "The top element is: " << s1.top() << std::endl; // Should be 30

    // Modifying the top element
    s1.top() = 33;
    std::cout << "After modification, the top element is: " << s1.top() << std::endl;

    // 5. pop(): Removes the top element. It does not return the element.
    std::cout << "Popping the top element...
";
    s1.pop();

    std::cout << "Now, the top element is: " << s1.top() << std::endl; // Should be 20

    // 6. emplace() (C++11): Constructs an element in-place at the top.
    s1.emplace(44);
    std::cout << "After emplacing 44, the top element is: " << s1.top() << std::endl;

    // Common pattern: process and pop until the stack is empty.
    std::cout << "
Processing and emptying the stack:
";
    while (!s1.empty()) {
        std::cout << "  - Processing and popping: " << s1.top() << std::endl;
        s1.pop();
    }
    std::cout << "Is s1 empty now? " << std::boolalpha << s1.empty() << std::endl;
}

// --- std::queue Demonstration ---
void demonstrate_queue() {
    std::cout << "

--- std::queue Masterclass (FIFO) ---

";

    // By default, std::queue also uses std::deque<int>
    std::queue<std::string> q1;

    std::cout << "--- Operations ---
";
    std::cout << "Is q1 empty initially? " << std::boolalpha << q1.empty() << std::endl;

    // 1. push(): Adds an element to the BACK of the queue.
    std::cout << "Pushing \"First\", \"Second\", \"Third\" into the queue...
";
    q1.push("First");
    q1.push("Second");
    q1.push("Third");

    std::cout << "Current size of q1: " << q1.size() << std::endl;

    // 2. front(): Returns a reference to the FRONT element (the oldest).
    std::cout << "The front element is: \"" << q1.front() << "\"" << std::endl;

    // 3. back(): Returns a reference to the BACK element (the newest).
    std::cout << "The back element is: \"" << q1.back() << "\"" << std::endl;

    // 4. pop(): Removes the FRONT element.
    std::cout << "Popping the front element...
";
    q1.pop();

    std::cout << "Now, the front element is: \"" << q1.front() << "\"" << std::endl; // "Second"

    // Common pattern: process and pop until the queue is empty.
    std::cout << "
Processing and emptying the queue:
";
    while (!q1.empty()) {
        std::cout << "  - Processing and popping: \"" << q1.front() << "\"" << std::endl;
        q1.pop();
    }
}

// --- std::priority_queue Demonstration ---
void demonstrate_priority_queue() {
    std::cout << "

--- std::priority_queue Masterclass (Heap) ---

";

    // By default, a priority_queue is a max-heap.
    // Underlying container is std::vector, comparator is std::less.
    std::priority_queue<int> pq1;

    std::cout << "--- Max-Heap Operations (default) ---
";
    // 1. push(): Adds an element and maintains the heap property. O(log N).
    std::cout << "Pushing 30, 100, 20, 80, 50...
";
    pq1.push(30);
    pq1.push(100);
    pq1.push(20);
    pq1.push(80);
    pq1.push(50);

    // 2. top(): Returns a const reference to the LARGEST element. O(1).
    std::cout << "The top (largest) element is: " << pq1.top() << std::endl; // 100

    // 3. pop(): Removes the largest element. O(log N).
    std::cout << "Popping the top element...
";
    pq1.pop();
    std::cout << "Now, the top element is: " << pq1.top() << std::endl; // 80

    std::cout << "
Processing and emptying the max-heap (sorted descending):
";
    while (!pq1.empty()) {
        std::cout << "  - Popping: " << pq1.top() << std::endl;
        pq1.pop();
    }

    // --- Min-Heap (requires custom arguments) ---
    // To create a min-heap, we must specify the underlying container
    // and a different comparator (std::greater).
    std::cout << "
--- Min-Heap Operations ---
";
    std::priority_queue<int, std::vector<int>, std::greater<int>> min_pq;

    std::cout << "Pushing 30, 100, 20, 80, 50 into min-heap...
";
    min_pq.push(30);
    min_pq.push(100);
    min_pq.push(20);
    min_pq.push(80);
    min_pq.push(50);

    std::cout << "The top (smallest) element is: " << min_pq.top() << std::endl; // 20

    std::cout << "
Processing and emptying the min-heap (sorted ascending):
";
    while (!min_pq.empty()) {
        std::cout << "  - Popping: " << min_pq.top() << std::endl;
        min_pq.pop();
    }
}


int main() {
    demonstrate_stack();
    demonstrate_queue();
    demonstrate_priority_queue();
    return 0;
}
```


| User Prompt: |
|-------------|
| bitset |

```cpp
#include <iostream>
#include <bitset>
#include <string>
#include <stdexcept> // For std::invalid_argument

// Helper function to print a bitset
template <size_t N>
void print_bitset(const std::string& name, const std::bitset<N>& bs) {
    std::cout << name << " (size " << N << "): " << bs << std::endl;
}

int main() {
    std::cout << "--- 1. Constructors and Initialization ---

";

    // 1.1. Default Constructor
    // All bits are initialized to 0.
    std::bitset<8> b1; // 00000000
    print_bitset("b1 (default)", b1);

    // 1.2. From an unsigned long long integer
    // The bits are a copy of the binary representation of the number.
    std::bitset<8> b2(42); // 42 is 00101010 in binary
    print_bitset("b2 (from 42)", b2);

    // 1.3. From a std::string
    // You can initialize from a string of '0's and '1's.
    std::string bit_str = "11010010";
    std::bitset<8> b3(bit_str);
    print_bitset("b3 (from string)", b3);

    // You can also initialize from a substring.
    // (string, position, number_of_chars, zero_char, one_char)
    std::bitset<4> b4("11110000", 4, 4); // Start at index 4, take 4 chars -> "0000"
    print_bitset("b4 (from substring)", b4);

    // You can specify custom characters for 0 and 1.
    std::bitset<8> b5("X.XX.X.X", 0, 8, '.', 'X'); // '.' is 0, 'X' is 1
    print_bitset("b5 (custom chars)", b5);


    std::cout << "

--- 2. Element Access and Testing ---

";

    // 2.1. operator[]: Access a bit by its position (0 is the rightmost bit).
    // Returns a special reference-like object that can be read or written.
    std::cout << "Bit at position 1 in b2 (00101010) is: " << b2[1] << std::endl; // 1
    std::cout << "Bit at position 2 in b2 is: " << b2[2] << std::endl; // 0
    b2[0] = 1; // Set the rightmost bit
    print_bitset("b2 (after b2[0]=1)", b2); // 00101011

    // 2.2. test(): Safely checks if a bit is set (is 1).
    // Throws std::out_of_range if the position is invalid.
    if (b2.test(1)) {
        std::cout << "b2.test(1) is true." << std::endl;
    }


    std::cout << "

--- 3. Modifiers (Changing Bits) ---

";

    // 3.1. set(): Sets all bits to 1, or a specific bit to 1.
    b1.set(); // Set all bits
    print_bitset("b1 (all set)", b1);
    b1.set(3, 0); // Set bit at pos 3 to 0 (false)
    print_bitset("b1 (pos 3 set to 0)", b1);

    // 3.2. reset(): Resets all bits to 0, or a specific bit to 0.
    b1.reset(); // Reset all bits
    print_bitset("b1 (all reset)", b1);
    b2.reset(1); // Reset bit at pos 1
    print_bitset("b2 (pos 1 reset)", b2);

    // 3.3. flip(): Flips all bits, or a specific bit.
    b2.flip(); // Flip all bits (bitwise NOT)
    print_bitset("b2 (flipped)", b2);
    b2.flip(0); // Flip the bit at pos 0
    print_bitset("b2 (pos 0 flipped)", b2);


    std::cout << "

--- 4. Querying and Capacity ---

";
    std::bitset<8> b_query("10110100");
    print_bitset("b_query", b_query);

    // 4.1. size(): Returns the number of bits (the compile-time constant N).
    std::cout << "b_query.size() = " << b_query.size() << std::endl;

    // 4.2. count(): Returns the number of bits that are set to 1. O(N) or faster.
    std::cout << "b_query.count() = " << b_query.count() << std::endl; // 4

    // 4.3. any(): Returns true if at least one bit is set to 1.
    std::cout << "b_query.any()? " << std::boolalpha << b_query.any() << std::endl;

    // 4.4. none(): Returns true if no bits are set to 1.
    std::cout << "b_query.none()? " << std::boolalpha << b_query.none() << std::endl;
    std::cout << "b1.none() (all zeros)? " << std::boolalpha << b1.none() << std::endl;

    // 4.5. all(): Returns true if all bits are set to 1.
    std::bitset<4> b_all;
    b_all.set();
    std::cout << "b_all.all()? " << std::boolalpha << b_all.all() << std::endl;


    std::cout << "

--- 5. Bitwise Operations ---

";
    std::bitset<8> op1("11001100");
    std::bitset<8> op2("10101010");
    print_bitset("op1", op1);
    print_bitset("op2", op2);

    // 5.1. AND (&, &=)
    print_bitset("op1 & op2", op1 & op2); // 10001000

    // 5.2. OR (|, |=)
    print_bitset("op1 | op2", op1 | op2); // 11101110

    // 5.3. XOR (^, ^=)
    print_bitset("op1 ^ op2", op1 ^ op2); // 01100110

    // 5.4. NOT (~)
    print_bitset("~op1", ~op1); // 00110011

    // 5.5. Left Shift (<<, <<=)
    print_bitset("op1 << 2", op1 << 2); // 00110000

    // 5.6. Right Shift (>>, >>=)
    print_bitset("op1 >> 2", op1 >> 2); // 00110011


    std::cout << "

--- 6. Conversions ---

";

    // 6.1. to_string(): Converts the bitset to a std::string.
    std::string s = b5.to_string('.', 'X');
    std::cout << "b5.to_string('.', 'X') = " << s << std::endl;

    // 6.2. to_ulong() / to_ullong(): Converts to an unsigned integer.
    // Throws std::overflow_error if the value cannot fit in the integer type.
    std::bitset<8> num_bs(150); // 10010110
    print_bitset("num_bs", num_bs);
    unsigned long val = num_bs.to_ulong();
    std::cout << "num_bs.to_ulong() = " << val << std::endl;

    std::bitset<65> too_big;
    too_big[64] = 1;
    try {
        too_big.to_ullong();
    } catch (const std::overflow_error& e) {
        std::cerr << "Caught expected exception: " << e.what() << std::endl;
    }

    return 0;
}
```
