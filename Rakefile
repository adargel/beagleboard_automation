require 'fileutils'

project_dir = Dir.pwd
crosstool_package = "crosstool-ng-1.10.0.tar.bz2"
crosstool_dir = "tools/#{crosstool_package.gsub(".tar.bz2", "")}"

task :default => [:build_all]

task :create_dirs do
  Dir.mkdir("tarballs") unless Dir.exists?("tarballs")
  Dir.mkdir("tools") unless Dir.exists?("tools")
end

task :get_tools => [:create_dirs] do
  Dir.chdir("#{project_dir}/tarballs")
  sh "wget http://ymorin.is-a-geek.org/download/crosstool-ng/#{crosstool_package}" unless File.exists?("#{crosstool_package}")
end

task :extract_tools => [:get_tools] do 
  Dir.chdir("#{project_dir}/tools")
  sh "tar xvjf ../tarballs/#{crosstool_package}"
end

namespace "crosstool-NG" do
  task :install => [:extract_tools] do
    Dir.chdir("#{project_dir}/tools/crosstool-ng-1.10.0")
    sh "./configure --local && make && make install"
  end

  task :build => [:install] do
    Dir.chdir(project_dir)
    FileUtils.cp("configs/crosstool-NG.config", "tools/crosstool-ng-1.10.0/.config")
    Dir.chdir("#{project_dir}/tools/crosstool-ng-1.10.0")
    sh "./ct-ng build"
  end
end
