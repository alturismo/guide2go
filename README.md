# guide2go 
guide2go

##  guide2go in docker with cron

after docker start check your config folder and do your setups, setup is persistent, start from scratch by delete them

cron options are updated on docker restart.

mounts to use as sample \
Container Path: /config <> /mnt/user/appdata/guide2go/_config/ \
Container Path: /guide2go <> /mnt/user/appdata/guide2go/ \
Container Path: /TVH <> /mnt/user/appdata/tvheadend/data/ << not needed if no TVHeadend is used \
while /mnt/user/appdata/ should fit to your system path ...

```
docker run -d \
  --name=guide2go \
  --net=bridge \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  -e TZ="Europe/Berlin" \
  -v /mnt/user/appdata/guide2go/_config:/config:rw \
  -v /mnt/user/appdata/guide2go/:/guide2go:rw \
  alturismo/guide2go
```

setup guide2go SD subscrition as follows or copy your existing .json files into your mounted /guide2go folder \
docker exec -it "dockername" guide2go -configure /guide2go/"your_epg_name".yaml

to test the cronjob functions \
docker exec -it "dockername" ./config/cronjob.sh

included functions are (all can be individual turned on / off)

guide2go - xmltv epg grabber for schedules direct, thanks to @marmei \
github: https://github.com/mar-mei/guide2go \
Schedules Direct web: http://www.schedulesdirect.org/

some small script lines cause i personally use tvheadend and get playlist for xteve and cp xml data to tvheadend

plex and/or emby direct epg update after guide2go update (no wait for scheduled tasks, trigger more often, ...)

so, credits to the programmers, i just putted this together in a docker to fit my needs
