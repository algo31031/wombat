# Wombat

[[![Gem Version](https://badge.fury.io/rb/wombat.png)](http://badge.fury.io/rb/wombat)][rubygems] [![CI Build Status](https://secure.travis-ci.org/felipecsl/wombat.png?branch=master)][travis] [![Dependency Status](https://gemnasium.com/felipecsl/wombat.png?travis)][gemnasium] [![Code Climate](https://codeclimate.com/github/felipecsl/wombat.png)][codeclimate] [![Coverage Status](https://coveralls.io/repos/felipecsl/wombat/badge.png?branch=master)][coveralls]

[rubygems]: http://rubygems.org/gems/wombat
[travis]: http://travis-ci.org/felipecsl/wombat
[gemnasium]: https://gemnasium.com/felipecsl/wombat
[codeclimate]: https://codeclimate.com/github/felipecsl/wombat
[coveralls]: https://coveralls.io/r/felipecsl/wombat?branch=master

Web scraper with an elegant DSL that parses structured data from web pages.

## Usage:

``gem install wombat``

Obs: Requires ruby 1.9.3 (activesupport requires Ruby version >= 1.9.3)

## Scraping a page:

The simplest way to use Wombat is by calling ``Wombat.crawl`` and passing it a block:

```ruby
require 'wombat'

Wombat.crawl do
  base_url "https://www.github.com"
  path "/"

  headline xpath: "//h1"
  subheading css: "p.subheading"

  what_is({ css: ".one-half h3" }, :list)

  links do
    explore xpath: '//*[@class="wrapper"]/div[1]/div[1]/div[2]/ul/li[1]/a' do |e|
      e.gsub(/Explore/, "Love")
    end

    features css: '.features'
    enterprise css: '.enterprise'
    blog css: '.blog'
  end
end
```

###### The code above is gonna return the following hash:

```ruby
{
  "headline"=>"Build software better, together.", 
  "subheading"=>"Powerful collaboration, code review, and code management for open source and private projects. Need private repositories? Upgraded plans start at $7/mo.", 
  "what_is"=>[
    "Great collaboration starts with communication.", 
    "Friction-less development across teams.", 
    "World's largest open source community.", 
    "Do more with powerful integrations."
  ], 
  "links"=>{
    "explore"=>"Love", 
    "features"=>"Features", 
    "enterprise"=>"Enterprise", 
    "blog"=>"Blog"
  }
}
```

### This is just a sneak peek of what Wombat can do. For the complete documentation, please check the links below:

### [Wiki](http://github.com/felipecsl/wombat/wiki)
### [API Documentation](http://rubydoc.info/gems/wombat/2.1.1/frames)
### [Changelog](https://github.com/felipecsl/wombat/wiki/Changelog)

## Contributing to Wombat

 * Check out the latest master to make sure the feature hasn't been implemented or the bug hasn't been fixed yet
 * Check out the issue tracker to make sure someone already hasn't requested it and/or contributed it
 * Fork the project
 * Start a feature/bugfix branch
 * Commit and push until you are happy with your contribution
 * Make sure to add tests for it. This is important so I don't break it in a future version unintentionally.
 * Please try not to mess with the Rakefile, version, or history. If you want to have your own version, or is otherwise necessary, that is fine, but please isolate to its own commit so I can cherry-pick around it.

## Contributors

 * Felipe Lima ([@felipecsl](https://github.com/felipecsl))
 * [List of all contributors](https://github.com/felipecsl/wombat/wiki/Contributors)

## Copyright

Copyright (c) 2012 Felipe Lima. See LICENSE.txt for further details.

