# 📚 Neon Dashboard Readme 📚

Neon Dashboard is a web-based visualization tool for exploring and analyzing neon data. It was created as part of the research project outlined in the paper (** add link).

***The original repository belongs to Negin Sobhani. My fork of this repository, https://github.com/negin513/neon_dashboard, is used to add some GitOps CICD automation and a Helm chart for Kubernetes.***

## GitOps Automation

GitHub Actions is used to trigger a workflow whenever a push is made to the neon_dashboard/ directory in the main branch of this repository. The workflow is setup to run on a self-hosted runner and will not start without one being connected to the repository. There is a github runner image on the NSF NCAR Harbor Container registry that can be used with the following command. 

`podman run -it --privileged -e REPO=NicholasCote/neon_dashboard -e TOKEN=${GITHUB_TOKEN} hub.k8s.ucar.edu/ncote/github-runner:2024-02-28.00.32`

```{note}
A GitHub token needs to be added as an environment variable with the following command `export GITHUB_TOKEN=<your_github_api_token>
```

This workflow will build a container image from the repository contents, push the image to the NSF NCAR Harbor Container registry, and update the Helm chart in the repository with the new container image. Argo CD is connected to the repository and checks for changes to the Helm chart every 3 minutes. When it sees the change in the Helm chart it will automatically sync and start using the new image. Changes to the number of replicas, CPU, or memory to use can also be made to the Helm chart and will be updated automatically to help tune performance. 

## 📄 Citing the Paper 📄

If you use Neon Dashboard in your research or work and want to cite the original paper, please use the following citation format [***].

🎉🎉🎉 Have fun exploring your neon data with Neon Dashboard! 🎉🎉🎉