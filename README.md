ShadowsocksR-libev for OpenWrt
===


���
---

 ����Ŀ�� [shadowsocksr-libev][1] �� OpenWrt �ϵ���ֲ  
 
 ��ƽ̨Ԥ����IPK���ڱ���Ŀreleasesҳ������

����
---

��������� [shadowsocksr-libev][1] �Ŀ�ִ���ļ�,�Լ�luci���ƽ���  

֧��SSR�ͻ��ˡ������ģʽ�������֧�ֲ��ֻ���ģʽ��֧�ֶ�˿ڣ�

֧��SOCK5����֧��UDP�м̣�֧�ֹ������

֧����������ģʽ��IP·��ģʽ��GFW�б�ģʽ��GFWList��

���н����Զ��ػ����������Զ�������֧�ַ������Զ��л���

����[KcpTun����][4]���˹��ܶ�·��������Ҫ��ϸߣ������ض�Ӧ�Ķ������ļ���·����ָ��Ŀ¼��������ʹ��

�ͻ��˼�������SS��SSR�ķ�������ʹ��SS������ʱ������Э��������Ϊorigin���������������Ϊplain

����ģʽ����
---
��IP·��ģʽ��
 - ���й���IP���β��ߴ�������IP�����ߴ���
 - ������ģʽ��ȱʡ���ߴ����б���IP���β��ߴ���

�ŵ㣺���������������ȷ���ʺ���·��SSR��������ͨ���������߷��ʹ�����վ���ٶȣ�

ȱ�㣺����BT����ʱ�������ӹ����IP�������SSR�����������������SSR��������·���ã�ͨ��������ʹ�����վ���ٶȲ���ֱ��

��GFW�б�ģʽ��
 - ֻ����GFW�б��е���վ�ߴ������������ߴ���
 - ������ģʽ��ȱʡ�����ߴ����б�����վ�ߴ���

�ŵ㣺Ŀ����ȷ��ֻ�з����б�����վ�Ż����SSR����������

ȱ�㣺GFW�б�����100%���Ǳ�ǽվ�㣬������Щ����վ��ֱ���ٶ�Զ�����ߴ��� 

ע�⣺���Ҫʹ��SSR for OpenWRT�ķ���˽����ֻ��Ľ��루ͨ��3G/4G���磩����ʹ��IP·��ģʽ��ԭ�����ֻ�ͨ�������������OpenWRT����ˣ��ֻ������Ҫ����google����ʹ�õ����ֻ��ϵ�DNS���������������Ǳ���Ⱦ�ģ�ָ�����һ�����IP����IP���ܺ�GFW�б�ƥ�䣬������ʹ��GFWģʽ�������ܿ�ѧ����


�����IP·��ģʽ�´�����������GFW�б�ģʽ���޷��������ʣ�����DNS�����Ƿ���ȷ���������Ƿ���UDPת�����Ƿ�������dns�����ͻ�ȣ�

��ѡ����               | ����
-------------------|--------------------
`dnsmasq-full`     | DNS ������Ⱦ�б����
`curl`             | ��ȡ DNS ������Ⱦ�б�ͷ�������������
`coreutils-base64` | base64 ���� DNS ������Ⱦ�б�ͷ�������������
`bash`             | ���������Ľű�ʹ�� bash ����������

