# 2-Pass-Linking-Loader

## Two-Pass Direct-Linking Loader

### Overview
This project implements a **Two-Pass Direct-Linking Loader** in C. The loader processes object program files, handles control sections, resolves external symbols, applies relocation information, and generates a formatted memory image ready for execution.

### Features
- **Pass One:**
  - Builds the External Symbol Table (ESTAB).
  - Computes addresses for control sections and external symbols.
- **Pass Two:**
  - Modifies object code using relocation and modification records.
  - Generates the final memory image for execution.
  - Handles multiple control sections and external symbols.
  - Outputs memory contents in a structured format.

---

### Files

#### Source Files
- **loader.c**: The main program implementing the two-pass loader.

#### Input Files
- **input.txt**: Contains the object program. Each record follows the assembler output format: Header (H), Definition (D), Text (T), Modification (M), and End (E).

#### Output Files
- **estab.txt**: Generated after Pass One, containing the ESTAB entries.
- **output.txt**: Generated after Pass Two, containing the loaded memory image.

---


#### Record Types:
1. **Header Record (H):**
   - Format: `H <program name> <starting address> <length>`
   - Example: `H COPY 000000 00107A`

2. **Definition Record (D):**
   - Format: `D <symbol> <address>`
   - Example: `D ALPHA 000010`

3. **Text Record (T):**
   - Format: `T <starting address> <length> <object code>`
   - Example: `T 000000 1E 141033281030481039...`

4. **Modification Record (M):**
   - Format: `M <address> <length> <operation><symbol>`
   - Example: `M 000007 05 +ALPHA`

5. **End Record (E):**
   - Format: `E <execution start address>`
   - Example: `E 000000`

---

### Output Format

#### Pass One Output (**estab.txt**)
This file contains the ESTAB entries in the format:
```
<Control Section> ** <Address> <Length>
** <External Symbol> <Address>
```

**Example Output:**
```
COPY ** 000000 00107A
** ALPHA 000010
```

#### Pass Two Output (**output.txt**)
The final loaded memory image, formatted as:
```
Address			Contents
---------------------------------------------------------------
0000		141033 281030 481039 00...
...
```

---

### How It Works

#### Pass One
1. Read **H records** to extract control section names, starting addresses, and lengths.
2. Read **D records** to extract external symbol definitions.
3. Compute absolute addresses by adding the program's starting address to relative addresses.
4. Store the information in the **ESTAB** and output it to **output.txt**.

#### Pass Two
1. Read **T records** to load object code into memory.
2. Use **M records** to adjust addresses using the **ESTAB**.
3. Format and output the final memory image to **final.txt**.

---

### Example Workflow

#### Input:
Provide the **input.txt** file with object program records.

#### Execution:
Run the loader program. Enter the desired starting address when prompted.

#### Output:
- View **estab.txt** for ESTAB entries.
- View **output.txt** for the loaded memory image.

---

### Dependencies
- Standard C libraries (e.g., `stdio.h`, `string.h`).


---


