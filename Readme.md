# Files may need to change:

## ci/LCP.json   Link to github

```
"env": {
    "JENKINS_ADMIN_USER_NAME": "lctjpteamdxp74",
    "JENKINS_URL": "https://ci-lctjpteamdxp74-infra.lfr.cloud",
    "LCP_CI_SCM_REPOSITORY_NAME": "lctjpteamdxp74",
    "LCP_CI_SCM_REPOSITORY_OWNER": "000benniu"
},
```

## Also need to change Environment Variables on CI service.


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
* properties files:   liferay/configs/XXX/portal-ext.properties

## Set session longer:
* https://help.liferay.com/hc/ja/articles/5394973917581--Unable-to-extend-the-HTTP-session-WARN-logs


## Fix back < button.

1. Control Panel -> Instance Settings -> Pages -> Redirect URLs
1. Security mode: DOMAIN
1. Allowed Domains: *.lfr.cloud

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

