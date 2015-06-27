#################
# To depoloy:
# $ jkb # => build the website
# $ gaa
# $ gcm "Message"
# $ rake
#################
# New post:
# $ rake post:new
# (you will be prompted to enter post name)
#################

require "rubygems"
require "tmpdir"
require "bundler/setup"
require "jekyll"
require "paint"

GITHUB_REPONAME = "gbanis/gbanis.github.io"
STOPWORDS = %w(i a about an are as at be by com for from how in is it of on or that the this to was what when where who will with the www)

namespace :new do
  task :post do
    desc "Creates a new blog post in _drafts folder"
    STDOUT.print "Enter post name:\n> "
    post_name = STDIN.gets.chomp
    post_slug = post_name
      .gsub(/how to/i, "howto")
      .gsub(/[^a-zA-Z ]/,'').gsub(/ +/,' ') # remove special characters and double spaces
      .split(" ")
      .map { |word| word.downcase }
      .keep_if { |word| !STOPWORDS.index(word) }
      .join("-")
    current_date = Time.now.getutc.strftime("%Y-%m-%d")
    file_path = "_posts/#{current_date}-#{post_slug}.md"
  `echo '---
layout:       post
title:        "#{post_name}"
description:  "Enter description"
date:         #{current_date} 12:00:00
tags:
  - enter tag
  - enter tag
author:       George Banis
---' > #{file_path}`
  end

  task :slides do
    desc "Creates a new slide in _drafts folder"
    STDOUT.print "Enter slide name:\n> "
    post_name = STDIN.gets.chomp
    post_slug = post_name
      .gsub(/how to/i, "howto")
      .gsub(/[^a-zA-Z ]/,'').gsub(/ +/,' ') # remove special characters and double spaces
      .split(" ")
      .map { |word| word.downcase }
      .keep_if { |word| !STOPWORDS.index(word) }
      .join("-")
    current_date = Time.now.getutc.strftime("%Y-%m-%d")
    file_path = "_posts/#{current_date}-#{post_slug}.html"
  `echo '---
layout:       slide
title:        "#{post_name}"
description:  "ENTER A DESCRIPTION HERE (150-160 CHARACTERS"
date:         #{current_date} 12:00:00
tags:
  - slides
  - enter tag
  - enter tag
author:       George Banis
---
<section data-markdown>
  <script type="text/template">
    Slide content in Markdown
  </script>
</section>
' > #{file_path}`
  end
end

namespace :site do
  desc "Generate blog files"
  task :generate do
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site"
    })).process
  end

  desc "Generate and depoloy: blog to master branch, source files to source branch"
  task :depoloy => [:generate] do
    # Commit your site files on master branch
    Dir.mktmpdir do |tmp|

      puts Paint["Creating temp dir with site files...", :yellow]
      cp_r "_site/.", tmp # Create temporary dir with _site files
      pwd = Dir.pwd # Save current dir
      Dir.chdir tmp # Change to temp dir
      puts Paint["[Done]\n", :green]

      puts Paint["Initializing repo...", :yellow]
      system "git init"
      puts Paint["[Done]\n", :green]

      puts Paint["Setting local user to: 'George Banis - gbanis@gmail.com'...", :yellow]
      system "git config --local user.name 'George Banis'"
      system "git config --local user.email 'gbanis@gmail.com'"
      puts Paint["[Done]\n", :green]

      puts Paint["Committing changes to git...", :yellow]
      system "git add ."
      puts "test"
      message = "Site updated at #{Time.now.utc}"
      system "git commit -m #{message.inspect}"
      puts Paint["[Done]\n", :green]

      puts Paint["Pushing (--force) to 'git@github.com-gbanis:#{GITHUB_REPONAME}.git'...", :yellow]
      system "git remote add origin git@github.com-gbanis:#{GITHUB_REPONAME}.git"
      system "git push origin master:refs/heads/master --force"
      puts Paint["[Done]\n", :green]

      # Change back to the original directory
      Dir.chdir pwd
    end
  end
end

task :default => ["site:depoloy"]

# Inspired by: http://ixti.net/software/2013/01/28/using-jekyll-plugins-on-github-pages.html
