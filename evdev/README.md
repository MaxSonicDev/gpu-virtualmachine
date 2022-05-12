# Setup evdev passthrough 

The eassiest solution to passthrough input in virtual machine is evdev passthrough. This solution passthrough input from mouse and keyboard on virtual machine. This is solution allow to use one combo mouse/keyboard for guest and host.

In first time, get a system path of your mouse and keyboard

```
l /dev/input/by-id
# or
ls /dev/input/by-id

```
Result :

```
╭─      ~ ············· ✔  maxence@Sumire  10:55:07    
╰─ l /dev/input/by-id
total 0
drwxr-xr-x. 2 root root 220  5 mai   21:39 .
drwxr-xr-x. 4 root root 580  5 mai   21:39 ..
lrwxrwxrwx. 1 root root  10  4 mai   13:10 usb-046d_Logitech_Webcam_C925e_F12B43DF-event-if00 -> ../event15
lrwxrwxrwx. 1 root root   9  4 mai   13:10 usb-Burr-Brown_from_TI_USB_Audio_CODEC-event-if03 -> ../event2
lrwxrwxrwx. 1 root root  10  4 mai   13:10 usb-Logitech_USB_Receiver-if02-event-mouse -> ../event14
lrwxrwxrwx. 1 root root   9  4 mai   13:10 usb-Logitech_USB_Receiver-if02-mouse -> ../mouse1
lrwxrwxrwx. 1 root root   9  4 mai   16:55 usb-©Microsoft_Corporation_Controller_0DB4C61-event-joystick -> ../event4
lrwxrwxrwx. 1 root root   6  4 mai   16:55 usb-©Microsoft_Corporation_Controller_0DB4C61-joystick -> ../js0
lrwxrwxrwx. 1 root root   9  5 mai   21:39 usb-SONiX_Calibur_V2_TE-event-kbd -> ../event3
lrwxrwxrwx. 1 root root   9  5 mai   21:39 usb-SONiX_Calibur_V2_TE-if01-event-mouse -> ../event5
lrwxrwxrwx. 1 root root   9  5 mai   21:39 usb-SONiX_Calibur_V2_TE-if01-mouse -> ../mouse0
╭─      ~ ············· ✔  maxence@Sumire  10:55:09    
╰─ 

```

In this case, i get Logitech USB Receiver Event mouse for my wireless mouse and SONiX Calibur V2 TE event kbd for my keyboard.

```
/dev/input/by-id/usb-Logitech_USB_Receiver-if02-event-mouse # Mouse
/dev/input/by-id/usb-SONiX_Calibur_V2_TE-event-kbd # Keyboard
```

This line need to added on libvirt configuration.

```
virsh edit <Your virtual machine> 
```

change the first line on configuration
```
<domain type='kvm' id='1' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>
```

and add before `</domain>` and remplace path with your mouse and keyboard

```
<qemu:commandline>
    <qemu:arg value='-object'/>
    <qemu:arg value='input-linux,id=mouse1,evdev=/dev/input/by-id/usb-Logitech_USB_Receiver-if02-event-mouse'/> # Mouse
    <qemu:arg value='-object'/>
    <qemu:arg value='input-linux,id=kbd1,evdev=/dev/input/by-id/usb-SONiX_Calibur_V2_TE-event-kbd,grab_all=on,repeat=on'/> # Keyboard
</qemu:commandline>
```
### Permission

with this configuration your are a highest chance to get a error with permission.
In first time, create dedicated user for qemu. 
```
useradd -s /usr/sbin/nologin -r -M -d /dev/null evdev
groupadd evdev
usermod -a -G input evdev
```

you need to edit `/etc/libvirt/qemu.conf` to set a dedicate user for launching virtual machine with evdev configuration. 
make a acl group on the begining of file:
```
cgroup_device_acl = [
        "/dev/null", "/dev/full", "/dev/zero", 
        "/dev/random", "/dev/urandom",
        "/dev/ptmx", "/dev/kvm", "/dev/kqemu",
        "/dev/rtc","/dev/hpet",
        "/dev/input/by-id/<Keybaord>",
        "/dev/input/by-id/<Mouse>"
]

```
replace <Keyboard> and <Mouse> with your Mouse/Keyboard path
after this put user/group Option 

```
user = "evdev"
group = "evdev"
```
If you use a SELinux distro based like Fedora or RHEL, SELinux denied evdev usage by default.
The rule to disable this :
```
'WIP'
```

