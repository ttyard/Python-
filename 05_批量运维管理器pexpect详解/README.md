# ϵͳ������ά������pexpect���

pexpect��Linux��expect��Python��װ��ͨ��pexpect���ǿ���ʵ�ֶ�ssh,ftp,passwd,telnet����������Զ��������������˹��������ﵽ�Զ�����Ŀ�ġ�

pexpect�ٷ���վ���ο� https://pexpect.readthedocs.io/en/stable/

## 1.��װpexpect

pexpect��ΪPython��һ����ͨģ�飬֧��pip,easy_install��ʽ��װ��

pip install pexpect  ��  easy_install pexpect

## 2.pexpect�ĺ������

������Ҫ���ܼ������������spawn��run��pxssh

### 2.1 spawn��

spawn�� pexpect����Ҫ�ӿڣ����������������Ӧ�ó������������Ĺ��캯�����壺

class pexpect.spawn(command, args=[], timeout=30, maxread=200, searchwindowssiz=None, logfile=None, cwd=None, env=None, ignore_sighup=True)

command: ������������֪��ϵͳ����磺

child = pexpect.spawn('/usr/bin/ftp') #����FTP�ͻ���

child = pexpect.spawn('/usr/bin/ssh user@wanglijie.cn') #����sshԶ����������

���ӳ�����Ҫ����ʱ��������ʹ��Python�б�����������

child = pexpect.spawn('/usr/bin/ftp', [])

child = pexpect.spawn('/usr/bin/ssh', ['user@wanglijie.cn'])

child = pexpect.spawn('ls', [-latr], ['/tmp'])

timeout: �ȴ�����ĳ�ʱʱ��

maxread: pexpect���ն˿���̨һ�ζ�ȡ������ֽ���

searchwindowssize: ƥ�仺�����ַ�����λ�ã�Ĭ���Ǵӿ�ʼλ��ƥ��

��Ҫע�⣺ pexpect�������shell�����е�Ԫ�ַ��������ض��� >, �ܵ� | �� * �ţ���Ȼ����ͨ���������������ַ���������Ϊ/bin/bash�������е��ã�
```
child = pexpect.spawn('/bin/bash -c "ls -l | grep LOG > logs.txt"')

child.expect(pexpect.EOF)
```

��ҲҲ����ͨ��������Ĳ�����Python�б����ʽ�����滻���Ӷ�ʹ���ǵ��﷨��ø���������

shell_cmd = 'ls -l |grep LOG > logs.txt'

child = pexpect.spawn('/bin/bash',['-c', shell_cmd])

child = expect(pexpect.EOF)

��ʱ����Դ�����Ҫpexpect��ȡ���������Ϣ���Ա����˽�ƥ��������pexpect�ṩ������;����һ��Ϊд����־�ļ�����һ��Ϊ�������׼�����

д����־�ļ��ķ�ʽʵ�����£�

child = pexpect.spawn('some_command')

fout = file ('mylog.txt','w')

child.logfile = fout

�������׼����ķ���ʵ�����£�

child = pexpect.spawn('some_command')

child.logfile = sys.stdout

��������ӣ�����ʵ��Զ��ssh��¼������ʾ/homeĿ¼�ļ��嵥,��ͨ����־�ļ���¼���е����������.
```
import pexpect
import sys
child = pexpect.spawn('ssh pactera@10.12.49.153')
fout = file('mylog.txt','w')
#child.logfile = sys.stdout

child.expect("password:")
child.sendline("pactera")
child.expect('#')
child.sendline('ls /home')
child.expect('#')
```
����Ϊmylog.txt��־���ݣ����Կ���pexpect������ȫ�������������Ϣ

(1)expect����

������һ���ӳ��������ƥ�����.

expect[pattern,timeout=-1,searchwindowssize=-1]

pattern��ʾ�ַ�����pattern.EOFָ�򻺴���β��(��ƥ����)��expect.TIMEOUTƥ��ȴ���ʱ��������ʽ����ǰ���������͵��б�List����patternΪһ���б�ʱ���Ҳ�ֹһ������Ԫ�ر�ƥ�䣬�򷵻صĽ�����ӳ���������ȳ��ֵ��Ǹ�Ԫ�أ��������б�����ߵ�Ԫ��(��С����ID)

timeoutָ��ƥ������ʱʱ�䣬��λΪ��(s)������ʱ������ʱ��expect��ƥ�䵽pexpect.TIMEOUT

searchwindowssize ƥ�仺�����ַ�����λ�ã�Ĭ�ϴӿ�ʼλ�ÿ�ʼƥ��

��pexpect.EOF��pexpect.TIMEOUT����Ϊexpect���б����ʱ��ƥ��ʱ�䷵�������б��е�����ID��

expect�����������ǳ����ĳ�Ա��before��after.befor��Ա���������ƥ��ɹ�֮ǰ�����ݡ�after��Ա�������ƥ��ɹ�֮������ݡ�

(2)read����

������Щ���뷽�������ö������ӳ�������Ӧ����������ɴ��������ǵı�׼������̡�

send(self, s) #����������س�

sendline(self, s='') #��������س�

sendcontrol(self, char) #���Ϳ����ַ�����child.sendcontrol('c') �ȼ��� ctrl+c

sendeof() #����EOF

## 2.2 run����

run��ʹ��pexpect���з�װ�ĵ����ⲿ����ĺ�����������os.system��os.popen����ͬ����ʹ��run()���Ի���������������������˳�״̬��

��������: pexpect.run(command, timeout=-1, withexitstatus=False, events=None, extra_args=None, logfile=None, cwd=None, env=None)

command:ϵͳ��֪�����������û��д����·��ʱ���᳢�����������·����

event: ��һ���ֵ䣬����expect��sendline�����Ķ�Ӧ��ϵ

������spawn��ʽ��ʾ����

from pexpect import *
child = spawn('scp foo user@example.com:.')
child.expect('(?i)password')
child.sendline(mypassword)

ʹ��fun����ʵ����������ݣ�

from pexpect import *
run('scp foo user@example.com:.', events={'(?i)password': mypassword})

## 2.3 pxssh ��

pxssh��pexpect�������࣬�����ssh�Ự����������һ���װ���ṩ��������ֱ�ӵĲ���������

pxssh�ඨ�壺 class pexpect.pxssh.pxssh(timeout=30, maxread=200, searchwindowssize=None, logfile=None, cwd=None, env=None)

pxssh���õ������������£�

login() #����ssh����

logout() #�Ͽ�����

prompt() #�ȴ�ϵͳ��ʾ�������ڵȴ�����ִ�н���


