cmrctl show 상황
```bash
=====================================================================
  CLUSTER     TYPE        NAME       STATUS           DETAIL         
----------- -------- -------------- -------- ------------------------
     COMMON  network         inter2       UP (private) 10.10.10.1/11019
     COMMON  network           pub1       UP (public) enp0s8
     COMMON  cluster            cls     DOWN inc: inter2, pub: pub1
        cls  service         tibero     DOWN Database, Active Cluster (auto-restart: OFF)
=====================================================================

```

```bash
[root@localhost.localdomain:/home/node1/tibero6]$ cmrctl del service --name tibero
CM: SIGSEGV caught...  making callstack
*** 2023/10/04 14:35:56.611 ***
*call stack tbcm       -CM_SID cm1[2331]
    [00] 0x0000000000406b20:0x00007f035d056ef0 = sig_segv_term + 0x0040
    [01] 0x00007f035dc37630:0x00007f035d057030 = __restore_rt + 0x0000
    [02] 0x0000000000457cfb:0x00007f035d057b80 = cm_conn_process_msg + 0x013b
    [03] 0x00000000004497ce:0x00007f035d057c20 = cm_ui_loop.constprop.13 + 0x014e
    [04] 0x000000000040cbb7:0x00007f035d057d90 = cm_thr_main + 0x04e7
    [05] 0x00007f035dc2fea5:0x00007f035d057ed0 = start_thread + 0x00c5

```
해결책 서비스를 밀고 다시 해보거나 바이너리 수정..? 확실치 않음
ㅊ