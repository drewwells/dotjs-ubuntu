desc "Install dotjs"
task :install => 'install:all'

namespace :install do
  task :all => [ :prompt, :jquery, :chrome, :daemon, :done ]

  task :prompt do
    puts "\e[1m\e[32mdotjs\e[0m"
    puts "\e[1m-----\e[0m"
    puts "I will install:", ""
    puts "1. The 'dotjs' Google Chrome Extension"
    puts "2. djsd(1) in ~/bin"
    print "Ok? (y/n) "

    begin
      until %w( k ok y yes n no ).include?(answer = $stdin.gets.chomp.downcase)
        puts "(psst... please type y or n)"
        puts "Install dotjs? (y/n)"
      end
    rescue Interrupt
      exit 1
    end

    exit 1 if answer =~ /n/
  end

  task :jquery do

    #download jquery if possible
    if File.executable? '/usr/bin/wget'
      puts 'Downloading latest jQuery'
      sh "wget http://code.jquery.com/jquery-1.6.2.min.js -O #{File.join(Dir.pwd,'ext','jquery.js')}" 
    end
  end

  task :done do
    puts "\e[1m\e[32mdotjs installation worked\e[0m"
    puts "Add `@reboot /path/to/home/bin/djsd -d` to your crontab"
  end

  desc "Install dotjs daemon"
  task :daemon do
    home = ENV['HOME']
    cp "bin/djsd", "#{home}/bin", :verbose => true
  end

  desc "Install Google Chrome extension"
  task :chrome do
    puts "Installing Google Chrome extension..."
    if File.exists?('/opt/google/chrome/google-chrome')
      sh "/opt/google/chrome/google-chrome builds/dotjs.crx &"
    elsif File.exists?('/usr/bin/chromium-browser')
      sh "/usr/bin/chromium-browser builds/dotjs.crx &"
    end
  end
end

desc "Uninstall dotjs"
task :uninstall => 'uninstall:all'

namespace :uninstall do
  task :all => [ :prompt, :daemon, :chrome, :done ]

  task :prompt do
    puts "\e[1m\e[32mdotjs\e[0m"
    puts "\e[1m-----\e[0m"
    puts "I will remove:", ""
    puts "1. djsd(1) from ~/bin"
    puts "3. The 'dotjs' Google Chrome Extension",""
    puts "I will not remove:", ""
    puts "1. ~/.js", ""
    print "Ok? (y/n) "

    begin
      until %w( k ok y yes n no ).include?(answer = $stdin.gets.chomp.downcase)
        puts "(psst... please type y or n)"
        puts "Uninstall dotjs? (y/n)"
      end
    rescue Interrupt
      exit 1
    end

    exit 1 if answer =~ /n/
  end

  task :done do
    if system("curl http://localhost:3131 &> /dev/null")
      puts "\e[31mdotjs uninstall failed\e[0m"
      puts "djsd is still running"
    else
      puts "\e[1m\e[32mdotjs uninstall worked\e[0m"
      puts "your ~/.js was not touched"
    end
  end

  desc "Uninstall dotjs daemon"
  task :daemon do
    home = ENV['HOME']
    rm "#{home}/bin/djsd", :verbose => true
  end

  desc "Uninstall Google Chrome extension"
  task :chrome do
    puts "\e[1mplease uninstall the google chrome extension manually:\e[0m"
    puts "google chrome > window > extensions > dotjs > uninstall"
  end
end
