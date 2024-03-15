# About LXC-SM React

- Please check [here](./liferay/client-extensions/react-loan-calculator/README.md)

# Backup service
* backup/LCP.json

```
  "env": {
    "LCP_BACKUP_CREATE_SCHEDULE": "0 16 * * *", // 1AM in UTC+9 
    "LCP_BACKUP_CLEANUP_SCHEDULE": "@monthly",
    "LCP_GCP_DATABASE_CHARSET": "utf8mb4",
    "LCP_GCP_DATABASE_COLLATION": "utf8mb4_unicode_ci"
  },
```
*参考：バックアップスケジュールの記入方法：https://crontab.guru/

# DXP 関連

* 利用可能バージョン:　https://releases-cdn.liferay.com/tools/workspace/.product_info.json
  * 設定ファイルPath:   liferay/configs/XXX/portal-ext.properties

* Enable the upgrade report `upgrade.report.enabled=true`
* 7.4uXX->7.4uXX manual: https://help.liferay.com/hc/en-us/articles/4415761553677-Installing-a-Bundled-Service-Pack-or-Update

### Config with longer session:
* https://help.liferay.com/hc/ja/articles/5394973917581--Unable-to-extend-the-HTTP-session-WARN-logs

### Fix back < button.
1. Control Panel -> Instance Settings -> Pages -> Redirect URLs
1. Security mode: DOMAIN
1. Allowed Domains: *.lfr.cloud

### Authentication Token Expiration Time
1. System Settings -> Users -> On-Demand Admin

### Hide node infomation for UAT / DEV
1. Open DXPC console. https://console.liferay.cloud/
1. Go to liferay Service -> environment-variables
1. Add Regular variables `LIFERAY_WEB_PERIOD_SERVER_PERIOD_DISPLAY_PERIOD_NODE` as `false`

### release feature flags
* System Settings > Release Feature Flags

### Allow virtual host domain.
```
1. Open DXPC console. https://console.liferay.cloud/
2.  Go to liferay Service -> environment-variables
3. Add Regular variables LIFERAY_VIRTUAL_PERIOD_HOSTS_PERIOD_VALID_PERIOD_HOSTS as *
```


# Web Server
* Basic AUTH:
  * 設定ファイル： webserver/configs/dev/conf.d/liferay.conf
  * Password設定ファイル: webserver/configs/common/public/.htpasswd

### エンコードされたパスワードの作成方法:

```
XXX/webserver/configs/dev/public > htpasswd -c .htpasswd [username]                                                                                                        
New password:
Re-type new password:
Adding password for user [username]
xxx/webserver/configs/dev/public > cat .htpasswd                                                                                                                      
[username]:$apr1$X1AsB9Op$MU0CSTdpHu.Vj2g/tLGTn1
```
### 参考
* NGINX - Restricting Access with HTTP Basic Authentication

https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-http-basic-authentication/


# そのほか参考：

* Service change log :https://help.liferay.com/hc/en-us/sections/360006251311-Services-Changelog

### Githubリポジトリの接続方法
1.Config CI from https://console.liferay.cloud/, connect with personal git project. (Also can use project provided by dxp cloud team as default. eg. https://github.com/dxpcloud/[projectID]).
```
JENKINS_ADMIN_USER_NAME [ProjectID] // keep as default
JENKINS_URL [CI's URL] // keep as default
LCP_CI_DEPLOY_TARGET  [dev] // keep as default
LCP_CI_SCM_REPOSITORY_NAME  [github's repo name]
LCP_CI_SCM_REPOSITORY_OWNER [github's user name]
LCP_CI_SCM_PROVIDER [github]
LCP_CI_SCM_TOKEN  [the token get from settings.]  // Get it from github. https://github.com/settings/tokens
```

2.Change the project's webhook on github site to trigger the CI build.
