# ansible-playbooks
This repo holds Ansible Playbooks I've created for use. Please test the playbooks in a lab environment before using them in your production environment.


# nginx-dev-qa-prod
This playbook installs nginx and sets up following 3 Domains, Document Root folder; and Server Block Files. Everything that needs to be done to have site.com, dev.site.com and qa.site.com are done with 1 Ansible playbook.

URL | Documentation Root | Server Block File
--- | --- | ---
dev.site.com | /data/www/site.com/*dev*.site.com | /etc/nginx/sites-available/*dev*.site.conf
qa.site.com | /data/www/site.com/*qa*.site.com | /etc/nginx/sites-available/*qa*.site.conf
site.com | /data/www/site.com/site.com | /etc/nginx/sites-available/site.conf

## Copy the playbook files to your Ansible controller
Copy folder nginx-dev-qa-prod/ to ~/ansible-playbook/nginx-dev-qa-prod/ or any other folder of your choice.

## How to deploy
To deploy the 3 URLs, only following command needs to be executed. Subsitute site.com with URL of your choice, such as mysite.com or secure.mysite.com.
Note --extra-vars. I picked this over using vars.yml because it's more flexible.
```
ansible-playbook --extra-vars "website_url=site.com" ~/ansible-playbook/nginx-dev-qa-prod/nginx-setup-master.yml -i ~/codes/ansible/hosts-file
```


## Doc Root is untouched
The playbook creates index.html and inserts "Hello World" note ONLY if index.html did not exist. If index.html already existed in the Doc Root directories, it will not be modified at all. This behavior is useful if you needed to reset nginx config, but would like to keep all website files the same. This helps speed up testing nginx config changes.
