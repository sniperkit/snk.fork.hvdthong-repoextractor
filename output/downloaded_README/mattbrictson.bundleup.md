# bundleup

[![Gem Version](https://badge.fury.io/rb/bundleup.svg)](http://badge.fury.io/rb/bundleup)
[![Build Status](https://travis-ci.org/mattbrictson/bundleup.svg?branch=master)](https://travis-ci.org/mattbrictson/bundleup)
[![Coverage Status](https://coveralls.io/repos/mattbrictson/bundleup/badge.svg?branch=master&service=github)](https://coveralls.io/github/mattbrictson/bundleup?branch=master)

**Run `bundleup` on a Ruby project containing a Gemfile to see what gem dependencies need updating.** It is a friendlier command-line interface to [Bundler’s][bundler] `bundle update` and `bundle outdated`.

You might like bundleup because it:

* shows you exactly what gems will be updated lets you decide whether to proceed
* uses color to call your attention to important gem updates (based on [Semver][])
* lets you know when a version "pin" in your Gemfile is preventing an update
* relies on standard Bundler output and does not patch code or use Bundler internals

Here it is in action:

<img src="https://raw.github.com/mattbrictson/bundleup/master/sample.png" width="599" height="553" alt="Sample output">


## Usage

Assuming you have a Ruby environment, all you need to do is install the bundleup gem:

```
gem install bundleup
```

Now, within a Ruby project you can run the bundleup command (the project needs to have a Gemfile and Gemfile.lock):

```
bundleup
```

That’s it!

Protip: Any extra command-line arguments will be passed along to `bundle update`. For example:

```
# Only upgrade development gems
bundleup --group=development
```

## How it works

bundleup starts by making a backup copy of your Gemfile.lock. Next it runs `bundle show`, then `bundle update` and `bundle show` again to find what gems versions are being used before and after Bundler does its updating magic. (Since gems are actually being installed into your Ruby environment during these steps, the process may take a few moments to complete, especially if gems with native extensions need to be compiled.)

Finally, bundleup runs `bundle outdated` to see the gems that were *not* updated due to Gemfile restrictions.

After displaying its findings, bundleup gives you the option of keeping the changes. If you answer "no", bundleup will restore your original Gemfile.lock from its backup, leaving your project untouched.


## Roadmap

bundleup is a very simple script at this point, but it could be more. Some possibilities:

* Automatically commit the Gemfile.lock changes with a nice commit message
* Integrate with bundler-audit to mark upgrades that have important security fixes
* Display relevant CHANGELOG entries for major upgrades
* Non-interactive mode

If you have other ideas, open an issue on GitHub!


## Contributing

Code contributions are also welcome! Read [CONTRIBUTING.md](CONTRIBUTING.md) to get started.


[bundler]: http://bundler.io
[Semver]: http://semver.org
