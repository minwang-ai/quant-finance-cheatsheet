[TOC]

# Hashing (hash map and sets)

## Interface of Hash Maps - Python vs. C++ 

### Python (Dictionary)
```python
# Declaration
hashmap_variable = {}

# Initialization
hashmap_variable = {key_1: value_1, key_2: value_2}

# Check if Key Exists / Not Exists
if key in hashmap_variable:
    pass
if key not in hashmap_variable:
    pass

# Insert（if the key doesn't exist yet）/ Access or Update （if the key exists）
# - Raise key error if the key does not exist
hashmap_variable[key] = value

# Access: retrieve the value
# Return default value if the key does not exist (no insertion)
value = hashmap_variable.get(key, default_value)

# Update with a new dictionary 
hashmap_variable.update(new_dict)

# Delete
# - Delete Key (raises error if the key does not exist)
del hashmap_variable[key]
# - Pop the value and then Delete the Key
value = hashmap_variable.pop(key)

# Get Size
len(hashmap_variable)

# Iterate
# - use .items() if need to access both keys and values:
for key, value in hashmap_variable.items():
    pass
# - use .keys() if only need to access keys:  
for key in hashmap_variable.keys():
    pass
# - use .values() if only need to access values: 
for value in hashmap_variable.values():
    pass

# remove all key-value pairs from a dictionary leaving it empty (in place modification and does not return any value).
hashmap_variable.clear()
```

### C++ (`unordered_map`)
```cpp
// Declaration & Initialization
unordered_map<key_type, value_type> hashmap_variable;
unordered_map<key_type, value_type> hashmap_variable = {{key_1, value_1},{key_2,value_2}};

// Check Key Exists / Not Exists
if (hashmap_variable.find(key) != hashmap_variable.end()) { /* ... */ }
if (hashmap_variable.find(key) == hashmap_variable.end()) { /* ... */ }

// Return default if missing
hashmap_variable.count(key) ? key_exist_default : else_default_value;

// Access (Creates key with default 0 if missing!)
hashmap_variable[key] = value;

// Delete Key (Safe if missing)
hashmap_variable.erase(key);

// Get Size
hashmap_variable.size();

//Iterate
for (auto const& [key, val] : hashmap_variable) { /* ... */ }
```
