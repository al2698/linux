linux

```markdown
ifconfig |grep inet |  | awk '{print $2}' #
apt-get install -- ##ubuntu
sum install --- ## centos
ctrl+a ##移到最前面
ctrl+e ##移到最後面
ls -a ##檢視隱藏檔案 .cache(隱藏檔案)
ls -l -h -a = ls -lha = ls -ahl
echo "123456" | passwd --stdin tom ##更改其他使用者密碼
shutdown -h now
shutdown -h +10
rm -rf * ##刪除全部檔案 rm:remove ,-r:recursive ,-f:force
echo 1 > /proc/sys/net/ipv4/ip_forward ##開熱點
echo 1 > /proc/sys/net/ipv4/ip_forward ##關熱點
```

linux破解

```
1.取得IP位址
	yum install nmap
進入單人模式
nmap,hydra
rockyou ## 密碼字典

靶機 2022/3/22
ip :192.168.60.3 ===>/root/flag.txt ?

加分
output.png ##找出圖片裡隱藏內容
a.zip ##解密
```

集縮比

```
```

PT test

```
滲透測試
```

堆疊(stacking)

```
```

```
"echo hi" > a.sh ##輸入echo hi 到a.sh
chmod +x a.sh ##change mod +x(可執行)
./a.sh ##執行結果 hi(加./增加安全性)
cat a.sh ##執行結果 echo hi
file a.sh ##可察看檔案屬性
file /usr/bin/data
usr ##放第三方可執行檔的地方
which ##可知道執行檔位置
echo "2" 1>a.txt == echo "2" >a.txt
ls /aaa ##會報錯
ls /aaa 2>error.txt ##把報錯寫入error.txt(2不能省略)
ls /tmp/aaa 1>a.txt 2>&1 ##1可省略
ls /tmp/aaa >/dev/null 2>&1 ##把內容丟掉
echo $? ##0執行成功 非0失敗
```

路徑

```
export PATH=$PATH:(路徑) ##更改路徑只在此視窗有用
gedit .bashrc ##永久更改路徑(不會在現在視窗立即生效)
source .bashrc (. .bashrc) ##使永久更改的路徑立即生效
```



df指令

```
df -h ##知道磁碟檔案大小
```

使用者

```
adduser tom ##新增使用者
echo "tom" | passwd --stiden tom ##修改使用者密碼
```

## 腳本

![photo_2022-06-13_10-25-02](C:\Users\b5102\Downloads\Telegram Desktop\5-3\photo_2022-06-13_10-25-02.jpg)

------

#  檔案收尋



link:https://blog.gtwang.org/linux/unix-linux-find-command-examples/

``` 
find /homw=e -iname/gtwang.txt ##-iname 代表不分大小寫
{r--} 4 {-w-} 2  {--x} 1
suid(4) sgid(2) stickybit(1) ##-rwsr-xr-x(477)
find . -type f -perm 0777
find . -type f -name "*.txt" -exec rm -f {} \; ##一次刪除所有集合的檔案
touch {a..z}.txt ##創建a~z個.txt檔
mkdir a ##創建資料夾a
```



## atime、mtime與ctime的區別

* access time： atime在讀取文件或執行文件時會修改，單位為天。
* modified time ：mtime 在文件寫入時會改變，單位為天。
* create time ：ctime在文件寫入，更改所有者，權限。鏈接時文件的ctime會隨之改變，單位為天。

##　suid(4) sgid(2) stickybit(1) ##-rwsr-xr-x(477)

`-perm` 可以指定檔案的權限，例如列出權限是 `777` 的所有檔案：

```
find . -type f -perm 0777
```

ps. rwx = 4+2+1 = 7

如果您將它們傳遞給`chmod`（命令行程序），則沒有區別。但是在 C 程序或類似程序中，`0777`是八進制（三組三個 1 位），`777`而是十進制，這是完全不同的位模式。（`chmod`將任何數字參數解釋為八進制，因此不需要前導零。）

```
0777 (octal)  == binary 0b 111 111 111   == permissions rwxrwxrwx  (== decimal 511)
777 (decimal) == binary 0b 1 100 001 001 == permissions sr----x--x (== octal 1411)
```

------



## find  /  -type  f  -name  '*.txt'

![photo_2022-05-03_10-33-19](C:\Users\b5102\Downloads\Telegram Desktop\5-3\photo_2022-05-03_10-33-19.jpg)

