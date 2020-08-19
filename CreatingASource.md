# Creating an online Source for Aerial

Creating an online source for Aerial requires two files. In order to get started, we recommend you check some of the sources available already in Aerial by going into Settings > Advanced, then clicking Show in Finder at the bottom. This will open Aerial's work directory, inside you will find the various sources currently in use, they contain each a `manifest.json` that contains general information about the source, and `entries.json` that contains information about your videos. 

## Source manifest format (manifest.json)

A source looks like this : 

```
{
      "name": "The name of your source",
      "description": "The description of your source",
      "scenes": [
        "landscape"
      ],
      "manifestUrl": "https://link/to/your/entries.json",
      "license": "https://link/to/your/licence",
      "more": "https://link/to/more/content/from/you",
      "local": false,
      "cacheable": true
}
```

Some fields are self explanatory, like name and description. For the others:
- scenes: an array that contains the scene type, individual types can be `landscape`, `city`, `countryside`, `space`, `sea`, `beach`
- manifestUrl: The online URL to your entries.json (see below)
- license: Optional, a link to your license file, if needed
- more: Optional, a link to more content from you, if needed
- local: false <- This is mandatory for an online source
- cacheable: can be true or false. If set to false, your videos will be part of the user's cache, and depending on their settings, they may periodically redownload your videos. If set to false, videos will not be part of the cache and be stored by Aerial in your source folder, they will not be deleted by cache rotation. We recommend you use true, if not, be congniscent of the fact you will be using what could be significant disk space from your users machines. 

## Video manifest format (entries.json)

Includes an array of objects for each video, each individual video looks like this (for the general structure, refer to an example on your machine) :

```
{
    "accessibilityLabel":"Video Location",
    "title":"Video Title",
    "timeOfDay":"sunset",
    "scene":"city",
    "id":"a_unique_id_for_your_video",
    "url-1080-H264":"https://your/video-1080-h264.mov",
    "url-1080-SDR":"https://your/video-1080-sdr.mov",
    "url-1080-HDR":"https://your/video-1080-hdr.mov",
    "url-4K-SDR":"https://your/video-4k-sdr.mov",
    "url-4K-HDR":"https://your/video-4k-hdr.mov",
    "pointsOfInterest" : {
      "0" : "Something interesting about your video happening at 0 seconds"
    }
},
```

This requires a bit more explanation : 
- accessibilityLabel: This is the "City"/"Country" name that will appear in the Sidebar
- title: This is the title that appears in the middle column below your video thumbnail
- timeOfDay: When was your video shot, can be `day`, `night`, `sunset`, `sunrise`
- scene: one of the scene types for that specific video (see above for the list)
- id: This must be a completely unique ID, not just to you but to everyone. So no "video1", we recommend you use a [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier).
- urls: Aerial can handle up to 5 video formats that mix 1080p/4K, H.264/HEVC, and SDR/HDR. You need at least one format, we **strongly** recommend to always at least have the lowest format available for compatibility purposes. 
- pointsOfInterest: An object that contains the various information that are shown while the video plays. The key is time in seconds, the value, the text. In the example above, only one poi will show at video start. You can have several, there **must** be at least 10 seconds between two points of interest. 

## Adding your source to Aerial

We highly recommend you use a JSON validator to make sure both files are valid, if they aren't, you won't be able to import your source. When you are confident you got it right, use the Add Online button in Settings > Sources and paste the link to your `manifest.json`, minus the `manifest.json`. 

If your file is at `https://my.aerial.videos/mynicesource/manifest.json`, then paste `https://my.aerial.videos/mynicesource/` to import your source. 

Remember that you can refer to the examples at the top of this repository.

