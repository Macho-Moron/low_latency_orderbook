# High-Performance C++ Matching Engine

This project is a low-latency limit order book (LOB) written in modern C++. It is designed to simulate the core trade matching logic of a high-frequency trading (HFT) system, focusing on performance, correctness, and efficient memory management.



## 🚀 Key Features

* **Low-Latency Performance:** Architected for high-speed order processing and matching, critical for financial exchange simulations.
* **Price-Time Priority:** Strictly enforces the price-time priority matching algorithm, a fundamental requirement for exchange logic, ensuring orders are executed fairly and correctly.
* **Efficient Order Matching:** Achieves `O(log N)` complexity for order lookups and matching by leveraging balanced binary search trees.
* **Constant-Time Cancellation:** A key optimization allows for order cancellations in `O(1)` time, a significant performance improvement over naive implementations.
* **Memory Safe:** Rigorously tested with Valgrind to identify and eliminate memory leaks, ensuring system stability.

## 🛠️ Architecture & Core Data Structures

The engine's performance is built upon a carefully selected set of C++ STL containers to handle the demands of a limit order book.

1.  **Sorted Price Levels (`std::map`):**
    The core of the order book is a `std::map<Price, OrderList>`, which maintains buy and sell orders sorted by price. This allows for efficient `O(log N)` lookup of the best bid and ask.

2.  **Order Queues (`std::list`):**
    At each price level, a `std::list<Order>` acts as a queue. This choice guarantees correct price-time priority by ensuring that orders are processed in the First-In, First-Out (FIFO) sequence they were received.

3.  **Direct Order Access (`std::unordered_map`):**
    To achieve `O(1)` cancellations, a secondary `std::unordered_map<OrderID, std::list<Order>::iterator>` is maintained. This hash map stores pointers (iterators) to the orders in their respective price-level lists, allowing for direct access and removal without needing to search through the book.

## ⚡ Tech Stack

* **Language:** C++ (Modern)
* **Core Libraries:** C++ Standard Template Library (STL)
* **Build System:** CMake
* **Testing & Profiling:** Valgrind (for memory leak detection), GDB

## ⚙️ Getting Started

### Prerequisites

* A C++ compiler (e.g., g++)
* CMake
* Make

### Installation and Compilation

1.  Clone the repository:
    ```bash
    git clone [https://github.com/your-username/cpp-matching-engine.git](https://github.com/your-username/cpp-matching-engine.git)
    cd cpp-matching-engine
    ```

2.  Build the project using CMake:
    ```bash
    mkdir build
    cd build
    cmake ..
    make
    ```

3.  Run the engine executable:
    ```bash
    ./matching_engine
    ```

## ✅ Validation and Correctness

The system's integrity was validated through:
* **Unit Testing:** A comprehensive suite of unit tests was developed to verify the correctness of the matching logic under various scenarios.
* **Memory Profiling:** Valgrind was used extensively to perform dynamic analysis, ensuring the application is free of memory leaks and pointer-related errors.

## ✍️ Author

* **Soham Pal**
