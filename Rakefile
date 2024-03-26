require 'rake'
require 'yaml'

desc "Generate ebook list and update Jekyll site"
task :generate_ebook_list do
  ebook_dir = 'path/to/your/ebook/repository'
  ebook_list_page = 'path/to/your/jekyll/pages/ebooks.md' # 举例位置

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

  # 写入文件
  File.open(ebook_list_page, 'w') { |file| file.write(content) }

  puts '电子书列表已生成。'
end

desc "Build the Jekyll site"
task :build => [:generate_ebook_list] do
  sh "bundle exec jekyll build"
end

desc "Serve the Jekyll site"
task :serve => [:generate_ebook_list] do
  sh "bundle exec jekyll serve"
end
