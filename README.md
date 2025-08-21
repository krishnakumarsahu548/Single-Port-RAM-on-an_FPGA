# Single-Port-RAM-on-an_FPGA
A Single Port RAM is a memory block that stores data in an array-like structure, where each location (address) holds a fixed-size piece of data (e.g., 8 bits).

# Key Features:

Single Port: One interface for both read and write operations.
Synchronous: Operations (read/write) are synchronized with a clock signal.
Control Signals:

Write Enable (we): When high, data is written to the specified address.
Address: Specifies the memory location for reading or writing.
Data In: The data to be written.
Data Out: The data read from the memory.


# Applications:
Used in caches, small buffers, or any system needing simple data storage.
