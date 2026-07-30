# ToolChain
## Researching

![QueenField](../main/icon.jpg)

**RISC-V Instruction Set Architecture**

| **RISC-V Extension**          | **Instruction Size** | **Data Size** | **Number of Registers** |
| ----------------------------- | -------------------- | ------------- | ----------------------- |
| **`I (Base Integer)`**        | `32`                 | `32, 64, 128` | `32 (x0–x31)`           |
| **`E (Base Embedded)`**       | `32`                 | `32, 64, 128` | `16 (x0–x15)`           |
| **`O (Base Extended)`**       | `64`                 | `32, 64, 128` | `1024 (x0–x1023)`       |
| **`C (Standard Compressed)`** | `16, 32`             | `32, 64, 128` | `32 (x0–x31)`           |

**OpenRISC Instruction Set Architecture**

| **OpenRISC Extension**             | **Instruction Size** | **Data Size** | **Number of Registers** |
|------------------------------------|----------------------|---------------|-------------------------|
| **`ORBIS32 (Base Integer)`**       | `32`                 | `32`          | `32`                    |
| **`ORBIS64 (Base Integer)`**       | `32`                 | `64`          | `32`                    |
| **`ORFPX32 (Standard Scalar)`**    | `32`                 | `32`          | `32`                    |
| **`ORFPX64 (Standard Scalar)`**    | `32`                 | `64`          | `32`                    |
| **`ORFPX64A32 (Standard Scalar)`** | `32`                 | `64`          | `32`                    |
| **`ORFPX64A64 (Standard Scalar)`** | `32`                 | `64`          | `64`                    |
| **`ORVDX32 (Specific Vector)`**    | `32`                 | `32`          | `32`                    |
| **`ORVDX64 (Specific Vector)`**    | `32`                 | `64`          | `32`                    |
| **`ORWDX32 (Specific Matrix)`**    | `32`                 | `32`          | `32`                    |
| **`ORWDX64 (Specific Matrix)`**    | `32`                 | `64`          | `32`                    |
| **`ORYDX32 (Specific Tensor)`**    | `32`                 | `32`          | `32`                    |
| **`ORYDX64 (Specific Tensor)`**    | `32`                 | `64`          | `32`                    |

* RISC-V / OpenRISC Opcodes
* RISC-V / OpenRISC Model
* RISC-V / OpenRISC Tests
* RISC-V / OpenRISC ISA Simulator
* RISC-V / OpenRISC GNU Compiler Collection
* RISC-V / OpenRISC Board Support Package
