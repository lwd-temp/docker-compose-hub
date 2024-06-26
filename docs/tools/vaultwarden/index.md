## vaultwarden

基于bitwarden的一个密码管理工具。

直接将vaultwarden配置写在docker-compose.yml的  `environment` 中即可，如果需要采用指定`env_file`配置，请修改当前目录下的.env文件。

```yaml
version: '3.8'
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden-server
    restart: always
    env_file:
      - .env
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - ./vaultwarden-data/:/data/
    ports:
      - "8072:80"
    environment:
      - TZ:Asia/Shanghai
      ## 如果采用挂载.env的方式，以下配置可以删除，均可在.env中配置
      - SIGNUPS_ALLOWED=false
      # 如果使用mysql数据库，放开这两行的配置即可。否则默认使用sqllite
      # - RUST_BACKTRACE=1
      # - DATABASE_URL=mysql://DB_USERNAME:DB_USER_PASSWORD@DB_URL:DB_PROT/DB_NAME
      - ADMIN_TOKEN=xxxxxxx
```
