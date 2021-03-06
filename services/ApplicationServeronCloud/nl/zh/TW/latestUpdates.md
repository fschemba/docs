---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 最新更新項目
{: #latest_updates}
前次更新：2016 年 8 月 17 日
{: .last-updated}

服務最新更新項目的清單。

## 2016 年 8 月 17 日：已更新 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 已將 WebSphere Application Server for Bluemix 二進位檔從 8.5.5.9 升級為 8.5.5.10
* 已解決會影響 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 的[數個安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window}，包括：
  * 影響 WebSphere Application Server 及「WebSphere Application Server Hypervisor Edition 管理主控台」的 Apache Struts 漏洞。
  * 使用 SIP 服務時的 IBM WebSphere Application Server 的潛在拒絕服務漏洞。
  * 可能會影響 WebSphere Application Server 所使用 IBM HTTP Server 的數個漏洞。
  * 容許重新導向 CGI 應用程式的 HTTP 資料傳輸流量的漏洞，而 CGI 應用程式可能會影響 IBM HTTP Server (IHS)。此漏洞稱為 "HTTPOXY"。
  * IBM WebSphere Application Server 中的「資訊揭露漏洞」。
  * IBM WebSphere Application Server 中僅發生在已啟用 Web 儲存器自訂內容 HttpSessionIdReuse 的環境中的潛在略過安全限制漏洞。


## 2016 年 6 月 24 日：已更新 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 新增的功能可讓客戶在建立新的*傳統 ND* 或*傳統 WebSphere* 實例時，選擇 8.5 版或 9.0 版。
* 已升級 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二進位檔，WebSphere Application Server Liberty（核心和 ND 方案）的新實例都會安裝修正套件 16.0.0.2。16.0.0.2 是 8.5.5.9 之後的下一個修正套件。從 16.0.0.2 開始，預設會安裝為這些方案支援的所有授權 Liberty 選購配件。
* 已解決會影響 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 的[數個安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window}，包括：
  * Apache Standard Taglibs 中的 XML External Entity Injection (XXE) 漏洞，會影響 IBM WebSphere Application Server。
  * 使用 WebSphere Application Server Liberty 設定檔 API Discovery 功能和 Swagger 文件時，安全可能不如預期。
  * IBM WebSphere Application Server Liberty 的「管理中心」可能有資訊揭露的漏洞。
  * IBM WebSphere Application Server 中可能有 HTTP 回應分割的漏洞。
  * OpenSSL Project 於 2016 年 5 月 3 日揭露的 OpenSSL 漏洞。

## 2016 年 6 月 13 日：已更新 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 已新增功能，透過建立使用 WebSphere Application Server for Bluemix RESTful API 的應用程式或 Script，讓客戶建置、佈建、管理及刪除虛擬機器實例。
* 已新增功能，讓客戶有固定數目的已停止實例，且不超過 10 個 IP 位址或 64 GB 的記憶體。客戶現在會針對已停止狀態的累計實例被收取減價 5% 的費用。

## 2016 年 4 月 26 日：已更新 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 已解決 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 中，啟用 FIPS 140-2 時的[潛在安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window}，以及 Samba 中的數項漏洞 - 包括 Badlock。
* 整合式細項服務維護。

## 2016 年 4 月 15 日：已更新 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 已將 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二進位檔從 8.5.5.8 升級為 8.5.5.9
* 解決了 IBM {{site.data.keyword.Bluemix_notm}} 的 Liberty for Java 中影響消費者使用 OpenID Connect (OIDC) 用戶端的[跨網站 Script 編制](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window}漏洞。
* 整合式細項服務維護。

## 2016 年 2 月 19 日：已更新 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* 為應用程式佔用大量記憶體的用戶端新增了一個選項，以套用更大型的虛擬機器來合理調整其環境的大小。用戶端可以選取具有特定資源大小、且最多包含 32 GB RAM 虛擬機器的給定 WebSphere Application Server 元件或單一系統。
* 將 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二進位從 8.5.5.7 升級到 8.5.5.8
* 解決了 IBM SDK Java Technology Edition 中影響 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 運行的多個漏洞，通常將其稱為 [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}。
* 解決了影響消費者使用 OAuth 提供者輸出的[跨網站 Script 編制](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window}漏洞。
* 整合式細項服務維護。

## 2015 年 12 月 11 日：已更新 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* 已將正式產品名稱從 IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} 變更為 IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* 已新增 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment Plan 的新功能。此方案包含具有兩個以上虛擬機器的 WebSphere Application Server Network Deployment Cell 環境。這些新的功能容許使用者設定叢集環境以獲得高可用性、失效接手及可擴充性。
* 已新增 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core Plan 的新功能。此方案包括如何使用 Liberty Collective，而這是一組 Liberty 設定檔（伺服器）的管理網域，並且包含兩個以上的虛擬機器。
* 已將 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二進位檔從 8.5.5.6 升級為 8.5.5.7
* 已解決處理 Java 物件解除序列化的 [Apache Commons Collections 漏洞](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window}。
* 已解決可容許 [HTTP 回應分割攻擊](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}的漏洞。
* 整合式細項服務維護。

## 2015 年 10 月 15 日：已更新 Application Server on Cloud
* 新增下列兩個新方案：
  * [WebSphere Application Server 傳統版第 9 版測試版](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* 細項服務維護
