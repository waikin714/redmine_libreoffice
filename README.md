# redmine_libreoffice
This is an image consist of 
- linux
- redmine:4.1.1
- libreoffice 

https://hub.docker.com/r/play714/redmine_libreoffice

## install redmine_more_previews steps
step 0: backup below item

db
- redmine attachments: /usr/src/redmine/files
- plugins: /usr/src/redmine/plugins
- themes: /usr/src/redmine/public/themes
- locales: /usr/src/redmine/config/locales/

step 1: libreoffice

docker file: https://hub.docker.com/r/play714/redmine_libreoffice

or download it manually:

1.1 create folder /usr/share/man/man1

1.2 download libreoffice
```
apt-get update && apt-get install -y --force-yes libreoffice
```

1.3 make suer soffice is installed

`which soffice`

1.4 test soffice
```
soffice --headless --convert-to html <the_file_you_want_to_preview>
```

it will product html file in the working directory.

step 2: redmine more previews

2.1 download this repository

2.2 rename folder name from 'redmine_more_previews-main' to 'redmine_more_previews'

2.3 make sure the folder structure of 'redmine_more_previews' is as below:

redmine_more_previews

├─.github

│ └─workflows

├─app

│ └─views

├─assets

│ └─images

├─config

│ └─locales

├─converters

├─...

2.4 put 'redmine_more_previews' folder to /usr/src/redmine/plugins

2.5 delete folder redmine_more_previews\converters\zippy\

because this cause bundle install error in my environment, and I don't need zippy.

zippy is use to lets you preview zip, tgz or tar-Files in the browser

2.6 go to redmine root folder and type bundle install

2.7 restart if need, my environment seems don't need

2.8 Go to redmine website -> Administration -> Plugins -> Redmine More Previews Configuration

Choose the following options

- use embed-tag or iframe-tag

- cache previews (speeds views, may bloat your rails root's tmp folder a bit)

- activate sub plugins above

for each sub plugin activate the file extension for files you want to preview

(if you choose two sub plugins converting the same file type, then a warning will be issued and the last activated sub plugin will do the conversion).
