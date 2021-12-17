# Role Based Access Control (RBAC)

Kubernetes has no concept of users or groups. It only identifies a user or a group using certificates signed by the `kubernetes ca certificate`.

Setting up RBAC on kubernetes is quite an involved process.

Following files in **[/etc/kubernetes/pki](https://kubernetes.io/docs/setup/best-practices/certificates/)**

* ca.crt
* ca.key

Roles are specific to namespaces, however, clusterroles are roles which exist across the entire cluster (careful with this role!).

## Setting up RBAC for a user 'Foobar'

Brief outline of the steps which will be required.

* Create a client certificate.
* Set the **Foobar** as the common name in the certificate.
* Sign the certificate with the `kubernetes ca` and `kubernetes ca key`.
* Create a role to allow user **Foobar** permissions for specific actions.
* Bind the role to the certificate using the same common name.

Lets go over these steps in a bit more detail and set things up for user **Foobar**.

1. openssl genrsa -out foobar.key 2048
2. openssl req -new -key foobar.key -out foobar.csr -subj "/CN=foo.bar/O=artists"
3. Copy the crt and key files from the cluster. These can typically be found at `/etc/kubernetes/pki`. However `k3d` saves these at `/var/lib/rancher/k3s/server/tls/client-ca.{crt,key}`
4. openssl x509 -req -in users/foobar.csr -CA client-ca.crt -CAkey client-ca.key -CAcreateserial -out users/foobar.crt -days 90
5. Create a kubeconfig file pointing to these new certificates.

## Resources

* [Kubernetes PKI Certificates and Requirements](https://kubernetes.io/docs/setup/best-practices/certificates/)
