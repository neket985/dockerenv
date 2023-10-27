docker build -t devops-image:1.0 .
docker run --rm -it -v /Users/smirnov/IdeaProjects/tsft/lib/devops/ansible-infr:/wd -w /wd --name devops-image devops-image:1.0
ansible-playbook -t metrics_clean -t metrics_install -i inventory/gidnp/release/inventory.ini combined_metrics.yml