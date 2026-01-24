# **Top JVM & Garbage Collection Interview Questions** (Senior Level)

### **🔥 Must-Know Fundamentals**

1. **What are the JVM memory areas and their roles?**
   ```
   - Heap (Young + Old Gen): Object storage
   - Metaspace (Java 8+): Class metadata  
   - Stack: Method frames, local vars
   - PC Register: Thread instruction pointer
   - Native Method Stack: JNI calls
   ```
   Note: String literals are stored in the String Pool (part of Heap Memory) in Java.

2. **Explain Young vs Old Generation GC?**
   ```
   Minor GC: Young Gen (fast, frequent)
   Major GC: Old Gen (slow, infrequent)  
   Full GC: Entire heap (most expensive)
   ```

3. **How does object promotion from Young to Old Gen work?**
   ```
   - Survives multiple Minor GCs in Survivor spaces
   - Age threshold exceeded (default: 15)
   - Survivor space full → Emergency promotion
   ```

***

### **🛠️ GC Algorithms Deep Dive**

4. **Compare Serial, Parallel, CMS, and G1 Collectors:**
   ```
   | Collector | Pause Type | Best For | Flags |
   |-----------|------------|----------|-------|
   | Serial    | STW        | Client   | -XX:+UseSerialGC |
   | Parallel  | STW        | Throughput | -XX:+UseParallelGC |
   | CMS       | Low Pause  | Resp Time| -XX:+UseConcMarkSweepGC |
   | G1        | Predictable| Large Heap| -XX:+UseG1GC (DEFAULT Java 9+) |
   ```

5. **What is Stop-The-World (STW) pause? When does it happen?**
   ```
   - JVM halts ALL app threads
   - Minor GC: Eden→Survivor copy
   - Major GC: Old Gen compaction  
   - Full GC: Entire heap
   ```

6. **G1 Collector internals?**
   ```
   - Divides heap into REGIONS (not generations)
   - Concurrent marking
   - Evacuation pauses (not STW full GC)
   - Predictable pause times via `-XX:MaxGCPauseMillis`
   ```

***

### **📊 Tuning & Monitoring**

7. **JVM Flags for GC Tuning:**
   ```
   -Xms, -Xmx: Initial/Max Heap
   -XX:NewRatio=2: Young:Old ratio  
   -XX:+UseG1GC: Enable G1
   -XX:MaxGCPauseMillis=200: Target pause
   -XX:+PrintGCDetails: GC logs
   ```

8. **How to analyze GC logs?**
   ```
   [GC 10K→5K(64K)] → Minor GC, before→after(free)
   [Full GC 100M→50M(512M)] → Full GC  
   GC(G1 Evacuation Pause) → G1 specific
   ```

9. **Tools for GC analysis?**
   ```
   - jstat, jmap, jcmd (CLI)
   - VisualVM, JConsole (GUI)
   - GCViewer, GCEasy (log analyzers)
   - MAT (Eclipse Memory Analyzer)
   ```

***

### **🚨 Advanced/Production Questions**

10. **Metaspace OOM vs PermGen OOM?**
    ```
    PermGen (Java 7): Fixed size → OOM on classloading
    Metaspace (Java 8+): Native memory → Unlimited (disk swap risk)
    ```

11. **When does Full GC happen? How to avoid?**
    ```
    Triggers: Old Gen full, Metaspace full, Promotion failure
    Avoid: Right-size heap, tune Survivor ratios, use G1
    ```

12. **Explain Mark-Word in object header?**
    ```
    64-bit: HashCode(31) | Age(4) | Lock(2) | GC State
    Used for: Lock state, HashCode caching, GC age tracking
    ```

13. **What is GC Overhead Limit?**
    ```
    >98% time in GC + <2% heap used → OOM
    Default: 98% threshold -XX:-UseGCOverheadLimit to disable
    ```

***

### **💡 Tricky Follow-ups**

14. **Java 9+ default GC? Why G1 over CMS?**
    ```
    G1 is default (region-based, predictable pauses)
    CMS deprecated (fragmentation, no compaction)
    ```

15. **`-XX:+PrintFlagsFinal` vs `-XX:+PrintCommandLineFlags`?**
    ```
    PrintFlagsFinal: ALL final values (computed)
    PrintCommandLineFlags: ONLY explicit flags
    ```

16. **`Differentiate JVM vs JDK vs JRE`?**
    ```txt
    JDK (Development)
    └── JRE (Runtime)
        └── JVM (Execution Engine)
            ├── GC
            ├── JIT Compiler
            └── Interpreter
    ```

17.  Can I run Java app with just JVM?
    ❌ No - JVM needs JRE libraries (java.lang.*, Collections, etc.)

**Pro Tip:** Practice with `jcmd <pid> GC.class_histogram` and `jmap -histo:live <pid>` during interviews!

**Master these → Senior Java interviews cleared** 🚀[1][2][3]
