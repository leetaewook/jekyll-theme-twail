require "rubygems"
require "tmpdir"
require "bundler/setup"
require "jekyll"

# TODO: Write your Github Repository name
GITHUB_REPONAME = "leetaewook/jekyll-theme-twail"

desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end

desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp

    pwd = Dir.pwd
    Dir.chdir tmp

    system "cd .."
    system "git init"
    system "git checkout -b gh-pages"
    system "git add ."
    # system "git config --global user.email you@example.com"
    # system "git config --global user.name Your Name"
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git remote add origin https://github.com/#{GITHUB_REPONAME}.git"
    system "git push origin gh-pages --force"

    Dir.chdir pwd
  end
end
