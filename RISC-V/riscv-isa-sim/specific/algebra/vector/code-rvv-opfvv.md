| instruction         | code                                                                                      |
|---------------------|-------------------------------------------------------------------------------------------|
| vfadd_vv.h          | // vfadd.vv vd, vs2, vs1                                                                  |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = VFP_OP_16(add, vs2, vs1);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_add(vs1, vs2);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_add(vs1, vs2);                                                                   |
|                     | })                                                                                        |
| vfclass_v.h         | // vfclass.v vd, vs2, vm                                                                  |
|                     | VI_VFP_V_LOOP                                                                             |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16(bf16_classify(vs2)) : f16(f16_classify(vs2));                     |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32(f32_classify(vs2));                                                              |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64(f64_classify(vs2));                                                              |
|                     | })                                                                                        |
| vfcvt_f_xu_v.h      | // vfcvt.f.xu.v vd, vd2, vm                                                               |
|                     | VI_VFP_CVT_INT_TO_FP(                                                                     |
|                     | { vd = ui32_to_f16(vs2); }, // BODY16                                                     |
|                     | { vd = ui32_to_f32(vs2); }, // BODY32                                                     |
|                     | { vd = ui64_to_f64(vs2); }, // BODY64                                                     |
|                     | uint                        // sign                                                       |
|                     | )                                                                                         |
| vfcvt_f_x_v.h       | // vfcvt.f.x.v vd, vd2, vm                                                                |
|                     | VI_VFP_CVT_INT_TO_FP(                                                                     |
|                     | { vd = i32_to_f16(vs2); }, // BODY16                                                      |
|                     | { vd = i32_to_f32(vs2); }, // BODY32                                                      |
|                     | { vd = i64_to_f64(vs2); }, // BODY64                                                      |
|                     | int                        // sign                                                        |
|                     | )                                                                                         |
| vfcvt_rtz_x_f_v.h   | // vfcvt.rtz.x.f.v vd, vd2, vm                                                            |
|                     | VI_VFP_CVT_FP_TO_INT(                                                                     |
|                     | { vd = f16_to_i16(vs2, softfloat_round_minMag, true); }, // BODY16                        |
|                     | { vd = f32_to_i32(vs2, softfloat_round_minMag, true); }, // BODY32                        |
|                     | { vd = f64_to_i64(vs2, softfloat_round_minMag, true); }, // BODY64                        |
|                     | int                                                      // sign                          |
|                     | )                                                                                         |
| vfcvt_rtz_xu_f_v.h  | // vfcvt.rtz.xu.f.v vd, vd2, vm                                                           |
|                     | VI_VFP_CVT_FP_TO_INT(                                                                     |
|                     | { vd = f16_to_ui16(vs2, softfloat_round_minMag, true); }, // BODY16                       |
|                     | { vd = f32_to_ui32(vs2, softfloat_round_minMag, true); }, // BODY32                       |
|                     | { vd = f64_to_ui64(vs2, softfloat_round_minMag, true); }, // BODY64                       |
|                     | uint                                                      // sign                         |
|                     | )                                                                                         |
| vfcvt_x_f_v.h       | // vfcvt.x.f.v vd, vd2, vm                                                                |
|                     | VI_VFP_CVT_FP_TO_INT(                                                                     |
|                     | { vd = f16_to_i16(vs2, softfloat_roundingMode, true); }, // BODY16                        |
|                     | { vd = f32_to_i32(vs2, softfloat_roundingMode, true); }, // BODY32                        |
|                     | { vd = f64_to_i64(vs2, softfloat_roundingMode, true); }, // BODY64                        |
|                     | int                                                      // sign                          |
|                     | )                                                                                         |
| vfcvt_xu_f_v.h      | // vfcvt.xu.f.v vd, vd2, vm                                                               |
|                     | VI_VFP_CVT_FP_TO_INT(                                                                     |
|                     | { vd = f16_to_ui16(vs2, softfloat_roundingMode, true); }, // BODY16                       |
|                     | { vd = f32_to_ui32(vs2, softfloat_roundingMode, true); }, // BODY32                       |
|                     | { vd = f64_to_ui64(vs2, softfloat_roundingMode, true); }, // BODY64                       |
|                     | uint                                                      // sign                         |
|                     | )                                                                                         |
| vfdiv_vv.h          | // vfdiv.vv  vd, vs2, vs1                                                                 |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = f16_div(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_div(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_div(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfmacc_vv.h         | // vfmacc.vv vd, rs1, vs2, vm    # vd[i] = +(vs2[i] * vs1[i]) + vd[i]                     |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = VFP_MULADD_16(vs1, vs2, vd);                                                         |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(vs1, vs2, vd);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(vs1, vs2, vd);                                                            |
|                     | })                                                                                        |
| vfmadd_vv.h         | // vfmadd: vd[i] = +(vd[i] * vs1[i]) + vs2[i]                                             |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = VFP_MULADD_16(vd, vs1, vs2);                                                         |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(vd, vs1, vs2);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(vd, vs1, vs2);                                                            |
|                     | })                                                                                        |
| vfmax_vv.h          | // vfmax                                                                                  |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = VFP_OP_16(max, vs2, vs1);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_max(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_max(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfmin_vv.h          | // vfmin vd, vs2, vs1                                                                     |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = VFP_OP_16(min, vs2, vs1);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_min(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_min(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfmsac_vv.h         | // vfmsac: vd[i] = +(vs1[i] * vs2[i]) - vd[i]                                             |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_mulAdd(vs1, vs2, bf16(vd.v ^ BF16_SIGN))                          |
|                     | :  f16_mulAdd(vs1, vs2,  f16(vd.v ^  F16_SIGN));                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(vs1, vs2, f32(vd.v ^ F32_SIGN));                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(vs1, vs2, f64(vd.v ^ F64_SIGN));                                          |
|                     | })                                                                                        |
| vfmsub_vv.h         | // vfmsub: vd[i] = +(vd[i] * vs1[i]) - vs2[i]                                             |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_mulAdd(vd, vs1, bf16(vs2.v ^ BF16_SIGN))                          |
|                     | :  f16_mulAdd(vd, vs1,  f16(vs2.v ^  F16_SIGN));                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(vd, vs1, f32(vs2.v ^ F32_SIGN));                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(vd, vs1, f64(vs2.v ^ F64_SIGN));                                          |
|                     | })                                                                                        |
| vfmul_vv.h          | // vfmul.vv vd, vs1, vs2, vm                                                              |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = VFP_OP_16(mul, vs1, vs2);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mul(vs1, vs2);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mul(vs1, vs2);                                                                   |
|                     | })                                                                                        |
| vfmv_f_s.h          | // vfmv_f_s: rd = vs2[0] (rs1=0)                                                          |
|                     | VI_VFP_COMMON;                                                                            |
|                     | uint64_t vs2_0 = 0;                                                                       |
|                     | const reg_t sew = P.VU.vsew;                                                              |
|                     | switch (sew) {                                                                            |
|                     | case e16:                                                                                 |
|                     | vs2_0 = P.VU.elt<uint16_t>(rs2_num, 0);                                                   |
|                     | break;                                                                                    |
|                     | case e32:                                                                                 |
|                     | vs2_0 = P.VU.elt<uint32_t>(rs2_num, 0);                                                   |
|                     | break;                                                                                    |
|                     | case e64:                                                                                 |
|                     | vs2_0 = P.VU.elt<uint64_t>(rs2_num, 0);                                                   |
|                     | break;                                                                                    |
|                     | default:                                                                                  |
|                     | require(0);                                                                               |
|                     | break;                                                                                    |
|                     | }                                                                                         |
|                     | // nan_extened                                                                            |
|                     | if (FLEN > sew) {                                                                         |
|                     | vs2_0 = vs2_0 or (UINT64_MAX << sew);                                                     |
|                     | }                                                                                         |
|                     | if (FLEN == 64) {                                                                         |
|                     | WRITE_FRD(f64(vs2_0));                                                                    |
|                     | } else {                                                                                  |
|                     | WRITE_FRD(f32(vs2_0));                                                                    |
|                     | }                                                                                         |
|                     | P.VU.vstart->write(0);                                                                    |
| vfncvt_f_f_w.h      | // vfncvt.f.f.w vd, vs2, vm                                                               |
|                     | VI_VFP_NCVT_FP_TO_FP(                                                                     |
|                     | { vd = P.VU.altfmt ? f32_to_bf16(vs2) : f32_to_f16(vs2); },      // BODY32                |
|                     | { vd = f64_to_f32(vs2); },                                       // BODY64                |
|                     | { require_zvfbfa_or_zvfhmin },                                   // CHECK32               |
|                     | { require(p->get_isa().get_zvd()); }                             // CHECK64               |
|                     | )                                                                                         |
| vfncvt_f_xu_w.h     | // vfncvt.f.xu.w vd, vs2, vm                                                              |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_NCVT_INT_TO_FP(                                                                    |
|                     | { vd = ui32_to_f16(vs2); },            // BODY32                                          |
|                     | { vd = ui64_to_f32(vs2); },            // BODY64                                          |
|                     | { require_extension(EXT_ZVFH); },      // CHECK32                                         |
|                     | { require(p->get_isa().get_zvf()); },  // CHECK64                                         |
|                     | uint                                   // sign                                            |
|                     | )                                                                                         |
| vfncvt_f_x_w.h      | // vfncvt.f.x.w vd, vs2, vm                                                               |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_NCVT_INT_TO_FP(                                                                    |
|                     | { vd = i32_to_f16(vs2); },             // BODY32                                          |
|                     | { vd = i64_to_f32(vs2); },             // BODY64                                          |
|                     | { require_extension(EXT_ZVFH); },      // CHECK32                                         |
|                     | { require(p->get_isa().get_zvf()); },  // CHECK64                                         |
|                     | int                                    // sign                                            |
|                     | )                                                                                         |
| vfncvt_rod_f_f_w.h  | // vfncvt.rod.f.f.w vd, vs2, vm                                                           |
|                     | VI_VFP_NCVT_FP_TO_FP(                                                                     |
|                     | {                                                              // BODY32                  |
|                     | softfloat_roundingMode = softfloat_round_odd;                                             |
|                     | vd = P.VU.altfmt ? f32_to_bf16(vs2) : f32_to_f16(vs2);                                    |
|                     | },                                                                                        |
|                     | {                                                              // BODY64                  |
|                     | softfloat_roundingMode = softfloat_round_odd;                                             |
|                     | vd = f64_to_f32(vs2);                                                                     |
|                     | },                                                                                        |
|                     | { require_zvfbfa_or_zvfh; },                                   // CHECK32                 |
|                     | { require(p->get_isa().get_zvd()); }                           // CHECK64                 |
|                     | )                                                                                         |
| vfncvt_rtz_x_f_w.h  | // vfncvt.rtz.x.f.w vd, vs2, vm                                                           |
|                     | VI_VFP_NCVT_FP_TO_INT(                                                                    |
|                     | { vd = P.VU.altfmt ? bf16_to_i8(vs2, softfloat_round_minMag, true)                        |
|                     | :  f16_to_i8(vs2, softfloat_round_minMag, true); },  // BODY16                            |
|                     | { vd = f32_to_i16(vs2, softfloat_round_minMag, true); }, // BODY32                        |
|                     | { vd = f64_to_i32(vs2, softfloat_round_minMag, true); }, // BODY64                        |
|                     | { require_zvfbfa_or_zvfh; },                             // CHECK16                       |
|                     | { require(p->get_isa().get_zvf()); },                    // CHECK32                       |
|                     | { require(p->get_isa().get_zvd()); },                    // CHECK64                       |
|                     | int                                                      // sign                          |
|                     | )                                                                                         |
| vfncvt_rtz_xu_f_w.h | // vfncvt.rtz.xu.f.w vd, vs2, vm                                                          |
|                     | VI_VFP_NCVT_FP_TO_INT(                                                                    |
|                     | { vd = P.VU.altfmt ? bf16_to_ui8(vs2, softfloat_round_minMag, true)                       |
|                     | :  f16_to_ui8(vs2, softfloat_round_minMag, true); },  // BODY16                           |
|                     | { vd = f32_to_ui16(vs2, softfloat_round_minMag, true); }, // BODY32                       |
|                     | { vd = f64_to_ui32(vs2, softfloat_round_minMag, true); }, // BODY64                       |
|                     | { require_zvfbfa_or_zvfh; },                              // CHECK16                      |
|                     | { require(p->get_isa().get_zvf()); },                     // CHECK32                      |
|                     | { require(p->get_isa().get_zvd()); },                     // CHECK64                      |
|                     | uint                                                      // sign                         |
|                     | )                                                                                         |
| vfncvt_x_f_w.h      | // vfncvt.x.f.w vd, vs2, vm                                                               |
|                     | VI_VFP_NCVT_FP_TO_INT(                                                                    |
|                     | { vd = P.VU.altfmt ? bf16_to_i8(vs2, softfloat_roundingMode, true)                        |
|                     | :  f16_to_i8(vs2, softfloat_roundingMode, true); },  // BODY16                            |
|                     | { vd = f32_to_i16(vs2, softfloat_roundingMode, true); }, // BODY32                        |
|                     | { vd = f64_to_i32(vs2, softfloat_roundingMode, true); }, // BODY64                        |
|                     | { require_zvfbfa_or_zvfh; },                             // CHECK16                       |
|                     | { require(p->get_isa().get_zvf()); },                    // CHECK32                       |
|                     | { require(p->get_isa().get_zvd()); },                    // CHECK64                       |
|                     | int                                                      // sign                          |
|                     | )                                                                                         |
| vfncvt_xu_f_w.h     | // vfncvt.xu.f.w vd, vs2, vm                                                              |
|                     | VI_VFP_NCVT_FP_TO_INT(                                                                    |
|                     | { vd = P.VU.altfmt ? bf16_to_ui8(vs2, softfloat_roundingMode, true)                       |
|                     | :  f16_to_ui8(vs2, softfloat_roundingMode, true); },  // BODY16                           |
|                     | { vd = f32_to_ui16(vs2, softfloat_roundingMode, true); }, // BODY32                       |
|                     | { vd = f64_to_ui32(vs2, softfloat_roundingMode, true); }, // BODY64                       |
|                     | { require_zvfbfa_or_zvfh; },                              // CHECK16                      |
|                     | { require(p->get_isa().get_zvf()); },                     // CHECK32                      |
|                     | { require(p->get_isa().get_zvd()); },                     // CHECK64                      |
|                     | uint                                                      // sign                         |
|                     | )                                                                                         |
| vfnmacc_vv.h        | // vfnmacc: vd[i] = -(vs1[i] * vs2[i]) - vd[i]                                            |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_mulAdd(bf16(vs2.v ^ BF16_SIGN), vs1, bf16(vd.v ^ BF16_SIGN))      |
|                     | :  f16_mulAdd( f16(vs2.v ^  F16_SIGN), vs1,  f16(vd.v ^  F16_SIGN));                      |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(f32(vs2.v ^ F32_SIGN), vs1, f32(vd.v ^ F32_SIGN));                        |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(f64(vs2.v ^ F64_SIGN), vs1, f64(vd.v ^ F64_SIGN));                        |
|                     | })                                                                                        |
| vfnmadd_vv.h        | // vfnmadd: vd[i] = -(vd[i] * vs1[i]) - vs2[i]                                            |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_mulAdd(bf16(vd.v ^ BF16_SIGN), vs1, bf16(vs2.v ^ BF16_SIGN))      |
|                     | :  f16_mulAdd( f16(vd.v ^  F16_SIGN), vs1,  f16(vs2.v ^  F16_SIGN));                      |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(f32(vd.v ^ F32_SIGN), vs1, f32(vs2.v ^ F32_SIGN));                        |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(f64(vd.v ^ F64_SIGN), vs1, f64(vs2.v ^ F64_SIGN));                        |
|                     | })                                                                                        |
| vfnmsac_vv.h        | // vfnmsac.vv vd, vs1, vs2, vm   # vd[i] = -(vs2[i] * vs1[i]) + vd[i]                     |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_mulAdd(bf16(vs1.v ^ BF16_SIGN), vs2, vd)                          |
|                     | :  f16_mulAdd( f16(vs1.v ^  F16_SIGN), vs2, vd);                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(f32(vs1.v ^ F32_SIGN), vs2, vd);                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(f64(vs1.v ^ F64_SIGN), vs2, vd);                                          |
|                     | })                                                                                        |
| vfnmsub_vv.h        | // vfnmsub: vd[i] = -(vd[i] * vs1[i]) + vs2[i]                                            |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_mulAdd(bf16(vd.v ^ BF16_SIGN), vs1, vs2)                          |
|                     | :  f16_mulAdd( f16(vd.v ^  F16_SIGN), vs1, vs2);                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_mulAdd(f32(vd.v ^ F32_SIGN), vs1, vs2);                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(f64(vd.v ^ F64_SIGN), vs1, vs2);                                          |
|                     | })                                                                                        |
| vfrec7_v.h          | // vfclass.v vd, vs2, vm                                                                  |
|                     | VI_VFP_V_LOOP                                                                             |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_recip7(vs2) : f16_recip7(vs2);                                    |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_recip7(vs2);                                                                     |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_recip7(vs2);                                                                     |
|                     | })                                                                                        |
| vfredmax_vs.h       | // vfredmax vd, vs2, vs1                                                                  |
|                     | bool is_propagate = false;                                                                |
|                     | VI_VFP_VV_LOOP_REDUCTION                                                                  |
|                     | ({                                                                                        |
|                     | vd_0 = f16_max(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f32_max(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f64_max(vd_0, vs2);                                                                |
|                     | })                                                                                        |
| vfredmin_vs.h       | // vfredmin vd, vs2, vs1                                                                  |
|                     | bool is_propagate = false;                                                                |
|                     | VI_VFP_VV_LOOP_REDUCTION                                                                  |
|                     | ({                                                                                        |
|                     | vd_0 = f16_min(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f32_min(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f64_min(vd_0, vs2);                                                                |
|                     | })                                                                                        |
| vfredosum_vs.h      | // vfredosum: vd[0] =  sum( vs2[*] , vs1[0] )                                             |
|                     | bool is_propagate = false;                                                                |
|                     | VI_VFP_VV_LOOP_REDUCTION                                                                  |
|                     | ({                                                                                        |
|                     | vd_0 = f16_add(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f32_add(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f64_add(vd_0, vs2);                                                                |
|                     | })                                                                                        |
| vfredusum_vs.h      | // vfredsum: vd[0] =  sum( vs2[*] , vs1[0] )                                              |
|                     | bool is_propagate = true;                                                                 |
|                     | VI_VFP_VV_LOOP_REDUCTION                                                                  |
|                     | ({                                                                                        |
|                     | vd_0 = f16_add(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f32_add(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f64_add(vd_0, vs2);                                                                |
|                     | })                                                                                        |
| vfrsqrt7_v.h        | // vfrsqrt7.v vd, vs2, vm                                                                 |
|                     | VI_VFP_V_LOOP                                                                             |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bf16_rsqrte7(vs2) : f16_rsqrte7(vs2);                                  |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_rsqrte7(vs2);                                                                    |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_rsqrte7(vs2);                                                                    |
|                     | })                                                                                        |
| vfsgnjn_vv.h        | // vfsgnn                                                                                 |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bfsgnj16(vs2.v, vs1.v, true, false)                                    |
|                     | :  fsgnj16(vs2.v, vs1.v, true, false);                                                    |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = fsgnj32(vs2.v, vs1.v, true, false);                                                  |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = fsgnj64(vs2.v, vs1.v, true, false);                                                  |
|                     | })                                                                                        |
| vfsgnj_vv.h         | // vfsgnj                                                                                 |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bfsgnj16(vs2.v, vs1.v, false, false)                                   |
|                     | :  fsgnj16(vs2.v, vs1.v, false, false);                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = fsgnj32(vs2.v, vs1.v, false, false);                                                 |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = fsgnj64(vs2.v, vs1.v, false, false);                                                 |
|                     | })                                                                                        |
| vfsgnjx_vv.h        | // vfsgnx                                                                                 |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = P.VU.altfmt ? bfsgnj16(vs2.v, vs1.v, false, true)                                    |
|                     | :  fsgnj16(vs2.v, vs1.v, false, true);                                                    |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = fsgnj32(vs2.v, vs1.v, false, true);                                                  |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = fsgnj64(vs2.v, vs1.v, false, true);                                                  |
|                     | })                                                                                        |
| vfsqrt_v.h          | // vsqrt.v vd, vd2, vm                                                                    |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_V_LOOP                                                                             |
|                     | ({                                                                                        |
|                     | vd = f16_sqrt(vs2);                                                                       |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_sqrt(vs2);                                                                       |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_sqrt(vs2);                                                                       |
|                     | })                                                                                        |
| vfsub_vv.h          | // vfsub.vv vd, vs2, vs1                                                                  |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP                                                                            |
|                     | ({                                                                                        |
|                     | vd = VFP_OP_16(sub, vs2, vs1);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f32_sub(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_sub(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfwadd_vv.h         | // vfwadd.vv vd, vs2, vs1                                                                 |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_add(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_add(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfwadd_wv.h         | // vfwadd.wv vd, vs2, vs1                                                                 |
|                     | VI_VFP_WV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_add(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_add(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfwcvt_f_f_v.h      | // vfwcvt.f.f.v vd, vs2, vm                                                               |
|                     | VI_VFP_WCVT_FP_TO_FP(                                                                     |
|                     | { vd = P.VU.altfmt ? bf16_to_f32(vs2) : f16_to_f32(vs2); },      // BODY16                |
|                     | { vd = f32_to_f64(vs2); },                                       // BODY32                |
|                     | { require_zvfbfa_or_zvfhmin },                                   // CHECK16               |
|                     | { require(p->get_isa().get_zvd()); }                             // CHECK32               |
|                     | )                                                                                         |
| vfwcvt_f_xu_v.h     | // vfwcvt.f.xu.v vd, vs2, vm                                                              |
|                     | VI_VFP_WCVT_INT_TO_FP(                                                                    |
|                     | { vd = P.VU.altfmt ? ui32_to_bf16(vs2) : ui32_to_f16(vs2); },                    // BODY8 |
|                     | { vd = ui32_to_f32(vs2); },                    // BODY16                                  |
|                     | { vd = ui32_to_f64(vs2); },                    // BODY32                                  |
|                     | { require_zvfbfa_or_zvfh; },                   // CHECK8                                  |
|                     | { require(p->get_isa().get_zvf()); },          // CHECK32                                 |
|                     | { require(p->get_isa().get_zvd()); },          // CHECK64                                 |
|                     | uint                                           // sign                                    |
|                     | )                                                                                         |
| vfwcvt_f_x_v.h      | // vfwcvt.f.x.v vd, vs2, vm                                                               |
|                     | VI_VFP_WCVT_INT_TO_FP(                                                                    |
|                     | { vd = P.VU.altfmt ? i32_to_bf16(vs2) : i32_to_f16(vs2); },                    // BODY8   |
|                     | { vd = i32_to_f32(vs2); },                    // BODY16                                   |
|                     | { vd = i32_to_f64(vs2); },                    // BODY32                                   |
|                     | { require_zvfbfa_or_zvfh; },                  // CHECK8                                   |
|                     | { require(p->get_isa().get_zvf()); },         // CHECK64                                  |
|                     | { require(p->get_isa().get_zvd()); },         // CHECK64                                  |
|                     | int                                           // sign                                     |
|                     | )                                                                                         |
| vfwcvt_rtz_x_f_v.h  | // vfwcvt.rtz.x.f.v vd, vs2, vm                                                           |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_WCVT_FP_TO_INT(                                                                    |
|                     | { vd = f16_to_i32(vs2, softfloat_round_minMag, true); }, // BODY16                        |
|                     | { vd = f32_to_i64(vs2, softfloat_round_minMag, true); }, // BODY32                        |
|                     | { require_extension(EXT_ZVFH); },                        // CHECK16                       |
|                     | { require(p->get_isa().get_zvf()); },                    // CHECK32                       |
|                     | int                                                      // sign                          |
|                     | )                                                                                         |
| vfwcvt_rtz_xu_f_v.h | // vfwcvt.rtz,xu.f.v vd, vs2, vm                                                          |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_WCVT_FP_TO_INT(                                                                    |
|                     | { vd = f16_to_ui32(vs2, softfloat_round_minMag, true); }, // BODY16                       |
|                     | { vd = f32_to_ui64(vs2, softfloat_round_minMag, true); }, // BODY32                       |
|                     | { require_extension(EXT_ZVFH); },                         // CHECK16                      |
|                     | { require(p->get_isa().get_zvf()); },                     // CHECK32                      |
|                     | uint                                                      // sign                         |
|                     | )                                                                                         |
| vfwcvt_x_f_v.h      | // vfwcvt.x.f.v vd, vs2, vm                                                               |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_WCVT_FP_TO_INT(                                                                    |
|                     | { vd = f16_to_i32(vs2, softfloat_roundingMode, true); }, // BODY16                        |
|                     | { vd = f32_to_i64(vs2, softfloat_roundingMode, true); }, // BODY32                        |
|                     | { require_extension(EXT_ZVFH); },                        // CHECK16                       |
|                     | { require(p->get_isa().get_zvf()); },                    // CHECK32                       |
|                     | int                                                      // sign                          |
|                     | )                                                                                         |
| vfwcvt_xu_f_v.h     | // vfwcvt.xu.f.v vd, vs2, vm                                                              |
|                     | VI_NON_ALTFMT_INSN                                                                        |
|                     | VI_VFP_WCVT_FP_TO_INT(                                                                    |
|                     | { vd = f16_to_ui32(vs2, softfloat_roundingMode, true); }, // BODY16                       |
|                     | { vd = f32_to_ui64(vs2, softfloat_roundingMode, true); }, // BODY32                       |
|                     | { require_extension(EXT_ZVFH); },                         // CHECK16                      |
|                     | { require(p->get_isa().get_zvf()); },                     // CHECK32                      |
|                     | uint                                                      // sign                         |
|                     | )                                                                                         |
| vfwmacc_vv.h        | // vfwmacc.vv vd, vs2, vs1                                                                |
|                     | VI_VFP_VV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_mulAdd(vs1, vs2, vd);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(vs1, vs2, vd);                                                            |
|                     | })                                                                                        |
| vfwmsac_vv.h        | // vfwmsac.vv  vd, vs2, vs1                                                               |
|                     | VI_VFP_VV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_mulAdd(vs1, vs2, f32(vd.v ^ F32_SIGN));                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(vs1, vs2, f64(vd.v ^ F64_SIGN));                                          |
|                     | })                                                                                        |
| vfwmul_vv.h         | // vfwmul.vv vd, vs2, vs1                                                                 |
|                     | VI_VFP_VV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_mul(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mul(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfwnmacc_vv.h       | // vfwnmacc.vv vd, vs2, vs1                                                               |
|                     | VI_VFP_VV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_mulAdd(f32(vs1.v ^ F32_SIGN), vs2, f32(vd.v ^ F32_SIGN));                        |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(f64(vs1.v ^ F64_SIGN), vs2, f64(vd.v ^ F64_SIGN));                        |
|                     | })                                                                                        |
| vfwnmsac_vv.h       | // vfwnmsac.vv vd, vs2, vs1                                                               |
|                     | VI_VFP_VV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_mulAdd(f32(vs1.v ^ F32_SIGN), vs2, vd);                                          |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_mulAdd(f64(vs1.v ^ F64_SIGN), vs2, vd);                                          |
|                     | })                                                                                        |
| vfwredosum_vs.h     | // vfwredosum.vs vd, vs2, vs1                                                             |
|                     | bool is_propagate = false;                                                                |
|                     | VI_VFP_VV_LOOP_WIDE_REDUCTION                                                             |
|                     | ({                                                                                        |
|                     | vd_0 = f32_add(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f64_add(vd_0, vs2);                                                                |
|                     | })                                                                                        |
| vfwredusum_vs.h     | // vfwredsum.vs vd, vs2, vs1                                                              |
|                     | bool is_propagate = true;                                                                 |
|                     | VI_VFP_VV_LOOP_WIDE_REDUCTION                                                             |
|                     | ({                                                                                        |
|                     | vd_0 = f32_add(vd_0, vs2);                                                                |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd_0 = f64_add(vd_0, vs2);                                                                |
|                     | })                                                                                        |
| vfwsub_vv.h         | // vfwsub.vv vd, vs2, vs1                                                                 |
|                     | VI_VFP_VV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_sub(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_sub(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vfwsub_wv.h         | // vfwsub.wv vd, vs2, vs1                                                                 |
|                     | VI_VFP_WV_LOOP_WIDE                                                                       |
|                     | ({                                                                                        |
|                     | vd = f32_sub(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | vd = f64_sub(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vmfeq_vv.h          | // vmfeq.vv vd, vs2, vs1                                                                  |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP_CMP                                                                        |
|                     | ({                                                                                        |
|                     | res = VFP_OP_16(eq, vs2, vs1);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = f32_eq(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = f64_eq(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vmfle_vv.h          | // vmfle.vv vd, vs2, rs1                                                                  |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP_CMP                                                                        |
|                     | ({                                                                                        |
|                     | res = VFP_OP_16(le, vs2, vs1);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = f32_le(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = f64_le(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vmflt_vv.h          | // vmflt.vv vd, vs2, vs1                                                                  |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP_CMP                                                                        |
|                     | ({                                                                                        |
|                     | res = VFP_OP_16(lt, vs2, vs1);                                                            |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = f32_lt(vs2, vs1);                                                                   |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = f64_lt(vs2, vs1);                                                                   |
|                     | })                                                                                        |
| vmfne_vv.h          | // vmfne.vv vd, vs2, rs1                                                                  |
|                     | require_zvfbfa                                                                            |
|                     | VI_VFP_VV_LOOP_CMP                                                                        |
|                     | ({                                                                                        |
|                     | res = !VFP_OP_16(eq, vs2, vs1);                                                           |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = !f32_eq(vs2, vs1);                                                                  |
|                     | },                                                                                        |
|                     | {                                                                                         |
|                     | res = !f64_eq(vs2, vs1);                                                                  |
|                     | })                                                                                        |
