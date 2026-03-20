| instruction  | code                                    |
|--------------|-----------------------------------------|
| vl1re16_v.h  | // vl1re16.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint16);                    |
| vl1re32_v.h  | // vl1re32.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint32);                    |
| vl1re64_v.h  | // vl1re64.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint64);                    |
| vl1re8_v.h   | // vl1re8.v vd, (rs1)                   |
|              | VI_LD_WHOLE(uint8);                     |
| vl2re16_v.h  | // vl2e16.v vd, (rs1)                   |
|              | VI_LD_WHOLE(uint16);                    |
| vl2re32_v.h  | // vl2re32.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint32);                    |
| vl2re64_v.h  | // vl2re64.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint64);                    |
| vl2re8_v.h   | // vl2re8.v vd, (rs1)                   |
|              | VI_LD_WHOLE(uint8);                     |
| vl4re16_v.h  | // vl4re16.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint16);                    |
| vl4re32_v.h  | // vl4re32.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint32);                    |
| vl4re64_v.h  | // vl4re64.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint64);                    |
| vl4re8_v.h   | // vl4re8.v vd, (rs1)                   |
|              | VI_LD_WHOLE(uint8);                     |
| vl8re16_v.h  | // vl8re16.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint16);                    |
| vl8re32_v.h  | // vl8re32.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint32);                    |
| vl8re64_v.h  | // vl8re64.v vd, (rs1)                  |
|              | VI_LD_WHOLE(uint64);                    |
| vl8re8_v.h   | // vl8re8.v vd, (rs1)                   |
|              | VI_LD_WHOLE(uint8);                     |
| vle16ff_v.h  | // vle16ff.v and vlseg[2-8]e16ff.v      |
|              | VI_LDST_FF(int16);                      |
| vle16_v.h    | // vle16.v and vlseg[2-8]e16.v          |
|              | VI_LD(0, (i * nf + fn), int16, false);  |
| vle32ff_v.h  | // vle32ff.v and vlseg[2-8]e32ff.v      |
|              | VI_LDST_FF(int32);                      |
| vle32_v.h    | // vle32.v and vlseg[2-8]e32.v          |
|              | VI_LD(0, (i * nf + fn), int32, false);  |
| vle64ff_v.h  | // vle64ff.v and vlseg[2-8]e64ff.v      |
|              | VI_LDST_FF(int64);                      |
| vle64_v.h    | // vle64.v and vlseg[2-8]e64.v          |
|              | VI_LD(0, (i * nf + fn), int64, false);  |
| vle8ff_v.h   | // vle8ff.v and vlseg[2-8]e8ff.v        |
|              | VI_LDST_FF(int8);                       |
| vle8_v.h     | // vle8.v and vlseg[2-8]e8.v            |
|              | VI_LD(0, (i * nf + fn), int8, false);   |
| vlm_v.h      | // vle1.v and vlseg[2-8]e8.v            |
|              | VI_LD(0, (i * nf + fn), int8, true);    |
| vloxei16_v.h | // vlxei16.v and vlxseg[2-8]e16.v       |
|              | VI_LD_INDEX(e16, true);                 |
| vloxei32_v.h | // vlxe32.v and vlxseg[2-8]ei32.v       |
|              | VI_LD_INDEX(e32, true);                 |
| vloxei64_v.h | // vlxei64.v and vlxseg[2-8]ei64.v      |
|              | VI_LD_INDEX(e64, true);                 |
| vloxei8_v.h  | // vlxei8.v and vlxseg[2-8]ei8.v        |
|              | VI_LD_INDEX(e8, true);                  |
| vlse16_v.h   | // vlse16.v and vlsseg[2-8]e16.v        |
|              | VI_LD(i * RS2, fn, int16, false);       |
| vlse32_v.h   | // vlse32.v and vlsseg[2-8]e32.v        |
|              | VI_LD(i * RS2, fn, int32, false);       |
| vlse64_v.h   | // vlse64.v and vlsseg[2-8]e64.v        |
|              | VI_LD(i * RS2, fn, int64, false);       |
| vlse8_v.h    | // vlse8.v and vlsseg[2-8]e8.v          |
|              | VI_LD(i * RS2, fn, int8, false);        |
| vluxei16_v.h | // vlxei16.v and vlxseg[2-8]e16.v       |
|              | VI_LD_INDEX(e16, true);                 |
| vluxei32_v.h | // vlxe32.v and vlxseg[2-8]ei32.v       |
|              | VI_LD_INDEX(e32, true);                 |
| vluxei64_v.h | // vlxei64.v and vlxseg[2-8]ei64.v      |
|              | VI_LD_INDEX(e64, true);                 |
| vluxei8_v.h  | // vlxei8.v and vlxseg[2-8]ei8.v        |
|              | VI_LD_INDEX(e8, true);                  |
| vs1r_v.h     | // vs1r.v vs3, (rs1)                    |
|              | VI_ST_WHOLE                             |
| vs2r_v.h     | // vs2r.v vs3, (rs1)                    |
|              | VI_ST_WHOLE                             |
| vs4r_v.h     | // vs4r.v vs3, (rs1)                    |
|              | VI_ST_WHOLE                             |
| vs8r_v.h     | // vs8r.v vs3, (rs1)                    |
|              | VI_ST_WHOLE                             |
| vse16_v.h    | // vse16.v and vsseg[2-8]e16.v          |
|              | VI_ST(0, (i * nf + fn), uint16, false); |
| vse32_v.h    | // vse32.v and vsseg[2-8]e32.v          |
|              | VI_ST(0, (i * nf + fn), uint32, false); |
| vse64_v.h    | // vse64.v and vsseg[2-8]e64.v          |
|              | VI_ST(0, (i * nf + fn), uint64, false); |
| vse8_v.h     | // vse8.v and vsseg[2-8]e8.v            |
|              | VI_ST(0, (i * nf + fn), uint8, false);  |
| vsm_v.h      | // vse1.v                               |
|              | VI_ST(0, (i * nf + fn), uint8, true);   |
| vsoxei16_v.h | // vsxei16.v and vsxseg[2-8]ei16.v      |
|              | VI_ST_INDEX(e16, true);                 |
| vsoxei32_v.h | // vsxei32.v and vsxseg[2-8]ei32.v      |
|              | VI_ST_INDEX(e32, true);                 |
| vsoxei64_v.h | // vsxei64.v and vsxseg[2-8]ei64.v      |
|              | VI_ST_INDEX(e64, true);                 |
| vsoxei8_v.h  | // vsxei8.v and vsxseg[2-8]ei8.v        |
|              | VI_ST_INDEX(e8, true);                  |
| vsse16_v.h   | // vsse16v and vssseg[2-8]e16.v         |
|              | VI_ST(i * RS2, fn, uint16, false);      |
| vsse32_v.h   | // vsse32.v and vssseg[2-8]e32.v        |
|              | VI_ST(i * RS2, fn, uint32, false);      |
| vsse64_v.h   | // vsse64.v and vssseg[2-8]e64.v        |
|              | VI_ST(i * RS2, fn, uint64, false);      |
| vsse8_v.h    | // vsse8.v and vssseg[2-8]e8.v          |
|              | VI_ST(i * RS2, fn, uint8, false);       |
| vsuxei16_v.h | // vsuxe16.v                            |
|              | VI_ST_INDEX(e16, true);                 |
| vsuxei32_v.h | // vsuxe32.v                            |
|              | VI_ST_INDEX(e32, true);                 |
| vsuxei64_v.h | // vsuxe64.v                            |
|              | VI_ST_INDEX(e64, true);                 |
| vsuxei8_v.h  | // vsuxe8.v                             |
|              | VI_ST_INDEX(e8, true);                  |
