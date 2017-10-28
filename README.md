> NOTE: Work-in-progess.  All feeds templates from the "classic" planet templates style need to get converted to embedded ruby (ERB)-style. 
>
> See [rss.xml.erb](https://github.com/gravitystorm/blogs.osm.org/blob/master/theme/rss.xml.erb)
> or [opml.xml.erb](https://github.com/gravitystorm/blogs.osm.org/blob/master/theme/opml.xml.erb) at the Open Street Map Blogs / Planet as working examples.


## Planet Planet <=> Pluto - Template Cheatsheet

    <TMPL_VAR name>                |  <%= site.title %>  or  <%= site.name %>
    <TMPL_VAR generator>           |  <%= Pluto.generator %>

    <TMPL_LOOP Channels>           |  <% site.feeds.each do |feed| %>
       <TMPL_VAR link>             |    <%= feed.url %>  or  <%= feed.link %>
       <TMPL_VAR name>             |    <%= feed.title %>  or  <%= feed.name %>
       <TMPL_VAR title>            |    <%= feed.title2 %>
       <TMPL_VAR url>              |    <%= feed.feed_url %>  or  <%= feed.feed %>
    </TMPL_LOOP>                   |  <% end %>

    <TMPL_LOOP Items>              |  <% items = site.items.latest.limit(24)
                                   |     ItemCursor.new( items ).each do |item,new_date,new_feed| %>
                                   |
      <TMPL_IF new_date>           |    <% if new_date %>
        <TMPL_VAR new_date>        |      <%= item.published %>
      </TMPL_IF>                   |    <% end %>
                                   |
      <TMPL_IF new_channel>        |    <% if new_feed %>
        <TMPL_VAR channel_link>    |      <%= item.feed.url %>  or  <%= item.feed.link %>
        <TMPL_VAR channel_name>    |      <%= item.feed.title %>  or  <%= item.feed.name %>
        <TMPL_VAR channel_title>   |      <%= item.feed.title2 %>
      </TMPL_IF>                   |    <% end %>
                                   |
      <TMPL_IF title>              |    <% if item.title %>
        <TMPL_VAR title>           |      <%= item.title %>
      </TMPL_IF>                   |    <% end %>
                                   |
      <TMPL_VAR content>           |    <% item.content %>
      <TMPL_VAR link>              |    <% item.url %>  or  <% item.link %>
      <TMPL_VAR date>              |    <% item.published %>
                                   |
      <TMPL_IF author>             |
        <TMPL_VAR author>          |    to be done
      </TMPL_IF>                   |
    </TMPL_LOOP>                   |  <% end %>

    <TMPL_VAR date>                |  <%= site.fetched %>     # site (planet) last updated


# `feeds` -  Pluto Template Pack - RSS 2.0, Atom, OPML, and Friends

## What's Pluto?

Pluto is a feed reader that lets you build web pages from published
web feeds. More [Pluto Project Site »](http://feedreader.github.io)



## Questions? Comments?

Send them along to the [wwwmake Forum/Mailing List](http://groups.google.com/group/wwwmake).
Thanks!
