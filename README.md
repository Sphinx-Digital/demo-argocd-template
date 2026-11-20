# demo-argocd-template

> Repo template pour les formations DevOps **Sphinx Digital**  
> Chaque stagiaire reçoit un fork de ce repo via `create-demo-user.sh`

## Structure

```
apps/
└── nginx/              ← Helm chart déployé par ArgoCD
    ├── Chart.yaml
    ├── values.yaml     ← Modifie ici pour changer la page
    └── templates/
        ├── deployment.yaml
        ├── service.yaml
        ├── ingress.yaml
        ├── configmap.yaml      ← Page HTML
        └── nginx-config.yaml   ← Config nginx non-root (port 8080)
```

## Exercice — modifier et déployer

1. Clonez votre repo (créé depuis ce template par votre formateur)
2. Editez `apps/nginx/values.yaml` :
   ```yaml
   homepage:
     title: "Mon App"
     message: "Hello depuis k3s !"
     color: "#f59e0b"   # orange
   ```
3. Commitez et pushez :
   ```bash
   git add .
   git commit -m "customisation page accueil"
   git push
   ```
4. Regardez ArgoCD synchro en temps réel → votre app est mise à jour

## Contraintes cluster (Kyverno + ResourceQuota)

| Contrainte | Valeur |
|---|---|
| Image autorisée | docker.io, ghcr.io, gcr.io |
| Tag `latest` | Interdit |
| Privileged / hostNetwork | Interdit |
| runAsNonRoot | Obligatoire |
| CPU max | 200m (500m quota namespace) |
| RAM max | 128Mi (512Mi quota namespace) |
| Pods max | 2 par namespace |

---

[sphinx-digital.com](https://sphinx-digital.com) · Formations · Consulting · DevOps
