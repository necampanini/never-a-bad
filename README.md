12.27.2014  --  0:34:42

Outlining the steps I've taken so far:

I've made an empty repo on github, logged into travis-ci and let it watch that specific repo.

(Aside: since the repo was private, travis-ci is using the trial pro version)

I pulled that repo down, and did a fresh jekyll install with:

gem install jekyll

This populated most of the project directory.

On github: went to 'Settings' of never-a-bad repo, and under Services checked travis-ci.

Next was adding a .travis.yml file, to tell travis what to do. In this case, it was bundle install and jekyll install.

travis-ci has a web app linter to validate the .travis.yml file. use this!

Next a simple Gemfile (capitalization counts) in the root directory. source and a single gem is all that was needed to have travis test running.

Note: the gemfile was issue3, and his readme was issue2. Whoops.
