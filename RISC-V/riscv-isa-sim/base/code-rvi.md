| instruction | code                                                        |
|-------------|-------------------------------------------------------------|
| add.h       | WRITE_RD(sext_xlen(RS1 + RS2));                             |
| addi.h      | WRITE_RD(sext_xlen(RS1 + insn.i_imm()));                    |
| addiw.h     | require_rv64;                                               |
|             | WRITE_RD(sext32(insn.i_imm() + RS1));                       |
| addw.h      | require_rv64;                                               |
|             | WRITE_RD(sext32(RS1 + RS2));                                |
| and.h       | WRITE_RD(RS1 & RS2);                                        |
| andi.h      | WRITE_RD(insn.i_imm() & RS1);                               |
| auipc.h     | WRITE_RD(sext_xlen(insn.u_imm() + pc));                     |
| beq.h       | if (RS1 == RS2)                                             |
|             | set_pc(BRANCH_TARGET);                                      |
| bge.h       | if (sreg_t(RS1) >= sreg_t(RS2))                             |
|             | set_pc(BRANCH_TARGET);                                      |
| bgeu.h      | if (RS1 >= RS2)                                             |
|             | set_pc(BRANCH_TARGET);                                      |
| blt.h       | if (sreg_t(RS1) < sreg_t(RS2))                              |
|             | set_pc(BRANCH_TARGET);                                      |
| bltu.h      | if (RS1 < RS2)                                              |
|             | set_pc(BRANCH_TARGET);                                      |
| bne.h       | if (RS1 != RS2)                                             |
|             | set_pc(BRANCH_TARGET);                                      |
| ebreak.h    | if (!STATE.debug_mode && (                                  |
|             | (!STATE.v && STATE.prv == PRV_M && STATE.dcsr->ebreakm) or  |
|             | (!STATE.v && STATE.prv == PRV_S && STATE.dcsr->ebreaks) or  |
|             | (!STATE.v && STATE.prv == PRV_U && STATE.dcsr->ebreaku) or  |
|             | (STATE.v && STATE.prv == PRV_S && STATE.dcsr->ebreakvs) or  |
|             | (STATE.v && STATE.prv == PRV_U && STATE.dcsr->ebreakvu))) { |
|             | throw trap_debug_mode();                                    |
|             | } else {                                                    |
|             | throw trap_breakpoint(STATE.v, pc);                         |
|             | }                                                           |
| ecall.h     | switch (STATE.prv)                                          |
|             | {                                                           |
|             | case PRV_U: throw trap_user_ecall();                        |
|             | case PRV_S:                                                 |
|             | if (STATE.v)                                                |
|             | throw trap_virtual_supervisor_ecall();                      |
|             | else                                                        |
|             | throw trap_supervisor_ecall();                              |
|             | case PRV_M: throw trap_machine_ecall();                     |
|             | default: abort();                                           |
|             | }                                                           |
| fence_i.h   | MMU.flush_icache();                                         |
| jal.h       | CHECK_RD();                                                 |
|             | reg_t tmp = npc;                                            |
|             | set_pc(JUMP_TARGET);                                        |
|             | WRITE_RD(tmp);                                              |
| jalr.h      | CHECK_RD();                                                 |
|             | reg_t tmp = npc;                                            |
|             | set_pc((RS1 + insn.i_imm()) & ~reg_t(1));                   |
|             | WRITE_RD(tmp);                                              |
|             | maybe_set_elp(insn.rs1());                                  |
| lb.h        | WRITE_RD(MMU.load<int8_t>(RS1 + insn.i_imm()));             |
| lbu.h       | WRITE_RD(MMU.load<uint8_t>(RS1 + insn.i_imm()));            |
| ld.h        | require((xlen == 64) or p->extension_enabled(EXT_ZILSD));   |
|             | if (xlen == 32) {                                           |
|             | WRITE_RD_PAIR(MMU.load<int64_t>(RS1 + insn.i_imm()));       |
|             | } else {                                                    |
|             | WRITE_RD(MMU.load<int64_t>(RS1 + insn.i_imm()));            |
|             | }                                                           |
| lh.h        | WRITE_RD(MMU.load<int16_t>(RS1 + insn.i_imm()));            |
| lhu.h       | WRITE_RD(MMU.load<uint16_t>(RS1 + insn.i_imm()));           |
| lui.h       | WRITE_RD(insn.u_imm());                                     |
| lw.h        | WRITE_RD(MMU.load<int32_t>(RS1 + insn.i_imm()));            |
| lwu.h       | require_rv64;                                               |
|             | WRITE_RD(MMU.load<uint32_t>(RS1 + insn.i_imm()));           |
| or.h        | WRITE_RD(RS1 or RS2);                                       |
| ori.h       | // prefetch.i/r/w hint when rd = 0 and i_imm[4:0] = 0/1/3   |
|             | WRITE_RD(insn.i_imm() or RS1);                              |
| sb.h        | MMU.store<uint8_t>(RS1 + insn.s_imm(), RS2);                |
| sd.h        | require((xlen == 64) or p->extension_enabled(EXT_ZILSD));   |
|             | if (xlen == 32) {                                           |
|             | MMU.store<uint64_t>(RS1 + insn.s_imm(), RS2_PAIR);          |
|             | } else {                                                    |
|             | MMU.store<uint64_t>(RS1 + insn.s_imm(), RS2);               |
|             | }                                                           |
| sh.h        | MMU.store<uint16_t>(RS1 + insn.s_imm(), RS2);               |
| sll.h       | WRITE_RD(sext_xlen(RS1 << (RS2 & (xlen-1))));               |
| slli.h      | require(SHAMT < xlen);                                      |
|             | WRITE_RD(sext_xlen(RS1 << SHAMT));                          |
| slliw.h     | require_rv64;                                               |
|             | WRITE_RD(sext32(RS1 << SHAMT));                             |
| sllw.h      | require_rv64;                                               |
|             | WRITE_RD(sext32(RS1 << (RS2 & 0x1F)));                      |
| slt.h       | WRITE_RD(sreg_t(RS1) < sreg_t(RS2));                        |
| slti.h      | WRITE_RD(sreg_t(RS1) < sreg_t(insn.i_imm()));               |
| sltiu.h     | WRITE_RD(RS1 < reg_t(insn.i_imm()));                        |
| sltu.h      | WRITE_RD(RS1 < RS2);                                        |
| sra.h       | WRITE_RD(sext_xlen(sext_xlen(RS1) >> (RS2 & (xlen-1))));    |
| srai.h      | require(SHAMT < xlen);                                      |
|             | WRITE_RD(sext_xlen(sext_xlen(RS1) >> SHAMT));               |
| sraiw.h     | require_rv64;                                               |
|             | WRITE_RD(sext32(int32_t(RS1) >> SHAMT));                    |
| sraw.h      | require_rv64;                                               |
|             | WRITE_RD(sext32(int32_t(RS1) >> (RS2 & 0x1F)));             |
| srl.h       | WRITE_RD(sext_xlen(zext_xlen(RS1) >> (RS2 & (xlen-1))));    |
| srli.h      | require(SHAMT < xlen);                                      |
|             | WRITE_RD(sext_xlen(zext_xlen(RS1) >> SHAMT));               |
| srliw.h     | require_rv64;                                               |
|             | WRITE_RD(sext32((uint32_t)RS1 >> SHAMT));                   |
| srlw.h      | require_rv64;                                               |
|             | WRITE_RD(sext32((uint32_t)RS1 >> (RS2 & 0x1F)));            |
| sub.h       | WRITE_RD(sext_xlen(RS1 - RS2));                             |
| subw.h      | require_rv64;                                               |
|             | WRITE_RD(sext32(RS1 - RS2));                                |
| sw.h        | MMU.store<uint32_t>(RS1 + insn.s_imm(), RS2);               |
| xor.h       | WRITE_RD(RS1 ^ RS2);                                        |
| xori.h      | WRITE_RD(insn.i_imm() ^ RS1);                               |
