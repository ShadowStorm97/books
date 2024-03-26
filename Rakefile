require 'rake'
require 'yaml'

desc "Generate ebook list and update Jekyll site"
task :generate_ebook_list do

  # Print the current working directory
  puts "Current working directory: #{Dir.pwd}"

  ebook_dir = './'
  ebook_list_page = './_pages/ebooks.md' 

  # List files in ebook_dir to ensure it's not empty
  puts "Listing files in ebooks directory:"
  Dir.glob("#{ebook_dir}/*").each do |file|
    puts file
  end

  # 存储分类文件夹及其下的电子书
  categories = {}

  # 扫描目录
  Dir.glob("#{ebook_dir}/**/*").each do |file|
    next if File.directory?(file)
    
    # 分类电子书
    category = File.basename(File.dirname(file))
    categories[category] ||= []
    categories[category] << File.basename(file)
  end

  # 准备写入 Markdown 文件的内容
  content = "# 电子书列表\n\n"
  categories.each do |category, ebooks|
    content << "## #{category}\n\n"
    ebooks.each do |ebook|
      # 这里根据需要使用 Markdown 格式创建链接
      # 假设电子书放在 'ebooks' 目录下，可以根据实际情况调整路径
      content << "- [#{ebook}](/ebooks/#{category}/#{ebook})\n"
    end
    content << "\n"
  end

  # 在写入文件之前确保目录存在
  FileUtils.mkdir_p(File.dirname(ebook_list_page))

  # 然后写入文件
  File.open(ebook_list_page, 'w') { |file| file.write(content) }
  puts '电子书列表已生成。'

  # Print the generated list content for debugging
  if File.exists?(ebook_list_page)
    puts "Content of #{ebook_list_page}:"
    puts File.read(ebook_list_page)
  else
    puts "Error: #{ebook_list_page} does not exist."
  end
end

desc "Build the Jekyll site"
task :build => [:generate_ebook_list] do
  sh "bundle exec jekyll build"
end

desc "Serve the Jekyll site"
task :serve => [:generate_ebook_list] do
  sh "bundle exec jekyll serve"
end
