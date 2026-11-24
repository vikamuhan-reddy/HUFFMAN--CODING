# Huffman Coding

## Aim

To implement Huffman coding to compress data using Python.

## Learning Objectives

-   Understand the concept of Huffman coding.
-   Calculate the frequency of each character in a string.
-   Generate binary codes based on character frequencies.
-   Understand how variable-length codes can be used for data
    compression.

## Software Required

1.  Anaconda -- Python 3.7
2.  Jupyter Notebook / VS Code
3.  Python standard libraries: `heapq` and `collections`

## Algorithm

### Step 1: Get the Input String

Get a string from the user as input. This string is used to calculate
character frequencies and generate Huffman codes.

### Step 2: Create Tree Nodes

Create a Node class containing the character, its frequency, and left
and right child nodes. Define a comparison method so that nodes can be
arranged by frequency in a priority queue.

### Step 3: Calculate Frequency of Occurrence

Use `Counter` to calculate how many times each character occurs in the
input string.

### Step 4: Build the Huffman Tree

Create a min-heap from the character nodes. Repeatedly remove the two
nodes with the lowest frequencies, combine them into a new node, and
insert the new node back into the heap. Continue until one root node
remains.

### Step 5: Generate and Print Huffman Codes

Traverse the Huffman tree. Add `0` when moving to the left child and `1`
when moving to the right child. Print each character, its frequency, and
its Huffman code.

## Program

``` python
import heapq
from collections import Counter

text = input("Enter a string: ")

class Node:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq

heap = [Node(char, freq) for char, freq in Counter(text).items()]
heapq.heapify(heap)

while len(heap) > 1:
    left = heapq.heappop(heap)
    right = heapq.heappop(heap)

    node = Node(None, left.freq + right.freq)
    node.left = left
    node.right = right

    heapq.heappush(heap, node)

codes = {}

def generate(node, code=""):
    if node.char is not None:
        codes[node.char] = code or "0"
    else:
        generate(node.left, code + "0")
        generate(node.right, code + "1")

if heap:
    generate(heap[0])

print("\\nCharacter\\tFrequency\\tHuffman Code")
for char, freq in Counter(text).items():
    print(f"{char!r}\\t\\t{freq}\\t\\t{codes[char]}")

print("\\nHuffman Coding Completed Successfully!")
```

## Output
<img width="336" height="137" alt="image" src="https://github.com/user-attachments/assets/ca153bd4-f373-4fe4-a318-100cf4986b0d" />




## Result

Thus, Huffman coding was successfully implemented to generate
variable-length codes for data compression using Python.
