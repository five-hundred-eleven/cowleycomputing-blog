---
title: 'Priority Queue'
description: "   This is a description of the project found here: <https://github.com/five-hundred-eleven/five_one_one_q>  five-one-one-q ==============  C-backed priority queue implementation, with support for a sort-like `key` argument.   The order of items returned by..."
date: '2023-09-17'
---


This is a description of the project found here: <https://github.com/five-hundred-eleven/five_one_one_q>

five-one-one-q
==============

C-backed priority queue implementation, with support for a sort-like `key` argument.

### Behavior

The order of items returned by `await q.get()` is as follows:

1. Lowest value of `key(item)` is first out.
2. If multiple items have a tied value of `key(item)`, FIFO is followed.

If the `first_out=five_one_one_q.HIGHEST` keyword argument is given to the constructor, the highest `key(item)` is first out.

For items put into the queue, `key(item)` must support the `<` operator, or if `first_out` is set to `HIGHEST`, the `>` operator.

This queue implementation is optimized for a small number of unique values of `key(item)` for the items in the queue. If the number of unique values of `key(item)` is large, the performance will be poor.

### Examples

The following assume an environment that supports `await`.

#### First:

```
import operator
import five_one_one_q

my_q = five_one_one_q.PriorityQueue(key=operator.itemgetter(0), first_out=five_one_one_q.LOWEST)

await my_q.put((3, "Alice"))
await my_q.put((1, "Eve"))
await my_q.put((2, "Bob"))

results = []
while not my_q.empty():
    item = await my_q.get()
    results.append(item)

print(results)

```

Will output the following:

```
# Lowest priority first out
[(1, 'Eve'), (2, 'Bob'), (3, 'Alice')]

```
#### Second:

```
import operator
import random
import five_one_one_q

my_q = five_one_one_q.PriorityQueue(key=operator.itemgetter(0), first_out=five_one_one_q.LOWEST)


for item_counter in range(20):
    # first item is a randomized priority
    # second item would be the place in a non-priority queue
    await my_q.put((random.randint(1, 3), item_counter))

results = []
while not my_q.empty():
    item = await my_q.get()
    results.append(item)

print(results)

```

Will output the following:

```
# Lowest priority first out
# Tied priority, first in first out
[(1, 1), (1, 2), (1, 5), (1, 7), (1, 8), (1, 14), (1, 18), (2, 3), (2, 4), (2, 9), (2, 11), (2, 12), (3, 0), (3, 6), (3, 10), (3, 13), (3, 15), (3, 16), (3, 17), (3, 19)]

```
#### Third:

```
import operator
import random
import five_one_one_q

my_q = five_one_one_q.PriorityQueue(key=operator.itemgetter(0), first_out=five_one_one_q.LOWEST)


for item_counter in range(20, 0, -1):
    # first item is a randomized priority
    # second item would be the REVERSED place in a non-priority queue
    await my_q.put((random.randint(1, 3), item_counter))

results = []
while not my_q.empty():
    item = await my_q.get()
    results.append(item)

print(results)

```

Will output the following:

```
# Lowest priority first out
# Tied priority, first in first out
[(1, 19), (1, 10), (1, 7), (1, 6), (1, 4), (1, 3), (2, 20), (2, 17), (2, 16), (2, 15), (2, 9), (2, 5), (2, 1), (3, 18), (3, 14), (3, 13), (3, 12), (3, 11), (3, 8), (3, 2)]

```
### Current Status

I have not seen unexpected exceptions raised by `await get()` or `await put(item)` in the current iteration. The order out is as expected.

TODO: This is a C-backed library meaning that object reference counts need to be handled manually. The library needs to be rigorously checked for memory leaks.

### Test Suite

The test suite depends on `pytest` and `pytest-asyncio`. To ensure that this library works "as advertised" the developer can run `make test`. Further test commands can be found in the Makefile, but these should not be necessary to run in most cases.

### Performance Discussion

Performance against the builtin `asyncio.PriorityQueue` can be analyzed by running `make test-performance` and then looking at `performance.log`. (Expanding and improving these tests is currently being worked on.)

Key takeaways are discussed below.

#### Randomized operations, small queue, small number of unique priorities

`five_one_one_q.PriorityQueue` is moderately faster.

```
2023-07-12 23:25:01,346 | INFO | Test: randomized put/get operations
	number of randomized put/get operations: 100000
	number of unique priorities: 2
	faster: five one one: 	0.059 seconds
	slower: asyncio: 	0.071 seconds
	difference: 16.971%

```
#### Randomized operations, small queue, large number of unique priorities

`asyncio.PriorityQueue` is moderately faster.

```
2023-07-12 23:25:03,717 | INFO | Test: randomized put/get operations
	number of randomized put/get operations: 100000
	number of unique priorities: 9223372036854775807
	faster: asyncio: 	0.076 seconds
	slower: five one one: 	0.103 seconds
	difference: 26.224%

```
#### `put`/`push`, large queue, small number of unique priorities

`asyncio.PriorityQueue` is slightly faster.

```
2023-07-12 23:24:49,634 | INFO | Test: put operations on a large queue
	number of put operations: 100000
	number of unique priorities: 2
	faster: asyncio: 	0.056 seconds
	slower: five one one: 	0.057 seconds
	difference: 1.239%

```
#### `put`/`push`, large queue, large number of unique priorities

`asyncio.PriorityQueue` is significantly faster.

```
2023-07-12 23:24:52,767 | INFO | Test: put operations on a large queue
	number of put operations: 100000
	number of unique priorities: 9223372036854775807
	faster: asyncio: 	0.062 seconds
	slower: five one one: 	1.596 seconds
	difference: 96.107%

```
#### `get`/`pop`, large queue, small number of unique priorities

`five_one_one_q.PriorityQueue` is significantly faster.

```
2023-07-12 23:24:53,584 | INFO | Test: get operations on a large queue
	number of get operations: 100000
	number of unique priorities: 2
	faster: five one one: 	0.047 seconds
	slower: asyncio: 	0.169 seconds
	difference: 71.880%

```
#### `get`/`pop`, large queue, large number of unique priorities

`asyncio.PriorityQueue` is significantly faster.

```
2023-07-12 23:25:00,921 | INFO | Test: get operations on a large queue
	number of get operations: 100000
	number of unique priorities: 9223372036854775807
	faster: asyncio: 	0.246 seconds
	slower: five one one: 	1.607 seconds
	difference: 84.727%

```
#### Conclusion

`five_one_one_q.PriorityQueue` performs well with a small number of unique priorities. However I recommend using it first and foremost for the usefulness of the `key` and `first_out` keyword arguments, and potential performance boosts second.

### Implementation Details

"Under the hood", this queue is implemented as a list of 2-tuples of  
(priority, collections.deque), which we refer to as "buckets". Because  
repeatedly constructing and destructing deques has a performance cost, the queue will tolerate up to 20 empty buckets. Allowing empty buckets allows for good performance if some buckets tend to fluctuate between being empty and not empty.

If the number of empty buckets exceeds 20, all empty buckets will be removed and the queue will change its cleaning strategy such that buckets will be removed immediately on becoming empty. This is intended to save memory if there are a large number of unique priorities.

The "20 max empty buckets" behavior may become configurable after I study the performance tradeoffs more.


