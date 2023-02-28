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


# DXP related

* Version:            liferay/gradle.properties
   * Find the latest version from :https://hub.docker.com/r/liferay/portal/tags
   * https://releases-cdn.liferay.com/tools/workspace/.product_info.json
* properties files:   liferay/configs/XXX/portal-ext.properties

## Config with longer session:
* https://help.liferay.com/hc/ja/articles/5394973917581--Unable-to-extend-the-HTTP-session-WARN-logs

## Fix back < button.

1. Control Panel -> Instance Settings -> Pages -> Redirect URLs
1. Security mode: DOMAIN
1. Allowed Domains: *.lfr.cloud

## Use screen name to login.

1. Control Panel -> Instance Settings -> User Authentication -> General

## Authentication Token Expiration Time
1. System Settings -> Users -> On-Demand Admin

## Hide node infomation
1. Open DXPC console. https://console.liferay.cloud/
1. Go to liferay Service -> environment-variables
1. Add Regular variables `LIFERAY_WEB_PERIOD_SERVER_PERIOD_DISPLAY_PERIOD_NODE` as `false`

## release feature flags
* System Settings > Release Feature Flags

# Web Server
* Basic AUTH:         webserver/configs/dev/conf.d/liferay.conf
* Password:       webserver/configs/common/public/.htpasswd

## how to create a password:

```
XXX/webserver/configs/dev/public > htpasswd -c .htpasswd [username]                                                                                                        
New password:
Re-type new password:
Adding password for user [username]
xxx/webserver/configs/dev/public > cat .htpasswd                                                                                                                      
[username]:$apr1$X1AsB9Op$MU0CSTdpHu.Vj2g/tLGTn1
```

# [DXPC] Steps after project provision.
1. Accept the invite from mail .
* You are invited to become an Admin member on project lctjpsteam1101
2. [Optional] Clone the project ot local, diff and check if there are any changes.
* Service change log :https://help.liferay.com/hc/en-us/sections/360006251311-Services-Changelog
3. Config CI from https://console.liferay.cloud/, connect with personal git project. (Also can use project provided by dxp cloud team as default. eg. https://github.com/dxpcloud/[projectID]).
```
JENKINS_ADMIN_USER_NAME [ProjectID] // keep as default
JENKINS_URL [CI's URL] // keep as default
LCP_CI_DEPLOY_TARGET  [dev] // keep as default
LCP_CI_SCM_REPOSITORY_NAME  [github's repo name]
LCP_CI_SCM_REPOSITORY_OWNER [github's user name]
LCP_CI_SCM_PROVIDER [github]
LCP_CI_SCM_TOKEN  [access_token]  // Get it from github. https://github.com/settings/tokens
```

4. Change the project's webhook on github site to trigger the CI build.

5. Change the ci/LCP.json   Link to github

```
"env": {
    "JENKINS_ADMIN_USER_NAME": "lctjpteamdxp74",
    "JENKINS_URL": "https://ci-lctjpteamdxp74-infra.lfr.cloud",
    "LCP_CI_SCM_REPOSITORY_NAME": "lctjpteamdxp74",
    "LCP_CI_SCM_REPOSITORY_OWNER": "000benniu"
},
```
