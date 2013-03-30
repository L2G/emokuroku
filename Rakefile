require 'gemoji'

# Set BOWLDERIZE true to omit middle fingers and potty-mouthed language
BOWLDERIZE = false

NSFW = %w( fu shit )

theme = {
    'Zodiac' => %w(
        aries taurus gemini cancer leo virgo libra scorpius sagittarius
        capricorn aquarius pisces
    ),
    'Ideographs' => %w(
        accept congratulations secret
        koko sa
        u5272 u5408 u55b6 u6307 u6708 u6709 u6e80 u7121 u7533 u7981 u7a7a
        white_flower ideograph_advantage
    ),
    'Hands' => %w(
        +1 -1
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
         END_HEAD

         emoji_list = Emoji.names
         emoji_list -= NSFW if BOWLDERIZE

         theme.each_pair do |name, theme_elements|
            index.print generate_index_block(name, theme_elements)
            emoji_list = emoji_list - theme_elements
         end

         index.print generate_index_block('Unclassified emoji', emoji_list)
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

#############################################################################
private

def generate_index_block(name, elements)
   out = "<h2>#{name}</h2>\n"

   elements.each do |name|
      out += "<table><caption>#{name}</caption><td>:#{name}:</td></table>\n"
   end
   out
end

# vim:ts=3:sw=3:et:
