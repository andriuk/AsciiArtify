---

Deployment Guide Using ArgoCD
=============================

This guide covers the steps to deploy an application using ArgoCD. Before proceeding, ensure you have deployed ArgoCD and obtained the necessary credentials. For more information on setting up ArgoCD, refer to the [POC Documentation](POC.md).

Accessing the ArgoCD Web Interface
----------------------------------

After logging into the ArgoCD web interface, proceed to create a new application.

### Creating a New Application

Click the `+ New APP` button to start the application setup process. Fill in the required fields as follows:

#### General Settings

*   **Application Name**: Name of your application.
*   **Project Name**: default (or specify if different).
*   **AUTO-CREATE NAMESPACE**: Check this option.

#### Source Configuration

*   **Repository URL**: `https://github.com/andriuk/go-demo-app`
*   **Revision**: `HEAD`
*   **Path**: `helm`

#### Destination Configuration

*   **Cluster URL**: `https://kubernetes.default.svc`
*   **Namespace**: `demo`

![app](/doc/img/mvp_1.png)

### Synchronization with GitHub Repository

Once the application configuration is complete, you should see a preview similar to the following:

Click on the `Sync` button to synchronize the application with the GitHub repository. The status after synchronization should appear as follows:

![status](/doc/img/mvp_2.png)


### Accessing the Deployed Application

To open access to the application, use the following command:


```bash
kubectl port-forward -n demo svc/ambassador 8088:80
```

Verify the application's accessibility using:

```bash
curl localhost:8088
```

### Testing the Application

You can test the application with an image upload as follows:


```bash
curl -F 'image=@/home/yuandrk/yu.png' localhost:8088/img/
```

The expected result should resemble the following animation:

![result](/doc/img/result.gif)

---