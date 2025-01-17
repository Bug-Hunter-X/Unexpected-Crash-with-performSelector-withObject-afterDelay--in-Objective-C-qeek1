# Objective-C performSelector Crash Bug

This repository demonstrates a potential crash scenario in Objective-C related to the `performSelector:withObject:afterDelay:` method.  Improper usage can lead to EXC_BAD_ACCESS exceptions if the target object is deallocated before the selector is executed.

**Problem:** The `performSelector:withObject:afterDelay:` method is used to invoke a method on an object after a specified delay. However, if the object is deallocated before the delay expires, attempting to invoke the selector on a deallocated object results in a crash. This is particularly problematic when dealing with temporary objects whose lifecycles are not carefully managed.

**Solution:**  Proper memory management is essential to prevent this crash.  Ensure the object you're performing the selector on remains valid throughout the specified delay.  Using blocks or Grand Central Dispatch (GCD) often provides better control and avoids the potential pitfalls of `performSelector`.  Avoid using `performSelector` if possible, and always validate selector usage in all circumstances.