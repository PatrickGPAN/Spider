# -*- coding: utf-8 -*-
import easygui
import requests
import os
import pandas as pd
import sys
import re
from bs4 import BeautifulSoup
import time
from requests.exceptions import ConnectionError

#用beautifulsoup很方便，而且要注意郑商所访问还要agent，gbk编码，代码写的比较简陋
#语意分析
title=[]
t=[]
url = ["http://www.shfe.com.cn/news/notice/", "http://www.dce.com.cn/dalianshangpin/yw/fw/jystz/ywtz/index.html","http://www.czce.com.cn/portal/jysdt/ggytz/A090601index_1.htm", "http://www.cffex.com.cn/jysgg/", "http://www.ine.cn/news/notice/"]
headers1={
    "Accept":"text/html,application/xhtml+xm…plication/xml;q=0.9,*/*;q=0.8",
    "Accept-Encoding":"gzip,deflate",
    "Accept-Language":"zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
    "Connection":"keep-alive",
    "Host":"www.shfe.com.cn",
    "Referer":"http://www.shfe.com.cn/news/notice/",
    "Upgrade-Insecure-Requests":"1",
    "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0"
}
headers2={
    "Host":"www.dce.com.cn",
    "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0",
    "Accept":"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
    "Accept-Language":"zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
    "Accept-Encoding":"gzip, deflate",
    "Connection":"keep-alive",
    "Upgrade-Insecure-Requests":"1"
}
headers3={
    "Host":"www.czce.com.cn",
    "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0",
    "Accept":"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
    "Accept-Language":"zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
    "Accept-Encoding":"gzip, deflate",
    "Connection":"keep-alive",
    "Upgrade-Insecure-Requests":"1"
}
headers4={
    "Host":"www.cffex.com.cn",
    "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0",
    "Accept":"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
    "Accept-Language":"zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
    "Accept-Encoding":"gzip, deflate",
    "Connection":"keep-alive",
    "Upgrade-Insecure-Requests":"1"
}
headers5={
    "Host":"www.ine.cn",
    "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0",
    "Accept":"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
    "Accept-Language":"zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
    "Accept-Encoding":"gzip, deflate",
    "Connection":"keep-alive",
    "Upgrade-Insecure-Requests":"1"
}

s=requests.session()
j=1
"""
response1 = s.get(url[0], headers=headers1)
text1 = response1.content
title1 = re.search('.*news/notice/.*', text1).group(0)
m = re.search('href=".*"', title1).group(0)
n1 = re.sub('href="', "", m)
n2 = re.sub('"', "", n1)
n3=n2.split(' ')
newurl="http://www.shfe.com.cn"+str(n3[0])
response2 = s.get(newurl, headers=headers1)
text2 = response2.content
soup = BeautifulSoup(text2)
print soup.prettify()
"""

