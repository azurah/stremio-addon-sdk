## Meta Object

Used as a response for [`defineMetaHandler`](../requests/defineMetaHandler.md)

``id`` - **required** - string, universal identifier; you may use a [prefix](./manifest.md##filtering-properties) unique to your add-on, for example `yt_id:UCrDkAvwZum-UTjHmzDI2iIw`

``type`` - **required** - string, type of the content; e.g. `movie`, `series`, `channel`, `tv` (see [Content Types](./content.types.md))

``name`` - **required** - string, name of the content

``genres`` - _optional_  - array of strings, genre/categories of the content; e.g. ``["Thriller", "Horror"]``

``poster`` - _optional_ - string, URL to png of poster; accepted aspect ratios: 1:0.675 (IMDb poster type) or 1:1 (square) ; you can use any resolution, as long as the file size is below 100kb; below 50kb is recommended

``posterShape`` - _optional_ - string, can be `square` (1:1 aspect) or `regular` (1:0.675) or `landscape` (1:1.77). If you don't pass this, `regular` is assumed

``background`` - _optional_ - string, the background shown on the stremio detail page ; heavily encouraged if you want your content to look good; URL to PNG, max file size 500kb

``logo`` - _optional_ - string, the logo shown on the stremio detail page ; encouraged if you want your content to look good; URL to PNG

``description`` - _optional_ - string, a few sentances describing your content

``releaseInfo`` - _optional_ - string, year the content came out ; if it's ``series`` or ``channel``, use a start and end years split by a tide - e.g. ``"2000-2014"``. If it's still running, use a format like ``"2000-"``

``director``, ``cast`` - _optional_  - directors and cast, both arrays of names (string)

``imdbRating`` -  _optional_ - string, IMDb rating, a number from 0.0 to 10.0 ; use if applicable

``dvdRelease`` - _optional_ - string, DVD release date

``released`` - _optional_ - string, ISO 8601, initial release date; for movies, this is the cinema debut, e.g. "2010-12-06T05:00:00.000Z"

``inTheaters`` - _optional_ - boolean, used only for ``movie`` type, whether this movie is still in theaters or not; if not provided, it will be decided based on ``released`` date

``videos`` - _optional_ - array of [``Video objects``](#video-object), used for ``channel`` and ``series``; if you do not provide this (e.g. for ``movie``), Stremio assumes this meta item has one video, and it's ID is equal to the meta item `id`

``certification`` - _optional_ - string, [MPAA rating](http://www.mpaa.org/film-ratings/) - can be "G", "PG", "PG-13", "R", "NC-17"

``runtime`` - _optional_ - string, human-readable expected runtime - e.g. "120m"

``language`` - _optional_ - string, spoken language

``country`` - _optional_ - string, official country of origin

``awards`` - _optional_ - string, human-readable that describes all the significant awards

``website`` - _optional_ - string, URL to official website


#### Video object

``id`` - **required** - string, ID of the video

``title`` - **required** - string, title of the video

``released`` - **required** - string, ISO 8601, publish date of the video; for episodes, this should be the initial air date, e.g. "2010-12-06T05:00:00.000Z"

``thumbnail`` - _optional_ - string, URL to png of the video thumbnail, in the video's aspect ratio, max file size 5kb

``streams`` - _optional_ - array of [``Stream Objects``](./stream.md), in case you can return links to streams while forming meta response, **you can pass and array of [``Stream Objects``](./stream.md)** to point the video to a HTTP URL, BitTorrent, YouTube or any other stremio-supported transport protocol; note that this is exclsuive: passing `video.streams` means that **Stremio will not** request any streams from other add-ons for that video; if you return streams that way, it is still recommended to implement the `streams` resource

``available`` - _optional_ - boolean, set to ``true`` to explicitly state that this video is available for streaming, from your add-on; no need to use this if you've passed ``stream``

``episode`` - _optional_ - number, episode number, if applicable

``season`` - _optional_ - number, season number, if applicable

``trailer`` - _optional_ - string, YouTube ID of the trailer video; use if this is an episode for a series

``overview`` - _optional_ - string, video overview/summary


##### Video object - series example

```javascript
{
    id: "tt0108778:1:1",
    title: "Pilot",
    released: new Date("1994-09-22 20:00 UTC+02"),
    season: 1,
    episode: 1,
    overview: "Monica and the gang introduce Rachel to the real world after she leaves her fiancé at the altar."
}
```

You can see a comprehensive example of how detailed Meta objects with videos are returned [here, on the Cinemeta add-on](https://v3-cinemeta.strem.io/meta/series/tt0386676/lastVideos=1.json)

##### Video object - YouTube video example (channels)


```javascript
{
    id: "yt_id:UCrDkAvwZum-UTjHmzDI2iIw:9bZkp7q19f0",
    title: "PSY - GANGNAM STYLE",
    released: new Date("2012-07-15 20:00 UTC+02"),
    thumbnail: "https://i.ytimg.com/vi/9bZkp7q19f0/hqdefault.jpg"
}
```

## Meta Preview Object

This is a shorter variant of the previously described [Meta Object](#meta-object)

Used as a response for [`defineCatalogHandler`](../requests/defineCatalogHandler.md)

``id`` - **required** - string, universal identifier; you may use a [prefix](./manifest.md##filtering-properties) unique to your add-on, for example `yt_id:UCrDkAvwZum-UTjHmzDI2iIw`

``type`` - **required** - string, type of the content; e.g. `movie`, `series`, `channel`, `tv` (see [Content Types](./content.types.md))

``name`` - **required** - string, name of the content

``poster`` - **required** - string, URL to png of poster; accepted aspect ratios: 1:0.675 (IMDb poster type) or 1:1 (square) ; you can use any resolution, as long as the file size is below 100kb; below 50kb is recommended

``posterShape`` - _optional_ - string, can be `square` (1:1 aspect) or `regular` (1:0.675) or `landscape` (1:1.77). If you don't pass this, `regular` is assumed

``background`` - _optional_ - string, the background shown on the stremio detail page ; heavily encouraged if you want your content to look good; URL to PNG, max file size 500kb

``logo`` - _optional_ - string, the logo shown on the stremio detail page ; encouraged if you want your content to look good; URL to PNG

``description`` - _optional_ - string, a few sentances describing your content

