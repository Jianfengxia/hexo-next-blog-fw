---
title: "filecmp比较文件夹的内容 - Python自动化运维"
date: 2017-06-21 08:00:00
updated: 2017-06-19 16:48:40
tags: ["Python"]
---
 
1. 安装Pip & Python 2.7 (or 3.6),并配置环境变量(默认安装会自动添加)
2. 设置Notepad++作为IDE开发工具:运行中输入命令cmd /k python "$(FULL_CURRENT_PATH)" & ECHO. & PAUSE & EXIT
3. 安装第三方库: pip install filecmp

Examples:
 
```python
 # -- coding: utf-8 --

 import filecmp

 

 a="E:\\python\\pyauto\\2\\filecmp\\dir1"

 b="E:\\python\\pyauto\\2\\filecmp\\dir2"

 

 dirobj=filecmp.dircmp(a,b,['test.py'])

 

 print "-------------------report---------------------"

 dirobj.report()

 print "-------------report_partial_closure-----------"

 dirobj.report_partial_closure()

 print "-------------report_full_closure--------------"

    dirobj.report_full_closure()

    

 print "left_list:"+ str(dirobj.left_list)

 print "right_list:"+ str(dirobj.right_list)

 print "common:"+ str(dirobj.common)

 print "left_only:"+ str(dirobj.left_only)

 print "right_only:"+ str(dirobj.right_only)

 print "common_dirs:"+ str(dirobj.common_dirs)

int "common_files:"+ str(dirobj.common_files)

int "common_funny:"+ str(dirobj.common_funny)

int "same_file:"+ str(dirobj.same_files)

iff_files:"+ str(dirobj.diff_files)

y_files:"+ str(dirobj.funny_files)

 Example(比较2个文件夹的不同之处):



ing: utf-8 --

in/env python

  

port os, sys

port filecmp

port re

 import shutil

st=[]



dir1, dir2):

     dircomp=filecmp.dircmp(dir1,dir2)

_in_one=dircomp.left_only

_in_one=dircomp.diff_files

=os.path.abspath(dir1)

     [holderlist.append(os.path.abspath( os.path.join(dir1,x) )) for x in only_in_one]

  [holderlist.append(os.path.abspath( os.path.join(dir1,x) )) for x in diff_in_one]

  if len(dircomp.common_dirs) > 0:

for item in dircomp.common_dirs:

             compareme(os.path.abspath(os.path.join(dir1,item)), \

          os.path.abspath(os.path.join(dir2,item)))

            return holderlist

    

    def main():

        if len(sys.argv) > 2:

            dir1=sys.argv[1]

            dir2=sys.argv[2]

        else:

            print "Usage: ", sys.argv[0], "datadir backupdir"

            sys.exit()

     

        source_files=compareme(dir1,dir2)

        dir1=os.path.abspath(dir1)

    

        if not dir2.endswith('/'): dir2=dir2+'/'

        dir2=os.path.abspath(dir2)

        destination_files=[]

        createdir_bool=False

    

        for item in source_files:

            destination_dir=re.sub(dir1, dir2, item)

            destination_files.append(destination_dir)

            if os.path.isdir(item):

                if not os.path.exists(destination_dir):

                    os.makedirs(destination_dir)

                    createdir_bool=True

    

        if createdir_bool:

            destination_files=[]

            source_files=[]

            source_files=compareme(dir1,dir2)

            for item in source_files:

                destination_dir=re.sub(dir1, dir2, item)

                destination_files.append(destination_dir)

    

        print "update item:"

        print source_files 

    

        copy_pair=zip(source_files,destination_files)

        for item in copy_pair:

            if os.path.isfile(item[0]):

                shutil.copyfile(item[0], item[1])

     

    if __name__ == '__main__':

        main()

  

