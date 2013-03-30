require 'gemoji'

INDEX = 'index.html'

task :index do
   File.unlink(INDEX) if File.exist?(INDEX)
   File.open(INDEX, 'w') do |index|
      index.puts <<-END_HEAD
---
layout: default
title: emokuroku
---
<table>
      END_HEAD
      Emoji.names.each_with_index do |name|
         index.puts "<tr><td>#{name}</td><td>:#{name}:</td></tr>"
      end
   end
end

desc "Build the site"
task :site => ['_site']

directory '_site'
file '_site' => [INDEX] do
   system('bin/jekyll')
end

task :default => :site
