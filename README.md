# Lunamark Website
Started with the [Jekyll Incorporated](http://incorporated.sendtoinc.com) and [Landing Page](https://github.com/swcool/landing-page-theme) Jekyll themes but made some modifications to suit the needs for the company website.


## Installation & Usage
    bundle install
    jekyll serve --watch

_Note: Requires Ruby version 1.9.3 =>. For example use [rbenv](https://github.com/sstephenson/rbenv)_   
    
## Configuration
Edit: _config.yml (general options), main.css (theme colors &amp; fonts)

```
lunamark.github.io/
├── _config.yml
├── _assets/
    ├── stylesheets/
        ├── main.scss
```

_Note: when editing _config.yml, you need to restart jekyll to see the changes.__

    
## Publish to Github Pages
1. Add your domain to _CNAME_
2. Edit your repo address at _Rakefile_
    
Run rake task. **NOTE: It will deploy the generated site to _master_ branch overwriting it**    
``` 
rake site:publish
```

## Authors

Originally build for [sendtoinc.com](https://sendtoinc.com), your workspace for sharing and organizing knowledge by [Karri Saarinen](http://github.com/ksaa) and [Jori Lallo](http://github.com/jorilallo)

Modified by [Paul Gower](http://github.com/pmgower) to build the website for his company, [Lunamark](http://lunamark.com)

## Copyright and license

Copyright 2016 Lunamark LLC under [The MIT License ](LICENSE)


## Alternatives to get it working locally with `rbenv`
* Install and use rbenv to instsall ruby. (this was tested with 2.6.1)
* `bundle install` failed on `ffi` so had to upgrade that gem to 1.10.0
* Had to use `bundle exec jekyll serve --watch` to get it to work rather than just `jeckyll serve --watch`
* Had to use `bundle exec rake site:publish` rather than just `rake site:publish`
