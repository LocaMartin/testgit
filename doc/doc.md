binary decoder of github pages (!binary) takes binary data in base64 and decode it its not printable like you can use filter like inspect and escape (try raw binary payloads)

┌──(loca㉿loca)-[~/testgit/doc]
└─$ curl -I https://locamartin.github.io/testgit/index.josn                                            
HTTP/2 200 
server: GitHub.com
content-type: application/octet-stream
last-modified: Mon, 22 Jun 2026 15:57:32 GMT
access-control-allow-origin: *
strict-transport-security: max-age=31556952
etag: "6a395b6c-21"
expires: Mon, 22 Jun 2026 16:21:17 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 1D9E:2E79D4:3A78:42DF:6A395EA4
accept-ranges: bytes
date: Mon, 22 Jun 2026 16:12:03 GMT
via: 1.1 varnish
age: 46
x-served-by: cache-ccu830047-CCU
x-cache: HIT
x-cache-hits: 1
x-timer: S1782144723.391206,VS0,VE1
vary: Accept-Encoding
x-fastly-request-id: 1673e671bbca5a488b8d39edbe18134f3bfaf62b
content-length: 33

                                                                                                                                                                                                                                              
┌──(loca㉿loca)-[~/testgit/doc]
└─$ curl -I https://locamartin.github.io/testgit/index.html
HTTP/2 200 
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Mon, 22 Jun 2026 15:57:32 GMT
access-control-allow-origin: *
strict-transport-security: max-age=31556952
etag: "6a395b6c-21"
expires: Mon, 22 Jun 2026 16:22:19 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: A44A:3E33EA:3981:428D:6A395EE3
accept-ranges: bytes
age: 0
date: Mon, 22 Jun 2026 16:12:19 GMT
via: 1.1 varnish
x-served-by: cache-ccu830039-CCU
x-cache: MISS
x-cache-hits: 0
x-timer: S1782144740.576285,VS0,VE270
vary: Accept-Encoding
x-fastly-request-id: 694527efa75485e7d1164387c41a43c464593a37
content-length: 33

                                                                                                                                                                                                                                              
┌──(loca㉿loca)-[~/testgit/doc]
└─$ curl -I https://locamartin.github.io/testgit/index.md  
HTTP/2 200 
server: GitHub.com
content-type: text/markdown; charset=utf-8
last-modified: Mon, 22 Jun 2026 15:57:32 GMT
access-control-allow-origin: *
strict-transport-security: max-age=31556952
etag: "6a395b6c-21"
expires: Mon, 22 Jun 2026 16:22:36 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 2424:64C4F:37D3:40F4:6A395EF2
accept-ranges: bytes
age: 0
date: Mon, 22 Jun 2026 16:12:36 GMT
via: 1.1 varnish
x-served-by: cache-ccu830037-CCU
x-cache: MISS
x-cache-hits: 0
x-timer: S1782144756.962123,VS0,VE263
vary: Accept-Encoding
x-fastly-request-id: 3dfb57246ea3cf4769899955c37446cdd3776075
content-length: 33

                                                                                                                                                                                                                                              
┌──(loca㉿loca)-[~/testgit/doc]
└─$ curl -I https://locamartin.github.io/testgit/index.rb
HTTP/2 200 
server: GitHub.com
content-type: application/octet-stream
last-modified: Mon, 22 Jun 2026 15:57:32 GMT
access-control-allow-origin: *
strict-transport-security: max-age=31556952
etag: "6a395b6c-21"
expires: Mon, 22 Jun 2026 16:27:00 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: C1D0:21659E:44C7:5059:6A395FFB
accept-ranges: bytes
age: 0
date: Mon, 22 Jun 2026 16:17:00 GMT
via: 1.1 varnish
x-served-by: cache-ccu830042-CCU
x-cache: MISS
x-cache-hits: 0
x-timer: S1782145020.161274,VS0,VE254
vary: Accept-Encoding
x-fastly-request-id: ce5a9066815f94fecc9c66382569c06f67411075
content-length: 33

                                                                                                                                                                                                                                              
┌──(loca㉿loca)-[~/testgit/doc]
└─$ nano doc.md
                                                                                                                                                                                                                                              
