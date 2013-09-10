task :default => :doc

task :doc do
  Dir.glob('**/*.txt').each do |src|
    Dir.chdir(File.dirname(src)) do
      src = File.basename(src)
      dest = src.sub(/\.txt/, '.html')
      if !File.exist?(dest) or File.mtime(src) > File.mtime(dest)
        sh "bundle exec mizuho -a max-width=55em --icons-dir \"../../icons\" \"#{src}\" -o \"#{dest}\""
      end
    end
  end
end
