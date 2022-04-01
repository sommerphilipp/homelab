cluster setup

### for internal use only DO NOT expose to web ###

### requires kubectl and kustomize to be installed and configured ###

1. dietpi
    1. ssh
2. k3s
3. kustomize build argocd/ | kubectl apply -f -
4. kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml
    - dns debugging pod
5. cloudflared
    - https://developers.cloudflare.com/cloudflare-one/tutorials/many-cfd-one-tunnel
6. longhorn
    - https://github.com/longhorn/longhorn/issues/1661 single node replication
7. kubectl apply -f mariadb.yaml
    - kubectl exec -it mariadb-0 -- mysql -uroot
        - create database photoprism character set = 'utf8mb4' collate = 'utf8mb4_unicode_ci';
        - create user photoprism identified by 'photoprism';
        - GRANT ALL PRIVILEGES ON photoprism.* to 'photoprism'@'%';
    - kubectl exec -it mariadb-0 -- mysql -uroot
        - create database gitea character set = 'utf8mb4' collate = 'utf8mb4_unicode_ci';
        - create user gitea identified by 'gitea';
        - GRANT ALL PRIVILEGES ON gitea.* to 'gitea'@'%';
8. kubectl apply -f photoprism.yaml
    - needs to be automated
        - kubectl exec -it photoprism-0 -n photoprism -- photoprism convert