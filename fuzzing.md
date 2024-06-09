## Answers to Lab Exercise 3 Part 2 - SeiP 2024
Name: Nikolaos Douranos

### Task 1
**Answer:** The program `simple_crash` triggers an `abort()` when it encounters sequences of consecutive numeric characters where one character is exactly one more than its predecessor. For instance, the input "444445444" results in an `abort()` because it might interpret '5' as a successor in a sequence, though this should be more carefully debugged to confirm the exact condition. Similarly, the input "ii444445444?iatWal?inpu" could contain a similar sequence triggering the `abort()`, suggesting that the code is very sensitive to specific patterns of consecutive increasing digits.

### Task 2
**Answer:** The crashes in `exercise2` were primarily caused by the program's handling of crew management operations within an airplane simulation. Specifically, the `abort()` is called when an attempt is made to land the airplane with no crew members available, following repeated 'fire' operations that reduce the crew count to zero or less.

**Detailed Findings:**
1. **Sequence of Events**: Input strings consisting of multiple 'f' operations (fire crew member) followed by an 'l' operation (land) consistently led to crashes. For example, the input sequence causing the crash included multiple firings until no crew members remained, immediately followed by a landing attempt.
2. **Abnormal Termination**: Each crash was accompanied by an `abort()` call, which is triggered in the `land()` function of the `Airplane` class when the `crew.num` is less than one. This was observed in GDB where the output from the program indicated repeated "You're out of here!" messages (indicating firing of crew members), followed by "Nobody left to land the plane!" just before the `abort()` call.

**Conclusion**:
The logical flaw in the `land()` function where it does not properly handle scenarios with zero crew members causes the program to abruptly terminate. Modifying this behavior to manage crew shortages more gracefully would prevent such crashes and improve the robustness of the program.

