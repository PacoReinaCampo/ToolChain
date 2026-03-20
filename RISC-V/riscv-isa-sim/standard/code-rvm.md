| instruction | code                                                                         |
|-------------|------------------------------------------------------------------------------|
| div.h       | require_extension('M');                                                      |
|             | sreg_t lhs = sext_xlen(RS1);                                                 |
|             | sreg_t rhs = sext_xlen(RS2);                                                 |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(UINT64_MAX);                                                        |
|             | else if (lhs == INT64_MIN && rhs == -1)                                      |
|             | WRITE_RD(lhs);                                                               |
|             | else                                                                         |
|             | WRITE_RD(sext_xlen(lhs / rhs));                                              |
| divu.h      | require_extension('M');                                                      |
|             | reg_t lhs = zext_xlen(RS1);                                                  |
|             | reg_t rhs = zext_xlen(RS2);                                                  |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(UINT64_MAX);                                                        |
|             | else                                                                         |
|             | WRITE_RD(sext_xlen(lhs / rhs));                                              |
| divuw.h     | require_extension('M');                                                      |
|             | require_rv64;                                                                |
|             | reg_t lhs = zext32(RS1);                                                     |
|             | reg_t rhs = zext32(RS2);                                                     |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(UINT64_MAX);                                                        |
|             | else                                                                         |
|             | WRITE_RD(sext32(lhs / rhs));                                                 |
| divw.h      | require_extension('M');                                                      |
|             | require_rv64;                                                                |
|             | sreg_t lhs = sext32(RS1);                                                    |
|             | sreg_t rhs = sext32(RS2);                                                    |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(UINT64_MAX);                                                        |
|             | else                                                                         |
|             | WRITE_RD(sext32(lhs / rhs));                                                 |
| mul.h       | require_either_extension('M', EXT_ZMMUL);                                    |
|             | WRITE_RD(sext_xlen(RS1 * RS2));                                              |
| mulh.h      | require_either_extension('M', EXT_ZMMUL);                                    |
|             | if (xlen == 64)                                                              |
|             | WRITE_RD(mulh(RS1, RS2));                                                    |
|             | else                                                                         |
|             | WRITE_RD(sext32((sext32(RS1) * sext32(RS2)) >> 32));                         |
| mulhsu.h    | require_either_extension('M', EXT_ZMMUL);                                    |
|             | if (xlen == 64)                                                              |
|             | WRITE_RD(mulhsu(RS1, RS2));                                                  |
|             | else                                                                         |
|             | WRITE_RD(sext32((sext32(RS1) * reg_t((uint32_t)RS2)) >> 32));                |
| mulhu.h     | require_either_extension('M', EXT_ZMMUL);                                    |
|             | if (xlen == 64)                                                              |
|             | WRITE_RD(mulhu(RS1, RS2));                                                   |
|             | else                                                                         |
|             | WRITE_RD(sext32(((uint64_t)(uint32_t)RS1 * (uint64_t)(uint32_t)RS2) >> 32)); |
| mulw.h      | require_either_extension('M', EXT_ZMMUL);                                    |
|             | require_rv64;                                                                |
|             | WRITE_RD(sext32(RS1 * RS2));                                                 |
| rem.h       | require_extension('M');                                                      |
|             | sreg_t lhs = sext_xlen(RS1);                                                 |
|             | sreg_t rhs = sext_xlen(RS2);                                                 |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(lhs);                                                               |
|             | else if (lhs == INT64_MIN && rhs == -1)                                      |
|             | WRITE_RD(0);                                                                 |
|             | else                                                                         |
|             | WRITE_RD(sext_xlen(lhs % rhs));                                              |
| remu.h      | require_extension('M');                                                      |
|             | reg_t lhs = zext_xlen(RS1);                                                  |
|             | reg_t rhs = zext_xlen(RS2);                                                  |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(sext_xlen(RS1));                                                    |
|             | else                                                                         |
|             | WRITE_RD(sext_xlen(lhs % rhs));                                              |
| remuw.h     | require_extension('M');                                                      |
|             | require_rv64;                                                                |
|             | reg_t lhs = zext32(RS1);                                                     |
|             | reg_t rhs = zext32(RS2);                                                     |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(sext32(lhs));                                                       |
|             | else                                                                         |
|             | WRITE_RD(sext32(lhs % rhs));                                                 |
| remw.h      | require_extension('M');                                                      |
|             | require_rv64;                                                                |
|             | sreg_t lhs = sext32(RS1);                                                    |
|             | sreg_t rhs = sext32(RS2);                                                    |
|             | if (rhs == 0)                                                                |
|             | WRITE_RD(lhs);                                                               |
|             | else                                                                         |
|             | WRITE_RD(sext32(lhs % rhs));                                                 |
