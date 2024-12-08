# I. system info
  ubuntu24 RTX4060Ti16G

# II. install issue
  1. numpy version mismatch
    conda create -n kscale-sim-library python=3.8.19
    conda activate kscale-sim-library
    make install


    conda create -n kscale-sim-library-dev python=3.8.19
    conda activate kscale-sim-library-dev
    make install-dev

  2. ImportError: libpython3.8.so.1.0: cannot open shared object file: No such file or directory

    find / -name libpython3.8.so.1.0
    export LD_LIBRARY_PATH=~/anaconda3/envs/kscale-sim-library/lib:$LD_LIBRARY_PATH
    conda env config vars set LD_LIBRARY_PATH=~/anaconda3/envs/kscale-sim-library/lib:$LD_LIBRARY_PATH

  3. MESA-INTEL: warning: cannot initialize blitter engine

    sudo dmesg | grep nvidia
      i915 ***error***

    disable i915(intel GPU driver)
    operation: 
      sudo vim /etc/default/grub
      GRUB_CMDLINE_LINUX_DEFAULT="quiet splash i915.modeset=0"
      sudo update-grub
      sudo reboot
      lsmod | grep i915 (Used by 0 process) (sudo dmesg | grep "Command line")
  4. 多次pull别人的代码出现未跟踪未移除文件及文件夹

    git clean -fd -x
    其中，-x 选项会清除.gitignore忽略的文件，而-f强制执行清理，-d则允许删除未跟踪的目录。
