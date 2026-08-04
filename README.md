# ToolChain
## Researching

![QueenField](../main/icon.jpg)

**RISC-V Instruction Set Architecture**

| **RISC-V Extension**          | **Instruction Size** | **Data Size** | **Number of Registers** |
|-------------------------------|----------------------|---------------|-------------------------|
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

**ToolChain Instruction Set Architecture**

* RISC-V / OpenRISC Opcodes
* RISC-V / OpenRISC Model
* RISC-V / OpenRISC Tests
* RISC-V / OpenRISC ISA Simulator
* RISC-V / OpenRISC GNU Compiler Collection
* RISC-V / OpenRISC Board Support Package

## RISC-V Instruction Set Architecture Opcodes

**I-Base**:

- riscv-opcodes/rv32_i
- riscv-opcodes/rv32_zicntr
- riscv-opcodes/rv32_zilsd
- riscv-opcodes/rv64_i
- riscv-opcodes/rv_i
- riscv-opcodes/rv_zibi
- riscv-opcodes/rv_zicbo
- riscv-opcodes/rv_zicfilp
- riscv-opcodes/rv_zicfiss
- riscv-opcodes/rv_zicntr
- riscv-opcodes/rv_zicond
- riscv-opcodes/rv_zicsr
- riscv-opcodes/rv_zifencei
- riscv-opcodes/rv_zihintntl
- riscv-opcodes/rv_zimop

**M-Standard**:

- riscv-opcodes/rv64_m
- riscv-opcodes/rv_m

**A-Standard**:

- riscv-opcodes/rv64_a
- riscv-opcodes/rv_a
- riscv-opcodes/rv64_zacas
- riscv-opcodes/rv_zabha
- riscv-opcodes/rv_zabha_zacas
- riscv-opcodes/rv_zacas
- riscv-opcodes/rv_zalasr
- riscv-opcodes/rv_zawrs

**C-Standard**:

- riscv-opcodes/rv32_c
- riscv-opcodes/rv32_c_f
- riscv-opcodes/rv32_zclsd
- riscv-opcodes/rv64_c
- riscv-opcodes/rv64_zcb
- riscv-opcodes/rv_c
- riscv-opcodes/rv_c_d
- riscv-opcodes/rv_c_zicfiss
- riscv-opcodes/rv_c_zihintntl
- riscv-opcodes/rv_zcb
- riscv-opcodes/rv_zcmop
- riscv-opcodes/rv_zcmp
- riscv-opcodes/rv_zcmt

**Specific**:

HF-Arithmetic:

- riscv-opcodes/rv64_zfh
- riscv-opcodes/rv_zfh
- riscv-opcodes/rv_zfhmin
- riscv-opcodes/rv_zfh_zfa

F-Arithmetic:

- riscv-opcodes/rv64_f
- riscv-opcodes/rv_f
- riscv-opcodes/rv_f_zfa
- riscv-opcodes/rv_zfbfmin

D-Arithmetic:

- riscv-opcodes/rv32_d_zfa
- riscv-opcodes/rv64_d
- riscv-opcodes/rv_d
- riscv-opcodes/rv_d_zfa
- riscv-opcodes/rv_d_zfhmin

Q-Arithmetic:

- riscv-opcodes/rv64_q
- riscv-opcodes/rv64_q_zfa
- riscv-opcodes/rv_q
- riscv-opcodes/rv_q_zfa
- riscv-opcodes/rv_q_zfhmin

V-Algebra:

- riscv-opcodes/rv_v
- riscv-opcodes/rv_v_aliases
- riscv-opcodes/rv_zvabd
- riscv-opcodes/rv_zvbb
- riscv-opcodes/rv_zvbc
- riscv-opcodes/rv_zvdot4a
- riscv-opcodes/rv_zvfbdot32f
- riscv-opcodes/rv_zvfbfmin
- riscv-opcodes/rv_zvfbfwma
- riscv-opcodes/rv_zvfofp4min
- riscv-opcodes/rv_zvfofp8min
- riscv-opcodes/rv_zvfqbdot8f
- riscv-opcodes/rv_zvfqldot8f
- riscv-opcodes/rv_zvfwbdot16bf
- riscv-opcodes/rv_zvfwldot16bf
- riscv-opcodes/rv_zvqbdot8i
- riscv-opcodes/rv_zvqldot8i
- riscv-opcodes/rv_zvzip