## 量檔案備份

![photo_2022-06-13_10-24-54](C:\Users\b5102\Downloads\Telegram Desktop\5-3\photo_2022-06-13_10-24-54.jpg)

![photo_2022-06-13_10-25-02](C:\Users\b5102\Downloads\Telegram Desktop\5-3\photo_2022-06-13_10-25-02.jpg)

```
cat /etc/resolv.conf ##可以修改ping(把resolv.conf當檔案)
cat < /etc/resolv.conf ##把resolv.conf當標準輸入
wc (word count)
cat <<EOF
grep name /etc/resolv.conf ##從resolv.conf中篩選name
cat /etc/resolv.conf | grep name ##從標準輸入讀
通配符(wildcard) *:是用來匹配檔案名稱的  正則表達室友來表達檔案內容的 (regular expression)
cat /etc/passwd | grep "h$" ##以h為結尾
cat /etc/hosts | grep -v "^$" ##可以去除空白行
```

## tac與cat差異

- cat 由第一行開始顯示文件內容
- tac 從最後一行開始顯示，可以看出tac 是cat 的倒著寫！

## cat <<EOF

`cat << EOF >  output.txt`：會把以下所有輸入放入output.txt中，然後最後結束時會輸入EOF(結束符號可以自訂)

```
e.g:
[root@centos7-1 user]# cat <<EOF > output.txt

> this is an apple .
> hello world
> EOF
> [root@centos7-1 user]# cat output.txt
> this is an apple .
> hello world
```

## <<<   here is a string

```bash
$ cat <<< 'hi there'
hi there
```



清空檔案方法：

1. access.log

2. : > access.log  OR  true > access.log

3. cat /dev/null> access.log
    cp /dev/null access.log
    dd if=dev/null of=access.log
    
4. echo > access.log

---

## [grep 參考](https://dotblogs.com.tw/xerion30476/2021/05/21/Linux)

# **顯示前後幾行**

```
grep -A 1 127 /etc/hosts ##after
grep -B 1 127 /etc/hosts ##befor
grep -C 1 127 /etc/hosts ##前跟後
```

## grep 應用

![photo_2022-06-14_07-26-37](C:\Users\b5102\Downloads\Telegram Desktop\5-10\photo_2022-06-14_07-26-37.jpg)

***

## **正規表示法**

`grep` 在搜尋關鍵字時，其實是以正規表示法的方式匹配文字的，所以一般的正規表示法都可以直接使用，以下是一些常用的範例。開頭與結尾是最常用的：

```
# a 開頭
ls | grep "^a"
# b 結尾
ls | grep "b$"
# a 或 b 開頭
ls | grep "^[ab]"
# a 或 b 結尾
ls | grep "[ab]$"
```

各種出現次數的指定：

```
# r 開頭，接著 o 出現零次以上
cat /etc/passwd | grep "^ro*"
# r 開頭，接著 o 出現零次或一次
cat /etc/passwd | egrep "^ro?"
# r 開頭，接著 o 出現一次以上
cat /etc/passwd | egrep "^ro+"
```

多種字眼的組合，也很常用：

```
# 含有 ab 或 cd
cat /etc/passwd | egrep "root|user|tom"
# 含有 ab 或 cd（另一種寫法，作用相同）
cat /etc/passwd | grep -E "root|user|tom" ##使用擴充型的正則表達式(同egrep)
```



如果只想要精準篩選出 net 這個單字，可以這樣寫：

```
# net 這個單字
grep -w net
```

***



# cat /etc/passwd | grep "^r.*h$" 

r.* ##任意字串的匹配

# vim

命令模式

```
w: write  
q:quit   
wq:write and quit   
q!:quit and give up modified things
```

## lsblk

lsblk 可以列出所有關於區塊設備 (Block devices) 的資訊. lsblk 主要是去讀取 sysfs 的資訊,關於 sysfs 請參考 http://benjr.tw/20857

```
[root@localhost ~]# lsblk 
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda           8:0    0   464G  0 disk 
├─sda1        8:1    0     1G  0 part /boot
└─sda2        8:2    0   463G  0 part 
  ├─cl-root 253:0    0    50G  0 lvm  /
  ├─cl-swap 253:1    0   7.9G  0 lvm  [SWAP]
  └─cl-home 253:2    0 405.1G  0 lvm  /home
sr0          11:0    1  1024M  0 rom 
```

