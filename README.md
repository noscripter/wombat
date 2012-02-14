# Wombat

[![CI Build Status](https://secure.travis-ci.org/intridea/omniauth.png?branch=master)](http://travis-ci.org/felipecsl/wombat)

Generic Web crawler with a DSL that parses structured data from web pages.

## Usage:

``gem install wombat``

Creating a crawler:

```ruby

# => github_crawler.rb

#coding: utf-8
require 'wombat'

class GithubCrawler
  include Wombat::Crawler

  base_url "http://www.github.com"
  list_page "/"

  headline "xpath=//h1"

  what_is "css=.column.secondary p", :html

  explore "xpath=//ul/li[2]/a" do |e|
    e.gsub(/Explore/, "LOVE")
  end

  benefits do |b|
    b.first_benefit "css=.column.leftmost h3"
    b.second_benefir "css=.column.leftmid h3"
    b.third_benefit "css=.column.rightmid h3"
    b.fourth_benefit "css=.column.rightmost h3"
  end
end
```

Running it:

```ruby
irb> GithubCrawler.new.crawl
   => 
   {
      "headline" => "1,316,633 people hosting over 3,951,378 git repositories", 
      "what_is" => "GitHub is the best way to collaborate with others.  Fork, send pull requests and manage all your <strong>public</strong> and <strong>private</strong> git repositories.",
      "explore" => "LOVE GitHub",
      "benefits" => {
        "first_benefit"  => "Team management", 
        "second_benefit" => "Code review", 
        "third_benefit"  => "Reliable code hosting", 
        "fourth_benefit" => "Open source collaboration"
      }
    }
```

### More advanced constructs like loops, following links, callbacks, etc. to be added/documented soon.


## Contributing to Wombat
 
 * Check out the latest master to make sure the feature hasn't been implemented or the bug hasn't been fixed yet
 * Check out the issue tracker to make sure someone already hasn't requested it and/or contributed it
 * Fork the project
 * Start a feature/bugfix branch
 * Commit and push until you are happy with your contribution
 * Make sure to add tests for it. This is important so I don't break it in a future version unintentionally.
 * Please try not to mess with the Rakefile, version, or history. If you want to have your own version, or is otherwise necessary, that is fine, but please isolate to its own commit so I can cherry-pick around it.

## Copyright

Copyright (c) 2011 Felipe Lima. See LICENSE.txt for further details.