if os.path.exists("lasttime1.csv"):
    while j==1:
        try:
            for i in range(0,5):
                item=url[i]
                #print item
                old=pd.read_csv("lasttime1.csv")
                lasttime=old['time'][i]
                if i == 0:
                    response1 = s.get(url[0], headers=headers1)
                    text1 = response1.content
                    #print text1
                    title1 = re.search('.*news/notice/.*', text1).group(0)
                    if title1 != lasttime:
                        t.append(title1)
                        m=re.search('title=".*"',title1).group(0)
                        n1=re.sub('title="',"",m)
                        n2=re.sub('"',"",n1)
                        str1='【上期所通知】'+n2
                        str2=str1.decode('utf-8', 'ignore').encode('gbk')
                        a = 'qq send group jsb '+str2
                        #a = 'qq send buddy Patrick ' + str2
                        os.popen(a, 'r', -1)
                    else:
                        t.append(title1)
                if i == 1:
                    response2 = s.get(url[1], headers=headers2)
                    text2 = response2.content
                    if text2:
                        title2 = re.search('.*</span><a href="/dalianshangpin/yw/fw/jystz/ywtz.*', text2).group(0)
                    if title2 != lasttime:
                        t.append(title2)
                        m=re.search('title=".*"',title2).group(0)
                        n1=re.sub('title="',"",m)
                        n2=re.sub('"',"",n1)
                        str1='【大商所通知】'+n2
                        str2=str1.decode('utf-8', 'ignore').encode('gbk')
                        a = 'qq send group jsb '+str2
                        #a = 'qq send buddy Patrick ' + str2
                        os.popen(a, 'r', -1)
                    else:
                        t.append(title2)
                if i == 2:
                    response3 = s.get(url[2], headers=headers3,)
                    text3 = response3.content
                    title3 = re.search('.*href=/portal/rootfiles.*', text3).group(0)
                    if title3 != lasttime:
                        t.append(title3)
                        m=re.search('title=.* ',title3).group(0).decode('gbk', 'ignore')
                        m1=m.split(" ")[0]
                        n1=re.sub('title=',"",m1)
                        #print title3.decode('utf-8')
                        str1='【郑商所通知】'+n1.encode('utf-8')
                        str2=str1.decode('utf-8', 'ignore').encode('gbk')
                        a = 'qq send group jsb '+str2
                        #a = 'qq send buddy Patrick ' + str2
                        os.popen(a, 'r', -1)
                    else:
                        t.append(title3)
                if i == 3:
                    response4 = s.get(url[3], headers=headers4)
                    text4 = response4.content
                    if text4:
                        #title4 = re.search('.*list_a_text.*', text4).group(0)
                        title4 = re.search('.*</a> <a', text4).group(0)
                    if title4 != lasttime:
                        t.append(title4)
                        #m=re.search('">.*</a><a',title4).group(0)
                        n1=re.sub('</a> <a',"",title4)
                        #n2=re.sub("</a><a","",n1)
                        str1='【中金所通知】'+n1
                        str2=str1.decode('utf-8', 'ignore').encode('gbk')
                        a = 'qq send group jsb '+str2
                        #a = 'qq send buddy Patrick ' + str2
                        os.popen(a, 'r', -1)
                    else:
                        t.append(title4)
                if i == 4:
                    response5 = s.get(url[4], headers=headers5)
                    text5 = response5.content
                    title5 = re.search('.*/news/notice/911.*', text5).group(0)
                    if title5 != lasttime:
                        t.append(title5)
                        m=re.search('title=".*"',title5).group(0)
                        n1=re.sub('title="',"",m)
                        n2=re.sub('"',"",n1)
                        str1='【能源中心通知】'+n2
                        str2=str1.decode('utf-8', 'ignore').encode('gbk')
                        a = 'qq send group jsb '+str2
                        #a = 'qq send buddy Patrick ' + str2
                        os.popen(a, 'r', -1)
                    else:
                        t.append(title5)
            pd.DataFrame(t, columns=['time']).to_csv("lasttime1.csv")
            print "Once Done"
        except ConnectionError as e:
            print e
            r = "No response"
            time.sleep(5)
            continue
        #easygui.msgbox("检测完成", title="Reminder", ok_button="OK")
        #sys.exit()
        time.sleep(120)
else:
    response1 = s.get(url[0], headers=headers1)
    text1 = response1.content
    title1 = re.search('.*news/notice/.*', text1).group(0)
    title.append(title1)

    response2 = s.get(url[1], headers=headers2)
    text2 = response2.content
    title2 = re.search('.*</span><a href="/dalianshangpin/yw/fw/jystz/ywtz.*', text2).group(0)
    title.append(title2)

    response3 = s.get(url[2], headers=headers3)
    text3 = response3.content
    title3 = re.search('.*href=/portal/rootfiles.*', text3).group(0)
    title.append(title3)

    response4 = s.get(url[3], headers=headers4)
    text4 = response4.content
    if text4:
        title4 = re.search('.*</a> <a', text4).group(0)
    title.append(title4)

    response5 = s.get(url[4], headers=headers5)
    text5 = response5.content
    title5 = re.search('.*/news/notice/911.*', text5).group(0)
    title.append(title5)

    pd.DataFrame(title,columns=['time']).to_csv("lasttime1.csv")
    easygui.msgbox("第一次更新完成", title="Reminder", ok_button="OK")
    sys.exit()
