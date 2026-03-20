| instruction   | code                                           |
|---------------|------------------------------------------------|
| vaaddu_vv.h   | // vaaddu.vv vd, vs2, vs1                      |
|               | VI_VV_ULOOP_AVG(+);                            |
| vaadd_vv.h    | // vaadd.vv vd, vs2, vs1                       |
|               | VI_VV_LOOP_AVG(+);                             |
| vasubu_vv.h   | // vasubu.vv vd, vs2, vs1                      |
|               | VI_VV_ULOOP_AVG(-);                            |
| vasub_vv.h    | // vasub.vv vd, vs2, vs1                       |
|               | VI_VV_LOOP_AVG(-);                             |
| vmv_x_s.h     | // vmv_x_s: rd = vs2[0]                        |
|               | require_vector(true);                          |
|               | require(insn.v_vm() == 1);                     |
|               | reg_t sew = P.VU.vsew;                         |
|               | reg_t rs2_num = insn.rs2();                    |
|               | reg_t res;                                     |
|               | switch (sew) {                                 |
|               | case e8:                                       |
|               | res = P.VU.elt<int8_t>(rs2_num, 0);            |
|               | break;                                         |
|               | case e16:                                      |
|               | res = P.VU.elt<int16_t>(rs2_num, 0);           |
|               | break;                                         |
|               | case e32:                                      |
|               | res = P.VU.elt<int32_t>(rs2_num, 0);           |
|               | break;                                         |
|               | case e64:                                      |
|               | res = P.VU.elt<uint64_t>(rs2_num, 0);          |
|               | break;                                         |
|               | default:                                       |
|               | abort();                                       |
|               | }                                              |
|               | WRITE_RD(sext_xlen(res));                      |
|               | P.VU.vstart->write(0);                         |
| vredand_vs.h  | // vredand.vs vd, vs2, vs1                     |
|               | VI_VV_LOOP_REDUCTION                           |
|               | ({                                             |
|               | vd_0_res &= vs2;                               |
|               | })                                             |
| vredmaxu_vs.h | // vredmaxu.vs vd, vs2, vs1                    |
|               | VI_VV_ULOOP_REDUCTION                          |
|               | ({                                             |
|               | vd_0_res = (vd_0_res >= vs2) ? vd_0_res : vs2; |
|               | })                                             |
| vredmax_vs.h  | // vredmax.vs vd, vs2 ,vs1                     |
|               | VI_VV_LOOP_REDUCTION                           |
|               | ({                                             |
|               | vd_0_res = (vd_0_res >= vs2) ? vd_0_res : vs2; |
|               | })                                             |
| vredminu_vs.h | // vredminu.vs vd, vs2, vs1                    |
|               | VI_VV_ULOOP_REDUCTION                          |
|               | ({                                             |
|               | vd_0_res = (vd_0_res <= vs2) ? vd_0_res : vs2; |
|               | })                                             |
| vredmin_vs.h  | // vredmin.vs vd, vs2, vs1                     |
|               | VI_VV_LOOP_REDUCTION                           |
|               | ({                                             |
|               | vd_0_res = (vd_0_res <= vs2) ? vd_0_res : vs2; |
|               | })                                             |
| vredor_vs.h   | // vredor.vs vd, vs2, vs1                      |
|               | VI_VV_LOOP_REDUCTION                           |
|               | ({                                             |
|               | vd_0_res ori vs2;                              |
|               | })                                             |
| vredsum_vs.h  | // vredsum.vs vd, vs2, vs1                     |
|               | VI_VV_LOOP_REDUCTION                           |
|               | ({                                             |
|               | vd_0_res += vs2;                               |
|               | })                                             |
| vredxor_vs.h  | // vredxor.vs vd, vs2, vs1                     |
|               | VI_VV_LOOP_REDUCTION                           |
|               | ({                                             |
|               | vd_0_res ^= vs2;                               |
|               | })                                             |
