# ToolChain
## Researching

![QueenField](../main/icon.jpg)

**Instruction Set Architecture**

| **RISC-V Extension**          | **Instruction Size (bits)** | **Data Size (bits)**                   | **Number of Registers** |
|-------------------------------|-----------------------------|----------------------------------------|-------------------------|
| **`I (Base Integer)`**        | `32`                        | `32 (RV32I), 64 (RV64I), 128 (RV128I)` | `32 (x0–x31)`           |
| **`E (Base Embedded)`**       | `32`                        | `32 (RV32E), 64 (RV64E), 128 (RV128E)` | `16 (x0–x15)`           |
| **`O (Base Extended)`**       | `64`                        | `32 (RV32O), 64 (RV64O), 128 (RV128O)` | `1024 (x0–x1023)`       |
| **`C (Standard Compressed)`** | `16, 32`                    | `32 (RV32C), 64 (RV64C), 128 (RV128C)` | `32 (x0–x31)`           |

| **OpenRISC Extension**             | **Instruction Size (bits)** | **Data Size (bits)** | **Number of Registers** |
|------------------------------------|-----------------------------|----------------------|-------------------------|
| **`ORBIS32 (Base Integer)`**       | `32`                        | `32`                 | `32`                    |
| **`ORBIS64 (Base Integer)`**       | `32`                        | `64`                 | `32`                    |
| **`ORFPX32 (Standard Scalar)`**    | `32`                        | `32`                 | `32`                    |
| **`ORFPX64 (Standard Scalar)`**    | `32`                        | `64`                 | `32`                    |
| **`ORFPX64A32 (Standard Scalar)`** | `32`                        | `64`                 | `32`                    |
| **`ORFPX64A64 (Standard Scalar)`** | `32`                        | `64`                 | `64`                    |
| **`ORVDX32 (Specific Vector)`**    | `32`                        | `32`                 | `32`                    |
| **`ORVDX64 (Specific Vector)`**    | `32`                        | `64`                 | `32`                    |
| **`ORWDX32 (Specific Matrix)`**    | `32`                        | `32`                 | `32`                    |
| **`ORWDX64 (Specific Matrix)`**    | `32`                        | `64`                 | `32`                    |
| **`ORYDX32 (Specific Tensor)`**    | `32`                        | `32`                 | `32`                    |
| **`ORYDX64 (Specific Tensor)`**    | `32`                        | `64`                 | `32`                    |

* RISC-V / OpenRISC Opcodes
* RISC-V / OpenRISC Model
* RISC-V / OpenRISC Tests
* RISC-V / OpenRISC ISA Simulator
* RISC-V / OpenRISC GNU Compiler Collection
* RISC-V / OpenRISC Board Support Package
