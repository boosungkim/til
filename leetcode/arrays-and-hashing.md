# Arrays & Hashing

Key concepts:
- Static arrays
- Dynamic arrays
- Hash map / Hash set
- Stacks
- Monotonic stack
- Kadane's algorithm

Key patterns:
- Problems involving the next greater or smaller element (monotonic stack)

## Tricks
### Character Frequency Vector

Map each string to a 26-length array where `index = ord(c) - ord('a')` and value is the count of that letter.

- Fixed array length, so `O(1)` pattern.
- Can convert array into a tuple to use as a dictionary key.

### Default to dictionary key to 0 if the key does not exist
```
example["key"] = example.get("key", 0) + value
```