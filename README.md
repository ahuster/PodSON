# PodSON

PodSON is a JSON-like format for podcast subscription and progress portability. It was designed to build off the commonly used OPML format to provide a specification that was purpose-built for sharing podcasts between podcast apps.



## Format

PodSON is valid JSON.

Every PodSON file contains a list of podcasts, contained in the `"podcasts":` array.

Each podcast includes the following elements:

- `podcast`, the name of the podcast
- `feedUrl`, the URL to the RSS feed
- `siteUrl`, the URL to the podcast website
- `subscribed`, a boolean that defines whether a podcast is actively subscribed to (i.e., if new episodes are automatically downloaded). If a podcast app does not have a mechanism to "unsubscribe" from podcasts without removing them entirely, it can ignore this element.
- `episodes`, an array of the currently-downloaded episodes of the podcast in the podcast app that generated the PodSON file

Episodes contain two elements:

- `guid`, the defined GUID of the episode from the RSS feed. This can either be a permalink or an actual GUID. The podcast app that is parsing the PodSON file should use the GUID to find the referenced episode in the podcast's RSS feed
- `playbackTime`, the current time that the podcast was most recently paused at, in HH:MM:SS format. The podcast app that is parsing the PodSON file should parse this element to import podcast listening progress from the other app.



## Example

The following example is valid PodSON (and JSON). It can also be found in this repository at `podcasts.podson`. 

```json
{
  "title": "Overcast Podcast Subscriptions",
  "podcasts": [
    {
      "podcast": "Do By Friday",
      "feedUrl": "https://rss.simplecast.com/podcasts/2389/rss",
      "siteUrl": "http://dobyfriday.com",
      "subscribed": "true",
      "episodes": [
        {
          "guid": "3fac534b-abbf-443a-b805-eb43ecec4e7f",
          "playbackTime": "00:40:34"
        },
        {
          "guid": "096466bb-2ee0-4018-a69e-ba4ee6e8420d",
          "playbackTime": "00:30:49"
        }
      ]
    }
  ]
}
```

