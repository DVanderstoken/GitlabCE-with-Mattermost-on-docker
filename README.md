Premi�re ex�cution avec

```
    mattermost['gitlab_enable'] = false
    # mattermost['gitlab_id'] = "d11390a0d78f287982a419e51e1969fc2863fd4ab13d2b112809bb7feecb066d"
    # mattermost['gitlab_secret'] = "644cd113afa5ff1c64a218ad8618cfc698407eee0b9e669cca71ffa94c5abee0"
```

Se connecter � Gitlab (root/ � d�finir), puis aller dans Settings --> Application et cr�er Mattermost avec 
```
    http://localhost:8065/signup/gitlab/complete
    http://localhost:8065/login/gitlab/complete 
```

A vérifier s'il faut cocher api dans les scopes.

R�cup�rer :
- l'application ID, et
- le Secret
Pour mettre � jour le fichier docker-compose.yml :
```
    mattermost['gitlab_enable'] = true
    # mattermost['gitlab_id'] = "{ApplicationID}"
    # mattermost['gitlab_secret'] = "{Secret}"
```	

Il subsiste un probl�me de droit pour Mattermost (cf. https://gitlab.com/gitlab-org/omnibus-gitlab/issues/4548) :

Se connecter au container Gitlab-web et ex�cuter le script suivant : 

```
chown -R mattermost:mattermost /opt/gitlab/embedded/service/mattermost/client/*
su -s /bin/bash mattermost
cd /opt/gitlab/service/mattermost
/opt/gitlab/embedded/bin/mattermost -c /var/opt/gitlab/mattermost/config.json config subpath --path /mattermost
exit
gitlab-ctl hup mattermost
```
