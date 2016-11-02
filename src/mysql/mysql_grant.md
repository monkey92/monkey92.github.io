#### mysql 授权

```
    create user 'user_name'@'host_name/ip' identified by 'password' password expire interval 180 day;
    grant all privileges on db_name.table_name to 'user_name'@'host_name/ip';
    # grant all privileges on *.* to 'user_name'@'host_name/ip'; 
```