┌──(loca㉿loca)-[~/testgit/doc]
└─$ curl -I https://locamartin.github.io/testgit/index.java
HTTP/2 200 
server: GitHub.com
content-type: text/x-java-source
last-modified: Mon, 22 Jun 2026 15:57:32 GMT
access-control-allow-origin: *
strict-transport-security: max-age=31556952
etag: "6a395b6c-21"
expires: Mon, 22 Jun 2026 16:29:16 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 1A8C:296DB8:5388:6075:6A396081
accept-ranges: bytes
age: 0
date: Mon, 22 Jun 2026 16:19:16 GMT
via: 1.1 varnish
x-served-by: cache-ccu830023-CCU
x-cache: MISS
x-cache-hits: 0
x-timer: S1782145157.596794,VS0,VE258
vary: Accept-Encoding
x-fastly-request-id: 6fa4d15c85192c2821f0bce40b2681a467719c02
content-length: 33


hosting json & ruby file with html/md syntax init trys to download when visited in browser but hosting ohter file type java,yml with html/md init shows raw text in browser java never asked to be donloaded

if index.md and index.html hosted at same time index.md show raw text and index.html show html content (html file priority)

lets first make note of every finding we did til now in markdown format like front matter injection works and leads to stored xss and potential RCE we used git "issue" to test external input and {{ site.pages }} executes even if its a json file and https://locamartin.github.io/testgit/billion.html does not billion.md execute but   "total_pages": "{{ site.pages | size }}",

  "first_page_meta": "{{ site.pages.first | inspect | escape }}"
 exploit.json make it execute and any other finding you remember 

