# MultiThreadingPython
## Prisha Sawhney
## 102116052
## 3CS10

This is a multithreading program written in Python that demonstrates parallel execution using threads.

## Overview

The program performs matrix multiplication using multiple threads to demonstrate the parallel processing capabilities of Python's threading module.

## Requirements

To run this program, you need:
- Python 3.x installed on your system
- Basic understanding of multithreading concepts in Python

## Usage

1. Clone this repository to your local machine
2. Navigate to the repository directory
3. Run the program using any notebook editor

## Methodology
- Import necessary libraries
```
import time
import threading
import random as r
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
```

- Create a constant matrix of the order 1000*1000
```
matrix1 = np.eye(1000)
```

- Created the task function that generates a random matrix and multiplies it with the constant matrix
```
def task(matrix1):
    matrix2 = np.random.rand(1000, 1000)
    result = np.dot(matrix1, matrix2)
    return
```

- Created a parametrized function for threading
```
def thread_task(num_of_threads):
    startTime = time.time()
    activeThreads = threading.active_count()
    
    print("Program Started for", num_of_threads, "threads")
    
    # Multiplying 100 matrices
    for i in range(100):
        t=threading.Thread(target=task, args=(matrix1,))
        t.start()
        while True:
            if threading.active_count() - activeThreads + 1 <= num_of_threads:
                break
            time.sleep(1)
    
    # Wait for all the threads to finish
    while True:
        if threading.active_count() == activeThreads:
            break
        else:
            print("Active Threads: ", threading.active_count())
            print("Threads left:", threading.active_count() - activeThreads)
            time.sleep(1)
            

    print("Program Finished for", num_of_threads, "threads")
    print("Time taken: ", time.time()-startTime)
    return time.time()-startTime
```

- Create a dataframe to store results
```
result = pd.DataFrame(columns=['Threads', 'Time (Sec)'])
```

- Calling the function and storing the results for different number of threads
```
for threads in range(1,11):
    new_row = pd.DataFrame({'Threads': [int(threads)], 'Time (Sec)': [thread_task(threads)]})
    result = pd.concat([result, new_row], ignore_index=True)
    print("\n")
```
- Displaying the results


 ![table](https://github.com/prishasawhney/Multithreading/blob/main/Table.png)
 
 
- Plotting the results


![graph](https://github.com/prishasawhney/Multithreading/blob/main/Graph.png)


- CPU Usage


![cpu usage](https://github.com/prishasawhney/Multithreading/blob/1e1d2e05ddadbd42cf3ab72906dab6ed78b6ea84/CPU%20Usage.png)


## Author

- [Prisha Sawhney](https://github.com/prishasawhney)