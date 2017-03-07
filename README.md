# Network-speed-fix-for-Win10
爬了很多巴哈的文設定後 在設定完成發現網速居然只剩40Mbps...<br />
心有不甘的我 將那些設定值比照微軟官網的技術文件<br />
發現了巴哈上文章一些不正確的地方或忽略的地方<br />
(小弟系統為windows10) 註冊碼(regedit)的地方將以縮寫表示<br />
以下註冊碼內容皆為"十進位"<br />

HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters 之目錄下<br />
新增一個名為 TcpMaxDupAcks 的 DWORD 值 並設定為 1<br />
此設定能將封包延遲送出調成1，也就是0延遲的意思<br />
新增一個名為 DefaultTTL 的 DWORD 值 並設定為 64<br />
此能縮小未傳送到目的地的封包存活時間<br />
新增一個名為 GlobalMaxTcpWindowSize 的 DWORD 值 並設定為 614400<br />
此能設定最大傳送之TCP封包大小，我對此數值的設定方法：網速(假設60Mbps)*10240，根據微軟的官方技術文件表示其大小不能超過4194303<br />
新增一個名為 EnablePMTUDiscovery 的 DWORD 值 並設定為 1<br />
根據微軟的技術文件，此設定能偵測並發現遠端伺服器的MTU，也就是最佳化MTU數值<br />
新增一個名為 EnablePMTUBHDetect 的 DWORD 值 並設定為 0<br />
與上方設定相輔相成，主要是為了避免被黑洞MTU吃掉<br />
<del>懶人包下載(點右鍵另存新檔)</del><br />

網卡中的QoS記得打開，不然沒有QoS標頭後TCP/IP的封包少了傳送優先權，變得連一些無關緊要的程式都在跟你搶網速，記得於gpedit.msc中設定QoS原則<br />

其一：電腦設定->系統管理範本->網路->QoS封包排程器<br />
點兩下修改限制可保留的頻寬<br />
<img src=http://i.imgur.com/ujthGjo.png width=800px><br />
<img src=http://i.imgur.com/ouAsaib.png width=800px><br /><br />
其二：電腦設定->Windows設定->以原則為依據的 QoS<br />
對 "以原則為依據的 QoS" 點右鍵<br />
<img src=http://i.imgur.com/P5ZkEnI.png width=800px><br /><br />
以建立 [OBS studio] (https://obsproject.com) 原則為例<br />
<img src=http://i.imgur.com/oz5eEDX.png width=800px><br />
<img src=http://i.imgur.com/sgNnXDI.png width=800px><br />
<img src=http://i.imgur.com/LToHhlh.png width=800px><br />
<img src=http://i.imgur.com/A3nWbu6.png width=800px><br /><br />
設定完成後記得重新啟動電腦
