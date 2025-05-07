# Sorting
## Insertion sort
- Een gesorteerde sublist definiëren, steeds een item uit het ongesorteerde deel op de goede plek in het gesorteerde deel plaatsen.
- Meestal **in-place** gedaan
- Voor elk ongesorteerde item:
	- Verschuif alle grotere waardes een plek naar rechts
	- Insert daarna het item op de goede plek
- Je kan tijdens het algoritme, items aan het einde toevoegen en het zal nog steeds werken
	- Dat noem je **online**
- Het houdt de relatieve positie van gelijke items aan
	- Dat noem je **stable**
- `O(1)` space complexity
- Best case: `O(n)` time complexity
- Worst case: `O(n^2)` time complexity
- Verschil tussen best- en worst case noem je **adaptive**
``` Python
FOR j = 2 to length(A)
	key = A[j]
	# Put A[j] into the sorted sequence A[1..j-1]
	i = j - 1
	WHILE i >= 0 AND A[i] > key
		A[i+1] = A[i]
		i--
	A[i+1] = key
```
## Bubble sort
- Steeds pairs van items vergelijken en ze verwisselen als de linker groter is dan de rechter
- **In-place**
- **Stable**
- **Niet online**
- Best case: `O(n)` time complexity
- Worst case: `O(n^2)` time complexity
- **Adaptive**
``` Python
DO
	swapped = false
	for i = 0 to N-2
		if array[i] > array[i+1]
			swap(array[i], array[i+1])
			swapped = true
WHILE swapped
```
## Merge sort
- Steeds opsplitsen door de helft en vervolgens op de goede volgorde weer combineren
- `O(nlogn)` time complexity
- **Niet adaptive**
- **Stable**
- **Niet online**
- **Niet in-place**
``` Python
MERGE-SORT(A, low, high)
	if low < high
		middle = (low + high) / 2
		MERGE-SORT(A, low, middle)
		MERGE-SORT(A, middle + 1, high)
		MERGE(A, low, high, middle)
```