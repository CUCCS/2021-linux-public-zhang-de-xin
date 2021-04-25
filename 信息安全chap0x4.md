
# 第四章实验   shell脚本编程基础

### 任务一：用bash编写一个图片批处理脚本
[imagemagick脚本.md](https://github.com/CUCCS/2021-linux-public-zhang-de-xin/files/6372192/imagemagick.md)

#### 实验步骤

##### 1.安装imagemagick

```bash
sudo apt-get install imagemagick
```

##### 2.实现以下功能

- 支持命令行参数方式使用不同功能

- 支持对指定目录下所有支持格式的图片文件进行批处理

- 支持以下常见图片批处理功能的单独使用或组合使用

  - 支持对jpeg格式图片进行图片质量压缩

    查看help脚本内置帮助信息：

    ```shell
    bash imagemagick.sh -h
    ```

    ```shell
    bash imagemagick.sh -a img/
    ```

    ```shell
    for img in `find ./ -name "*.[jJ][pP][gG]"`; do
                    convert -resize 85%*85% $img $img-resized;
                    rm $img;
                    mv $img-resized $img
                    echo $img
    done
    ```

  - 支持对jpeg/png/svg格式图片在保持原始宽高比的前提下压缩分辨率

    ```shell
    bash imagemagick.sh -b img/
    ```

    ```shell
    #缩放为原来的50%，不知道质量压缩和保持长宽比压缩有什么区别
    convert page200.jpeg -resize 50% page100.jpeg
    convert page200.png -resize 50% page100.png
    convert page200.svg -resize 50% page100.svg
    #批量缩放为50%，并存放到 newdir 目录中，如果没有 -path 语句，新生成的 png 文件将会覆盖原始文件
    mogrify -path newdir -resize 50% *.jpeg
    mogrify -path newdir -resize 50% *.png
    mogrify -path newdir -resize 50% *.svg
    ```

  - 支持对图片批量添加自定义文本水印

    ```shell
    bash imagemagick.sh -c img/
    ```

    ```shell
    #这个是添加图片水印的，文本水印是在图片上输入文本吗
    composite -dissolve 15 -tile wmark_image.png   page200.png  wmark_tiled.png
    #图片上添加文本，-fill 文字的颜色。-font 和 -pointsize 设定字体和大小。
    #格式：-annotate {SlewX}x{SlewY}+{X}+{Y} "字符串"。其中 +X+Y是所在的相对位置。而 {SlewX}x{SlewY} 则表示倾斜的角度。
    convert page200b.png -font 楷体 -fill white -undercolor #00000080 -gravity South -annotate 0x0+0+10 @anno-utf8.txt anno.png
    ```

  - 支持批量重命名（统一添加文件名前缀或后缀，不影响原始文件扩展名）

    ```shell
    bash imagemagick.sh -d img/
    ```

    ```shell
    #前缀加入字符串(x1)
    rename 's/^/x1/' *
    #后缀加入字符串(x1)
    rename 's/$/x1/' *
    
    #将所有.jpg文件中的x1替换成x2
    rename -n 's/x1/x2/' *.jpg
    rename -v 's/x1/x2/' *.jpg
    #-n：打印效果但不执行
    #-v：执行修改并打印结果
    #s：替换
    #x1：原文件中需要被替换的字符
    #x2：用来替换的字符
    ```

    ```shell
    #shell脚本方法，保存为rename.sh，终端里执行./rename.sh
    #!/bin/bash
    
    let i=1                               # define an incremental variable
    path=/                                # add your file path here
    cd ${path}
    mkdir bak                             # make a backup directory
    
    for file in *.jpg                     # *.jpg means all jpg files in current directory
    do
        cp ${file} bak
        mv ${file} ${i}.jpg
        echo "${file} renamed as ${i}.jpg"
        let i=i+1
    done
    ```

  - 支持将png/svg图片统一转换为jpg格式图片

    ```shell
    bash imagemagick.sh -e img/
    ```

    ```shell
    #将当前目录下的所有 gif 文件，转换为 png 格式，并将其存放在 newdir 目录下
    mogrify -path newdir -format jpg  *.png
    #将当前目录下的所有 gif 文件，转换为 png 格式，并将其存放在 newdir 目录下
    mogrify -path newdir -format jpg  *.svg
    ```

### 任务二：用bash编写一个文本批处理脚本，对以下附件分别进行批量处理完成相应的数据统计任务
[worldcup.md](https://github.com/CUCCS/2021-linux-public-zhang-de-xin/files/6372195/worldcup.md)

[worldcup 数据.md](https://github.com/CUCCS/2021-linux-public-zhang-de-xin/files/6372198/worldcup.md)

#### 实验步骤

[2014世界杯运动员数据](https://c4pr1c3.github.io/LinuxSysAdmin/exp/chap0x04/worldcupplayerinfo.tsv)

- 统计不同年龄区间范围（20岁以下、[20-30]、30岁以上）的球员**数量**、**百分比**

  ```shell
  bash worldcup.sh -a
  ```

  ```shell
  #统计不同年龄区间范围（20岁以下、[20-30]、30岁以上）的球员数量、百分比
              awk -F "\t" '{
          #BEGIN 是在文本处理之前执行的语句，文本没有开始处理，谈不上第一行
          BEGIN {x=0; y=0; z=0; sum=0;} #分别用来统计20岁以下、[20-30]、30岁以上的人数、总人数
          #执行统计的操作
          $6!="Age" {
              if($6>=0&&$6<20)
                 {x++;}
              if($6<=30)
                 {y++;}
              else
                 {z++;}
              sum++;
          }
          #END 是在文本处理完成之后执行的语句，文本处理完成，当前行就是最后一行
          #打印统计结果
          END {
              printf("Age\tCount\tPercentage\n");
              printf("<20\t%d\t%f%\n",x,x*100.0/sum);
              printf("[20,30]\t%d\t%f%\n",y,y*100.0/sum);
              printf(">30\t%d\t%f%\n",z,z*100.0/sum);
          }}'  worldcupplayerinfo.tsv
  ```

- 统计不同场上位置的球员**数量**、**百分比**

  ```shell
  bash worldcup.sh -b
  ```

  ```shell
  #统计不同场上位置的球员数量、百分比
          awk -F "\t" '{
              BEGIN {sum=0}
          $5!="Position" {
              #遍历取值，相同的在对应的数组里+1，突然觉得这种字符串下标的数组挺好用
              p[$5]++;
              sum++;
          }
          END {
              printf("Position\tCount\tPercentage\n");
              for(i in p) {
                  printf("%13s\t%d\t%f%\n",i,p[i],p[i]*100.0/sum);
              }
          }}'  worldcupplayerinfo.tsv
  ```

- 名字最长的球员是谁？名字最短的球员是谁？

  ```shell
  bash worldcup.sh -c
  ```

  ```shell
  #名字最长的球员是谁？名字最短的球员是谁？
              awk -F "\t" '{
          BEGIN {max=0; min=100;}
          $9!="Player" {
              l=length($9);
              name[$9]=l;
              if(l>max)
                 {max=l;}
              if(l<min)
                 {min=l;}
          }
          END {
              for(i in name) {
                  if(name[i]==max) {
                      printf("The longest name is %s\n", i);
                  }
                  else  if(name[i]==min) {
                      printf("The shortest name is %s\n", i);
                  }
              }
          }}' worldcupplayerinfo.tsv
  ```

- 年龄最大的球员是谁？年龄最小的球员是谁？

  ```shell
  bash worldcup.sh -d
  ```

  ```shell
  #年龄最大的球员是谁？年龄最小的球员是谁？
              awk -F "\t" '{
          BEGIN {max=0; min=100;}
          $6!="Age" {
              age=$6;
              name[$6]=age;
              if(age>max)
                 {max=l;}
              if(age<min)
                 {min=l;}
          }
          END {
              for(i in name) {
                  if(name[i]==max) {
                      printf("The oldest player is %d\n", i);
                  }
                  else  if(name[i]==min) {
                      printf("The youngest player is %d\n", i);
                  }
              }
          }}' worldcupplayerinfo.tsv
  ```

  查看帮助信息：

  ```shell
  bash worldcup.sh -h
  ```

[Web服务器访问日志](https://c4pr1c3.github.io/LinuxSysAdmin/exp/chap0x04/web_log.tsv.7z)

[web.md](https://github.com/CUCCS/2021-linux-public-zhang-de-xin/files/6372199/web.md)


- 统计访问来源主机TOP 100和分别对应出现的总次数

  查看帮助信息

  ```shell
  bash web.sh -h
  ```

  ```shell
  bash web.sh -a
  ```

  ```shell
  printf "%40s\t%s\n" "TOP100_host" "count"
      awk -F "\t" '{
      {host[$1]++;} 
      END {
      for(i in host){
          printf("%40s\t%d\n",i,host[i]);
          }
        }
      }' web_log.tsv | sort -g -k 2 -r | head -100
      #sort 默认的排序方式是升序，如果想改成降序，就加个-r就搞定了
      #用-k 来指定列数
      #-g 一般数字排序
      #head -100 前100个
        ;;
  ```

- 统计访问来源主机TOP 100 IP和分别对应出现的总次数

  ```shell
  bash web.sh -b
  ```

  ```shell
  #这里看不太懂，ip是如何获取的，源文件里面没有直接给ip的列，是通过host算出来的吗
        printf "%20s\t%s\n" "TOP100_IP" "count"
      awk -F "\t" '{
      {if(match($1, /^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$/)) ip[$1]++;}
      END { for(i in ip) {printf("%20s\t%d\n",i,ip[i]);} }
      }' web_log.tsv | sort -g -k 2 -r | head -100
        ;;
  ```

- 统计最频繁被访问的URL TOP 100

  ```shell
  bash web.sh -c
  ```

  ```shell
  printf "%55s\t%s\n" "TOP100_URL" "count"
      awk -F "\t" '{
      {url[$5]++;}
      END { 
      for(i in url) {
          printf("%55s\t%d\n",i,url[i]);
         }
       }
      }' web_log.tsv | sort -g -k 2 -r | head -100
        ;;
  ```

- 统计不同响应状态码的出现次数和对应百分比

  ```shell
  bash web.sh -d
  ```

  ```shell
  awk -F "\t" '{
      BEGIN {
      printf("code\tcount\tpercentage\n");
      }
      {code[$6]++;}
      END {
      for(i in code) {
           printf("%s\t%d\t%f%\n",i,code[i],100.0*code[i]/(NR-1));
         }
       }
      }' web_log.tsv
        ;; 
  ```

- 分别统计不同4XX状态码对应的TOP 10 URL和对应出现的总次数

  ```shell
  bash web.sh -e
  ```

  ```shell
  printf "%55s\t%s\n" "code=403 URL" "count"
      awk -F "\t" '{
      { if($6=="403") code[$5]++;}
      END {
      for(i in code) {
     		 printf("%55s\t%d\n",i,code[i]);
      	} 
        }
      }' web_log.tsv | sort -g -k 2 -r | head -10
  
      printf "%55s\t%s\n" "code=404 URL" "count"
      awk -F "\t" '{
      { if($6=="404") code[$5]++;}
      END {
      for(i in code) {
      	  printf("%55s\t%d\n",i,code[i]);
          } 
        }
      }' web_log.tsv | sort -g -k 2 -r | head -10
        ;;
  ```

- 给定URL输出TOP 100访问来源主机

  ```shell
  bash web.sh -f
  ```

  ```shell
  printf "%40s\t%s\n" "TOP100_host" "count"
      awk -F "\t" '{
      {if("'"$1"'"==$5) {host[$1]++;} }
      END { 
      for(i in host) {
             printf("%40s\t%d\n",i,host[i]);
          } 
        }
      }' web_log.tsv | sort -g -k 2 -r | head -100
        ;;
  ```

#### 实验问题

刚开始学着在Ubuntu环境下写shell脚本的时候，保存不了，一直报错。最后我发现，只要把

```shell
#！/usr/bin/env bash
```

开头这一句删除就可以保存并执行shell脚本，不知道为什么，我没有把代码打错，报错提示好像是！的问题，不过后面我没有继续测试了。

#### 实验总结

虽然和C语言之类的语法挺相似的，但是要写shell脚本还是要查好多东西，图片处理和文本处理的代码不查根本不会做，还有些地方不查根本看不懂。不过思路并不难，思路比计算机语言学科做的编程作业简单，难的是语法。我还把文本文件导入了excel查看



