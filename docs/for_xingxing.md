```
#! /bin/bash
dir=$1
totalTime=0
fileCount=0
function getMp3FileInfo(){
	str=$(afinfo "$1"|grep duration|awk '{print $3}')
	# sub1=${str#*duration: }
	# totalTime='expr $totalTime + $str'
	if test -z "$str"
		then
			echo error -- $1
		else
			minute=$(echo "scale=2;$str/60"|bc)
			echo $1 的时间是 $str 秒 $minute 分钟
			c=$(echo "$str+$totalTime"|bc)
			totalTime=$c
			((fileCount=$fileCount+1))
	fi

}
for mp3File in ./*
do
	filetype=$(file -b "$mp3File" | awk '{print $1}')
	if [ "$filetype"x = Audiox ]
		then 
		getMp3FileInfo "$mp3File"
		# echo $mp3File is file
	fi
done
echo 总时间 $totalTime

doubleHour=$(echo "scale=6;$totalTime/3600"|bc)
hour=$(echo "$totalTime/3600"|bc)

doubleMinute=$(echo "scale=6;($totalTime/3600-$hour)*60"|bc)
minute=$(echo ${doubleMinute%.*})

doubleSecond=$(echo "$totalTime%60"|bc)
second=$(echo ${doubleSecond%.*})

echo 总时间 $hour:$minute:$second
echo 共 $fileCount 个音频文件

```
