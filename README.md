# ARCHE CI/CD Finish Action

Packs in one action all the steps done at the end of an ARCHE microservices build, test and redeploy GitHub workflow:

* login into the docker hub
* push the image into the docker hub
* redeploy the image on the ACDH cluster
* push the code coverage logs to the coveralls

Use with something like:

```yaml
- uses: acdh-oeaw/arche_cicd_finish_action@main
  with:
    pushAndRedeploy: ${{ github.event_name == 'release' && github.event.action == 'published' || inputs.deploy }}
    dockerhubLogin: ${{ secrets.DOCKER_USERNAME }}
    dockehubPassword: ${{ secrets.DOCKER_PASSWORD }}
    imageName: arche-something
    imageTag: latest # optional, default "latest"
    rancherBaseUrl: https://rancher.acdh-dev.oeaw.ac.at/v3 # optional
    rancherProject: arche-something
    rancherNamespace: arche-something
    rancherToken: ${{ secrets.RANCHERTOKEN }}
    coverallsToken: ${{ secrets.coverallsToken }}
    cloverPath: build/logs/clover.xml # optional, default "build/logs/clover.xml"
```

most probably:

```yaml
- uses: acdh-oeaw/arche_cicd_finish_action@main
  with:
    pushAndRedeploy: ${{ github.event_name == 'release' && github.event.action == 'published' || inputs.deploy }}
    dockerhubLogin: ${{ secrets.DOCKER_USERNAME }}
    dockehubPassword: ${{ secrets.DOCKER_PASSWORD }}
    imageName: $RANCHER_NAMESPACE
    rancherProject: $RANCHER_PROJECT
    rancherNamespace: $RANCHER_NAMESPACE
    rancherToken: ${{ secrets.RANCHERTOKEN }}
    coverallsToken: ${{ secrets.coverallsToken }}
```
