Creating Custom Windows ISO
Windows AIK
https://go.microsoft.com/fwlink/?linkid=2162950

VirtIO Drivers from Fedora
https://github.com/virtio-win/virtio-win-pkg-scripts/blob/master/README.md
Windows 20XX ISO
https://portal.azure.com/education

How to inject drivers
http://woshub.com/integrate-drivers-to-windows-install-media/

Create 3 Folders
 ./ISO ./Drivers ./Mount

Extract image from ISO (sources/install.wim

List Images in wim file
 get-WindowsImage -ImagePath .\install.wim

Mount Image to mount directory
 Mount-WindowsImage -Path .\mount\ -ImagePath D:\sources\install.wim
 
Adding Drivers to Image
 Add-WindowsDriver -Path .\mount\ -Driver .\drivers\ -Recurse -Verbose
 
Save image
 Dismount-WindowsImage -Path .\mount\ –Save
 
 Make New ISOs
 oscdimg -n -d -m -bC:\Users\User\Documents\WinWork\iso\boot\etfsboot.com C:\Users\User\Documents\WinWork\iso C:\Users\User\Documents\WinWork\custom-w2kss.iso
 
 etfsboot.com