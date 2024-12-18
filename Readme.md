# MINIMIZE MAXIMUM DISTENCE BETWEEN GAS STATION

# problem is that there is array given in wich each number show one gas station and one integer also given like k so how to place k more station in between or outside the station whaich is present in array so maximum distence between two station can be minimum

def minimiseMaxDistance(arr, k):
n = len(arr) # size of array
howMany = [0] \* (n - 1)

    # Pick and place k gas stations:
    for gasStations in range(1, k + 1):
        # Find the maximum section and insert the gas station:
        maxSection = -1
        maxInd = -1
        for i in range(n - 1):
            diff = arr[i + 1] - arr[i]
            sectionLength = diff / (howMany[i] + 1)
            if sectionLength > maxSection:
                maxSection = sectionLength
                maxInd = i
        # insert the current gas station:
        howMany[maxInd] += 1

    # Find the maximum distance i.e. the answer:
    maxAns = -1
    for i in range(n - 1):
        diff = arr[i + 1] - arr[i]
        sectionLength = diff / (howMany[i] + 1)
        maxAns = max(maxAns, sectionLength)
    return maxAns

arr = [1, 2, 3, 4, 5]
k = 4
ans = minimiseMaxDistance(arr, k)
print("The answer is:", ans)

# YOU CAN DO THIS CODE USING PRIORITY QUEUE FOR BETTER OPTIMIZATION

import heapq
def minimiseMaxDistance(arr, k):
n = len(arr) # size of array.
howMany = [0] \* (n - 1)
pq = []

    # insert the first n-1 elements into pq
    # with respective distance values:
    for i in range(n - 1):
        heapq.heappush(pq, ((-1)*(arr[i + 1] - arr[i]), i))

    # Pick and place k gas stations:
    for gasStations in range(1, k + 1):
        # Find the maximum section
        # and insert the gas station:
        tp = heapq.heappop(pq)
        secInd = tp[1]

        # insert the current gas station:
        howMany[secInd] += 1

        inidiff = arr[secInd + 1] - arr[secInd]
        newSecLen = inidiff / (howMany[secInd] + 1)
        heapq.heappush(pq, (newSecLen*(-1), secInd))

    return pq[0][0]*(-1)

arr = [1, 2, 3, 4, 5]
k = 4
ans = minimiseMaxDistance(arr, k)
print("The answer is:", ans)

# median of two sorted array

