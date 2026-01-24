# JVM Memory Areas

1. **What are the JVM memory areas and their roles?**
   ```
   - Heap (Young + Old Gen): Object storage
   - Metaspace (Java 8+): Class metadata  
   - Stack: Method frames, local vars
   - PC Register: Thread instruction pointer
   - Native Method Stack: JNI calls
   ```
   Note: String literals are stored in the String Pool (part of Heap Memory) in Java.
