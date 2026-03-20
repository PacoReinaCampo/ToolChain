| instruction | code                                                                                 |
|-------------|--------------------------------------------------------------------------------------|
| fadd_d.h    | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_add(FRS1_D, FRS2_D));                                                |
|             | set_fp_exceptions;                                                                   |
| fclass_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | WRITE_RD(f64_classify(FRS1_D));                                                      |
| fcvt_d_l.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_rv64;                                                                        |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(i64_to_f64(RS1));                                                        |
|             | set_fp_exceptions;                                                                   |
| fcvt_d_lu.h | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_rv64;                                                                        |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(ui64_to_f64(RS1));                                                       |
|             | set_fp_exceptions;                                                                   |
| fcvt_d_s.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f32_to_f64(FRS1_F));                                                     |
|             | set_fp_exceptions;                                                                   |
| fcvt_d_w.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(i32_to_f64((int32_t)RS1));                                               |
|             | set_fp_exceptions;                                                                   |
| fcvt_d_wu.h | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(ui32_to_f64((uint32_t)RS1));                                             |
|             | set_fp_exceptions;                                                                   |
| fcvt_l_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_rv64;                                                                        |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_RD(f64_to_i64(FRS1_D, RM, true));                                              |
|             | set_fp_exceptions;                                                                   |
| fcvt_lu_d.h | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_rv64;                                                                        |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_RD(f64_to_ui64(FRS1_D, RM, true));                                             |
|             | set_fp_exceptions;                                                                   |
| fcvt_s_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_F(f64_to_f32(FRS1_D));                                                     |
|             | set_fp_exceptions;                                                                   |
| fcvt_w_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_RD(sext32(f64_to_i32(FRS1_D, RM, true)));                                      |
|             | set_fp_exceptions;                                                                   |
| fcvt_wu_d.h | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_RD(sext32(f64_to_ui32(FRS1_D, RM, true)));                                     |
|             | set_fp_exceptions;                                                                   |
| fdiv_d.h    | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_div(FRS1_D, FRS2_D));                                                |
|             | set_fp_exceptions;                                                                   |
| feq_d.h     | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | WRITE_RD(f64_eq(FRS1_D, FRS2_D));                                                    |
|             | set_fp_exceptions;                                                                   |
| fld.h       | require_extension('D');                                                              |
|             | require_fp;                                                                          |
|             | WRITE_FRD(f64(MMU.load<uint64_t>(RS1 + insn.i_imm())));                              |
| fle_d.h     | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | WRITE_RD(f64_le(FRS1_D, FRS2_D));                                                    |
|             | set_fp_exceptions;                                                                   |
| flt_d.h     | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | WRITE_RD(f64_lt(FRS1_D, FRS2_D));                                                    |
|             | set_fp_exceptions;                                                                   |
| fmadd_d.h   | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_mulAdd(FRS1_D, FRS2_D, FRS3_D));                                     |
|             | set_fp_exceptions;                                                                   |
| fmax_d.h    | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | bool greater = f64_lt_quiet(FRS2_D, FRS1_D) or                                       |
|             | (f64_eq(FRS2_D, FRS1_D) && (FRS2_D.v & F64_SIGN));                                   |
|             | if (isNaNF64UI(FRS1_D.v) && isNaNF64UI(FRS2_D.v))                                    |
|             | WRITE_FRD_D(f64(defaultNaNF64UI));                                                   |
|             | else                                                                                 |
|             | WRITE_FRD_D((greater or isNaNF64UI(FRS2_D.v) ? FRS1_D : FRS2_D));                    |
|             | set_fp_exceptions;                                                                   |
| fmin_d.h    | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | bool less = f64_lt_quiet(FRS1_D, FRS2_D) or                                          |
|             | (f64_eq(FRS1_D, FRS2_D) && (FRS1_D.v & F64_SIGN));                                   |
|             | if (isNaNF64UI(FRS1_D.v) && isNaNF64UI(FRS2_D.v))                                    |
|             | WRITE_FRD_D(f64(defaultNaNF64UI));                                                   |
|             | else                                                                                 |
|             | WRITE_FRD_D((less or isNaNF64UI(FRS2_D.v) ? FRS1_D : FRS2_D));                       |
|             | set_fp_exceptions;                                                                   |
| fmsub_d.h   | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_mulAdd(FRS1_D, FRS2_D, f64(FRS3_D.v ^ F64_SIGN)));                   |
|             | set_fp_exceptions;                                                                   |
| fmul_d.h    | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_mul(FRS1_D, FRS2_D));                                                |
|             | set_fp_exceptions;                                                                   |
| fmv_d_x.h   | require_extension('D');                                                              |
|             | require_rv64;                                                                        |
|             | require_fp;                                                                          |
|             | WRITE_FRD(f64(RS1));                                                                 |
| fmv_x_d.h   | require_extension('D');                                                              |
|             | require_rv64;                                                                        |
|             | require_fp;                                                                          |
|             | WRITE_RD(FRS1.v[0]);                                                                 |
| fnmadd_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_mulAdd(f64(FRS1_D.v ^ F64_SIGN), FRS2_D, f64(FRS3_D.v ^ F64_SIGN))); |
|             | set_fp_exceptions;                                                                   |
| fnmsub_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_mulAdd(f64(FRS1_D.v ^ F64_SIGN), FRS2_D, FRS3_D));                   |
|             | set_fp_exceptions;                                                                   |
| fsd.h       | require_extension('D');                                                              |
|             | require_fp;                                                                          |
|             | MMU.store<uint64_t>(RS1 + insn.s_imm(), FRS2.v[0]);                                  |
| fsgnj_d.h   | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | WRITE_FRD_D(fsgnj64(freg(FRS1_D), freg(FRS2_D), false, false));                      |
| fsgnjn_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | WRITE_FRD_D(fsgnj64(freg(FRS1_D), freg(FRS2_D), true, false));                       |
| fsgnjx_d.h  | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | WRITE_FRD_D(fsgnj64(freg(FRS1_D), freg(FRS2_D), false, true));                       |
| fsqrt_d.h   | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_sqrt(FRS1_D));                                                       |
|             | set_fp_exceptions;                                                                   |
| fsub_d.h    | require_either_extension('D', EXT_ZDINX);                                            |
|             | require_fp;                                                                          |
|             | softfloat_roundingMode = RM;                                                         |
|             | WRITE_FRD_D(f64_sub(FRS1_D, FRS2_D));                                                |
|             | set_fp_exceptions;                                                                   |
