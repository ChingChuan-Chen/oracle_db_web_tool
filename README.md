# WOT - Web Oracle Tool

##  設計目標
Web Oracle Tool (下面簡稱WOT)目標為以Oracle Database為核心，構建一系列的web services及web views，並提供自動部署、監控、主動即時的Alarm系統、Admin頁面以及重要元件HA機制，所形成的一個完整解決方案。

## 架構圖

![](images/架構圖.svg)

## 系統需求 (許願中)

###  Web Services
  a. 待定

###  Web View
  - [ ] 支援LDAP登入，並以username控制可以查詢的DB (如目前的JASDA)
  - SQL編輯器，支援function, table, column提示
     - [ ] syntax highlight
     - [ ] theme selection (bright or dark)
     - [ ] 右鍵view table, query data, edit data
     - [ ] function提示
     - [ ] table提示
     - [ ] column提示
     - [ ] 查詢execusion plan
  - procedure, function編輯器，並支援儲存
     - [ ] view procedure/function
     - [ ] edit procedure/function
  - select SQL查詢，並顯示資料於grid
     - [ ] view
     - [ ] lock (see [lock sql](https://docs.oracle.com/cd/E17952_01/mysql-5.6-en/lock-tables.html))
     - [ ] perform insert / update on grid
  - [ ] 執行transaction SQL，並提供commit按鈕
  - [ ] 執行procedure
  - 查看table schema
    - basic info (owner, name, tablespace)
      - [ ] view
    - columns info
      - [ ] view
      - [ ] edit
    - key info (see [PRIMARY KEY](https://www.w3schools.com/sql/sql_primarykey.asp), [FOREIGN KEY](https://www.w3schools.com/sql/sql_foreignkey.asp))
    - index info
      - [ ] view
      - [ ] edit
    - checks info (see [CHECK](https://www.w3schools.com/sql/sql_check.asp))
      - [ ] view
      - [ ] edit
    - table privilege
      - [ ] view
      - [ ] edit
    - partition info
      - [ ] view
      - [ ] edit

###  Admin頁面
  - [ ] 可以設定group, connection部分
  - [ ] Web View權限管理 (卡user view/edit權限)
  - [ ] 查詢locked table
  - [ ] 砍特定session (for long run, table lock等)

###  系統服務監控
  - [ ] 暫定搭配zabbix，定時確認service存活狀態，然後寄信並自動重啟，設定可export，也可一次性部署到到各台

###  主動即時的Alarm系統
  - [ ] 暫定用grafana，可以拉KPI圖表並設定alarm mail，其設定可以export跟import
  - [ ] 自動砍table lock (可以在Admin頁面設定時間)

###  元件HA機制
  - [ ] middleware採group方式搭配nginx and GDNS
  - [ ] 使用web server多台搭配nginx for 2. and 3.
  - Database with high availability for server logging, service logging, connection setting and group setting
    - [ ] solution survey
    - [ ] build-up

###  自動部署
  - [ ] 使用shell撰寫，自動安裝並啟動服務 for 1, 2, 3
  - [ ] 自動部署6-c，並initialize tables

### 測試Oracle部署
  - [X] 安裝: [My Blogger](http://chingchuan-chen.github.io/posts/201607/2016-07-24-deployment-of-oracle-database.html)
  - [ ] 倒入測試資料 [IMDb Datasets](https://www.imdb.com/interfaces/)

## References
  1. Database with HA
    1. [ProxySQL安裝配置](https://dwj999.github.io/ProxySQL-%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE%E8%AF%A6%E8%A7%A3%E5%8F%8A%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB%E3%80%81%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1.html)
    1. [Consul, ProxySQL, and MySQL HA](https://dzone.com/articles/consul-proxysql-and-mysql-ha?utm_medium=feed&utm_source=feedpress.me&utm_campaign=Feed:%20dzone)
