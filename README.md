### Github Latest Release Downloading Script (Private Repository)

```
ID={YOUR_GITHUB_ID}
PW={YOUR_GITHUB_PASSWORD}
OWNER={OWNER}
REPO={REPOSITORY}

curl -u $ID:$PW https://api.github.com/repos/$OWNER/$REPO/releases/latest > latest.json
TAG_NAME=`cat latest.json | jq '.tag_name' |  tr -d '"'`
URL="https://github.com/$OWNER/$REPO/archive/$TAG_NAME.zip"
curl -O -J -L -u $ID:$PW $URL
```

Alternate options:

```
TOKEN={TOKEN}

wget --auth-no-challenge --header='Accept:application/octet-stream' https://$TOKEN:@api.github.com/repos/$OWNER/$REPO/releases/assets/$TAG_NAME -O $TAG_NAME.zip

curl -O -J -L -H "Accept: application/octet-stream" https://$TOKEN:@api.github.com/repos/$OWNER/$REPO/releases/assets/$TAG_NAME

curl -O -J -L -H "Accept: application/octet-stream" https://api.github.com/repos/$OWNER/$REPO/releases/assets/$TAG_NAME?access_token=$TOKEN
```
