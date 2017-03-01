# About this Repo

This repository provides Dockerfile which provides builds Ansible from source code + few additional libraries.
 * https://hub.docker.com/r/peru/ansible_latest/

## Usage

You can run it like this:

```
ANSIBLE_VAULT_PASSWORD_FILE=${ANSIBLE_VAULT_PASSWORD_FILE:-"~/.ansible/vault.password"}

DOCKER_PARAMETERS="
  run --interactive --tty --rm \
  --env SSH_AUTH_SOCK=/ssh-agent \
  --env ANSIBLE_VAULT_PASSWORD_FILE=/home/ansible/.vault_pass.txt
  --volume ${ANSIBLE_VAULT_PASSWORD_FILE}:/home/ansible/.vault_pass.txt:ro \
  --volume $SSH_AUTH_SOCK:/ssh-agent \
  --volume $HOME/.aws:/home/ansible/.aws:ro \
  --volume $HOME/.ansible:/home/ansible/.ansible:ro \
  --volume $HOME/.ansible/tmp:/home/ansible/.ansible/tmp \
  --volume $HOME/.ansible/cp:/home/ansible/.ansible/cp \
  --volume $PWD:/home/ansible/ansible_project:ro \
  --name=ansible_latest-$$ --label=ansible_latest peru/ansible_latest \
"

sudo docker $DOCKER_PARAMETERS ansible-playbook site.yml
```

Or something easier:

```
docker run --interactive --rm --volume $PWD:/home/ansible/ansible_project:ro peru/ansible_latest ansible-playbook --version
```

## License

BSD


## Author Information

This repo was created in 2017 by <petr.ruzicka@gmail.com>
