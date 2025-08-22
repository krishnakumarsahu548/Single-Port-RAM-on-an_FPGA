# Single-Port-RAM-on-an_FPGA
A Single Port RAM is a memory block that stores data in an array-like structure, where each location (address) holds a fixed-size piece of data (e.g., 8 bits).
# Block Digram
![WhatsApp Image 2025-08-22 at 19 31 30_dfc1572f](https://github.com/user-attachments/assets/e55f4ff5-d2a1-4670-8d09-2166f015a7c0)

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
# How It Works
This is a Single Port RAM designed for an FPGA, with the following characteristics:

 Memory Array:

reg [7:0] ram [7:0] defines a memory array with 8 locations (depth = 8), each storing an 8-bit value (width = 8 bits).
Valid addresses range from 0 to 7 (requiring only 3 bits, but the input add is 8 bits, which we’ll address later).


Inputs:

clk: Clock signal for synchronous operations.
rst: Active-high reset signal to clear the memory.
wr: Write enable signal (when high, enables writing).
add[7:0]: 8-bit address input to select a memory location.
din[7:0]: 8-bit data input for writing to memory.


Output:

dout[7:0]: 8-bit data output for reading from memory.


Reset Operation:

On the rising edge of clk, if rst is high, a for loop sets all 8 memory locations (ram[0] to ram[7]) to 8'd0 (0 in decimal).
This is a synchronous reset because it depends on the clock.


Write Operation:

If rst is low and wr is high, the data from din is written to the memory location specified by add on the rising edge of clk.
For example, if add = 2 and din = 90, then ram[2] <= 90.


Read Operation:

The output dout is combinational (not clock-dependent).
If wr is low (0), dout outputs the data stored at ram[add].
If wr is high (1), dout is set to 8'd0 (0), meaning no valid read output during a write.


Single Port Nature:

Since it’s a single-port RAM, only one operation (read or write) can occur per clock cycle. The code prioritizes write when wr = 1, and dout is forced to 0 during writes.

# How the Testbench Works
The testbench simulates the RAM’s behavior by driving the inputs (rst, clk, wr, add, din) and observing the output (dout). Let’s break down the sequence of operations based on the initial block, assuming a clock period of 100ns (since #50 toggles the clock, so full period = 100ns).

Initialization (t = 0 ns):

rst = 1, clk = 0, wr = 1, add = 0, din = 0.
The RAM is in reset mode, and no operations occur yet (waiting for a clock edge).


t = 50 ns:

Inputs change: add = 2, din = 90, rst = 0.
At the next rising clock edge (t ≈ 50 ns, since always #50 clk = ~clk starts toggling):

rst = 0, wr = 1, so the RAM writes din = 90 to ram[2].
dout = 0 (since wr = 1).




t = 150 ns (50 + 100):

Inputs change: add = 3, din = 91.
At the next rising clock edge (t ≈ 150 ns):

wr = 1, so ram[3] <= 91.
dout = 0.  etc

# output Waveform
<img width="1622" height="451" alt="image" src="https://github.com/user-attachments/assets/0729b968-50bd-4f91-a1e5-aa0b7613fa0d" />
