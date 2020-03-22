# Digital Ocean Spaces

## s3cmd

### Installing (expounding on [these instructions](https://s3tools.org/download)):

- `wget https://github.com/s3tools/s3cmd/archive/master.zip`
- `unzip master.zip`
- `cd s3cmd-master`
- `apt-get install python-setuptools`
- `python setup.py install` (Tested with Python 2)

### [Setting up with Spaces](https://www.digitalocean.com/docs/spaces/resources/s3cmd/)

- `s3cmd --configure`
- Paste in access key, then secret from Digital Ocean
- Paste in Spaces endpoint (e.g. `nyc3.digitaloceanspaces.com`)
- Paste in `%(bucket)s.nyc3.digitaloceanspaces.com` for the bucket URL template.
- Say yes (just enter to accept default) when asked to use https.

### 'rsync'ing up to Spaces

- `s3cmd sync <path to src dir ending in slash> s3://<bucket>/<directory>/`
  - The destination must also end in a slash.
  - You can put `--dry-run` after `sync` to get it to say what it would copy.
  - You can use `—skip-existing` to avoid comparing existing files.
  - Use `--exclude '<dir or file pattern>'` to skip directories you don't want to upload. For directory patterns, use a trailing slash.
  - Use `--acl-public` to make these files publicly readable via a browser.
  - There is no `-a` like there is in rsync.
  - e.g. `s3cmd sync --exclude .git/ --acl-public /usr/share/nginx/html/dir/thing/ s3://bucket-name/dir/thing
`

### Copying a single file

- `s3cmd put filename s3://bucket/dir/`
  - `s3cmd cp` didn't seem to work for me.
