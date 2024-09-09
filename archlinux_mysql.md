# arch linux 安装 mysql

## １　安装

1. 更新源

    ```shell
    sudo pacman -Syy
    ```

2. 安装包

    ```shell
    sudo pacman -S mariadb
    sudo pacman -S mariadb-libs
    ```

3. 初始化

    ```shell
    sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
    ```

    > 遇到报错：
    > changing ownership of '/var/lib/mysql': Operation not permitted
Cannot change ownership of the database directories to the 'mysql'
user.  Check that you have the necessary permissions and try again.
    >
    > 原因：没有　`root`　权限，所以需要加上　`sudo`
    > 当然也可以直接进入　root 权限角色

4. 添加角色

    1. 进入数据库

        ```shell
        mariadb -u root -p
        ```

        > 没有密码，直接回车进入

    2. 创建角色

    ```mysql
    <!-- １．创建用户密码 -->
    CREATE USER '[username]'@'localhost' IDENTIFIED BY '[password]';

    <!--　２．赋予权限， -->
    <!-- 下面代码是赋予[username]用户全部权限 -->    
    GRANT ALL PRIVILEGES ON mydb.* TO '[username]'@'localhost';

    <!-- ３．退出 -->
    quit
    <!-- 或 -->
    \q
    ```

## 2 配置

MariaDB配置选项按给定顺序从以下文件中读取

```text
    /etc/my.cnf 
    /etc/my.cnf.d/ 
    ~/.my.cnf
```

> 创建一个扩展名为 .cnf 的配置文件 /etc/my.cnf.d/ ，以确保升级保留您的配置。
>
> 我在这里创建了文件　`myMariadb.cnf`　用以保存我的配置
