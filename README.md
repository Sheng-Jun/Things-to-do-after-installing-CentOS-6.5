# Things to do after installing CentOS 6.5

1. 將自己帳號加入sudoer名單   

<pre><code>su root #(獲得root權限)   
chmod +w /etc/sudoers   
vi /etc/sudoers   </code></pre>
加入 <code>帳號名 ALL=(ALL) ALL</code> 後退出vi
<pre><code>chmod -w /etc/sudoers   
exit #(退出root權限)   </code></pre>

2. 自動上網

<pre><code>sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0   </code></pre>
更改 <code>ONBOOT=no</code> 為 <code>ONBOOT=yes</code>   

3. 匯入數位簽章

<pre><code>sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6   </code></pre>

4. 新增EPEL到軟體倉庫/匯入數位簽章

<pre><code>wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm   
sudo rpm -Uvh epel-release-6*.rpm   
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6   </code></pre>

5. 新增Remi到軟體倉庫/匯入數位簽章   

<pre><code>wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm 
sudo rpm -Uvh remi-release-6*.rpm
sudo vi /etc/yum.repos.d/remi.repo</code></pre>

更改 <code>enabled=0</code> 為 <code>enabled=1</code>   

<pre><code>sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-remi</code></pre>

6. 更新系統   

<pre><code>sudo yum update</code></pre>

7. Guest Additions   

裝置>插入GuestAdditionsCD映像
完成後, 共享資料將出現在 /media 下
<pre><code>sudo vi /etc/group</code></pre>
在 <code>vboxsf:x:492:</code> 後新增自己帳號
接著建立一個simbolic link連到共享資料夾
<pre><code>ln -s /media/共享資料夾 [任選的地方]</code></pre>

8. 安裝文泉驛微米黑字型>設為終端機, 瀏覽器字體   

<pre><code>sudo yum install wqy-mircohei-fonts</code></pre>

9. 安裝Adobe Reader   

<pre><code>wget http://ardownload.adobe.com/pub/adobe/reader/unix/9.x/9.5.5/enu/AdbeRdr9.5.5-1_i486linux_enu.rpm
sudo yum install nspluginwrapper.i686 libcanberra-gtk2.i686 gtk2-engines.i686 PackageKit-gtk-module.i686
sudo yum localinstall AdbeRdr9.5.5-1_i486linux_enu.rpm</code></pre>

10. 安裝Dejavu Viewer   

<pre><code>sudo yum install djview4</code></pre>

11. 安裝壓縮格式   

<pre><code>sudo yum install unrar p7zip p7zip-plugins</code></pre>

12. 調整檔案管理   

系統>偏好設定>檔案管理>運作方式:總是以瀏覽視窗開啟

# Install minimal desktop on CentOS 6.3

ref: https://unix.stackexchange.com/questions/61892/install-minimal-desktop-on-centos-6-3

1. <code># yum groupinstall basic-desktop desktop-platform x11 fonts</code>

2. <code># vi /etc/inittab</code>

Then change <code>id:3:initdefault:</code> to <code>id:5:initdefault:</code>

3. <code># reboot</code>

# Install minimal desktop on CentOS 7

ref1: https://www.centos.org/forums/viewtopic.php?t=47088

ref2: https://dokuwiki.tachtler.net/doku.php?id=tachtler:centos_7_-_minimal_desktop_installation

1. <code># yum groupinstall "X Window System"</code>

2. <code># yum install gnome-classic-session gnome-terminal nautilus-open-terminal control-center liberation-mono-fonts</code>

3. <code># unlink /etc/systemd/system/default.target</code>

4. <code># ln -sf /lib/systemd/system/graphical.target /etc/systemd/system/default.target</code>

5. <code># reboot</code>

# Config ssh to local VM Centos

ref1: https://luppeng.wordpress.com/2017/07/17/enabling-virtualbox-host-only-adapter-on-mac-os-x/

ref2: http://slopjong.de/2013/05/14/virtualbox-make-your-virtual-machine-accessible-from-your-host-system-but-not-from-the-local-network/

1. Create a new virtual network interface (VirtualBox 5.2.X)

    Launch VirtualBox and click on “File > Host Network Manager” on the Menu Bar (Or press “Command” + “W” )
    
    Click on the “Create” button in the Host Network Manager window
    
    This will create a host-only network called “vboxnet0”
    
    Select if you want this Host-only network to have DHCP Server enabled
    
    Close the Host Network Manager Window
    
2. Change the adapter type of your virtual machine

    Settings.> Enable an adapter (Host-only Adapter) and attach it to vboxnet0.
    


