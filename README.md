Django and MySQL on OpenShift
===================

This git repository helps you get up and running quickly with a Django
and MySQL installation on OpenShift.


Running on OpenShift
--------------------

Create an account at http://openshift.redhat.com/

Install the RHC client tools if you have not already done so:
    
    sudo gem install rhc

Create a python-2.6 application

    rhc app create -a django -t python-2.6

Install a mysql-5.1 cartridge

    rhc cartridge add mysql-5.1 -a django

Add this upstream repo

    cd django
    git remote add upstream -m master git://github.com/iepathos/django-mysql-example.git
    git pull -s recursive -X theirs upstream master

Then push the repo upstream

    git push

Admin user name and password
----------------------------
SSH to your application to create a super user for your new Django and MySQL app

    ssh $uuid@django-$yournamespace.rhcloud.com
    
Activate virtual environment

    source $OPENSHIFT_HOMEDIR/python-2.6/virtenv/bin/activate
    
Setup export path for Python egg cache

    export PYTHON_EGG_CACHE=$OPENSHIFT_HOMEDIR/python-2.6/virtenv/lib/python2.6

Create super user

    $OPENSHIFT_HOMEDIR/python-2.6/virtenv/bin/python $OPENSHIFT_HOMEDIR/app-root/repo/wsgi/openshift/manage.py createsuperuser

	
That's it. You can now checkout your application at:

    http://django-$yournamespace.rhcloud.com

