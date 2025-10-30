# LFU-Cache-in-Java
Problem Statement:

Design and implement an LFU Cache that supports these operations in O(1) average time:

get(key) → return value (if present), otherwise -1

put(key, value) → insert or update key-value pair


If the cache is full, remove the least frequently used key.
If multiple keys have the same frequency, remove the least recently used one.


---

🔹 Example:

Input:
LFUCache cache = new LFUCache(2);
cache.put(1, 1);
cache.put(2, 2);
cache.get(1);      // returns 1
cache.put(3, 3);   // evicts key 2 (least freq)
cache.get(2);      // returns -1 (not found)
cache.get(3);      // returns 3
cache.put(4, 4);   // evicts key 1
cache.get(1);      // returns -1
cache.get(3);      // returns 3
cache.get(4);      // returns 4

Output: [1, -1, 3, -1, 3, 4]


---

💡 Approach:

We need O(1) time operations → combine 3 data structures:

Data Structure	Purpose

Map<Integer, Node>	Key → Node (stores key, value, frequency)
Map<Integer, LinkedHashSet<Node>>	Frequency → Set of Nodes (maintains LRU order)
int minFreq	Keeps track of smallest frequency


Every time we call:

get() → increase frequency of that key’s node

put() → insert new node or update existing one

If cache full → remove least frequently used node from lowest frequency set


✅ Output:

1
-1
3
-1
3
4


---

⚙️ Complexity:

Operation	Time	Space

get()	O(1)	O(n)
put()	O(1)	O(n)



---

🧠 Key Takeaways:

Combines HashMap + LinkedHashSet for O(1) operations.

Maintains both frequency and recency (LRU within LFU).