X-Cryptography:

- riscv-opcodes/rv32_zk
- riscv-opcodes/rv32_zkn
- riscv-opcodes/rv32_zknd
- riscv-opcodes/rv32_zkne
- riscv-opcodes/rv32_zknh
- riscv-opcodes/rv32_zks
- riscv-opcodes/rv64_zk
- riscv-opcodes/rv64_zkn
- riscv-opcodes/rv64_zknd
- riscv-opcodes/rv64_zkne
- riscv-opcodes/rv64_zknh
- riscv-opcodes/rv64_zks
- riscv-opcodes/rv_zk
- riscv-opcodes/rv_zkn
- riscv-opcodes/rv_zknh
- riscv-opcodes/rv_zks
- riscv-opcodes/rv_zksed
- riscv-opcodes/rv_zksh

V-Cryptography:

- riscv-opcodes/rv_zvkg
- riscv-opcodes/rv_zvkn
- riscv-opcodes/rv_zvkned
- riscv-opcodes/rv_zvknha
- riscv-opcodes/rv_zvknhb
- riscv-opcodes/rv_zvks
- riscv-opcodes/rv_zvksed
- riscv-opcodes/rv_zvksh

B-Parallelism:

- riscv-opcodes/rv32_zbb
- riscv-opcodes/rv32_zbkb
- riscv-opcodes/rv32_zbs
- riscv-opcodes/rv64_zba
- riscv-opcodes/rv64_zbb
- riscv-opcodes/rv64_zbkb
- riscv-opcodes/rv64_zbp
- riscv-opcodes/rv64_zbs
- riscv-opcodes/rv_zba
- riscv-opcodes/rv_zbb
- riscv-opcodes/rv_zbc
- riscv-opcodes/rv_zbkb
- riscv-opcodes/rv_zbkc
- riscv-opcodes/rv_zbkx
- riscv-opcodes/rv_zbp
- riscv-opcodes/rv_zbs

P-Parallelism:

- riscv-opcodes/rv32_p
- riscv-opcodes/rv64_p
- riscv-opcodes/rv_p

S-Privilege:

- riscv-opcodes/rv_s
- riscv-opcodes/rv_sdext
- riscv-opcodes/rv_smrnmi
- riscv-opcodes/rv_ssctr
- riscv-opcodes/rv_svinval
- riscv-opcodes/rv_svinval_h
- riscv-opcodes/rv_system

H-Privilege:

- riscv-opcodes/rv64_h
- riscv-opcodes/rv_h

## RISC-V Instruction Set Architecture Model

## RISC-V Instruction Set Architecture Tests

**RISCV-V User**:

- riscv-tests/rv32ui
- riscv-tests/rv64ui
- riscv-tests/rv64uziccid
- riscv-tests/rv32um
- riscv-tests/rv64um
- riscv-tests/rv32ua
- riscv-tests/rv64ua
- riscv-tests/rv32uc
- riscv-tests/rv64uc
- riscv-tests/rv32uzfh
- riscv-tests/rv64uzfh
- riscv-tests/rv32uf
- riscv-tests/rv64uf
- riscv-tests/rv32ud
- riscv-tests/rv64ud
- riscv-tests/rv32uzba
- riscv-tests/rv64uzba
- riscv-tests/rv32uzbb
- riscv-tests/rv64uzbb
- riscv-tests/rv32uzbc
- riscv-tests/rv64uzbc
- riscv-tests/rv32uzbkb
- riscv-tests/rv64uzbkb
- riscv-tests/rv32uzbkx
- riscv-tests/rv64uzbkx
- riscv-tests/rv32uzbs
- riscv-tests/rv64uzbs

**RISCV-V Superuser**:

- riscv-tests/rv32si
- riscv-tests/rv64si
- riscv-tests/rv64ssvnapot

**RISCV-V Machine**:

- riscv-tests/rv32mi
- riscv-tests/rv64mi
- riscv-tests/rv64mzicbo

## RISC-V Instruction Set Architecture Simulator

## RISC-V Instruction Set Architecture GNU Compiler Collection

## RISC-V Instruction Set Architecture Board Support Package
