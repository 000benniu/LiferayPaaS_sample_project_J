## Files may need to change:

# ci/LCP.json   Link to github
    '''
"env": {
    "JENKINS_ADMIN_USER_NAME": "lctjpteamdxp74",
    "JENKINS_URL": "https://ci-lctjpteamdxp74-infra.lfr.cloud",
    "LCP_CI_SCM_REPOSITORY_NAME": "lctjpteamdxp74",
    "LCP_CI_SCM_REPOSITORY_OWNER": "000benniu"
},
  '''

# Also need change Environment Variables on CI service.

## Backup service
backup/LCP.json

'''
  "env": {
    "LCP_BACKUP_CREATE_SCHEDULE": "0 16 * * *", // 1AM in UTC+9
    "LCP_BACKUP_CLEANUP_SCHEDULE": "@monthly",
    "LCP_BACKUP_RETENTION_PERIOD": "30",
    "LCP_GCP_DATABASE_CHARSET": "utf8mb4",
    "LCP_GCP_DATABASE_COLLATION": "utf8mb4_unicode_ci"
  },
'''


## DXP related
Version:            liferay/gradle.properties
properties files:   liferay/configs/XXX/portal-ext.properties

## Web Server
Basic AUTH:         webserver/configs/dev/conf.d/liferay.conf
    Password:       webserver/configs/common/public/.htpasswd

# how to create a passowrd:
'''
XXX/webserver/configs/dev/public > htpasswd -c .htpasswd [username]                                                                                                        
New password:
Re-type new password:
Adding password for user [username]
xxx/webserver/configs/dev/public > cat .htpasswd                                                                                                                      
[username]:$apr1$X1AsB9Op$MU0CSTdpHu.Vj2g/tLGTn1
'''