lsblk 會列出所有 區塊設備 (Block devices) 的資訊,可以使用 -d 參數,顯示主要 區塊設備 (Block devices) 的資訊.

## lsblk -f

![photo_2022-06-14_07-36-15](C:\Users\b5102\Downloads\Telegram Desktop\5-17\photo_2022-06-14_07-36-15.jpg)

```
ext2 ext3 ext4 xfs (linux常用掛載檔案格式)
```

umount /media

```
卸載USB ##必須離開USB目錄
```

USB

```
vfat 不需要驅動程式
備份USB把檔案變成xfat
```

找尋在線的使用者：

![photo_2022-05-17_11-59-07](C:\Users\b5102\Downloads\Telegram Desktop\5-17\photo_2022-05-17_11-59-07.jpg)

in centos system, uid < 1000 (system account), >=1000 (normal user account)
system account (nologin)  , user account (bash)

# FIND尋找檔案Grep可以找得更廣

## linux 開機執行的第一個程式

![photo_2022-05-24_09-40-46](C:\Users\b5102\Downloads\Telegram Desktop\5-24\photo_2022-05-24_09-40-46.jpg)

## 為什麼init會被systemb取代

1. 啟動時間過長
2. 系統浪費資源

當我們在終端下執行**pstree**命令時，即**以樹的形式顯示所有進程的層次**時，會發現應該是**init進程**的地方卻變成了**systemd**。

![20191102185815236](C:\Users\b5102\Downloads\Telegram Desktop\5-31\20191102185815236.png)


```
free -m ##看memory使用情形
```

## 看到執行程式花的時間

```
user1@vm1:~$ uptime
#(1)      (2)                (3)                    (4)   (5)   (6)
 03:13:58 up 4 days, 22:45,  1 user,  load average: 0.00, 0.00, 0.00
```

| ctrl+c       | ctrl+z       |
| ------------ | ------------ |
| 中斷程式執行 | 丟到背景執行 |

```
ps ：將某個時間點的程序運作情況擷取下來
[root@www ~]# ps aux <==觀察系統所有的程序資料 
[root@www ~]# ps -lA <==也是能夠觀察所有系統的資料
[root@www ~]# ps axjf <==連同部分程序樹狀態
選項與參數：
-A ：所有的 process 均顯示出來，與 -e 具有同樣的效用；
-a ：不與 terminal 有關的所有 process ；
-u ：有效使用者 (effective user) 相關的 process ；
x ：通常與 a 這個參數一起使用，可列出較完整資訊。
輸出格式規劃：
l ：較長、較詳細的將該 PID 的的資訊列出；
j ：工作的格式 (jobs format)
-f ：做一個更為完整的輸出。
```



## 符號

```
#	註解
;	不管前面的指令成功與否後面的指令都會繼續執行
&&	前面的指令如果失敗後面的就會拒絕執行
```

```
$$	
$?	可以看下的只領有沒有成功(有=0,沒有=非0值)
$#	輸入參數的個數
$_	$0可知道命令本身
$@	
!!	
```

![photo_2022-06-14_06-11-13](C:\Users\b5102\Downloads\Telegram Desktop\6-7\photo_2022-06-14_06-11-13.jpg)

![photo_2022-06-14_06-11-16](C:\Users\b5102\Downloads\Telegram Desktop\6-7\photo_2022-06-14_06-11-16.jpg)

![photo_2022-06-14_06-11-20](C:\Users\b5102\Downloads\Telegram Desktop\6-7\photo_2022-06-14_06-11-20.jpg)

***

# zombie process ; orphan process

zombie process

```
當child process執行完成後就會變成zombie process ,parents process 會將它回收
如果parents process 沒回收會一直存在
```

orphan process

```
當child process還在執行中parents process死掉就會變成orphan process
```

***

su 跟 su-差別：

* su 後面不加用戶是默認切到root
* su 是不改變當前變量
* su - 是改變為切換到用戶的變量

也就是說su只能獲得root的執行權限，不能獲得環境變量
而su -是切換到root並獲得root的環境變量及執行權限

![photo_2022-06-14_06-03-32](C:\Users\b5102\Downloads\Telegram Desktop\6-7\photo_2022-06-14_06-03-32.jpg)
