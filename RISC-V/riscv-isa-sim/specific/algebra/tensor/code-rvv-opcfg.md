| instruction | code                                                                |
|-------------|---------------------------------------------------------------------|
| vsetivli.h  | require_vector_novtype(false);                                      |
|             | WRITE_RD(P.VU.set_vl(insn.rd(), -1, insn.rs1(), insn.v_zimm10()));  |
| vsetvl.h    | require_vector_novtype(false);                                      |
|             | WRITE_RD(P.VU.set_vl(insn.rd(), insn.rs1(), RS1, RS2));             |
| vsetvli.h   | require_vector_novtype(false);                                      |
|             | WRITE_RD(P.VU.set_vl(insn.rd(), insn.rs1(), RS1, insn.v_zimm11())); |
