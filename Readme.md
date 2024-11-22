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
