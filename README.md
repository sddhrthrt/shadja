## Shadja

### Setup

This app has been set up according to [digitalocean's setup guide for Flask and Nginx](https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-gunicorn-and-nginx-on-ubuntu-18-04). This decision was made to get quickly started with development on a VM, but in future we might move to a app service like DigitalOcean's Apps.

The app lives in the VM at `/home/ubuntu/src/shadja`. To get access to `ubuntu` user on VM, ask in #infra.

The `nginx` server is set up to serve `shadja.py`'s `app` object. So follow any Flask development model, but let the `app` object in `shadja.py` be the app.


### Development workflow

Make any edits wherever you prefer to edit code. Push changes to this repo. Follow Pull Requests workflow - create a Pull Request from your branch to master. Merge after peer review.

### Running locally

- Install mysql, libmysql-dev, libpython-dev
- set up your local mysql.
    - a user `shadja` with `<whatever>` password 
    - a database `shadja_dev`
    - `GRANT ALL PRIVILEGES` to `shadja` on `shadja_dev.*`
- Activate your virtualenv
- pip install -r requirements.txt
- run in shell: `export MYSQL_PASSWORD="<whatever>"`
- run in shell: `flask db init`
- `flask db migrate -m "initial migration"`
- `flask db upgrade`
- ...

This is where I'm at now.
Now, db is created, ideally poller should be able to run off of db and persist
all new found availabilities per pin to db. Should also be able to send 
notifications via email (but email sender is not implemented yet)


### Deployment

To update the server with any changes you have made to the app, 
- either check out your branch on the VM 
- or (if your changes are in master) update master branch in VM. 

Now, your code should be there in the VM at `/home/ubuntu/src/shadja`.

Then, run

```
sudo systemctl restart shadja
```

The website is running at http://143.110.252.209/

### Plan
Refer to our [issue board](https://github.com/sddhrthrt/shadja/issues).
