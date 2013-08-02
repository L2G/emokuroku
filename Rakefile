require 'gemoji'
require 'yaml'

# Set BOWLDERIZE true to omit middle fingers and potty-mouthed language
BOWLDERIZE = false
NSFW = %w( fu shit )

theme = YAML.load_file('_themes.yml') 
#############################################################################
INDEX = 'index.html'

task INDEX => ['_themes.yml'] do
   unless uptodate?(INDEX, ['Rakefile', '_themes.yml']) 

      File.unlink(INDEX) if File.exist?(INDEX)
      File.open(INDEX, 'w') do |index|
         index.puts <<-END_HEAD
---
layout: default
title: emokuroku
---
<h1>Emokuroku</h1>
<p>An emoji catalog still in development. If it seems out of date by the time you get here, please try <a href="http://www.emoji-cheat-sheet.com/">Emoji Cheat Sheet</a>.</p>
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
   if (ENV['PORT'] and ENV['IP'])
      # Probably running on Cloud9
      system('rackup', '-o', ENV['IP'], '-p', ENV['PORT'])
   else
      system('bin/jekyll', '--server', '--auto')
   end
end

task :default => :site

#############################################################################
private

def generate_index_block(name, elements)
   out = "<h2>#{name}</h2>\n<div class='#{name.downcase.gsub(/ /,'_')}'>\n"

   elements.each do |element|
      out += "<table><caption>#{element}</caption><td>:#{element}:</td></table>\n"
   end
   out
end

# vim:ts=3:sw=3:et:
