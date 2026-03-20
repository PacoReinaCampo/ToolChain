| instruction | code                                                                                  |
|-------------|---------------------------------------------------------------------------------------|
| fadd_q.h    | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_add(f128(FRS1), f128(FRS2)));                                          |
|             | set_fp_exceptions;                                                                    |
| fclass_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | WRITE_RD(f128_classify(f128(FRS1)));                                                  |
| fcvt_d_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_to_f64(f128(FRS1)));                                                   |
|             | set_fp_exceptions;                                                                    |
| fcvt_l_q.h  | require_extension('Q');                                                               |
|             | require_rv64;                                                                         |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_RD(f128_to_i64(f128(FRS1), RM, true));                                          |
|             | set_fp_exceptions;                                                                    |
| fcvt_lu_q.h | require_extension('Q');                                                               |
|             | require_rv64;                                                                         |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_RD(f128_to_ui64(f128(FRS1), RM, true));                                         |
|             | set_fp_exceptions;                                                                    |
| fcvt_q_d.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f64_to_f128(f64(FRS1)));                                                    |
|             | set_fp_exceptions;                                                                    |
| fcvt_q_l.h  | require_extension('Q');                                                               |
|             | require_rv64;                                                                         |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(i64_to_f128(RS1));                                                          |
|             | set_fp_exceptions;                                                                    |
| fcvt_q_lu.h | require_extension('Q');                                                               |
|             | require_rv64;                                                                         |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(ui64_to_f128(RS1));                                                         |
|             | set_fp_exceptions;                                                                    |
| fcvt_q_s.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f32_to_f128(f32(FRS1)));                                                    |
|             | set_fp_exceptions;                                                                    |
| fcvt_q_w.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(i32_to_f128((int32_t)RS1));                                                 |
|             | set_fp_exceptions;                                                                    |
| fcvt_q_wu.h | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(ui32_to_f128((uint32_t)RS1));                                               |
|             | set_fp_exceptions;                                                                    |
| fcvt_s_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_to_f32(f128(FRS1)));                                                   |
|             | set_fp_exceptions;                                                                    |
| fcvt_w_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_RD(sext32(f128_to_i32(f128(FRS1), RM, true)));                                  |
|             | set_fp_exceptions;                                                                    |
| fcvt_wu_q.h | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_RD(sext32(f128_to_ui32(f128(FRS1), RM, true)));                                 |
|             | set_fp_exceptions;                                                                    |
| fdiv_q.h    | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_div(f128(FRS1), f128(FRS2)));                                          |
|             | set_fp_exceptions;                                                                    |
| feq_q.h     | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | WRITE_RD(f128_eq(f128(FRS1), f128(FRS2)));                                            |
|             | set_fp_exceptions;                                                                    |
| fle_q.h     | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | WRITE_RD(f128_le(f128(FRS1), f128(FRS2)));                                            |
|             | set_fp_exceptions;                                                                    |
| flq.h       | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | uint128_t v = MMU.load<uint128_t>(RS1 + insn.i_imm());                                |
|             | float128_t f = { uint64_t(v), uint64_t(v >> 64) };                                    |
|             | WRITE_FRD(f);                                                                         |
| flt_q.h     | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | WRITE_RD(f128_lt(f128(FRS1), f128(FRS2)));                                            |
|             | set_fp_exceptions;                                                                    |
| fmadd_q.h   | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_mulAdd(f128(FRS1), f128(FRS2), f128(FRS3)));                           |
|             | set_fp_exceptions;                                                                    |
| fmax_q.h    | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | bool greater = f128_lt_quiet(f128(FRS2), f128(FRS1)) or                               |
|             | (f128_eq(f128(FRS2), f128(FRS1)) && (f128(FRS2).v[1] & F64_SIGN));                    |
|             | if (isNaNF128(f128(FRS1)) && isNaNF128(f128(FRS2)))                                   |
|             | WRITE_FRD(f128(defaultNaNF128()));                                                    |
|             | else                                                                                  |
|             | WRITE_FRD(greater or isNaNF128(f128(FRS2)) ? FRS1 : FRS2);                            |
|             | set_fp_exceptions;                                                                    |
| fmin_q.h    | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | bool less = f128_lt_quiet(f128(FRS1), f128(FRS2)) or                                  |
|             | (f128_eq(f128(FRS1), f128(FRS2)) && (f128(FRS1).v[1] & F64_SIGN));                    |
|             | if (isNaNF128(f128(FRS1)) && isNaNF128(f128(FRS2)))                                   |
|             | WRITE_FRD(f128(defaultNaNF128()));                                                    |
|             | else                                                                                  |
|             | WRITE_FRD(less or isNaNF128(f128(FRS2)) ? FRS1 : FRS2);                               |
|             | set_fp_exceptions;                                                                    |
| fmsub_q.h   | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_mulAdd(f128(FRS1), f128(FRS2), f128_negate(f128(FRS3))));              |
|             | set_fp_exceptions;                                                                    |
| fmul_q.h    | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_mul(f128(FRS1), f128(FRS2)));                                          |
|             | set_fp_exceptions;                                                                    |
| fnmadd_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_mulAdd(f128_negate(f128(FRS1)), f128(FRS2), f128_negate(f128(FRS3)))); |
|             | set_fp_exceptions;                                                                    |
| fnmsub_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_mulAdd(f128_negate(f128(FRS1)), f128(FRS2), f128(FRS3)));              |
|             | set_fp_exceptions;                                                                    |
| fsgnjn_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | WRITE_FRD(fsgnj128(FRS1, FRS2, true, false));                                         |
| fsgnj_q.h   | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | WRITE_FRD(fsgnj128(FRS1, FRS2, false, false));                                        |
| fsgnjx_q.h  | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | WRITE_FRD(fsgnj128(FRS1, FRS2, false, true));                                         |
| fsq.h       | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | uint128_t v = FRS2.v[0] or (uint128_t(FRS2.v[1]) << 64);                              |
|             | MMU.store<uint128_t>(RS1 + insn.s_imm(), v);                                          |
| fsqrt_q.h   | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_sqrt(f128(FRS1)));                                                     |
|             | set_fp_exceptions;                                                                    |
| fsub_q.h    | require_extension('Q');                                                               |
|             | require_fp;                                                                           |
|             | softfloat_roundingMode = RM;                                                          |
|             | WRITE_FRD(f128_sub(f128(FRS1), f128(FRS2)));                                          |
|             | set_fp_exceptions;                                                                    |
