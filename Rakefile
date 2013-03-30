require 'gemoji'

# Set BOWLDERIZE true to omit middle fingers and potty-mouthed language
BOWLDERIZE = true

NSFW = %w( fu shit )

theme = {
    'Zodiac' => %w(
        aries taurus gemini cancer leo virgo libra scorpio sagittarius capricorn
        aquarius pisces
    )
}

#############################################################################
INDEX = 'index.html'

task INDEX do
   unless uptodate?(INDEX, ['Rakefile']) 

      File.unlink(INDEX) if File.exist?(INDEX)
      File.open(INDEX, 'w') do |index|
         index.puts <<-END_HEAD
---
layout: default
title: emokuroku
---
<table>
         END_HEAD

         emoji_list = Emoji.names
         emoji_list -= NSFW if BOWLDERIZE

         emoji_list.each_slice(5) do |row|
            index.print '<tr>'
            row.each do |name|
               index.print "<td>:#{name}:</td>"
            end
            index.puts '</tr>'
            index.print '<tr>'
            row.each do |name|
               index.print "<td>#{name}</td>"
            end
            index.puts '</tr>'
         end

         index.puts '</table>'
      end
   end
end

desc "Build the site"
task :site do
   Rake::Task[INDEX].execute
   system('bin/jekyll')
end

desc "Run a local server"
task :server do
   Rake::Task[INDEX].execute
   system('bin/jekyll', '--server')
end

task :default => :site

# vim:sw=3:
