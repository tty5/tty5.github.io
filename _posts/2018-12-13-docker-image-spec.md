# docker image

```
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/python    2.7                 f67e752245d6        2 weeks ago         908 MB
```

#获取tag list
```
curl  https://pqbap4ya.mirror.aliyuncs.com/v2/library/python/tags/list
```

#获取manifest
```
根据digest获取manifest
curl -H "Accept: application/vnd.docker.distribution.manifest.v2+json" https://pqbap4ya.mirror.aliyuncs.com/v2/library/python/manifests/sha256:0bfc35ca8afbf04440152f1b8b15b928d99ba4a319e4967d50166bab6f40e084

curl -H "Accept: application/vnd.docker.distribution.manifest.v2+json" https://pqbap4ya.mirror.aliyuncs.com/v2/library/python/manifests/2.7

{
   "schemaVersion": 2,
   "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
   "config": {
      "mediaType": "application/vnd.docker.container.image.v1+json",
      "size": 7304,
      "digest": "sha256:f67e752245d645cd8f06b25786676e59f08638e57b6f1ee7021525a732da4aa4"
   },
   "layers": [
      {
         "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
         "size": 45320257,
         "digest": "sha256:54f7e8ac135a5f502a6ee9537ef3d64b1cd2fa570dc0a40b4d3b6f7ac81e7486"
      },
```

#获取image config
```
curl  https://pqbap4ya.mirror.aliyuncs.com/v2/library/python/blobs/sha256:f67e752245d645cd8f06b25786676e59f08638e57b6f1ee7021525a732da4aa4

diff_ids": [
            "sha256:90d1009ce6fe3102fee728742a3bd73eea2b39c88cdda99977a3fb130dbc17ac
```

#获取layer 解压
```
curl  https://pqbap4ya.mirror.aliyuncs.com/v2/library/python/blobs/sha256:54f7e8ac135a5f502a6ee9537ef3d64b1cd2fa570dc0a40b4d3b6f7ac81e7486 -L |gunzip |sha256sum
90d1009ce6fe3102fee728742a3bd73eea2b39c88cdda99977a3fb130dbc17ac
```

#layer解压出来的就是diff_ids

#image id 就是config file的sha256

#image digest是manifest的sha256, image digest唯一确定镜像

#image id获取不了manifest, 因为可以好几个manifest, 里面的image id是一样的 layer的传输方式不一样
