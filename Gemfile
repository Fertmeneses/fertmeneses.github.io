# For local preview only (not published — excluded in _config.yml).
# Lean toolchain that builds fast on any modern Ruby and mirrors what
# GitHub Pages runs for this site (core Jekyll + these two allowlisted plugins).
#
# Preview with Docker (no system Ruby needed):
#   docker run --rm -v "$PWD":/srv/jekyll -p 4000:4000 jekyll/jekyll:4.2.2 \
#     jekyll serve --host 0.0.0.0
# then open http://localhost:4000
source "https://rubygems.org"

gem "jekyll", "~> 4.2"

group :jekyll_plugins do
  gem "jekyll-seo-tag"
  gem "jekyll-readme-index"
end
