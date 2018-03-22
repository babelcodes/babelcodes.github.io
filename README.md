# babel.codes.github.io

Tower of Programming Languages

## Development

## Add new Feature

- Ensure it is present in the `/_config.yml/allFeatures` property (aka the reference list for the homepage)
- By default, the features of the list are mark as `unknown`
  - If a file `Language/Property.md` exists the property is `Supported`
  - To say that it is not the case for this language, copy the `JavaScript/Generics.md` file for your property 

## Setup

### Jekyll

Version 3.5.* bug!

```
gem uninstall jekyll
gem install jekyll -v 3.4.5
```

* Broken Links checkers
  * http://www.brokenlinkcheck.com/broken-links.php
  * http://www.smartinsights.com/search-engine-optimisation-seo/link-building/site-link-checking-tools/
  * `google3cbd8f0799f83e10.html` is for Google website checker
    * https://www.google.com/webmasters/tools/dashboard?hl=fr&siteUrl=http://ioskit.github.io/&authuser=0

https://github.com/Shopify/liquid/wiki/Liquid-for-Designers
https://docs.shopify.com/themes/liquid-documentation/filters/string-filters#split
http://alanwsmith.com/jekyll-liquid-date-formatting-examples

```
gem install jekyll-gist
```

### Troubleshooting

```
MacBook-Pro-de-Jacques:ioskit.github.io jacques$ jekyll serve --watch
/Users/jacques/.rvm/gems/ruby-2.2.0/gems/safe_yaml-1.0.4/lib/safe_yaml/psych_resolver.rb:4:in `<class:PsychResolver>': uninitialized constant Psych::Nodes (NameError)
	from /Users/jacques/.rvm/gems/ruby-2.2.0/gems/safe_yaml-1.0.4/lib/safe_yaml/psych_resolver.rb:2:in `<module:SafeYAML>'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/gems/safe_yaml-1.0.4/lib/safe_yaml/psych_resolver.rb:1:in `<top (required)>'
	from /Users/jacques/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems/core_ext/kernel_require.rb:69:in `require'
	from /Users/jacques/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems/core_ext/kernel_require.rb:69:in `require'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/gems/safe_yaml-1.0.4/lib/safe_yaml/load.rb:131:in `<module:SafeYAML>'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/gems/safe_yaml-1.0.4/lib/safe_yaml/load.rb:26:in `<top (required)>'
	from /Users/jacques/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems/core_ext/kernel_require.rb:69:in `require'
	from /Users/jacques/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems/core_ext/kernel_require.rb:69:in `require'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/gems/jekyll-3.3.1/lib/jekyll.rb:29:in `<top (required)>'
	from /Users/jacques/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems/core_ext/kernel_require.rb:69:in `require'
	from /Users/jacques/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems/core_ext/kernel_require.rb:69:in `require'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/gems/jekyll-3.3.1/exe/jekyll:6:in `<top (required)>'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/bin/jekyll:23:in `load'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/bin/jekyll:23:in `<main>'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/bin/ruby_executable_hooks:15:in `eval'
	from /Users/jacques/.rvm/gems/ruby-2.2.0/bin/ruby_executable_hooks:15:in `<main>'
```

You can do:

```
gem uninstall psych
gem install psych -v 2.0.5
```

### Versions:

- https://pages.github.com/versions/


## Run locally

```
jekyll serve
```

## Add new iOS version

* Replace current version in `/_config.xml#currentVersions`
* Update `_kits/*.md#status` and `_features/*.md#status`

# Resources

- http://jekyll.tips/jekyll-cheat-sheet/