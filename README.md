# AI-Fundamentals-HISDP
Touseef Khan is pursuing a High Impact Skill Development Program in Data Science, focusing on mastering data analysis, machine learning, and statistical modeling to solve real-world problems and handle complex datasets.
My code
This code performs the task of finding the nearest neighbors between two sets of points using different distance metrics. Here’s a breakdown of each part:

1.Imports:
import numpy as np
This imports the numpy library, which is used for array manipulation and mathematical operations.

2. calculate_distance function:

def calculate_distance(point1, point2, p):
    if p == 1:
        return np.sum(np.abs(point1 - point2))  # Manhattan distance
    elif p == 2:
        return np.sqrt(np.sum((point1 - point2) ** 2))  # Euclidean distance
    elif p == np.inf:
        return np.max(np.abs(point1 - point2))  # Chebyshev distance
    else:
        raise ValueError("Unsupported norm. Choose 1, 2, or ∞.")

Purpose: This function calculates the distance between two points (point1 and point2) using a specified norm p.
Norms:
p = 1: Manhattan Distance (sum of absolute differences between coordinates).
p = 2: Euclidean Distance (straight-line distance between points).
p = np.inf: Chebyshev Distance (maximum absolute difference between coordinates).
If a value of p other than 1, 2, or ∞ is passed, it raises a ValueError.

3. find_nearest_neighbors function:

def find_nearest_neighbors(array1, array2, p):
    nearest_neighbors = []
    for point1 in array1:
        distances = [calculate_distance(point1, point2, p) for point2 in array2]
        nearest_index = np.argmin(distances)
        nearest_neighbors.append((point1, array2[nearest_index]))
    return nearest_neighbors
    
Purpose: This function takes two arrays of points (array1 and array2) and finds the nearest neighbor in array2 for each point in array1, based on the distance metric p.
Steps:
Loop through each point in array1: For each point1 in array1, it calculates the distance to each point in array2 using the calculate_distance function.
Find the nearest point: The distances are stored in a list, and the index of the smallest distance is found using np.argmin(distances), which gives the index of the nearest point in array2.
Store the pair: The pair (point1, nearest_neighbor) is added to nearest_neighbors.
Returns: A list of tuples, where each tuple contains a point from array1 and its nearest neighbor from array2.

4. Input arrays:

array1 = np.array([[1, 2], [3, 4], [5, 6]])
array2 = np.array([[7, 8], [2, 1], [3, 3]])
p = 2  # Euclidean distance
array1 and array2 are 2D arrays representing points in a 2-dimensional space.
p = 2 specifies that Euclidean distance will be used to measure the distances.

5. Finding and printing the nearest neighbors:

nearest_pairs = find_nearest_neighbors(array1, array2, p)
for pair in nearest_pairs:
    print(f"Point {pair[0]} in array1 is closest to point {pair[1]} in array2.")
Purpose: Calls find_nearest_neighbors to get the closest point from array2 for each point in array1 based on Euclidean distance (since p = 2).
Output: The nearest neighbors are printed in a readable format.

Example Output:
For the given arrays and p = 2 (Euclidean distance), the output would look like:


Point [1 2] in array1 is closest to point [2 1] in array2.
Point [3 4] in array1 is closest to point [3 3] in array2.
Point [5 6] in array1 is closest to point [7 8] in array2.
In this example:

The point [1, 2] from array1 is closest to [2, 1] in array2.
[3, 4] is closest to [3, 3].
[5, 6] is closest to [7, 8].
Summary:
calculate_distance handles distance calculation using different norms.
find_nearest_neighbors finds the nearest neighbor from array2 for each point in array1.
The program outputs which points in array1 are closest to which points in array2 using the chosen distance metric (p = 2 for Euclidean in this case).
