# bbrplus
Linux bbrplus kernel 4.14 self-compiled version  
with nvme_core.io_timeout patch (otherwise will got extreme long boot time on some VMs, like AWS EC2 5th-Gen)

<br/>
<br/>
<br/>

***based on original version***  
https://github.com/cx9208/bbrplus

<br/>
<br/>
<br/>

## patch & build bbrplus kernel youself

<br/>
<br/>

### 1) get convert patch on this repository, use git or direct download
        (e.g., convert_official_linux-4.14.169+_src_to_bbrplus.patch)

<br/>
<br/>

### 2) download officaial linux kernel
        say 4.14.199        
            wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.14.199.tar.gz

<br/>
<br/>

### 3) extract the tarball & cd extracted directory
        tar zxvf linux-4.14.199.tar.gz && cd linux-4.14.199

<br/>
<br/>

### 4) copy convert patch to extracted kernel directory
        something like
            cp ../convert_official_linux-4.14.169+_src_to_bbrplus.patch .

<br/>
<br/>

### 5) do the patch job
        patch -p1 < convert_official_linux-4.14.169+_src_to_bbrplus.patch

<br/>
<br/>

(if no error or failed on previous step)
### 6) install dependencies for building kernels

<br/>

***CentOS***  
sudo yum groupinstall Development tools  
sudo yum install ncurses-devel bc gcc gcc-c++ ncurses ncurses-devel cmake elfutils-libelf-devel openssl-devel rpm-build redhat-rpm-config asciidoc hmaccalc perl-ExtUtils-Embed xmlto audit-libs-devel binutils-devel elfutils-devel elfutils-libelf-devel newt-devel python-devel zlib-devel

<br/>

press "y" key when asked

<br/>

***Debian/Ubuntu***  
sudo apt install build-essential libncurses5-dev  
sudo apt build-dep linux

<br/>

press "y" key when asked

<br/>
<br/>

### 7) config build parameters based on you current kernel settings
        make oldconfig

<br/>

press Enter key when asked (if you dont know what is what)


<br/>
<br/>

### 8) disable debug info & module signing
        scripts/config --disable DEBUG_INFO && scripts/config --disable MODULE_SIG


<br/>
<br/>

### 9) build your kernel

<br/>

***CentOS***   
make rpm-pkg LOCALVERSION=-bbrplus 2>&1 | tee build.log

<br/>

***Debian/Ubuntu***  
make deb-pkg LOCALVERSION=-bbrplus 2>&1 | tee build.log

<br/>

if anything goes wrong check the "build.log" file

<br/>
<br/>

(if not failed on previous step)
### 10) collect you kernel package files, do test on some other linux box

<br/>

***CentOS files***   
located in  
/"user home dir"/rpmbuild/RPMS/x86_64/

<br/>

***Debian/Ubuntu files***  
located in  
parent directory  
