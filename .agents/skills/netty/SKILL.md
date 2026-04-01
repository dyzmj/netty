```markdown
# netty Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill provides a comprehensive guide to the development patterns, coding conventions, and common workflows in the `netty` repository. The codebase is primarily Java (with some C), focused on high-performance networking, and follows consistent conventions for file organization, commit messages, and test practices. This document will help contributors quickly align with the project's standards and streamline their workflow using suggested commands.

## Coding Conventions

### File Naming
- **Java files:** Use PascalCase for class names and file names.
  - Example: `ChannelHandler.java`, `ByteBufUtil.java`
- **Test files:** Also use PascalCase, typically mirroring the class under test.
  - Example: `ChannelHandlerTest.java`

### Import Style
- **Relative imports** are preferred, referencing classes from the same or sibling packages.
  ```java
  import io.netty.util.concurrent.Future;
  import io.netty.channel.ChannelHandler;
  ```

### Export Style
- **Named exports** via public classes and interfaces.
  ```java
  public class ChannelHandler { ... }
  public interface ByteBuf { ... }
  ```

### Commit Messages
- **Freeform style**; no strict prefix, but auto-port and release commits use specific prefixes (e.g., `Auto-port 4.1:`, `Prepare for release`).
- **Average length:** ~66 characters.

## Workflows

### Auto-port Fix or Feature to 4.1
**Trigger:** When a fix or feature is merged to a mainline branch and needs to be ported to the 4.1 branch.  
**Command:** `/auto-port`

1. Cherry-pick the relevant commit from the source branch.
2. Apply changes to the same files in the 4.1 branch:
   - Implementation files (`*/src/main/java/**/*.java`, `*/src/main/c/**/*.c`)
   - Test files (`*/src/test/java/**/*.java`)
3. Update or add corresponding test files if necessary.
4. Commit with a message starting with `Auto-port 4.1:` and reference the original PR/commit.
5. Add co-author attribution if applicable.

**Example commit message:**
```
Auto-port 4.1: Fix ByteBuf leak in ChannelHandler (from #12345)
Co-authored-by: @contributor
```

---

### Test Stabilization or Diagnostic Improvement
**Trigger:** When a test is observed to be flaky, timing out, or failing nondeterministically in CI.  
**Command:** `/stabilize-test`

1. Identify the problematic test method(s) in test files (`*/src/test/java/**/*.java`).
2. Add synchronization primitives (e.g., barriers, latches) to coordinate threads.
3. Increase or adjust timeouts as needed.
4. Capture and report stack traces or exceptions from worker threads.
5. Optionally, add or adjust annotations (e.g., `@Isolated`) to control test isolation.
6. Commit changes with a message referencing test stability or diagnostics.

**Example:**
```java
@Test(timeout = 5000)
public void testConcurrentAccess() throws Exception {
    CyclicBarrier barrier = new CyclicBarrier(2);
    // ... test logic ...
}
```

---

### Release Version Bump and POM Update
**Trigger:** When preparing to release a new version or move to the next development iteration.  
**Command:** `/release-bump`

1. Update the version number in all `pom.xml` files across modules.
2. Commit with a message indicating release preparation or next iteration.
3. Affect all modules' `pom.xml` files in a single commit.

**Example commit message:**
```
Prepare for release 4.1.100.Final
```

---

### Feature or Bugfix with Corresponding Tests
**Trigger:** When adding a new feature or fixing a bug that requires test coverage.  
**Command:** `/feature-with-tests`

1. Modify or add implementation files (`*/src/main/java/**/*.java`, `*/src/main/c/**/*.c`).
2. Add or update test files in the corresponding test directory (`*/src/test/java/**/*.java`).
3. Commit both implementation and test changes together.

**Example:**
```java
// Implementation
public class NewFeatureHandler { ... }

// Test
public class NewFeatureHandlerTest {
    @Test
    public void testNewFeature() { ... }
}
```

## Testing Patterns

- **Test Framework:** Not explicitly detected, but tests are written in Java using standard conventions (likely JUnit).
- **Test File Pattern:** Test files are located in `*/src/test/java/**/*.java` and named with the `*Test.java` suffix.
- **Test Practices:**
  - Use of timeouts, synchronization primitives, and annotations for isolation.
  - Tests are updated or added alongside feature or bugfix commits.
  - Diagnostic improvements are common for flaky or timing-sensitive tests.

**Example Test:**
```java
import org.junit.Test;

public class ChannelHandlerTest {
    @Test(timeout = 2000)
    public void testHandlerBehavior() {
        // test logic
    }
}
```

## Commands

| Command            | Purpose                                                      |
|--------------------|--------------------------------------------------------------|
| /auto-port         | Cherry-pick and port a fix/feature to the 4.1 branch         |
| /stabilize-test    | Improve stability or diagnostics of flaky/timing-sensitive tests |
| /release-bump      | Update all pom.xml files for a new release or iteration      |
| /feature-with-tests| Add a feature or bugfix with corresponding tests             |
```