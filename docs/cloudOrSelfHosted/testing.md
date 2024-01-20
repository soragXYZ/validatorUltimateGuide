This page is under construction

- general: sudo apt install dmidecode
- testing disk speed: sudo apt install fio
- testing CPU: sudo apt install sysbench
- network speed: sudo apt install speedtest
- ram: info: sudo lshw -short -C memory
- ram: test: sysbench memory --memory-block-size=1G --memory-total-size=20G --memory-oper=write run