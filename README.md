# IJK
#!/bin/sh # onex v0.1  logo="\033[01;33m   ___  _ __   ___\033[01;31m__  __ \033[01;33m / _ \\| '_ \\ / _ \033[01;31m\\ \\/ / \033[01;33m|
#!/bin/sh
# onex v0.1

logo="\033[01;33m
  ___  _ __   ___\033[01;31m__  __
\033[01;33m / _ \\| '_ \\ / _ \033[01;31m\\ \\/ /
\033[01;33m| (_) | | | |  __/\033[01;31m>  < 
\033[01;33m \___/|_| |_|\\___\033[01;31m/_/\_\\
"

# checking for system home dir
if [ -d $HOME ]; then
  home=$HOME
else
  home="~/"
fi

# checking for system bin dir
if [ -d /data/data/com.termux/files/usr/bin ]; then
  bin="/data/data/com.termux/files/usr/bin"
elif [ -d /usr/bin ]; then
  bin="/usr/bin"
elif [ -d /bin ]; then
  bin="/bin"
elif [ -d /usr/sbin ]; then
  bin="/usr/sbin"
elif [ -d /sbin ]; then
  bin="/sbin"
fi

# checking for configuration dir
if [ -d /data/data/com.termux/files/usr/etc ]; then
  conf_dir="/data/data/com.termux/files/usr/etc"
elif [ -d /usr/etc ]; then
  conf_dir="/usr/etc"
elif [ -d /etc ]; then
  conf_dir="/etc"
fi

# configuration files
if [ -d $conf_dir/onex ]; then
  if [ -e $conf_dir/onex/data/tools.dat ]; then
    tools_data="$conf_dir/onex/data/tools.dat"
  fi
  if [ -e $conf_dir/onex/data/category.dat ]; then
    category_data="$conf_dir/onex/data/category.dat"
  fi
else
  if [ -e data/tools.dat ]; then
    tools_data="data/tools.dat"
  fi
  if [ -e data/category.dat ]; then
    category_data="data/category.dat"
  fi
fi

# checking for system root access
if [ -e /usr/lib/sudo ]; then
  sudo="sudo"
elif [ -e /usr/bin/sudo ]; then
  sudo="sudo"
elif [ -e /usr/sbin/sudo ]; then
  sudo="sudo"
elif [ -e /lib/sudo ]; then
  sudo="sudo"
elif [ -e /bin/sudo ]; then
  sudo="sudo"
elif [ -e /sbin/sudo ]; then
  sudo="sudo"
elif [ -e /data/data/com.termux/files/usr/bin/sudo ]; then
  sudo="sudo"
else
  sudo=""
fi

# checking for system package manager
if [ -e /bin/apt ]; then
  pac="apt-get"
  system="linux"
elif [ -e /bin/apt-get ]; then
  pac="apt-get"
  system="linux"
elif [ -e /usr/bin/apt-get ]; then
  pac="apt-get"
  system="linux"
elif [ -e /sbin/apt-get ]; then
  pac="apt-get"
  system="linux"
elif [ -e /usr/sbin/apt-get ]; then
  pac="apt-get"
  system="linux"
elif [ -e /bin/apk ]; then
  pac="apk"
  system="linux"
elif [ -e /usr/bin/apk ]; then
  pac="apk"
  system="linux"
elif [ -e /sbin/apk ]; then
  pac="apk"
  system="linux"
elif [ -e /usr/sbin/apk ]; then
  pac="apk"
  system="linux"
elif [ -e /bin/yum ]; then
  pac="yum"
  system="fedora"
elif [ -e /usr/bin/yum ]; then
  pac="yum"
  system="fedora"
elif [ -e /sbin/yum ]; then
  pac="yum"
  system="fedora"
elif [ -e /usr/sbin/yum ]; then
  pac="yum"
  system="fedora"
elif [ -e /bin/brew ]; then
  pac="brew"
  system="mac"
elif [ -e /usr/bin/brew ]; then
  pac="brew"
  system="mac"
elif [ -e /sbin/brew ]; then
  pac="brew"
  system="mac"
elif [ -e /usr/sbin/brew ]; then
  pac="brew"
  system="mac"
elif [ -e /data/data/com.termux/files/usr/bin/pkg ]; then
  pac="pkg"
  system="termux"
elif [ -e /data/data/com.termux/files/usr/bin/apt ]; then
  pac="apt"
  system="termux"
elif [ -e /data/data/com.termux/files/usr/bin/apt-get ]; then
  pac="apt-get"
  system="termux"
fi

# setup process
clear
echo "$logo"
echo "\033[01;32m Installing .... \033[00m"
sleep 1
echo "\033[01;33m Running setup .... \033[00m"
sleep 1

# installing dependency
if [ ! -e $bin/wget ]; then
  if [ $sudo ]; then
    $sudo $pac install wget -y
  else
    $pac install wget -y
  fi
fi
if [ ! -e $bin/curl ]; then
  if [ $sudo ]; then
    $sudo $pac install curl -y
  else
    $pac install curl -y
  fi
fi
if [ ! -e $bin/git ]; then
  if [ $sudo ]; then
    $sudo $pac install git -y
  else
    $pac install git -y
  fi
fi

# removing old one
if [ -e $bin/onex ]; then
  if [ -d $conf_dir/onex ]; then
    if [ $sudo ]; then
      $sudo rm -rf $bin/onex
      $sudo rm -rf $conf_dir/onex
    else
      rm -rf $bin/onex
      rm -rf $conf_dir/onex
    fi
  fi
fi

# install onex
if [ $0 = "install" -o $0 = "./install" ]; then
  if [ -e onex ]; then
    if [ $sudo ]; then
      $sudo mv -v onex $bin
      $sudo chmod +x $bin/onex
    else
      mv -v onex $bin
      chmod +x $bin/onex
    fi
  fi
  cd ..
  if [ -d onex ]; then
    if [ $sudo ]; then
    $sudo mv -v onex $conf_dir
    else
      mv -v onex $conf_dir
    fi
  fi
else
  if [ -e onex/onex ]; then
    if [ $sudo ]; then
      $sudo mv -v onex/onex $bin
      $sudo chmod +x $bin/onex
    else
      mv -v onex/onex $bin
      chmod +x $bin/onex
    fi
  fi
  if [ -d onex ]; then
    if [ $sudo ]; then
    $sudo mv -v onex $conf_dir
    else
      mv -v onex $conf_dir
    fi
  fi
fi

# check onex is installed or not
if [ -e $bin/onex ]; then
  if [ -d $conf_dir/onex ]; then
    clear
    echo "$logo"
    echo " \033[00mOnex \033[01;32minstalled successfully !!"
    echo " \033[01;32mtype \033[00m'onex -h'\033[01;32m for more.\033[00m"
  else
    clear
    echo "$logo"
    echo " \033[01;31mSorry \033[00m: onex \033[01;31mis not installed !!"
    echo " \033[01;32mPlease try again\033[00m"
  fi
fi
