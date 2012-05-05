require 'rubygems'
require 'bundler'
require 'pathname'
require 'logger'
require 'fileutils'
require 'sprockets'

ROOT = Pathname(File.dirname(__FILE__))
LOGGER = Logger.new(STDOUT)
BUNDLES = %w(all.css all.js)
PUBLIC_DIR = ROOT.join("public")
SOURCE_DIR = ROOT.join("app/assets")

task :build do
  sprockets = Sprockets::Environment.new(ROOT) do |env|
    env.logger = LOGGER
  end

  sprockets.append_path(SOURCE_DIR.join("javascripts").to_s)
  sprockets.append_path(SOURCE_DIR.join("stylesheets").to_s)

  BUNDLES.each do |bundle|
    assets = sprockets.find_asset(bundle)
    prefix, basename = assets.pathname.to_s.split("/")[-2..-1]
    FileUtils.mkpath PUBLIC_DIR.join(prefix)
    assets.write_to(PUBLIC_DIR.join(prefix, basename))
  end
end
