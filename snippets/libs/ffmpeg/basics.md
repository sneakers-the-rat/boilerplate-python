## Speed Up/Slow Down Video
[Reference](https://trac.ffmpeg.org/wiki/How%20to%20speed%20up%20/%20slow%20down%20a%20video)

To speed up 4x
``` -filter:v "setpts=0.25*PTS"```
To slow down 4x
``` -filter:v "setpts=4*PTS"```

### Smoothing
```-filter:v "minterpolate='mi_mode=mci:mc_mode=aobmc:vsbmc=1:fps=120'"```


## Resizing Video
Resize to `width:height`
```-filter:v "scale=1920:1080"```

Preserve aspect ratio by constraining height to `720px` and using `-1` for width
```-filter:v "scale=-1:720"```


## Change Framerate
[Reference](https://trac.ffmpeg.org/wiki/ChangingFrameRate)

using the `-r` flag takes place after all filtering, but before encoding
`-r 30`


## Convert a directory

using [[shell#^cd49dd | loops]]

replacing the extnesion
```
for i in *.avi;
do 
  ffmpeg -i "$i" "${i%.*}.mp4";
done
```