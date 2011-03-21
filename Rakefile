task :default => [:build_all]

namespace "xtools" do
  task :download do
    Dir.mkdir('tarballs') unless Dir.exists? 'tarballs'
	Dir.chdir 'tarballs'
    sh "wget http://ymorin.is-a-geek.org/download/crosstool-ng/crosstool-ng-1.10.0.tar.bz2"
  end
  task :build_all do
    puts "Hello from the rakefile."
  end
end
  