# Access denied for user 'root'@'localhost' (using password: NO)

Mysql忘記root密碼

->Mysql -u root 會報錯

Access denied for user 'root'@'localhost' (using password: NO)

進入root帳號的方法root帳號要重新啟動 加上--skip-grant-tables繞過帳號權限與密碼認證
但會造成server斷線


sudo /usr/local/mysql/support-files/mysql.server stop


sudo /usr/local/mysql/support-files/mysql.server start --skip-grant-tables
mysql


必須重新啟動一次沒有skip的start
(適用於忘記root密碼，才能進去root中更改)


2.正常進入root


mysql -u root -p

password:kuanweitsai
