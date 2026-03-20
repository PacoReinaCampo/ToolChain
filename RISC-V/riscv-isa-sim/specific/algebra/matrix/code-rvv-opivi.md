| instruction     | code                                                                                                |
|-----------------|-----------------------------------------------------------------------------------------------------|
| vadc_vim.h      | // vadc.vim vd, vs2, simm5, v0                                                                      |
|                 | VI_XI_LOOP_WITH_CARRY                                                                               |
|                 | ({                                                                                                  |
|                 | vd = (uint128_t)((op_mask & simm5) + (op_mask & vs2) + carry);                                      |
|                 | })                                                                                                  |
| vadd_vi.h       | // vadd.vi vd, simm5, vs2, vm                                                                       |
|                 | VI_VI_LOOP                                                                                          |
|                 | ({                                                                                                  |
|                 | vd = simm5 + vs2;                                                                                   |
|                 | })                                                                                                  |
| vand_vi.h       | // vand.vi vd, simm5, vs2, vm                                                                       |
|                 | VI_VI_LOOP                                                                                          |
|                 | ({                                                                                                  |
|                 | vd = simm5 & vs2;                                                                                   |
|                 | })                                                                                                  |
| vmadc_vi.h      | // vmadc.vi vd, vs2, simm5                                                                          |
|                 | #include "vmadc_vim.h"                                                                              |
| vmadc_vim.h     | // vmadc.vim vd, vs2, simm5, v0                                                                     |
|                 | VI_XI_LOOP_CARRY                                                                                    |
|                 | ({                                                                                                  |
|                 | res = (((op_mask & simm5) + (op_mask & vs2) + carry) >> sew) & 0x1u;                                |
|                 | })                                                                                                  |
| vmerge_vim.h    | // vmerge.vim vd, vs2, simm5                                                                        |
|                 | VI_VI_MERGE_LOOP                                                                                    |
|                 | ({                                                                                                  |
|                 | vd = use_first ? simm5 : vs2;                                                                       |
|                 | })                                                                                                  |
| vmseq_vi.h      | // vseq.vi vd, vs2, simm5                                                                           |
|                 | VI_VI_LOOP_CMP                                                                                      |
|                 | ({                                                                                                  |
|                 | res = simm5 == vs2;                                                                                 |
|                 | })                                                                                                  |
| vmsgtu_vi.h     | // vmsgtu.vi  vd, vd2, simm5                                                                        |
|                 | VI_VI_ULOOP_CMP                                                                                     |
|                 | ({                                                                                                  |
|                 | res = vs2 > (insn.v_simm5() & (UINT64_MAX >> (64 - P.VU.vsew)));                                    |
|                 | })                                                                                                  |
| vmsgt_vi.h      | // vsgt.vi  vd, vs2, simm5                                                                          |
|                 | VI_VI_LOOP_CMP                                                                                      |
|                 | ({                                                                                                  |
|                 | res = vs2 > simm5;                                                                                  |
|                 | })                                                                                                  |
| vmsleu_vi.h     | // vmsleu.vi vd, vs2, simm5                                                                         |
|                 | VI_VI_ULOOP_CMP                                                                                     |
|                 | ({                                                                                                  |
|                 | res = vs2 <= (insn.v_simm5() & (UINT64_MAX >> (64 - P.VU.vsew)));                                   |
|                 | })                                                                                                  |
| vmsle_vi.h      | // vsle.vi vd, vs2, simm5                                                                           |
|                 | VI_VI_LOOP_CMP                                                                                      |
|                 | ({                                                                                                  |
|                 | res = vs2 <= simm5;                                                                                 |
|                 | })                                                                                                  |
| vmsne_vi.h      | // vsne.vi  vd, vs2, simm5                                                                          |
|                 | VI_VI_LOOP_CMP                                                                                      |
|                 | ({                                                                                                  |
|                 | res = vs2 != simm5;                                                                                 |
|                 | })                                                                                                  |
| vmv1r_v.h       | // vmv1r.v vd, vs2                                                                                  |
|                 | #include "vmvnfr_v.h"                                                                               |
| vmv2r_v.h       | // vmv2r.v vd, vs2                                                                                  |
|                 | #include "vmvnfr_v.h"                                                                               |
| vmv4r_v.h       | // vmv4r.v vd, vs2                                                                                  |
|                 | #include "vmvnfr_v.h"                                                                               |
| vmv8r_v.h       | // vmv8r.v vd, vs2                                                                                  |
|                 | #include "vmvnfr_v.h"                                                                               |
| vmv_v_i.h       | // vmv.v.i vd, simm5                                                                                |
|                 | VI_VI_MERGE_LOOP                                                                                    |
|                 | ({                                                                                                  |
|                 | vd = simm5;                                                                                         |
|                 | })                                                                                                  |
| vnclipu_wi.h    | // vnclipu: vd[i] = clip(round(vs2[i] + rnd) >> simm)                                               |
|                 | VI_VI_LOOP_NARROW                                                                                   |
|                 | ({                                                                                                  |
|                 | VRM xrm = P.VU.get_vround_mode();                                                                   |
|                 | uint64_t uint_max = UINT64_MAX >> (64 - P.VU.vsew);                                                 |
|                 | uint64_t sign_mask = UINT64_MAX << P.VU.vsew;                                                       |
|                 | uint128_t result = vs2_u;                                                                           |
|                 | unsigned shift = zimm5 & ((sew * 2) - 1);                                                           |
|                 | // rounding                                                                                         |
|                 | INT_ROUNDING(result, xrm, shift);                                                                   |
|                 | // unsigned shifting to rs1                                                                         |
|                 | result = result >> shift;                                                                           |
|                 | // saturation                                                                                       |
|                 | if (result & sign_mask) {                                                                           |
|                 | result = uint_max;                                                                                  |
|                 | P_SET_OV(1);                                                                                        |
|                 | }                                                                                                   |
|                 | vd = result;                                                                                        |
|                 | })                                                                                                  |
| vnclip_wi.h     | // vnclip: vd[i] = clip(round(vs2[i] + rnd) >> simm)                                                |
|                 | VI_VI_LOOP_NARROW                                                                                   |
|                 | ({                                                                                                  |
|                 | VRM xrm = P.VU.get_vround_mode();                                                                   |
|                 | int64_t int_max = INT64_MAX >> (64 - P.VU.vsew);                                                    |
|                 | int64_t int_min = INT64_MIN >> (64 - P.VU.vsew);                                                    |
|                 | int128_t result = vs2;                                                                              |
|                 | unsigned shift = zimm5 & ((sew * 2) - 1);                                                           |
|                 | // rounding                                                                                         |
|                 | INT_ROUNDING(result, xrm, shift);                                                                   |
|                 | result = result >> shift;                                                                           |
|                 | // saturation                                                                                       |
|                 | if (result < int_min) {                                                                             |
|                 | result = int_min;                                                                                   |
|                 | P_SET_OV(1);                                                                                        |
|                 | } else if (result > int_max) {                                                                      |
|                 | result = int_max;                                                                                   |
|                 | P_SET_OV(1);                                                                                        |
|                 | }                                                                                                   |
|                 | vd = result;                                                                                        |
|                 | })                                                                                                  |
| vnsra_wi.h      | // vnsra.vi vd, vs2, zimm5                                                                          |
|                 | VI_VI_LOOP_NSHIFT                                                                                   |
|                 | ({                                                                                                  |
|                 | vd = vs2 >> (zimm5 & (sew * 2 - 1));                                                                |
|                 | })                                                                                                  |
| vnsrl_wi.h      | // vnsrl.vi vd, vs2, zimm5                                                                          |
|                 | VI_VI_LOOP_NSHIFT                                                                                   |
|                 | ({                                                                                                  |
|                 | vd = vs2_u >> (zimm5 & (sew * 2 - 1));                                                              |
|                 | })                                                                                                  |
| vor_vi.h        | // vor                                                                                              |
|                 | VI_VI_LOOP                                                                                          |
|                 | ({                                                                                                  |
|                 | vd = simm5 or vs2;                                                                                  |
|                 | })                                                                                                  |
| vrgather_vi.h   | // vrgather.vi vd, vs2, zimm5 vm # vd[i] = (zimm5 >= VLMAX) ? 0 : vs2[zimm5];                       |
|                 | require_align(insn.rd(), P.VU.vflmul);                                                              |
|                 | require_align(insn.rs2(), P.VU.vflmul);                                                             |
|                 | require(insn.rd() != insn.rs2());                                                                   |
|                 | require_vm;                                                                                         |
|                 | reg_t zimm5 = insn.v_zimm5();                                                                       |
|                 | VI_LOOP_BASE                                                                                        |
|                 | switch (sew) {                                                                                      |
|                 | case e8:                                                                                            |
|                 | P.VU.elt<uint8_t>(rd_num, i, true) = zimm5 >= P.VU.vlmax ? 0 : P.VU.elt<uint8_t>(rs2_num, zimm5);   |
|                 | break;                                                                                              |
|                 | case e16:                                                                                           |
|                 | P.VU.elt<uint16_t>(rd_num, i, true) = zimm5 >= P.VU.vlmax ? 0 : P.VU.elt<uint16_t>(rs2_num, zimm5); |
|                 | break;                                                                                              |
|                 | case e32:                                                                                           |
|                 | P.VU.elt<uint32_t>(rd_num, i, true) = zimm5 >= P.VU.vlmax ? 0 : P.VU.elt<uint32_t>(rs2_num, zimm5); |
|                 | break;                                                                                              |
|                 | default:                                                                                            |
|                 | P.VU.elt<uint64_t>(rd_num, i, true) = zimm5 >= P.VU.vlmax ? 0 : P.VU.elt<uint64_t>(rs2_num, zimm5); |
|                 | break;                                                                                              |
|                 | }                                                                                                   |
|                 | VI_LOOP_END;                                                                                        |
| vrsub_vi.h      | // vrsub.vi vd, vs2, imm, vm   # vd[i] = imm - vs2[i]                                               |
|                 | VI_VI_LOOP                                                                                          |
|                 | ({                                                                                                  |
|                 | vd = simm5 - vs2;                                                                                   |
|                 | })                                                                                                  |
| vsaddu_vi.h     | // vsaddu vd, vs2, zimm5                                                                            |
|                 | VI_VI_ULOOP                                                                                         |
|                 | ({                                                                                                  |
|                 | bool sat = false;                                                                                   |
|                 | vd = vs2 + (insn.v_simm5() & (UINT64_MAX >> (64 - P.VU.vsew)));                                     |
|                 | sat = vd < vs2;                                                                                     |
|                 | vd ori -(vd < vs2);                                                                                 |
|                 | P_SET_OV(sat);                                                                                      |
|                 | })                                                                                                  |
| vsadd_vi.h      | // vsadd.vi vd, vs2 simm5                                                                           |
|                 | VI_CHECK_SSS(false);                                                                                |
|                 | VI_LOOP_BASE                                                                                        |
|                 | bool sat = false;                                                                                   |
|                 | switch (sew) {                                                                                      |
|                 | case e8: {                                                                                          |
|                 | VI_PARAMS(e8);                                                                                      |
|                 | vd = sat_add<int8_t, uint8_t>(vs2, vsext(simm5, sew), sat);                                         |
|                 | break;                                                                                              |
|                 | }                                                                                                   |
|                 | case e16: {                                                                                         |
|                 | VI_PARAMS(e16);                                                                                     |
|                 | vd = sat_add<int16_t, uint16_t>(vs2, vsext(simm5, sew), sat);                                       |
|                 | break;                                                                                              |
|                 | }                                                                                                   |
|                 | case e32: {                                                                                         |
|                 | VI_PARAMS(e32);                                                                                     |
|                 | vd = sat_add<int32_t, uint32_t>(vs2, vsext(simm5, sew), sat);                                       |
|                 | break;                                                                                              |
|                 | }                                                                                                   |
|                 | default: {                                                                                          |
|                 | VI_PARAMS(e64);                                                                                     |
|                 | vd = sat_add<int64_t, uint64_t>(vs2, vsext(simm5, sew), sat);                                       |
|                 | break;                                                                                              |
|                 | }                                                                                                   |
|                 | }                                                                                                   |
|                 | P_SET_OV(sat);                                                                                      |
|                 | VI_LOOP_END                                                                                         |
| vslidedown_vi.h | // vslidedown.vi vd, vs2, rs1                                                                       |
|                 | VI_CHECK_SLIDE(false);                                                                              |
|                 | const reg_t sh = insn.v_zimm5();                                                                    |
|                 | VI_LOOP_BASE                                                                                        |
|                 | reg_t offset = 0;                                                                                   |
|                 | bool is_valid = (i + sh) < P.VU.vlmax;                                                              |
|                 | if (is_valid) {                                                                                     |
|                 | offset = sh;                                                                                        |
|                 | }                                                                                                   |
|                 | switch (sew) {                                                                                      |
|                 | case e8: {                                                                                          |
|                 | VI_XI_SLIDEDOWN_PARAMS(e8, offset);                                                                 |
|                 | vd = is_valid ? vs2 : 0;                                                                            |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | case e16: {                                                                                         |
|                 | VI_XI_SLIDEDOWN_PARAMS(e16, offset);                                                                |
|                 | vd = is_valid ? vs2 : 0;                                                                            |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | case e32: {                                                                                         |
|                 | VI_XI_SLIDEDOWN_PARAMS(e32, offset);                                                                |
|                 | vd = is_valid ? vs2 : 0;                                                                            |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | default: {                                                                                          |
|                 | VI_XI_SLIDEDOWN_PARAMS(e64, offset);                                                                |
|                 | vd = is_valid ? vs2 : 0;                                                                            |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | }                                                                                                   |
|                 | VI_LOOP_END                                                                                         |
| vslideup_vi.h   | // vslideup.vi vd, vs2, rs1                                                                         |
|                 | VI_CHECK_SLIDE(true);                                                                               |
|                 | const reg_t offset = insn.v_zimm5();                                                                |
|                 | VI_LOOP_BASE                                                                                        |
|                 | if (P.VU.vstart->read() < offset && i < offset)                                                     |
|                 | continue;                                                                                           |
|                 | switch (sew) {                                                                                      |
|                 | case e8: {                                                                                          |
|                 | VI_XI_SLIDEUP_PARAMS(e8, offset);                                                                   |
|                 | vd = vs2;                                                                                           |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | case e16: {                                                                                         |
|                 | VI_XI_SLIDEUP_PARAMS(e16, offset);                                                                  |
|                 | vd = vs2;                                                                                           |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | case e32: {                                                                                         |
|                 | VI_XI_SLIDEUP_PARAMS(e32, offset);                                                                  |
|                 | vd = vs2;                                                                                           |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | default: {                                                                                          |
|                 | VI_XI_SLIDEUP_PARAMS(e64, offset);                                                                  |
|                 | vd = vs2;                                                                                           |
|                 | }                                                                                                   |
|                 | break;                                                                                              |
|                 | }                                                                                                   |
|                 | VI_LOOP_END                                                                                         |
| vsll_vi.h       | // vsll.vi  vd, vs2, zimm5                                                                          |
|                 | VI_VI_ULOOP                                                                                         |
|                 | ({                                                                                                  |
|                 | vd = vs2 << (zimm5 & (sew - 1));                                                                    |
|                 | })                                                                                                  |
| vsra_vi.h       | // vsra.vi vd, vs2, zimm5                                                                           |
|                 | VI_VI_LOOP                                                                                          |
|                 | ({                                                                                                  |
|                 | vd = vs2 >> (insn.v_zimm5() & (sew - 1));                                                           |
|                 | })                                                                                                  |
| vsrl_vi.h       | // vsrl.vi vd, vs2, zimm5                                                                           |
|                 | VI_VI_ULOOP                                                                                         |
|                 | ({                                                                                                  |
|                 | vd = vs2 >> (zimm5 & (sew - 1));                                                                    |
|                 | })                                                                                                  |
| vssra_vi.h      | // vssra.vi vd, vs2, zimm5                                                                          |
|                 | VI_VI_LOOP                                                                                          |
|                 | ({                                                                                                  |
|                 | VRM xrm = P.VU.get_vround_mode();                                                                   |
|                 | int sh = insn.v_zimm5() & (sew - 1);                                                                |
|                 | int128_t val = vs2;                                                                                 |
|                 | INT_ROUNDING(val, xrm, sh);                                                                         |
|                 | vd = val >> sh;                                                                                     |
|                 | })                                                                                                  |
| vssrl_vi.h      | // vssra.vi vd, vs2, zimm5                                                                          |
|                 | VI_VI_ULOOP                                                                                         |
|                 | ({                                                                                                  |
|                 | VRM xrm = P.VU.get_vround_mode();                                                                   |
|                 | int sh = zimm5 & (sew - 1);                                                                         |
|                 | uint128_t val = vs2;                                                                                |
|                 | INT_ROUNDING(val, xrm, sh);                                                                         |
|                 | vd = val >> sh;                                                                                     |
|                 | })                                                                                                  |
| vxor_vi.h       | // vxor                                                                                             |
|                 | VI_VI_LOOP                                                                                          |
|                 | ({                                                                                                  |
|                 | vd = simm5 ^ vs2;                                                                                   |
|                 | })                                                                                                  |
