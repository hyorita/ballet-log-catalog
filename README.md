# Ballet Log — Ballet Class Music Catalog

A curated catalogue of ballet class accompanists and their albums, published as static JSON
for the [Ballet Log](https://apps.apple.com/us/app/ballet-log/id6759671182) iOS app.

Ballet class music is a small, scattered corner of the catalogue on every streaming service.
Pianists who accompany class release steadily — often a volume a year, sometimes one a month —
but the recordings are hard to find unless you already know whose name to search for, and
national storefronts rarely surface accompanists working in other countries. This catalogue
exists to make those recordings findable.

## Endpoints

```
https://hyorita.github.io/ballet-log-catalog/v1/catalog.json
https://hyorita.github.io/ballet-log-catalog/v1/albums/<albumId>.json
```

`catalog.json` is the index — artists and albums with cover art and links.
Track listings and 30-second previews live in the per-album files, fetched on demand.

The `v1/` path is part of the contract. Breaking changes ship under a new prefix so that
older app versions keep reading the schema they were built against.

## Shape

```jsonc
// catalog.json
{
  "schemaVersion": 1,
  "catalogVersion": 1,
  "artists": [{
    "id": "andrew-holdsworth",
    "appleArtistIds": [364757357],     // an artist can be split across several Apple IDs
    "name": "Andrew Holdsworth",
    "affiliation": { "en": "London · music for the RAD syllabuses" },
    "note": { "en": "The largest catalogue in the field, and still releasing." },
    "kind": "classical",
    "albumCount": 41,
    "latestRelease": "2026-08-24"
  }],
  "albums": [{
    "id": "1849364374",
    "artistId": "andrew-holdsworth",
    "title": "Music for Ballet Class - Repertoire, Vol. 4",
    "releaseDate": "2026-08-24",
    "artwork": "https://is1-ssl.mzstatic.com/.../600x600bb.jpg",
    "appleUrl": "https://music.apple.com/...",
    "level": ["advanced"],
    "part": ["barre", "centre"],
    "themes": ["repertoire"]
  }]
}
```

```jsonc
// albums/1849364374.json
{
  "albumId": "1849364374",
  "tracks": [{
    "id": 1849364375,
    "n": 1,
    "title": "Sleeping Beauty, Op 66: Sarabande Blues (Warm Up on a Very Slow Swung 3)",
    "seconds": 133,
    "preview": "https://audio-ssl.itunes.apple.com/...",
    "exercise": "warmup",     // parsed from the title; null when it can't be determined
    "meter": "3/4",           // parsed; usually null
    "counts": "16x8"          // parsed; rarely present
  }]
}
```

`exercise` is one of `warmup` `plie` `tendu` `degage` `rond-de-jambe` `fondu` `frappe`
`developpe` `petit-battement` `grand-battement` `stretch` `port-de-bras` `adagio`
`pirouette` `allegro` `petit-allegro` `grand-allegro` `echappe` `variation` `coda`
`reverence`. Track titles in this repertoire usually name the exercise they were written
for, which is what makes the catalogue searchable by movement rather than only by title.

## Source and rights

Album metadata, cover art URLs and preview URLs come from the public iTunes Search API.
No API key is involved and nothing is scraped.

**Cover art is not redistributed here.** The `artwork` field is a URL to Apple's own CDN;
clients load it directly from Apple and display it alongside a link to Apple Music.
Audio is likewise never copied — `preview` points at Apple's 30-second preview asset.

## Corrections

Details about a working musician should be right. If an affiliation, name, or album
listing here is wrong — or if you are one of these musicians and would rather not be
listed — please open an issue and it will be corrected or removed.

## Selection

Artists are chosen by hand: people who actually accompany ballet class, with a catalogue
worth browsing, across as many countries and teaching traditions as can be found. It is
not a ranking, and it is not automated — album count in particular is a poor guide to
what is worth hearing.