����
---

 - �� OpenWrt �� [SDK][S] ���루���뻷����Ubuntu 64λϵͳ��������ǵ�һ�α��룬��������OpenWrt�����������
   ```bash
   sudo apt-get install gawk libncurses5-dev libz-dev zlib1g-dev  git ccache
   ```
 
 - ����·������Ӧƽ̨��SDK

   ```bash
   # �� ar71xx ƽ̨Ϊ��
   tar xjf OpenWrt-SDK-15.05-ar71xx-generic_gcc-4.8-linaro_uClibc-0.9.33.2.Linux-x86_64.tar.bz2
   cd OpenWrt-SDK-*
   # ��װ feeds
   ./scripts/feeds update packages
   ./scripts/feeds install libpcre
   # ��ȡ Makefile
   git clone https://github.com/gdwgi1225/openwrt-ssr.git package/openwrt-ssr
   # ѡ��Ҫ����İ� 
   #luci ->3. Applications-> luci-app-shadowsocksR         ԭʼ�汾
   #luci ->3. Applications-> luci-app-shadowsocksR-GFW     GFWList�汾
   #V1.1.6�Ժ�汾ȡ�����������Ŀͻ��˺ͷ���ˣ�������Ҫ�����޸�makefile�����V1.1.5�汾
   make menuconfig
   
   #���û�а�װpo2lmo����װ����ѡ��
   pushd package/openwrt-ssr/tools/po2lmo
   make && sudo make install
   popd
   #���������ļ�����ѡ��
   po2lmo ./package/openwrt-ssr/files/luci/i18n/shadowsocksr.zh-cn.po ./package/openwrt-ssr/files/luci/i18n/shadowsocksr.zh-cn.lmo
   
   # ��ʼ����
    make package/openwrt-ssr/compile V=99
   ```
 - LEDE���벹��
 
   LEDE��OpenWRT����һ���汾��LEDE��SDK����xzѹ����������xz -d��ѹ���ص�SDK�����ٰ������������
   
   ʹ��LEDE��SDK���룬���ܻ���ʾ�Ҳ���zlib��openssl�ļ�����������������
 
   ```bash
   ./scripts/feeds update
   #�������base���ִ����޸�SDKĿ¼�µ�feeds.conf.default�ļ�������source.git;HEAD����Ϊ��source.git��
   
   ./scripts/feeds install zlib
   ./scripts/feeds install libopenssl
   ```
 - Pandorabox(�˶���)���벹��
 
  �˶���Ҳ��Openwrt����һ�����ư汾����16.10�汾��SDK����ʱ�޷�ʹ��feed��ȡ��װ������Ҫ�Ƚ�libpcre��zlib��libopenssl��makefile����SDK��packageĿ¼����make menuconfig
  
  ����������makefile���Դ�[��������][8]
   
��װ
--- 
������������⣺libopenssl��libpthread��ipset��ip��iptables-mod-tproxy��libpcre��GFW�汾��������dnsmasq-full��coreutils-base64��opkg���Զ���װ�������ļ�

�������������������������ֱ���luci-app-shadowsocksR��ԭʼ�汾����luci-app-shadowsocksR-GFW��GFW�汾�����û�������Ҫѡ������һ����װ����

ԭʼ�汾ֻ֧��IP·��ģʽ��������OpenWRTϵͳ�Ķ����٣�����dns��������������Ⱦ����Զ��SSR���������½��ж���DNS�������ɺ�����DNS�������һ��ʹ�ã�

GFW�汾֧��IP·��ģʽ��GFW�б�ģʽ����ж��ԭ�е�dnsmasq����ӹ�OpenWRT��������������������Ⱦ��ʵ��׼ȷ������SSR���������迪��UDPת����

���ѣ������װGFW�汾����ͣ�õ�ǰ���������Ⱦ�����������������Ҫռ��UDP 5353�˿�

������ɹ���luci-app-shadowsocksR*_all.ipkͨ��winscp�ϴ���·������/tmpĿ¼��ִ�����

   ```bash
   #ˢ��opkg�б�
   opkg update
   
   #ɾ��dnsmasq��GFW�汾��һ�ΰ�װ���ֶ�ж��dnsmasq����������²���Ҫ��
   opkg remove dnsmasq 
   
   #��װ�����
   opkg install /tmp/luci-app-shadowsocksR*_all.ipk 
   ```
��Ҫ����KcpTun����ӱ���Ŀreleasesҳ��������վ��[��վ1][4]��[��վ2][7]������·����ƽ̨��Ӧ�Ķ������ļ��������ļ�����Ϊssr-kcptun������/usr/binĿ¼

��װ��ǿ�ҽ�������·��������Ϊluci�л�����ƣ�����������װIPK���粻������ʱ�����һЩĪ����������⣻��GFW�汾�ᰲװ���޸ġ�����dnsmasq-full����װ�����������·����

