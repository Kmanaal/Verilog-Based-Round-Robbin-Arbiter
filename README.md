# Verilog-Based-Round-Robbin-Arbiter

The goal of this arbiter design is to manage resource allocation among multiple requests in a sequential (round-robin) manner. Here’s the breakdown of the design process: 
### State Definition: 
  Define each state corresponding to the request lines, which are S1, S2, S3, and S4, with an additional idle state S_idle. 
### State Transition: 
  Define a round-robin logic for state transitions so that the arbiter moves to the next active request if the current request is not asserted or has been served. 
### Priority Rotation: 
  The arbiter starts from req[0] (lowest index) and goes up to req[3] (highest index). Once it reaches req[3], it cycles back to req[0]. 
### Grant Output Logic: 
  A single grant line (grant) corresponds to each request line (req). When a request line is active, the arbiter asserts the corresponding grant output.
### Reset Behavior:
  On reset (`rst`), the system returns to the `S_idle` state, halting all operations and awaiting new requests.
### Handling of Multiple Requests:
  In the case of multiple requests being active simultaneously, the arbiter still follows the round-robin rule, giving preference to the next request in line based on the current state. This ensures that each request gets fair access, preventing any request from being starved.For example, if req[1] and req[3] are both asserted simultaneously, the arbiter will grant grant[0] for req[1], then move to the next state (S2) for req[3].
