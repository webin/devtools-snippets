require 'kramdown'

task :build do

    template = File.read("template.html");
    regex = /<!-- REPLACE -->/

    markup = ""
    all_folders = Dir["snippets/**/"]

    all_folders.drop(1).each do |folder|
        file = folder.split("/")[1];
        js_file = "#{folder}#{file}.js";
        print "hello " + folder + file + "\n"

        readme = File.read(folder + "Readme.md")
        krammed = Kramdown::Document.new(readme).to_html

        cmd = "pygmentize -f html " + js_file
        content = `#{cmd}`

        new_heading = "<h3><a href='#{js_file}'>#{file}.js</a> <a href='##{file}'>#</a></h3>"
        krammed = krammed.gsub(/<h3.*<\/h3>/, new_heading);
        krammed = "<div class='snippet'>" + krammed + "</div>";
        markup = markup + "<div id='" + file + "'>" + krammed + content + "</div>"
    end

    File.open("index.html", "w") do |io|
        io.write template.gsub(regex, markup)
    end

end

task :default => [:build]
