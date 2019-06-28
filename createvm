REM @echo off	
REM =============================================================
REM === Create a VM and start OS installation
REM =============================================================

SET vmname=winsvr2016
SET vboxmanagecmd="C:\Program Files\Oracle\VirtualBox\vboxmanage.exe"
SET bridgeNetAdapter="Killer E2400 Gigabit Ethernet Controller"
SET unamepasswd=--username administrator --password password
SET vmdir=d:\virtual-machines
SET isodir=d:\iso-images

ECHO Create the VM...
%vboxmanagecmd% createvm --name %vmname% --ostype Windows2016_64 --register
%vboxmanagecmd% modifyvm %vmname% --memory 2048
%vboxmanagecmd% createhd --filename %vmdir%\%vmname%\%vmname%.vmdk --size 20000 --format VMDK
%vboxmanagecmd% storagectl %vmname% --name "SATA Controller" --add sata --controller IntelAhci
%vboxmanagecmd% storageattach %vmname% --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium %vmdir%\%vmname%\%vmname%.vmdk
%vboxmanagecmd% storagectl %vmname% --name "IDE Controller" --add ide --controller PIIX4
%vboxmanagecmd% storageattach %vmname% --storagectl "IDE Controller" --port 1 --device 0 --type dvddrive --medium %isodir%\Windows_Server_2016_Datacenter_EVAL_en-us_14393_refresh.iso
%vboxmanagecmd% modifyvm %vmname% --nic1 bridged --bridgeadapter1 %bridgeNetAdapter%
REM %vboxmanagecmd% sharedfolder add %vmname% -name "installpackages" -hostpath "d:\install-packages"
%vboxmanagecmd% startvm %vmname%
