# modbus-server
A Modbus-TCP slave based on the modbus crate.

Based on http://www.modbus.org/docs/Modbus_Application_Protocol_V1_1b.pdf

To run: 

./target/debug/modbus-server slave --addr 127.0.0.1:5020

TODO:

    1. Add error handling. [DONE]
    
       The Modbus standard imposes limits on reads and writes
       to keep PDUs within the 255 byte limit. Server side enforcement
       needs to happen,
       
    2. Modularize the parsing to make this work for RS-485 [DONE]
    
       Change the parse function so that it can forego interpreting
       the MBAP. And add code to intepret and calculate the checksum.
       
    3. Come back to using channels ? [DONE]

       Channels are the way to use the Actor Model in Rust,
       and the Actor Model is how stuff gets develoiped in this sector.
       Plus, the Arc module has `unsafe` code in it, so reverting to
       channels makes this a better proof of concept, and allows more
       flexibility in modifying the Registers on the back end for
       simulations. 

    4. Define a structure and a trait for the Modbus block, with blankRegisters as one implementation.
    
       The structure should have the 4 register blocks, with size optional, and the trait should require the 
       call() method, with a request and response PDU. That allows the same thing to be implemented for RS-485,
       with the only change required applying to the parse() function. It needs to split the MBAP parse off. 
       
    5. Enable multiple slaves on one por. (I.e. array indexed by MBAP) [DONE]