����
---

   �����ͨ��luci���ã� ֧�ֵ�����������:  
   
   �ͻ��˷��������ã�

   ����           | ��������   | ˵��
   ---------------|------------|-----------------------------------------------
   auth_enable    | ������     | һ����֤����[0.�ر� 1.����],��Ҫ�����ͬʱ֧��
   switch_enable  | ������     | �˷������Ƿ�����Զ��л�
   server         | ��������   | ��������ַ, ������ IP �����������Ƽ�ʹ��IP��ַ
   server_port    | ��ֵ       | �������˿ں�, С�� 65535   
   local_port     | ��ֵ       | ���ذ󶨵Ķ˿ں�, С�� 65535
   timeout        | ��ֵ       | ��ʱʱ�䣨�룩, Ĭ�� 60   
   password       | �ַ���     | ��������õ�����
   encrypt_method | �ַ���     | ���ܷ�ʽ, [����ο�][2]
   protocol       | �ַ���     | ����Э�飬Ĭ��"origin"[����ο�][3]
   obfs           | �ַ���     | ���������Ĭ��"plain" [����ο�][3]
   obfs_param     | �ַ���     | ����������� [����ο�][3]
   fast_open      | ������     | TCP���ٴ� [����ο�][3]
   kcp_enable     | ������     | KcpTun��������
   kcp_port       | ��ֵ       | KcpTun�������˿ں�, С�� 65535
   kcp_password   | �ַ���     | KcpTun���룬���ձ�ʾ"it's a secrect"
   kcp_param      | �ַ���     | KcpTun����[����ο�][4]
   
   �ͻ����������ã�
   
   ����                        | ����
   ----------------------------|-----------------------------------------------------------
   ȫ�ַ�����                  | ѡ��Ҫ���ӵ�SSR TCP���������
   UDP�м̷�����               | ѡ��Ҫ���ӵ�SSR UDP���������
   ���ý��̼��                | ���ú�ɶ����н��̽��м�أ����ֱ����Զ�����
   �����Զ��л�                | ���ú����ȱʡ���������ʧЧ�������Զ��л����������õĴ��������
   �Զ��л��������            | ��鵱ǰ����������Ƿ���Ч��ʱ�����ڣ�Ĭ��10���ӣ�600�룩
   �л���鳬ʱʱ��            | ���������˿ڻ�������ͨ�Եĳ�ʱʱ�䣬Ĭ��3����
   DNS������ʽ                 | ��UDP�����ʽ����Pdnsd��ʽ��TCP��������������GFW�汾���У���װpdnsd����ʾ��
   ���������DNS��ת��         | ����DNS�����ԭʼ�汾���У�
   �����DNS�����ض˿�         | DNS������ض˿ڣ�ԭʼ�汾���У�GFW�̶�Ϊ5353��
   DNS��������ַ�Ͷ˿�         | DNS����ת���ķ�������һ������Ϊgoogle��dns��ַ
   SOCKS5����-������           | ����SOCKS�����SSR������
   SOCKS5����-���ض˿�         | ����SOCKS����ı��ض˿ڣ�ע��˶˿ڲ��ܺ�SSR�����������еı��ض˿���ͬ��
   ���ʿ���-������IP�б�       | IP·��ģʽʱ��Ч������ָ����Ź���IP���ε��ļ�����Щ���β���������
   ���ʿ���-���ⱻ����IP       | IP·��ģʽʱ��Ч��������Ӷ���Ĳ����������Ŀ��IP��ַ
   ���ʿ���-ǿ���ߴ���IP       | ���������Ҫ���������Ŀ��IP��ַ
   ·�������ʿ���              | ���ڿ���·���������Ƿ��ߴ���������·��������BT���ص����
   �������ʿ���                | ���Կ�����������ЩIP���ߴ�����Щ�����ߴ�������ָ�������б��ڻ��б���IP
   ���������б�                | ����IP�б�����ָ�����
   
   
   ��������ã�

   ����           | ��������   | ˵��
   ---------------|------------|-----------------------------------------------
   enable         | ������     | �Ƿ����ô˷���������
   server         | �ַ���     | ����������IP��ַ, һ��Ϊ0.0.0.0
   server_port    | ��ֵ       | �����������˿ں�, С�� 65535
   timeout        | ��ֵ       | ��ʱʱ�䣨�룩, Ĭ�� 60
   password       | �ַ���     | ��������õ�����
   encrypt_method | �ַ���     | ���ܷ�ʽ, [����ο�][2]
   protocol       | �ַ���     | ����Э�飬Ĭ��"origin"[����ο�][3]
   obfs           | �ַ���     | ���������Ĭ��"plain" [����ο�][3]
   obfs_param     | �ַ���     | ����������� [����ο�][3]
   fast_open      | ������     | TCP���ٴ� [����ο�][3]
   
   ��ĳЩopenwrt�ϵ�kcptun����ѹ����������⣬����ڽ����ϼ����ˡ�--nocomp��������ȱʡΪ��ѹ�������ڷ����Ҳʹ�÷�ѹ��ģʽ
   
   ��Ҫ��kcptun����־��������kcptun����������"--nocomp --log /var/log/kcptun.log"����־�ᱣ����ָ���ļ���
   
   IP·��ģʽ�������ļ�Ϊ/etc/china_ssr.txt,������������IP���Σ�һ����ٱ䶯��������£���Ҫ���£����ڡ�״̬��ҳ�����
   
   GFW�б�ģʽ�������ļ�Ϊ/etc/dnsmasq.ssr/gfw_list.conf���������б�ǽ��վ��������£����ڡ�״̬��ҳ�����
   
   ���Ҫ�Զ���GFW������Ŀ¼/etc/dnsmasq.ssr�´���һ���ļ���������ȡ������myrules.conf�����ļ��а�Ҫ����������Ҫ��ӵ���ַ������Ҫ���google.com.hk���������������У�
   ```
   server=/.google.com.hk/127.0.0.1#5353
   ipset=/.google.com.hk/gfwlist
   ```
   ��Ӻ�ִ��/etc/init.d/dnsmasq restart����dnsmasq
   
   ������ΪGFW�汾���У������ļ�Ϊ/etc/dnsmasq.ssr/ad.conf����ԭ���ǽ������վ��IP��ַ����Ϊ127.0.0.1��ʹ�õ����ݿ�Ϊeasylistchina+easylist��������ģ��ȱʡδ��װ���û��ڡ�״̬��ҳ����¹�����ݿ���Զ��򿪣���򿪹����˺�������⣬��ɾ�����ļ�������dnsmasq
   
   �Զ��л�˵�����ڷ��������������ĳЩ�������������Զ��л����أ���Щ�����������һ�������Զ��л��ķ��������ϣ�����Щ�������е�ĳһ����Ϊȫ�ַ�����ʹ�ã�������ȫ���Զ��л�����ʱ�����ȫ�ַ��������ϣ����Զ��ڼ�����Ѱ�ҿ��õķ����������л�����������ü�����ںͳ�ʱʱ�䡣ÿ�μ��ʱ���ж�ȱʡ�������Ƿ�ָ�������������������Զ��л���ȱʡ��������ע���Զ��л���������·�����ļ�⣬����ڡ�·�������ʿ��ơ���Ӧ������Ϊ����������
   
   �Զ��л��ͽ��̼�ص���־������OpenWRT�ġ�ϵͳ��־���в鿴
   
   GFW�汾ȱʡʹ��DNS�����UDP����ʽ����������Ҫ��SS/SSR������֧��UDPת���������������֧��UDPת����UDP��ʽ�Ľ����������⣬����ʹ��Pdnsd����TCP��ʽ������DNS�����������û������а�װpdnsd����װ����ڿͻ��˽�����֡�DNS������ʽ��ѡ�������ѡ��ʹ��pdnsd��ʽ����������pdnsdȱʡ��TCPģʽ�������û���������DNS��������ַ�Ͷ˿ڣ����õ�DNS��������֧��TCP��ʽ��ѯ
   
   �ٷ��°汾���Ѿ�ȡ����pdnsd�����أ���Ҫ���أ�����14.07�汾�в��ң���ar71xx�����ص�ַΪ��
   http://downloads.openwrt.org/barrier_breaker/14.07/ar71xx/generic/packages/oldpackages/pdnsd_1.2.9a-par-a8e46ccba7b0fa2230d6c42ab6dcd92926f6c21d_ar71xx.ipk
   
   �ٷ�openssl��ipk�ڱ���ʱȥ����camellia��idea�����㷨�����ʹ�ùٷ���libopenssl�����޷�ʹ�������ּ��ܷ�ʽ������ʹ�ã������±���openssl�����滻


����ͽ��鷴��
---
������ҳ���ϵġ�Issues������ʹ���������

��ͼ  
---
�ͻ��ˣ�

![luci000](http://iytc.net/img/ssr9.jpg)

����ˣ�

![luci000](http://iytc.net/img/ssr82.jpg)

״̬ҳ�棺

![luci000](http://iytc.net/img/ssr120.jpg)

  [1]: https://github.com/gdwgi1225/shadowsocks-libev
  [2]: https://github.com/shadowsocks/luci-app-shadowsocks/wiki/Encrypt-method
  [3]: https://github.com/shadowsocksrr/shadowsocks-rss/wiki/config.json
  [4]: https://github.com/xtaci/kcptun
  [5]: https://github.com/shadowsocks/openwrt-shadowsocks
  [6]: https://github.com/shadowsocks/luci-app-shadowsocks  
  [7]: https://github.com/bettermanbao/openwrt-kcptun/releases 
  [8]: http://iytc.net/tools/pand.rar 
  [S]: https://wiki.openwrt.org/doc/howto/obtain.firmware.sdk

