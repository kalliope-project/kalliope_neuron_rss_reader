# rss_reader

## Synopsis

This neuron access to a RSS feed and gives their items.

## Installation
```
kalliope install --git-url https://github.com/kalliope-project/kalliope_neuron_rss_reader.git
```

## Options

| parameter | required | default | choices | comment               |
|-----------|----------|---------|---------|-----------------------|
| feed_url  | YES      |         |         | Url of the feed.      |
| max_items | NO       | 30      |         | Max items to returns. |

## Return Values

| Name     | Description                                                                            | Type    | sample                          |
|----------|----------------------------------------------------------------------------------------|---------|---------------------------------|
| feed     | Title of the feed                                                                      | string  | The Verge                       |
| items    | A List with feed items (see [RSS spec](https://validator.w3.org/feed/docs/rss2.html))  | list    |                                 |

## Synapses example

Simple example. This is based on a file_template

```
  - name: "news-theVerge"
    signals:
      - order: "What are the news from the verge ?"
    neurons:
      - rss_reader:
          feed_url: "http://www.theverge.com/rss/index.xml"
          file_template: templates/en_rss.j2
          
```

A example with max items set to 10. This is based on a file_template
```
  - name: "news-sport"
    signals:
      - order: "What are the sport news ?"
    neurons:
      - rss_reader:
          feed_url: "https://sports.yahoo.com/top/rss.xml"
          max_items: 10
          file_template: templates/en_rss.j2    
```

Here the content of the `en_rss.j2`
```
Here's the news from {{ feed }}

{% set count = 1 %}
{% for item in items %}
News {{ count }}. {{ item.title }}.
{% set count = count + 1 %}
{% endfor %}
```
## Notes

## License

Copyright (c) 2016. All rights reserved.

Kalliope is covered by the MIT license, a permissive free software license that lets you do anything you want with the source code, 
as long as you provide back attribution and ["don't hold you liable"](http://choosealicense.com/). For the full license text see the [LICENSE.md](LICENSE.md) file.

