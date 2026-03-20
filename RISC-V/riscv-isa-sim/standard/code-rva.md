| instruction | code                                                                                                  |
|-------------|-------------------------------------------------------------------------------------------------------|
| amoadd_d.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](uint64_t lhs) { return lhs + RS2; }));                            |
| amoadd_w.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](uint32_t lhs) { return lhs + RS2; })));                    |
| amoand_d.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](uint64_t lhs) { return lhs & RS2; }));                            |
| amoand_w.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](uint32_t lhs) { return lhs & RS2; })));                    |
| amomax_d.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](int64_t lhs) { return std::max(lhs, int64_t(RS2)); }));           |
| amomaxu_d.h | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](uint64_t lhs) { return std::max(lhs, RS2); }));                   |
| amomaxu_w.h | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](uint32_t lhs) { return std::max(lhs, uint32_t(RS2)); }))); |
| amomax_w.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](int32_t lhs) { return std::max(lhs, int32_t(RS2)); })));   |
| amomin_d.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](int64_t lhs) { return std::min(lhs, int64_t(RS2)); }));           |
| amominu_d.h | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](uint64_t lhs) { return std::min(lhs, RS2); }));                   |
| amominu_w.h | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](uint32_t lhs) { return std::min(lhs, uint32_t(RS2)); }))); |
| amomin_w.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](int32_t lhs) { return std::min(lhs, int32_t(RS2)); })));   |
| amoor_d.h   | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](uint64_t lhs) { return lhs or RS2; }));                           |
| amoor_w.h   | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](uint32_t lhs) { return lhs or RS2; })));                   |
| amoswap_d.h | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](uint64_t UNUSED lhs) { return RS2; }));                           |
| amoswap_w.h | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](uint32_t UNUSED lhs) { return RS2; })));                   |
| amoxor_d.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.amo<uint64_t>(RS1, [&](uint64_t lhs) { return lhs ^ RS2; }));                            |
| amoxor_w.h  | require_extension(EXT_ZAAMO);                                                                         |
|             | WRITE_RD(sext32(MMU.amo<uint32_t>(RS1, [&](uint32_t lhs) { return lhs ^ RS2; })));                    |
| lr_d.h      | require_extension(EXT_ZALRSC);                                                                        |
|             | require_rv64;                                                                                         |
|             | WRITE_RD(MMU.load_reserved<int64_t>(RS1));                                                            |
| lr_w.h      | require_extension(EXT_ZALRSC);                                                                        |
|             | WRITE_RD(MMU.load_reserved<int32_t>(RS1));                                                            |
| sc_d.h      | require_extension(EXT_ZALRSC);                                                                        |
|             | require_rv64;                                                                                         |
|             | bool have_reservation = MMU.store_conditional<uint64_t>(RS1, RS2);                                    |
|             | WRITE_RD(!have_reservation);                                                                          |
| sc_w.h      | require_extension(EXT_ZALRSC);                                                                        |
|             | bool have_reservation = MMU.store_conditional<uint32_t>(RS1, RS2);                                    |
|             | WRITE_RD(!have_reservation);                                                                          |
