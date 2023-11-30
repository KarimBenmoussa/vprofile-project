# Déploiment d'une application multi-tiers sur des clusters Kubernetes


## Requirement
- Kubernetes cluster
- Containered Apps 
- EBS Volume pour DB Pod


1) Créer un cluster K8's sur AWS (EC2) via Kops, lancer ce cluster via Kops
2) Sur l'EC2, crée un EBS via Kubectl.
3) Récupérer les images paths des apps sur Docker Hub (vprofile/vprofileapp et vprofile/vprofiledb. Elles ont été crée sur la branche docker docker/Docker-files/app/Dockerfile et des données importantes ont été mappés dans docker/src/main/resources/application.properties pour que notre application puissent accéder aux backend services)
4) Dans docker/src/main/resources/application.properties il faut encrypter les mdp de rabbitmq et de mysql, puis sur la définiton de notre pod, on pourra accéder aux mdps.
5) Créer la définition du secret kubernetes/vpro-app/app-secret.yml
6) Créer le secret (depuis le dossier kube-app) en lancant kubect create -f app-secret.yaml
7) kubectl get secret
8) kubectl describe secret (pour checker les mdp)
9) Créer la définition du db dans kubernetes/vpro-app/vprodbdep.yml (run db with deployment)
10) Il est important que notre EBS ait un tag sinon le créer via cmd aws ou depuis la console. Pour que le pod s'attache à ce volume EBS. Sinon permission denied error. (key: KubernetesCluster, value: nomduclustercrée dans 1))
11) kubectl create -f vprodbdep.yaml
12) kubectl get deploy, kubectl get pod, kubectl describe pod
13) On doit créer un service pour que notre pod application puisse accéder à la DB -> kubernetes/vpro-app/db-CIP.yml
14) Répéter l'opération pour le pod Memcached à déployé -> mcdep.yaml 9) 10) 11) et 12)
15) Répéter l'opération pour le pod Application web à déployé -> mcdep.yaml 9) 10) 11) et 12) vproappdep.yml
16) On peut tester l'IP de Load Balancer en exécutant kubectl get svc
17) Possible de définir notre @Ip avec route 53