def median(a, b): # size of two given arrays:
n1, n2 = len(a), len(b)

    arr3 = []
    # apply the merge step:
    i, j = 0, 0
    while i < n1 and j < n2:
        if a[i] < b[j]:
            arr3.append(a[i])
            i += 1
        else:
            arr3.append(b[j])
            j += 1

    # copy the left-out elements:
    arr3.extend(a[i:])
    arr3.extend(b[j:])

    # Find the median:
    n = n1 + n2
    if n % 2 == 1:
        return float(arr3[n // 2])

    median = (arr3[n // 2] + arr3[(n // 2) - 1]) / 2.0
    return median

if **name** == "**main**":
a = [1, 4, 7, 10, 12]
b = [2, 3, 6, 15]
print("The median of two sorted arrays is", "{:.1f}".format(median(a, b)))

approach 2

def median(a, b): # size of two given arrays:
n1, n2 = len(a), len(b)
n = n1 + n2 # total size # required indices:
ind2 = n // 2
ind1 = ind2 - 1
cnt = 0
ind1el, ind2el = -1, -1

    # apply the merge step:
    i, j = 0, 0
    while i < n1 and j < n2:
        if a[i] < b[j]:
            if cnt == ind1:
                ind1el = a[i]
            if cnt == ind2:
                ind2el = a[i]
            cnt += 1
            i += 1
        else:
            if cnt == ind1:
                ind1el = b[j]
            if cnt == ind2:
                ind2el = b[j]
            cnt += 1
            j += 1

    # copy the left-out elements:
    while i < n1:
        if cnt == ind1:
            ind1el = a[i]
        if cnt == ind2:
            ind2el = a[i]
        cnt += 1
        i += 1
    while j < n2:
        if cnt == ind1:
            ind1el = b[j]
        if cnt == ind2:
            ind2el = b[j]
        cnt += 1
        j += 1

    # Find the median:
    if n % 2 == 1:
        return float(ind2el)

    return float(ind1el + ind2el) / 2.0

if **name** == "**main**":
a = [1, 4, 7, 10, 12]
b = [2, 3, 6, 15]
print("The median of two sorted arrays is", "{:.1f}".format(median(a, b)))

approach 3 binary search 3

def median(a, b):
n1, n2 = len(a), len(b) # if n1 is bigger swap the arrays:
if n1 > n2:
return median(b, a)

    n = n1 + n2  # total length
    left = (n1 + n2 + 1) // 2  # length of left half
    # apply binary search:
    low, high = 0, n1
    while low <= high:
        mid1 = (low + high) // 2
        mid2 = left - mid1
        # calculate l1, l2, r1, and r2;
        l1, l2, r1, r2 = float('-inf'), float('-inf'), float('inf'), float('inf')
        if mid1 < n1:
            r1 = a[mid1]
        if mid2 < n2:
            r2 = b[mid2]
        if mid1 - 1 >= 0:
            l1 = a[mid1 - 1]
        if mid2 - 1 >= 0:
            l2 = b[mid2 - 1]

        if l1 <= r2 and l2 <= r1:
            if n % 2 == 1:
                return max(l1, l2)
            else:
                return (float(max(l1, l2)) + float(min(r1, r2))) / 2.0

        # eliminate the halves:
        elif l1 > r2:
            high = mid1 - 1
        else:
            low = mid1 + 1
    return 0  # dummy statement

a = [1, 4, 7, 10, 12]
b = [2, 3, 6, 15]
print("The median of two sorted arrays is {:.1f}".format(median(a, b)))

# finding the kth element of two sorted array of different size

def kthElement(a, b, m, n, k):
arr3 = []

                # Apply the merge step:
                i, j = 0, 0
                while i < m and j < n:
                    if a[i] < b[j]:
                        arr3.append(a[i])
                        i += 1
                    else:
                        arr3.append(b[j])
                        j += 1

                # Copy the left-out elements:
                arr3.extend(a[i:])
                arr3.extend(b[j:])
                return arr3[k - 1]

            if __name__ == "__main__":
                a = [2, 3, 6, 7, 9]
                b = [1, 4, 8, 10]
                print("The k-th element of two sorted arrays is:", kthElement(a, b, len(a), len(b), 5))

# binary search approach

def kthElement(a, b, m, n, k):
if m > n:
return kthElement(b, a, n, m, k)

    left = k  # length of left half

    # apply binary search:
    low = max(0, k - n)
    high = min(k, m)
    while low <= high:
        mid1 = (low + high) // 2
        mid2 = left - mid1
        # calculate l1, l2, r1, and r2
        l1 = float('-inf')
        l2 = float('-inf')
        r1 = float('inf')
        r2 = float('inf')
        if mid1 < m:
            r1 = a[mid1]
        if mid2 < n:
            r2 = b[mid2]
        if mid1 - 1 >= 0:
            l1 = a[mid1 - 1]
        if mid2 - 1 >= 0:
            l2 = b[mid2 - 1]

        if l1 <= r2 and l2 <= r1:
            return max(l1, l2)

        # eliminate the halves:
        elif l1 > r2:
            high = mid1 - 1
        else:
            low = mid1 + 1

    return 0  # dummy statement

a = [2, 3, 6, 7, 9]
b = [1, 4, 8, 10]
print("The k-th element of two sorted arrays is:", kthElement(a, b, len(a), len(b), 5))

# in given 2d matrix return that row that has maximum 1's and if more than one row have same max 1's then return smallest row.

def rowWithMax1s(matrix, n, m):
cnt_max = 0
index = -1

    # traverse the matrix:
    for i in range(n):
        cnt_ones = sum(matrix[i])
        if cnt_ones > cnt_max:
            cnt_max = cnt_ones
            index = i
    return index

if **name** == "**main**":
matrix = [[1, 1, 1], [0, 0, 1], [0, 0, 0]]
n = 3
m = 3
print("The row with maximum no. of 1's is:", rowWithMax1s(matrix, n, m))

2nd approach binary approach

def lowerBound(arr, n, x):
low = 0
high = n - 1
ans = n

    while low <= high:
        mid = (low + high) // 2
        # maybe an answer
        if arr[mid] >= x:
            ans = mid
            # look for smaller index on the left
            high = mid - 1
        else:
            low = mid + 1  # look on the right
    return ans

def rowWithMax1s(matrix, n, m):
cnt_max = 0
index = -1

    # traverse the rows:
    for i in range(n):
        # get the number of 1's:
        cnt_ones = m - lowerBound(matrix[i], m, 1)
        if cnt_ones > cnt_max:
            cnt_max = cnt_ones
            index = i
    return index

matrix = [[1, 1, 1], [0, 0, 1], [0, 0, 0]]
n = 3
m = 3
print("The row with maximum no. of 1's is:", rowWithMax1s(matrix, n, m))
