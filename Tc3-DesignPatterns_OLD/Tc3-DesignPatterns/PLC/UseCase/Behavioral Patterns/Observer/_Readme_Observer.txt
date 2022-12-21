Full implementation of the observer design pattern


1 publisher that notifies changes of an event 
2 subscribers themselves fetch the updated event in the publisher after an update request

The event itself is undefined in the observer base blocks and are to be implemented in the application blocks

REMARK
The implementation is the full observer pattern as described by GOF
The implementation can be made shorter in a way that the observee writes the event directly in the registered observer's memory space
but then the code that is now FB_Observer needs to be repeated in every observee and lacks re-usability of code 

