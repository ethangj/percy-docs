# Percy command-line interface [<i class="fa fa-github" aria-hidden="true"></i>](https://github.com/percy/percy-cli)

[![](https://travis-ci.org/percy/percy-cli.svg?branch=master)](https://travis-ci.org/percy/percy-cli)
[![](https://badge.fury.io/rb/percy-cli.svg)](https://rubygems.org/gems/percy-cli)

Percy makes it very simple to integrate visual diff testing with **static websites**, no matter where the site is hosted or what tools were used to generate it.

This can be especially useful for static sites generated by [Jekyll](http://jekyllrb.com/) (ie. for GitHub Pages), [Grow](http://growsdk.org), or any other static site generator.

## Installation

First, install the Percy command-line client:

```bash
$ gem install percy-cli
```

If you already have the client installed, you can update your old version by running:

```bash
$ gem update percy-cli
```

## Authentication

Percy CLI relies on the `PERCY_TOKEN` environment variable for authenticating and authorizing access to each repository.

You can temporarily set this in your local shell session by exporting the variable:

```bash
$ export PERCY_TOKEN=aaabbbcccdddeeefff
$ percy snapshot _site/
```

Or you can set it just for the current command:

```bash
$ PERCY_TOKEN=aaabbbcccdddeeefff percy snapshot _site/
```

<div class="Alert Alert--warning">
  <strong>IMPORTANT: Keep your Percy token secret.</strong> Anyone with access to your token can consume your account quota. They will not be able to read data because the token is write-only.

  See the <strong>Setup</strong> guides for how to securely set environment variables in your CI service.
</div>

## Usage

If your static site exists in a directory called `_site`, it's as simple as this:

```bash
$ percy snapshot _site/
```

That's it!

For example:

```bash
$ percy snapshot _site/
Creating build...
Uploading build resources...
Uploading snapshot (1/3): /index.html
Uploading snapshot (2/3): /404.html
Uploading snapshot (3/3): /about/index.html
Finalizing build...
Done! Percy is now processing, you can view the visual diffs here:
https://percy.io/fotinakis/percy-examples/builds/140
```

Percy now starts rendering pages and generating visual diffs for your site.

Under the hood, Percy only uploads files that have changed. So, after the first time this command is run, future runs will likely be very fast.

### Responsive testing

Pass the `--widths` flag with a comma-separated list of widths.

```bash
$ percy snapshot --widths "375,1280" _site/
```

### Limit pages for testing

If you have a very large site, you might want to limit the number of pages that are actually uploaded to Percy while testing. You can pass the `snapshot_limit` flag to do this:

```bash
$ percy snapshot _site/ --snapshot_limit 10
```

### Base URL path

If your static files are hosted in a sub-directory instead of the webserver root, you will need to provide the `--baseurl` flag:

```bash
$ percy snapshot _site/ --baseurl "/my-subdir"
```

For Jekyll users, this should be set to the same as your `baseurl` config setting.

### Responsive visual diffs

See [responsive visual diffs](/docs/integrations/responsive) for how to test responsive designs in Percy.

## Changelog

*   [percy-cli releases on GitHub](https://github.com/percy/percy-cli/releases)

## Contributing

1.  Fork it ([https://github.com/percy/percy-cli/fork](https://github.com/percy/percy-cli/fork))
2.  Create your feature branch (`git checkout -b my-new-feature`)
3.  Commit your changes (`git commit -am 'Add some feature'`)
4.  Push to the branch (`git push origin my-new-feature`)
5.  Create a new Pull Request