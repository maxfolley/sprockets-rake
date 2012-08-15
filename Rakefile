require 'rubygems'
require 'bundler'
require 'pathname'
require 'logger'
require 'fileutils'
require 'sprockets'
require 'yui/compressor'

ROOT = Pathname(File.dirname(__FILE__))
LOGGER = Logger.new(STDOUT)
BUNDLES = %w(application.css application.js head.js)
PUBLIC_DIR = ROOT.join("public")
SOURCE_DIR = ROOT.join("views")

task :build do
  sprockets = Sprockets::Environment.new(ROOT) do |env|
    env.logger = LOGGER
    env.css_compressor = YUI::CssCompressor.new
    env.js_compressor = YUI::JavaScriptCompressor.new
  end

  sprockets.append_path(SOURCE_DIR.join("javascripts").to_s)
  sprockets.append_path(SOURCE_DIR.join("stylesheets").to_s)

  BUNDLES.each do |bundle|
    assets = sprockets.find_asset(bundle)
    puts assets.pathname
    prefix, basename = assets.pathname.to_s.split("/")[-2..-1]
    FileUtils.mkpath PUBLIC_DIR.join(prefix)
    filename = PUBLIC_DIR.join(prefix, basename)
    assets.write_to(filename)
  end
end