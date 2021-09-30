## if语句

```shell
#!/bin/bash
read a	#用户输入
read b	#用户输入
if (( $a == $b ))
then
        echo "a=b"

elif (( $a > $b ))
then
        echo "a>b"

elif (( $a < $b ))
then
        echo "a<b"

else
        echo "a!=b"
fi           
```

## for循环1.0

```shell
#!/bin/bash
sum = 0
for ((i=1; i<=100; i++))	#循环遍历
do
        ((sum += i))
done

echo "The sum is : $sum"
#结果
The sum is : 5050
```

## for循环2.0

```shell
#!/bin/bash
sum = 0
for n in {1..100}	# n在这个范围
do
        ((sum+=n))
done
echo $sum
#结果
5050
```

### 测试一个网段是否能ping通

```shell
#!/bin/bash
network="192.168.1."	#默认网段
i=0			#后边主机
for     ((i=1;i<=254;i++))      #循环遍历
do
if ping -c 1 ${network}${i} >/dev/null  #如果ping通了不要输出
        then    #输出这些  
           echo "${network}${i} Ping is success"
        else    #否则
            echo "${network}${i} Ping is NONONO"
        fi
done
```

