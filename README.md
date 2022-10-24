# Karavan in OpenShift Dev Spaces

This is a basic repo to demonstrate running Karavan in OpenShift Dev Spaces 3.1 using the (Tech Preview) VS Code IDE.

1. Install OpenShift Dev Spaces Operator from OperatorHub
2. Create a namespace for the instance of OpenShift Dev Spaces:
   `oc adm new-project openshift-devspaces`
3. Install OpenShift Dev Spaces into a new namespace (should be `openshift-devspaces`) - default settings are fine.
4. Once Dev Spaces has been fully installed, determine the URL for Dev Spaces:
   `oc get route devspaces -o jsonpath={.spec.host} -n openshift-devspaces`
5. You can then launch a new "dev space" using this GitHub repo :


```
DSURL=$(oc get route devspaces -o jsonpath={.spec.host} -n openshift-devspaces)
echo "https://$DSURL/#https://github.com/mgubaidullin/devspaces-karavan.git"
```

When the workspace first launches, you will see "Karavan" as a "Recommended" extension to install.  Install it!  Unfortunatly, right now there is no way to "force" install an extension.

**NOTE:** If you're using a cluster from RHPDS there will be **limit ranges** added to your dev spaces namespace that will be too small and keep your workspace from starting.  You can either delete the `limitrange` object from your namespace (it will be of the pattern `<useranem>-devspaces`) or you can pre-create your namespace with `oc adm` to skip the new project template and avoid the limitrange from the start.

```
oc adm new-project <username>-devspaces
```
