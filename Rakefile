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

task :clean do
  Dir.glob('**/*.html').each do |file|
    File.unlink(file)
  end
end

task :deploy do
  system 'git checkout gh-pages'
  system 'git merge master'
  Rake::Task['clean'].invoke
  Rake::Task['doc'].invoke
  system 'git add **/*.html'
  system 'git commit -m "generate the HTML document"'
  system 'git push origin gh-pages'
  system 'git checkout japanese'
end