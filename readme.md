Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

https://git-scm.com/

## How to Setup Quick Dump Git Server

The quickest way to export an repository over the http web is to use a Dump Git Server.

1. Run this command first on the git repository

    cd /path/to/myrepo
    git update-server-info

2. Server the files:
    
    python3 -m http.server --bind 0.0.0.0 --directory $(pwd) 8001

3. Now you may clone it with:
    
    git clone http://localhost:8001/.git myrepo