| Component | Version | Source Code / Repository Link |
| :--- | :--- | :--- |
| **Core Engines & Interpreters** | | |
| Ruby | 3.3.8 | [github.com/ruby/ruby](https://github.com/ruby/ruby/tree/v3_3_8) |
| Jekyll | 3.10.0 | [github.com/jekyll/jekyll](https://github.com/jekyll/jekyll/tree/v3.10.0) |
| Liquid | 4.0.4 | [github.com/Shopify/liquid](https://github.com/Shopify/liquid/tree/v4.0.4) |
| **Heavyweight Parsers & Security Layers** | | |
| Nokogiri | 1.19.4 | [github.com/sparklemotion/nokogiri](https://github.com/sparklemotion/nokogiri/tree/v1.19.4) |
| Safe YAML | 1.0.5 | [github.com/dtao/safe_yaml](https://github.com/dtao/safe_yaml/tree/1.0.5) |
| HTML Pipeline | 2.14.3 | [github.com/gjtorikian/html-pipeline](https://github.com/gjtorikian/html-pipeline/tree/v2.14.3) |
| Kramdown | 2.4.0 | [github.com/vmg/kramdown](https://github.com/vmg/kramdown/tree/2.4.0) |
| Kramdown Parser GFM | 1.1.0 | [github.com/kramdown/parser-gfm](https://github.com/kramdown/parser-gfm/tree/v1.1.0) |
| Rouge | 3.30.0 | [github.com/rouge-ruby/rouge](https://github.com/rouge-ruby/rouge/tree/v3.30.0) |
| Sass | 3.7.4 | [github.com/sass/rubysass](https://github.com/sass/rubysass/tree/3.7.4) |
| **GitHub Master Ecosystem & Extensions** | | |
| github-pages (Meta-gem) | 232 | [github.com/github/pages-gem](https://github.com/github/pages-gem/tree/v232) |
| jekyll-github-metadata | 2.16.1 | [github.com/github/jekyll-github-metadata](https://github.com/github/jekyll-github-metadata/tree/v2.16.1) |
| jekyll-remote-theme | 0.4.3 | [github.com/github/jekyll-remote-theme](https://github.com/github/jekyll-remote-theme/tree/v0.4.3) |
| github-pages-health-check | 1.18.2 | [github.com/github/github-pages-health-check](https://github.com/github/github-pages-health-check/tree/v1.18.2) |
| jekyll-commonmark-ghpages | 0.5.1 | [github.com/github/jekyll-commonmark-ghpages](https://github.com/github/jekyll-commonmark-ghpages/tree/v0.5.1) |
| **Jekyll Functional Plugins** | | |
| jekyll-sass-converter | 1.5.2 | [github.com/jekyll/jekyll-sass-converter](https://github.com/jekyll/jekyll-sass-converter/tree/v1.5.2) |
| jekyll-redirect-from | 0.16.0 | [github.com/jekyll/jekyll-redirect-from](https://github.com/jekyll/jekyll-redirect-from/tree/v0.16.0) |
| jekyll-sitemap | 1.4.0 | [github.com/jekyll/jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap/tree/v1.4.0) |
| jekyll-feed | 0.17.0 | [github.com/jekyll/jekyll-feed](https://github.com/jekyll/jekyll-feed/tree/v0.17.0) |
| jekyll-gist | 1.5.0 | [github.com/jekyll/jekyll-gist](https://github.com/jekyll/jekyll-gist/tree/v1.5.0) |
| jekyll-paginate | 1.1.0 | [github.com/jekyll/jekyll-paginate](https://github.com/jekyll/jekyll-paginate/tree/v1.1.0) |
| jekyll-coffeescript | 1.2.2 | [github.com/jekyll/jekyll-coffeescript](https://github.com/jekyll/jekyll-coffeescript/tree/v1.2.2) |
| jekyll-seo-tag | 2.8.0 | [github.com/jekyll/jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag/tree/v2.8.0) |
| jekyll-avatar | 0.8.0 | [github.com/jekyll/jekyll-avatar](https://github.com/jekyll/jekyll-avatar/tree/v0.8.0) |
| jekyll-include-cache | 0.2.1 | [github.com/jekyll/jekyll-include-cache](https://github.com/jekyll/jekyll-include-cache/tree/v0.2.1) |
| jemoji | 0.13.0 | [github.com/jekyll/jemoji](https://github.com/jekyll/jemoji/tree/v0.13.0) |
| jekyll-mentions | 1.6.0 | [github.com/jekyll/jekyll-mentions](https://github.com/jekyll/jekyll-mentions/tree/v1.6.0) |
| jekyll-relative-links | 0.6.1 | [github.com/jekyll/jekyll-relative-links](https://github.com/jekyll/jekyll-relative-links/tree/v0.6.1) |
| jekyll-optional-front-matter| 0.3.2 | [github.com/jekyll/jekyll-optional-front-matter](https://github.com/jekyll/jekyll-optional-front-matter/tree/v0.3.2) |
| jekyll-readme-index | 0.3.0 | [github.com/jekyll/jekyll-readme-index](https://github.com/jekyll/jekyll-readme-index/tree/v0.3.0) |
| jekyll-default-layout | 0.1.5 | [github.com/jekyll/jekyll-default-layout](https://github.com/jekyll/jekyll-default-layout/tree/v0.1.5) |
| jekyll-titles-from-headings | 0.5.3 | [github.com/jekyll/jekyll-titles-from-headings](https://github.com/jekyll/jekyll-titles-from-headings/tree/v0.5.3) |
| **Supported Whitelisted UI Themes** | | |
| minima | 2.5.1 | [github.com/jekyll/minima](https://github.com/jekyll/minima/tree/v2.5.1) |
| jekyll-swiss | 1.0.0 | [github.com/broccolini/swiss](https://github.com/broccolini/swiss/tree/v1.0.0) |
| jekyll-theme-primer | 0.6.0 | [github.com/pages-themes/primer](https://github.com/pages-themes/primer/tree/v0.6.0) |
| jekyll-theme-architect | 0.2.0 | [github.com/pages-themes/architect](https://github.com/pages-themes/architect/tree/v0.2.0) |
| jekyll-theme-cayman | 0.2.0 | [github.com/pages-themes/cayman](https://github.com/pages-themes/cayman/tree/v0.2.0) |
| jekyll-theme-dinky | 0.2.0 | [github.com/pages-themes/dinky](https://github.com/pages-themes/dinky/tree/v0.2.0) |
| jekyll-theme-hacker | 0.2.0 | [github.com/pages-themes/hacker](https://github.com/pages-themes/hacker/tree/v0.2.0) |
| jekyll-theme-leap-day | 0.2.0 | [github.com/pages-themes/leap-day](https://github.com/pages-themes/leap-day/tree/v0.2.0) |
| jekyll-theme-merlot | 0.2.0 | [github.com/pages-themes/merlot](https://github.com/pages-themes/merlot/tree/v0.2.0) |
| jekyll-theme-midnight | 0.2.0 | [github.com/pages-themes/midnight](https://github.com/pages-themes/midnight/tree/v0.2.0) |
| jekyll-theme-minimal | 0.2.0 | [github.com/pages-themes/minimal](https://github.com/pages-themes/minimal/tree/v0.2.0) |
| jekyll-theme-modernist | 0.2.0 | [github.com/pages-themes/modernist](https://github.com/pages-themes/modernist/tree/v0.2.0) |
| jekyll-theme-slate | 0.2.0 | [github.com/pages-themes/slate](https://github.com/pages-themes/slate/tree/v0.2.0) |
| jekyll-theme-tactile | 0.2.0 | [github.com/pages-themes/tactile](https://github.com/pages-themes/tactile/tree/v0.2.0) |
| jekyll-theme-time-machine | 0.2.0 | [github.com/pages-themes/time-machine](https://github.com/pages-themes/time-machine/tree/v0.2.0) |

---

Configuration file: _config.yml
--- Filters Loaded (via Jekyll/Liquid modules) ---
absolute_url
array_to_sentence_string
cgi_escape
date_to_long_string
date_to_rfc822
date_to_string
date_to_xmlschema
group_by
group_by_exp
inspect
jsonify
markdownify
normalize_whitespace
number_of_words
pop
push
relative_url
sample
sassify
scssify
shift
slugify
smartify
sort
strip_index
to_integer
unshift
uri_escape
where
where_exp
xml_escape

--- Available Tags ---
assign
break
capture
case
comment
continue
cycle
decrement
for
if
ifchanged
include
increment
raw
tablerow
unless
highlight
include_relative
link
post_url
feed_meta

--- Site Configuration Keys ---
baseurl
collections
collections_dir
config
data_dir
defaults
description
destination
detach
encoding
excerpt_separator
exclude
future
highlighter
host
include
includes_dir
incremental
keep_files
kramdown
layouts_dir
limit_posts
liquid
lsi
markdown
markdown_ext
paginate_path
permalink
plugins
plugins_dir
port
quiet
rdiscount
redcarpet
remote_theme
safe
show_dir_listing
show_drafts
source
strict_front_matter
timezone
title
unpublished
verbose
whitelist

--- Interesting Methods on 'site' Object ---
!
!=
!~
<=>
==
===
baseurl
baseurl=
categories
class
cleanup
clone
collection_names
collections
collections_path
config
config=
converters
converters=
data
data=
define_singleton_method
dest
display
docs_to_write
documents
drafts
drafts=
dup
each_site_file
ensure_not_in_dest
enum_for
eql?
equal?
exclude
exclude=
extend
file_read_opts
file_read_opts=
find_converter_instance
freeze
frontmatter_defaults
frozen?
future
future=
gems
gems=
generate
generators
generators=
hash
highlighter
highlighter=
in_dest_dir
in_source_dir
in_theme_dir
include
include=
includes_load_paths
incremental?
inspect
instance_eval
instance_exec
instance_of?
instance_variable_defined?
instance_variable_get
instance_variable_set
instance_variables
instantiate_subclasses
is_a?
itself
keep_files
keep_files=
kind_of?
layouts
layouts=
limit_posts
limit_posts=
liquid_renderer
lsi
lsi=
method
methods
nil?
object_id
pages
pages=
permalink_style
permalink_style=
plugin_manager
plugin_manager=
plugins
plugins=
post_attr_hash
posts
print_stats
private_methods
process
protected_methods
public_method
public_methods
public_send
publisher
read
reader
reader=
regenerator
relative_permalinks_are_deprecated
remove_instance_variable
render
reset
respond_to?
safe
safe=
send
setup
show_drafts
show_drafts=
singleton_class
singleton_method
singleton_methods
site_data
site_payload
source
static_files
static_files=
tags
tap
theme
theme=
then
time
time=
to_enum
to_json
to_liquid
to_s
to_yaml
unpublished
unpublished=
write
yield_self
