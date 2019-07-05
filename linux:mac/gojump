#!/bin/sh
conf_path=~/.gojump

if [ ! -f "$conf_path" ]; then
    echo "The gojump config file does not exists! Please set ~/.gojump."
    exit 1
fi

if [ ! -s $conf_path ]; then
    echo "The gojump config file is empty!"
    exit 1
fi

i=0
param=$1
cat $conf_path |grep -v grep| grep $param | awk -F '=' '{print $2}' | while read -r line;
do 
    let 'i++'
    echo $i "$(echo $line | awk '{print $1,$3}')"
done
read -p "请选择:" ip_no
i=0
set timeout 30
cat $conf_path |grep -v grep| grep $param | awk -F '=' '{print $2}' | while read -r line;
do 
   i=`expr $i + 1`
   if [ $i == $ip_no ]; then
        array=(${line// / })
        host="root@${array[0]}"
        port="${array[1]}"
        password="${array[3]}"
        cat << EOF >/tmp/gojump 
            spawn ssh -p $port $host
            expect {
                "(yes/no)?"
                {send "yes\n"; exp_continue }
                "password:"
                {send "$password\n" }
            }
            interact
EOF
        break
   fi
done

/usr/bin/expect -f /tmp/gojump