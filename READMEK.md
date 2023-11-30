# Déploiment d'une application multi-tiers sur des clusters Kubernetes


## Requirement
- Kubernetes cluster
- Containered Apps 
- EBS Volume pour DB Pod


1) Créer un cluster sur AWS (EC2) via Kops, lancer ce cluster via Kops
2) Sur l'EC2 crée un EBS via Kubectl.
3) Récupérer les images paths des apps sur le Hub (vprofile/vprofileapp et vprofile/vprofiledb. Elles ont été crée sur la branche docker docker/Docker-files/app/Dockerfile et des données importantes ont été mappés dans docker/src/main/resources/application.properties pour que notre application puissent accéder aux backedn services)
4) Dans docker/src/main/resources/application.properties il faut encrypter les mdp de rabbitmq et de mysql, puis sur la définiton de notre pod, on pourra accéder aux mdps.
5) Créer la définition du secret kubernetes/vpro-app/app-secret.yml
6) Créer le secret (depuis le dossier kube-app) en lancant kubect create -f app-secret.yaml
7) kubectl get secret
8) kubectl describe secret (pour checker les mdp)
9) Créer la définition du db dans kubernetes/vpro-app/vprodbdep.yml (run db with deployment)
