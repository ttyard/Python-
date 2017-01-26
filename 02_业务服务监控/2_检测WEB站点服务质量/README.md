# ʹ��pycurl̽��WEB��������

## ģ�鳣�÷���˵��
pycurl.Curl()��ʵ�ִ���һ��libcurl����Curl��������޲�����

����ʹ��˵����� http://curl.haxx.se/libcurl/c/libcurl-tutorial.html

�������Curl���󼸸����õķ�����
close(): ��Ӧlibcurl���е�curl_easy_cleanup�������޲�����ʵ�ֹرա�����Curl����

perform(): ��Ӧlibcurl���е�curl_easy_perform�������޲�����ʵ��Curl����������ύ��

setopt(option,value): ��Ӧlibcurl���е�curl_easy_setopt����������optionͨ��libcurl�ĳ�����ָ��������value��ֵ������option��������һ���ַ��������͡������͡��ļ������б�����ȡ�

�����оٳ��õĳ����б�

c = pycurl.Curl() #����һ��curl����

c.setopt(pycurl.CONNECTTIMEOUT, 5) #���ӵĵȴ�ʱ�䣬����Ϊ0������

c.setopt(pycurl.TIMEOUT, 5) #����ʱʱ��

c.setopt(pycurl.NOPROGRESS, 0) #�Ƿ��������ؽ���������0����

c.setopt(pycurl.MAXREDIRS, 5) #ָ��HTTP�ض���������

c.setopt(pycurl.FORBID_REUSE, 1) #��ɽ�����ǿ�ƶϿ����ӣ�������

c.setopt(pycurl.FRESH_CONNECT, 1) #ǿ�ƻ�ȡ�µ����ӣ�����������е�����

c.setopt(pycurl.DNS_CACHE_TIMEOUT, 60) #���ñ���DNS��Ϣ��ʱ�䣬Ĭ��Ϊ120s

c.setopt(pycurl.URL,"http://www.baidu.com") #ָ�������URL

c.setopt(pycurl.USERAGENT,"mOZILLA/5.2 (Compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322; .NET CLR 2.0.50324)") #��������HTTPͷ��User-Agent

c.setopt(pycurl.HEADERFUNCTION, getheader) # �����ص�HTTP HEADERָ�򵽻ص�����getheader

c.setopt(pycurl.WRITEFUNCTION, getbody) #�����ص������ض��򵽻ص�����getbody

c.setopt(pycurl.WRITEHEADER, fileobj) #�����ص�HTTP HEADER ����fileobj�ļ�����

c.setopt(pycurl.WRITEDATA, fileobj) #�����ص�HTML���ݶ���fileobj�ļ�����

getinfo(option)��������Ӧlibcurl���е�curl_easy_getinfo����������option��ͨ��libcurl�ĳ�����ָ���ġ������оٵĳ����б�

c = pycurl.Curl() #����һ��curl����

c.getinfo(pycurl.HTTP_CODE) #���ص�HTTP״̬��

c.getinfo(pycurl.TOTAL_TIME) #������������ĵ���ʱ��

c.getinfo(pycurl.NAMELOOKUP_TIME) #DNS���������ĵ���ʱ��

c.getinfo(pycurl.CONNECT_TIME) #�������������ĵ���ʱ��

c.getinfo(pycurl.PRETRANSFER_TIME) #�ӽ������ӵ�׼�����������ĵ�ʱ��

c.getinfo(pycurl.STARTRANSFER_TIME)#�ӽ������ӵ���ʼ���������ĵ�ʱ��

c.getinfo(pycurl.REDIRECT_TIME)#�ض��������ĵ�ʱ��

c.getinfo(pycurl.SIZE_UPLOAD)#�ϴ����ݰ���С

c.getinfo(pycurl.SIZE_DOWNLOAD)#�������ݰ���С

c.getinfo(pycurl.SPEED_DOWNLOAD)#ƽ�������ٶ�

c.getinfo(pycurl.SPEED_UPLOAD) #ƽ���ϴ��ٶ�

c.getinfo(pycurl.HEADER_SIZE) #HTTPͷ����С


