# Lecture 4 Answers

1.  
The command filescan.nextLine() is needed because after you read the first integer in the file, there may be other "garbage" (data) and also a newline that needs to be processed before you begin to read the channel data line by line. 

The substring(1) is required since the nextInt() method will read only the channel number which means the channel name begins with a space. Using substring(1) removes the space from the channel.

2. 
```java
public int search1(String channelName) {
	// Precondition: Channel names are sorted in channelArray in increasing order.
	for (int i = 0; i < numChannels; i++) {
		// if channel numbers match, exit since we found it
		if (channelArray[i].getName().equals(channelName)) {
			System.out.println("Number of array cells examined: " + (i+1));
			return channelArray[i].getNumber();
		}
		// if next channel name in array is lexicographically after what we want, 
		// then stop searching since it can't be in the array later 
		// (array is sorted in increasing order)
		if (channelArray[i].getName().compareTo(channelName) > 0) {
			System.out.println("Number of array cells examined: " + (i+1));
			return channelArray[i].getNumber();
		}
	}
	// Whole array was examined and channel was not there
	System.out.println("Number of array cells examined: " + numChannels);
	return -1;
}
```

3.
```java
public int search2(String channelName) {
	// Precondition: Channel names are sorted in channelArray in increasing order.
	int min = 0;
	int max = numChannels-1;
	int mid = 0;
	boolean found = false;
	int cellsExamined = 0;
	while (!found && min <= max) {
		mid = (min + max) / 2;
		cellsExamined++;
		if (channelArray[mid].getName().equals(channelName))
			found = true;
		else if (channelName.compareTo(channelArray[mid].getName()) < 0)
			max = mid - 1;
		else
			min = mid + 1;
	}
	System.out.println("Number of array cells examined: " + cellsExamined);
	if (found) return channelArray[mid].getNumber();
	else return -1;
}

```
