| instruction  | code                                                                  |
|--------------|-----------------------------------------------------------------------|
| c_add.h      | require_extension(EXT_ZCA);                                           |
|              | WRITE_RD(sext_xlen(RVC_RS1 + RVC_RS2));                               |
| c_addi4spn.h | require_extension(EXT_ZCA);                                           |
|              | require(insn.rvc_addi4spn_imm() != 0);                                |
|              | WRITE_RVC_RS2S(sext_xlen(RVC_SP + insn.rvc_addi4spn_imm()));          |
| c_addi.h     | require_extension(EXT_ZCA);                                           |
|              | WRITE_RD(sext_xlen(RVC_RS1 + insn.rvc_imm()));                        |
| c_addw.h     | require_extension(EXT_ZCA);                                           |
|              | require_rv64;                                                         |
|              | WRITE_RVC_RS1S(sext32(RVC_RS1S + RVC_RS2S));                          |
| c_and.h      | require_extension(EXT_ZCA);                                           |
|              | WRITE_RVC_RS1S(RVC_RS1S & RVC_RS2S);                                  |
| c_andi.h     | require_extension(EXT_ZCA);                                           |
|              | WRITE_RVC_RS1S(RVC_RS1S & insn.rvc_imm());                            |
| c_beqz.h     | require_extension(EXT_ZCA);                                           |
|              | if (RVC_RS1S == 0)                                                    |
|              | set_pc(pc + insn.rvc_b_imm());                                        |
| c_bnez.h     | require_extension(EXT_ZCA);                                           |
|              | if (RVC_RS1S != 0)                                                    |
|              | set_pc(pc + insn.rvc_b_imm());                                        |
| c_ebreak.h   | require_extension(EXT_ZCA);                                           |
|              | if (!STATE.debug_mode && (                                            |
|              | (!STATE.v && STATE.prv == PRV_M && STATE.dcsr->ebreakm) or            |
|              | (!STATE.v && STATE.prv == PRV_S && STATE.dcsr->ebreaks) or            |
|              | (!STATE.v && STATE.prv == PRV_U && STATE.dcsr->ebreaku) or            |
|              | (STATE.v && STATE.prv == PRV_S && STATE.dcsr->ebreakvs) or            |
|              | (STATE.v && STATE.prv == PRV_U && STATE.dcsr->ebreakvu))) {           |
|              | throw trap_debug_mode();                                              |
|              | } else {                                                              |
|              | throw trap_breakpoint(STATE.v, pc);                                   |
|              | }                                                                     |
| c_jal.h      | require_extension(EXT_ZCA);                                           |
|              | if (xlen == 32) {                                                     |
|              | reg_t tmp = npc;                                                      |
|              | set_pc(pc + insn.rvc_j_imm());                                        |
|              | WRITE_REG(X_RA, tmp);                                                 |
|              | } else { // c.addiw                                                   |
|              | require(insn.rvc_rd() != 0);                                          |
|              | WRITE_RD(sext32(RVC_RS1 + insn.rvc_imm()));                           |
|              | }                                                                     |
| c_jalr.h     | require_extension(EXT_ZCA);                                           |
|              | reg_t tmp = npc;                                                      |
|              | set_pc(RVC_RS1 & ~reg_t(1));                                          |
|              | WRITE_REG(X_RA, tmp);                                                 |
|              | maybe_set_elp(insn.rvc_rs1());                                        |
| c_j.h        | require_extension(EXT_ZCA);                                           |
|              | set_pc(pc + insn.rvc_j_imm());                                        |
| c_jr.h       | require_extension(EXT_ZCA);                                           |
|              | require(insn.rvc_rs1() != 0);                                         |
|              | set_pc(RVC_RS1 & ~reg_t(1));                                          |
|              | maybe_set_elp(insn.rvc_rs1());                                        |
| c_ld.h       | require_extension(EXT_ZCA);                                           |
|              | require((xlen == 64) or p->extension_enabled(EXT_ZCLSD));             |
|              | if (xlen == 32) {                                                     |
|              | WRITE_RVC_RS2S_PAIR(MMU.load<int64_t>(RVC_RS1S + insn.rvc_ld_imm())); |
|              | } else {                                                              |
|              | WRITE_RVC_RS2S(MMU.load<int64_t>(RVC_RS1S + insn.rvc_ld_imm()));      |
|              | }                                                                     |
| c_ldsp.h     | require_extension(EXT_ZCA);                                           |
|              | require((xlen == 64) or p->extension_enabled(EXT_ZCLSD));             |
|              | require(insn.rvc_rd() != 0);                                          |
|              | if (xlen == 32) {                                                     |
|              | WRITE_RD_PAIR(MMU.load<int64_t>(RVC_SP + insn.rvc_ldsp_imm()));       |
|              | } else {                                                              |
|              | WRITE_RD(MMU.load<int64_t>(RVC_SP + insn.rvc_ldsp_imm()));            |
|              | }                                                                     |
| c_li.h       | require_extension(EXT_ZCA);                                           |
|              | WRITE_RD(insn.rvc_imm());                                             |
| c_lui.h      | require_extension(EXT_ZCA);                                           |
|              | if (insn.rvc_rd() == 2) { // c.addi16sp                               |
|              | require(insn.rvc_addi16sp_imm() != 0);                                |
|              | WRITE_REG(X_SP, sext_xlen(RVC_SP + insn.rvc_addi16sp_imm()));         |
|              | } else if (insn.rvc_imm() != 0) { // c.lui                            |
|              | WRITE_RD(insn.rvc_imm() << 12);                                       |
|              | } else if ((insn.rvc_rd() & 0x11) == 1) { // c.mop.N                  |
|              | if (insn.rvc_rd() == 5 && p->extension_enabled(EXT_ZICFISS)) {        |
|              | #include "c_sspopchk_x5.h"                                            |
|              | } else if (insn.rvc_rd() == 1 && p->extension_enabled(EXT_ZICFISS)) { |
|              | #include "c_sspush_x1.h"                                              |
|              | } else {                                                              |
|              | #include "c_mop_N.h"                                                  |
|              | }                                                                     |
|              | } else {                                                              |
|              | require(false);                                                       |
|              | }                                                                     |
| c_lw.h       | require_extension(EXT_ZCA);                                           |
|              | WRITE_RVC_RS2S(MMU.load<int32_t>(RVC_RS1S + insn.rvc_lw_imm()));      |
| c_lwsp.h     | require_extension(EXT_ZCA);                                           |
|              | require(insn.rvc_rd() != 0);                                          |
|              | WRITE_RD(MMU.load<int32_t>(RVC_SP + insn.rvc_lwsp_imm()));            |
| c_mv.h       | require_extension(EXT_ZCA);                                           |
|              | WRITE_RD(RVC_RS2);                                                    |
| c_or.h       | require_extension(EXT_ZCA);                                           |
|              | WRITE_RVC_RS1S(RVC_RS1S or RVC_RS2S);                                 |
| c_sd.h       | require_extension(EXT_ZCA);                                           |
|              | require((xlen == 64) or p->extension_enabled(EXT_ZCLSD));             |
|              | if (xlen == 32) {                                                     |
|              | MMU.store<uint64_t>(RVC_RS1S + insn.rvc_ld_imm(), RVC_RS2S_PAIR);     |
|              | } else {                                                              |
|              | MMU.store<uint64_t>(RVC_RS1S + insn.rvc_ld_imm(), RVC_RS2S);          |
|              | }                                                                     |
| c_sdsp.h     | require_extension(EXT_ZCA);                                           |
|              | require((xlen == 64) or p->extension_enabled(EXT_ZCLSD));             |
|              | if (xlen == 32) {                                                     |
|              | MMU.store<uint64_t>(RVC_SP + insn.rvc_sdsp_imm(), RVC_RS2_PAIR);      |
|              | } else {                                                              |
|              | MMU.store<uint64_t>(RVC_SP + insn.rvc_sdsp_imm(), RVC_RS2);           |
|              | }                                                                     |
| c_slli.h     | require_extension(EXT_ZCA);                                           |
|              | require(insn.rvc_zimm() < xlen);                                      |
|              | WRITE_RD(sext_xlen(RVC_RS1 << insn.rvc_zimm()));                      |
| c_srai.h     | require_extension(EXT_ZCA);                                           |
|              | require(insn.rvc_zimm() < xlen);                                      |
|              | WRITE_RVC_RS1S(sext_xlen(sext_xlen(RVC_RS1S) >> insn.rvc_zimm()));    |
| c_srli.h     | require_extension(EXT_ZCA);                                           |
|              | require(insn.rvc_zimm() < xlen);                                      |
|              | WRITE_RVC_RS1S(sext_xlen(zext_xlen(RVC_RS1S) >> insn.rvc_zimm()));    |
| c_sub.h      | require_extension(EXT_ZCA);                                           |
|              | WRITE_RVC_RS1S(sext_xlen(RVC_RS1S - RVC_RS2S));                       |
| c_subw.h     | require_extension(EXT_ZCA);                                           |
|              | require_rv64;                                                         |
|              | WRITE_RVC_RS1S(sext32(RVC_RS1S - RVC_RS2S));                          |
| c_sw.h       | require_extension(EXT_ZCA);                                           |
|              | MMU.store<uint32_t>(RVC_RS1S + insn.rvc_lw_imm(), RVC_RS2S);          |
| c_swsp.h     | require_extension(EXT_ZCA);                                           |
|              | MMU.store<uint32_t>(RVC_SP + insn.rvc_swsp_imm(), RVC_RS2);           |
| c_xor.h      | require_extension(EXT_ZCA);                                           |
|              | WRITE_RVC_RS1S(RVC_RS1S ^ RVC_RS2S);                                  |
