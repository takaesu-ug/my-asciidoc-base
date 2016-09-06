source_files = Rake::FileList.new("**/*.adoc") do |fl|
  fl.exclude("~*")
  fl.exclude("README.adoc")
  fl.exclude(%r{\Aasciidoctor-fopub/})
  fl.exclude(%r{\Avendor/})
end

task default: :pdf

task pdf: source_files.ext('.pdf')
task html: source_files.ext('.html')

rule '.pdf' => '.adoc' do |t|
  dirname = File.dirname t.source
  basename = File.basename t.source, '.adoc'
  xml_file = "#{dirname}/#{basename}.xml"
  fopub_path = Gem.bin_path('asciidoctor-fopub', 'fopub')
  docbook_xsl_ja_path = File.join(File.dirname(File.dirname(fopub_path)), 'src', 'dist', 'docbook-xsl-ja')
  sh %Q{
    bundle exec asciidoctor -a lang=ja -b docbook -d book \
      -r asciidoctor-diagram -r asciidoctor-diagram-cacoo #{t.source} && \
    ./vendor/bin/fopub -t #{docbook_xsl_ja_path} #{xml_file} \
      -param alignment left \
      -param body.font.family Meiryo \
      -param dingbat.font.family Meiryo \
      -param monospace.font.family Meiryo \
      -param title.color Teal \
      -param text.color dimgray \
      -param sans.font.family Meiryo \
      -param title.font.family Meiryo && \
    open #{t.name}
  }
end

rule '.html' => '.adoc' do |t|
  sh "bundle exec asciidoctor --backend html5 -r asciidoctor-diagram -r asciidoctor-diagram-cacoo -o #{t.name} #{t.source} && open #{t.name}"
end

task :watch do
  target = ENV['TARGET'] || 'pdf'
  sh "bundle exec filewatcher '*.adoc' 'bundle exec rake #{target}'"
end
