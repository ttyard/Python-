# Python��ϵͳ��ȫ

## 1.��������ʽ�Ĳ���ɨ�����

  Clam AntVirue(ClamAV)��һ����ѿ�Դ�ķ��������,����벡������½���������ѷ���.ĿǰClamAV�ṩLinux/Unix�ķ��ְ汾���ṩ������ɱ������ɨ��ȷ���pyClamd(http://xael.org/norman/ppython/pyclamd)��һ��Python������ģ�飬������Pythonֱ��ʹ��ClamAV����ɨ���ػ�����clamd��ʵ�ָ��µĲ�����⹦�ܡ����⣬pyClamdģ��Ҳ�ǳ��������ϵ��������е�ƽ̨���С�
  
  yum install -y clamav clamd clamav-update
  chkconfig --levels 234 clamd on
  /usr/bin/freshclam
  setenforce 0 
  
  �����ػ����̼���IP�����ļ������ݲ�ͬ���������޸ļ�����IP��
  sed -i -e '/^TCPADDR/{ s/127.0.0.1/0.0.0.0/;}' /etc/clamd.conf
  /etc/init.d/clamd start 
  
### ����ģ�鳣�÷���
  
pyClamad�ṩ�������ؼ��࣬һ��ΪClamdNetworkSocket()�࣬ʵ��ʹ�������׽��ֲ���clamd����һ��ΪClamdUnixSocket()�࣬ʵ��ʹ��Unix�׽��������clamd.�����ඨ��ķ�����ȫһ����

__init__(self,host='127.0.0.1',port=3310,timeout=None)��������ClamdNetworkSocket��ĳ�ʼ��������hostΪ��������IP��portΪ���Ӷ˿ںţ�Ĭ�϶˿ں���3310

contscan_file(self,file) ������ʵ��ɨ��ָ�����ļ���Ŀ¼����ɨ��ʱ����������ֲ���������ֹ��fileΪָ�����ļ���Ŀ¼�ľ���·����

multiscan_file(self,file),ʵ�ֶ��߳�ɨ��ָ�����ļ���Ŀ¼����˻����ٶȸ��죬��ɨ��ʱ����������ֲ���������ֹ��fileΪָ�����ļ���Ŀ¼�ľ���·��

scan_file(self,file),ʵ��ɨ��ָ�����ļ���Ŀ¼����ɨ�跢��������ֲ���ʱ��ֹ��

shutdown(self),ǿ�ƹر�clamd���̲��˳�

stats(self),��ȡClamscan��ǰ״̬��

reload(self),ǿ������clamd���������⣬ɨ��ǰ����reload����

EICAR(self),����EICAR�����ַ����������ɾ��в����������ַ��������ڲ��ԡ�


