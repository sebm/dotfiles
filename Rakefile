vim_dotfiles = [
  '.vimrc.after',
  '.vimrc.before',
  '.gvimrc.after'
]

namespace :backup_dotfiles do
  task :default => :all

  desc "Backup vim dotfiles to repostory"
  task :vim do
    vim_dotfiles.each do |f|
      path_to_dotfile = File.expand_path(File.join('~', f))

      if File.file? path_to_dotfile
        cp path_to_dotfile, File.join(File.dirname(__FILE__), 'vim', f)
      end
    end
  end

  desc "Backup all dotfiles to repository"
  task :all => [:vim] do
    puts "Copied all dotfiles to repository"
  end
end

task :backup_dotfiles => "backup_dotfiles:all"

