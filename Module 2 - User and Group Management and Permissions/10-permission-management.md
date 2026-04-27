Linux permissions manage **who** can do **what** to a file or directory using three categories and three actions.

### 1. The Three Classes (Who)

- **Owner (u):** User owner.
- **Group (g):** Group owner.
- **Others (o):** Other

### 2. The Three Actions (What)

| Letter | Number | Action on File         | Action on Directory     |
| :----- | :----- | :--------------------- | :---------------------- |
| **r**  | **4**  | **Read** contents      | List files inside       |
| **w**  | **2**  | **Write**/Edit file    | Add/Delete files inside |
| **x**  | **1**  | **Execute** as program | "Enter" (cd) into it    |

### 3. How to Read Them

When you run `ls -l`, permissions look like `rwxr-xr--`:

- **rwx**: Owner can do everything ($4+2+1=7$).
- **r-x**: Group can read and enter ($4+1=5$).
- **r--**: Others can only read ($4$).
- **Numeric Shortcut**: This example is **754**.

---

**Quick Command:** `chmod 755 file.sh` sets permissions so the owner can do anything, while others can only read and execute.
