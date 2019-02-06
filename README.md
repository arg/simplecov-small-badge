# SimpleCovSmallBadge

[![Build Status](...)](...)
[![Depfu](...)](...)
![Coverage]()

*SimpleCovBadge* is a gem that can be added to the `Gemfile` and will produce a file called `coverage_badge.png` in the `coverage` directory.
It could be looking as follows dependent on how it is configured.

...

The idea is to created a badge for [SimpleCov](https://github.com/colszowka/simplecov) to create a persistable image that shows the coverage in percent as a badge.

## Installation

The badge creation is dependent on the [MiniMagic gem](https://github.com/colszowka/simplecov) which requires the [ImageMagick](http://www.imagemagick.org/index.php) software.
It can be installed in your Ruby library or rails app as part of the `Gemfile` as follows.

```
# In your gemfile
gem 'simplecov-small-badge', :require => false
```

This gem is an alternative and inspired by the great work in the other gem [simplecov-badge](https://github.com/matthew342/simplecov-badge) which does a similar badge but looks different and cannot easily made small. So it's mostly an optical alternative.

## Usage

Whereever you are integrating `SimpleCov` you can configure the `SimpleCovSmallBadge` gem as any formater can be configured. The default integration could looks as follows:

```
# Wherever your SimpleCov.start block is (spec_helper.rb, test_helper.rb, or .simplecov)
SimpleCov.start do
	require 'simple-cov-small-badge'
	# add your normal SimpleCov configs
	add_filter "/app/model"
	# configure any options you want for SimpleCov::Formatter::BadgeFormatter
	SimpleCovSmallBadge.configure do |config|
      # switches on logging for convert
      config.log_level = 'debug'
      # does not created rounded borders
      config.rounded_border = false
      # set the background for the title to darkgrey
      config.background_color = 'darkgrey'
    end
	# call SimpleCov::Formatter::BadgeFormatter after the normal HTMLFormatter
	SimpleCov.formatter = SimpleCov::Formatter::MultiFormatter[
		SimpleCov::Formatter::HTMLFormatter,
		SimpleCovSimpleBadge::Formatter,
	]
end
```

## Integration into CI via github-pages

See [SimpleCovBadge - if you want to store your coverage in github pages](https://github.com/matthew342/simplecov-badge#if-you-want-to-store-your-coverage-reports-in-github-pages)

## Configuration Options

The behaviour of `SimpleCovBadge` can be influenced by configuration options. 

## Development

After checking out the repo, run `bundle update` to install dependencies. Then, run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release` to create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

1. Fork it ( https://github.com/marcgrimme/simplecov_small_badge/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request