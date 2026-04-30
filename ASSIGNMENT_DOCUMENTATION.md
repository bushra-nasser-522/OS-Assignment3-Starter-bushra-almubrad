# Assignment 3 - Complete Documentation

**Student Name**: [Your Full Name]  
**Student ID**: [Your ID]  
**Date Submitted**: [Submission Date]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - [Apr 29, 2026, 10:15 AM]
**What I implemented**: 
I started the code and added my student ID.
**Challenges encountered**: 
I didn’t really understand how threads use the same variables.
**How I solved it**: 
I looked at the shared variables and tried to understand them.
**Testing approach**: 
I ran the code and checked what happens.
**Time spent**: 
30 minutes

---

### Entry 2 - [Apr 29, 2026, 10:50 AM]
**What I implemented**: 
I added locks.

**Challenges encountered**: 
The values were not always correct.

**How I solved it**: 
I used lock and unlock

**Testing approach**: 
I ran the code again more than once.

**Time spent**: 
1 hour

---

### Entry 3 - [Apr 29, 2026, 11:50 AM]
**What I implemented**: 
I added semaphore. 

**Challenges encountered**: 
More than one process was running together.

**How I solved it**: 
I used semaphore with 1 permit.

**Testing approach**: 
I checked that processes run one by one.

**Time spent**: 
1 hour

---

### Entry 4 - [Apr 29, 2026, 1:20 PM]
**What I implemented**: 
I fixed the counters.

**Challenges encountered**: 
Threads were changing the same values.

**How I solved it**: 
I used separate locks.

**Testing approach**: 
I checked the final numbers.

**Time spent**: 
1 hour

---

### Entry 5 - [Date, Time]
**What I implemented**: 

**Challenges encountered**: 

**How I solved it**: 

**Testing approach**: 

**Time spent**: 

---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:

[Your answer here - 4-6 sentences with code examples]

contextSwitchCount is a shared variable so more than one thread can change it at the same time and this may give a wrong value. This happens because threads can run contextSwitchCount++ together. Also executionLog is an ArrayList so it is not safe when many threads use executionLog.add(message). This can lead to wrong data or unexpected behavior.

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:

[Your answer here - explain your implementation choices]
Lock is for protecting data.
Semaphore is for controlling access.
I used lock for variables and semaphore for CPU.

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:

[Your answer here - reference try-finally blocks, lock ordering, etc.]
Deadlock means nothing runs because threads are waiting.
I used try-finally to always release locks and avoid getting stuck.
Also, I didn’t use nested locks to prevent circular waiting.
This helps the program run without stopping.

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:

[Your answer here - explain coarse-grained vs fine-grained locking, independence of counters, concurrency implications. Show understanding of when to use each approach. 5-8 sentences expected.]

I used separate locks for each counter so this is fine-grained locking. I chose this because contextSwitchCount and completedProcessCount and totalWaitingTime are independent variables. Using one lock would be easier but it makes threads wait more. Separate locks allow more than one thread to work at the same time. This gives better performance and better concurrency.


---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 
contextSwitchCount, completedProcessCount, totalWaitingTime
**Why they need protection**: 
because more than one thread can change them
**Synchronization mechanism used**: 
ReentrantLock
**Code snippet**:
```java
// Paste your implementation here
contextSwitchLock.lock();
try {
    contextSwitchCount++;
} finally {
    contextSwitchLock.unlock(); 
}
```

**Justification**: 
 the values don’t become wrong

---

### Critical Section #2: Execution Log

**What resource**: 
executionLog

**Why it needs protection**: 
because ArrayList is not thread safe

**Synchronization mechanism used**: 
ReentrantLock
**Code snippet**:
```java
// Paste your implementation here
executionLogLock.lock();
try {
    executionLog.add(message);
} finally {
    executionLogLock.unlock();
}
```

**Justification**: 
to avoid errors when threads add data

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 
to control CPU

**Number of permits and why**: 
1 so only one process runs

**Where implemented**: 
in run()
**Code snippet**:
```java
// Paste your implementation here
cpuSemaphore.acquire();
try {
} finally {
    cpuSemaphore.release();
}
```

**Effect on program behavior**: 
processes run one by one

---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results
Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
I ran the program 5 times 
java SchedulerSimulationSync
```

**Results**: 
(Show that running multiple times produces consistent, correct results)
The program worked fine every time.

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)
Without synchronization, shared variables like contextSwitchCount and executionLog can be changed at the same time by different threads, and this may give wrong values.

**Conclusion**: 
Synchronization keeps everything correct.

---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 

**Results**: 

**What this proves**: 

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 

**Actual values**: 

**Analysis**: 

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 

**Results**: 

**What I learned**: 

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 

**Example 2**: 

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]

---

## Part 6: GitHub Repository Information

**Repository URL**: 

**Number of commits**: 

**Commit messages**: 
1. 
2. 
3. 
4. 

---

## Summary

**Total time spent on assignment**: 

**Key takeaways**: 
1. 
2. 
3. 

**Most challenging aspect**: 

**What I'm most proud of**: 

---

**End of Documentation**
