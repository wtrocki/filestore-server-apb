# FH-Sync Server APB

## Local Development

### Requirements

- [apb](https://github.com/ansibleplaybookbundle/ansible-playbook-bundle/blob/master/README.md#installing-the-apb-tool)
- local [catasb](https://github.com/fusor/catasb) or similar oc cluster, which is configured to read from your docker org.

**NOTE:**
Due to our usage of an older version of the ASB, it is recommended using the `apb` CLI like the following:

```bash
alias apb='docker run --rm --privileged -v $PWD:/mnt -v $HOME/.kube:/.kube -v /var/run/docker.sock:/var/run/docker.sock -u $UID docker.io/feedhenry/apb'
```

Instead of the `abp` alias, you might want to use a modified alias, such as `apb-fh`, to not conflict w/ other versions that might be installed already on your machine.

### Process

After making your required changes, update the `apb.yml` to point at your own docker organisation, run:

```bash
make DOCKERORG=<your docker org> DOCKERHOST=<defaulting to docker.io>
```

Login to your oc cluster:

```bash
oc login -u developer -p any
```

Now you can run `apb bootstrap` to update the catalog in your local cluster and see your local copy of this apb image.

If no changes were made to the apb.yml, then you do not need to run bootstrap for the changes to the ansible playbooks to be reflected in your local cluster (this is because the image already exists in your local docker registry).

## Submitting Changes

To submit a change, please follow these instructions:

- Fork this repo.
- Make changes in your own repo, and use your own docker org while developing.
- Submit a pull request to this master on this repo.
